# Instalación base - Arch Linux 

## Comprobar el modo de arranque para UEFI
```shell 
ls /sys/firmware/efi/efivars
# Listar 
localectl list-keymaps
# ejemplo de teclado en español es
loadkeys es

timedatectl set-ntp true
``` 
## Comprobar red y conexión a Wifi

```shell  
iwlist wlan0 scan
# wifi WLAN
iwctl --passphrase 'pass' station wlan0 connect 'essid-name'
# o: iwctl --> station wlan0 scan --> station wlan0 connect 'essid-name'
```
## Esquema de Particiónes
```shell
cgdisk /dev/sda
#   Type     Value Code                    Size        Format Type  
# ---------------------------------------------------------------------------    
# 1 Boot 'EFI System (EF00)'        --> +550M   -->   mkfs.fat -F32 /dev/sda1
# 2 Swap 'Linux Swap (8200)'        --> +2G     -->   mkswap /dev/sda2
# 3 Root 'Linux-x86-64 root(8304)'  --> +20G    -->   mkfs.ext4 /dev/sda3
# 4 Home 'Linux Home (8302)'        --> +100G   -->   mkfs.ext4 /dev/sda4
```
### Montar las Particiones:
```shell
# Mount: Root
mount /dev/sda3 /mnt/
# Swap>
swapon /dev/sda2
# Boot Directory
mkdir -p /mnt/boot/efi/
# Mount: Boot
mount /dev/sda1 /mnt/boot/efi/
# Home Directory
mkdir -p /mnt/home
# Mount: Home Directory
mount /dev/sda4 /mnt/home
```

### Instalación (instalar paquetes esenciales)
```shell
pacstrap /mnt base base-devel linux linux-firmware networkmanager grub efibootmgr nano vim intel-ucode # linux-headers linux-lts 
# optional: intel-ucode | amd-ucode
```

```shell
# Este archivo se utiliza para especificar los sistemas de archivos que se montan automáticamente durante el arranque del sistema
genfstab -U /mnt >> /mnt/etc/fstab
```

### Login with root 
```shell
arch-chroot /mnt 
```

```shell
# Seleccionar el Idioma: buscar segun el idioma, ej.: #es_ES.UTF-8 < Descomentar quitando #>
nano /etc/locale.gen
# Construir
locale-gen
# set local config
echo LANG=es_ES.UTF-8 > /etc/locale.conf
# symbolic link
# Alternatively: timedatectl list-timezones | grep Zurich
ln -s /usr/share/zoneinfo/Zone1/Zone_2 /etc/localtime
# Alternatively
ln -sf /usr/share/zoneinfo/$(curl https://ipapi.co/timezone) /etc/localtime
# set keyboard lang: es, us, en, fr, la-latin1
echo KEYMAP=es > /etc/vconsole.conf

```
### Grub
```shell
grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=Arch
# grub-install --target=x86_64-efi --efi-directory=/efi --removable
grub-mkconfig -o /boot/grub/grub.cfg  
#optional configure video resolution
nano /etc/default/grub
# and setting video=1920x1080:
# GRUB_CMDLINE_LINUX_DEFAULT ="loglevel=3 quiet video=1920x1080" 
# Add 'single' for rescue mode
# Add 'pci=nocrs', touchpad
# And build grub configuration
# grub-mkconfig -o /boot/grub/grub.cfg
```
### Add Hostname
```shell
echo pc_name > /etc/hostname
```
### hosts file config
```shell
# Editar el hosts con: nano /etc/hosts
127.0.0.1   localhost.localdomain   localhost
::1         localhost.localdomain   localhost
127.0.1.1   pc_name.localdomain     pc_name
```

### Add Password to root user
```shell
passwd
# exit and umount root user
exit
umount -R /mnt 
reboot
```

### User add
```shell
useradd -m user #-s /bin/bash
passwd user
nano /etc/sudoers
```
###  Network Manager Enable
```shell
sudo systemctl enable NetworkManager
sudo systemctl start NetworkManager
ping -c 3 archlinux.org
```

```shell
sudo pacman -S reflector rsync python --noconfirm
# fast servers
sudo reflector --verbose --latest 15 --sort rate --save /etc/pacman.d/mirrorlist
```

## Directory structure: Desktop, Documents, Pictures
```shell 
pacman -S xdg-user-dirs
```
