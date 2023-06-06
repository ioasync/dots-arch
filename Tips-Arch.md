 
<h2 align="center"> <samp>Tips para Arch Linux</samp></h2>


## Cambiar Idioma del Teclado en Terminal
```shell
localectl list-x11-keymap-layouts
localectl set-x11-keymap <código-de-idioma>
sudo localectl set-x11-keymap es,us
```
## Para montar particiones ntfs y exfat
```shell
sudo pacman -S exfat-utils ntfs-3g
```
### Montar un USB o Disco Externo
```shell
# Crear un directorio para montar el dispositivo ej.:
mkdir -p /media/external
# Seleccionamos el dispositivo externo ej.: sdb1
sudo mount /dev/sdb1 /media/external
```
## Conectarse a un Red Wi-Fi
```shell
 # Opción 1:usando iwctl, donde wlan0, es el nombre de la interfaz
iwlist wlan0 scan
iwctl --passphrase 'contraseña' station wlan0 connect 'NombreDeRed'  
# Opción 2: usando nmcli
nmcli dev wifi list
nmcli dev wifi con "essid-name" password "password"
```
## Instalación de Maquina Virtual:

### Usando VirtualBox
```shell
sudo pacman -S virtualbox virtualbox-host-dkms virtualbox-ext-oracle
yay -S virtualbox virtualbox-host-dkms virtualbox-ext-oracle
```
### Instalando KVM, QUEMU y Virt Manager

```shell
sudo pacman -Syy
sudo pacman -S archlinux-keyring
sudo pacman -S qemu virt-manager virt-viewer dnsmasq vde2 bridge-utils openbsd-netcat
#
sudo pacman -S ebtables iptables
# libguestfs is a set of tools used to access and modify virtual machine (VM) disk images.
sudo pacman -S libguestfs
# Start KVM libvirt service
sudo systemctl enable libvirtd.service
sudo systemctl start libvirtd.service
```

## Quitar permiso de Ejecución de un fichero sin perder otras propiedades:

```shell
chmod -R -a -x ~/Descarga/async
```
## Copiar Archivos usando RSYNC
```shell
# Copia de carpetas
rsync -avhP /origen/ /destino/ 
# Copia de archivos mediante su extension del directorio actual
rsync -av --progress --partial --include="*.docx" --include="*.mkv" --exclude="*" ./ /ruta/a/la/raiz/de/tu/USB/
```
## Descarga de Man
```shell
sudo pacman -S man-pages
```
## Grep Tips: manejo basico(usando plocate)
```shell
locate picom | grep "/home/io/picom.conf" | xargs vim
locate picom | grep "picom.conf" | head -n 1 | xargs vim # Muestra la primera linea
locate picom | grep "picom.conf" | sed -n '2p' | xargs vim # Muestra  la segunda linea
```
## Configuración de la pantalla
```shell
# para elegir la pantalla
xrandr
# Para filtrar solo las pantallas que esten activas
xrandr | grep ' connected' | awk '{print $1}'
# De otra forma usando directamente 'awk'
xrandr | awk '/ connected/ {print $1}'
# Usando solo la pantalla que esta conectada por hdmi(previamente obteniendo el nombre de la pantalla)
 xrandr --output VGA-1 --off --output HDMI-1 --mode 1920x1080
```
## Comprobar el driver de video en uso
```shell
lspci -k | grep -A 2 -E "(VGA|3D)"
```
## Establececer fondo de pantalla usando 'feh'
```shell
sudo pacman -S feh
feh --bg-fill /ruta/a/tu/fondo/de/pantalla.jpg
# En i3: ~/.config/i3/config # Agregar
# exec --no-startup-id feh --bg-fill /ruta/a/tu/fondo/de/pantalla.jpg
```

## Agregar Fuentes
```shell
# Directorio recomendado para almacenar las fuentes de usuario es ~/.local/share/fonts/.
mkdir -p ~/.local/share/fonts/ 
# Para todo el sistema "/usr/share/fonts/"
mkdir -p /usr/share/fonts/
# Ejemplo descargamos la fuente JetBrainsMono y la copiamos en el directorio
wget https://github.com/ryanoasis/nerd-fonts/releases/download/v2.3.3/JetBrainsMono.zip
cp JetBrainsMono.zip ~/.local/share/fonts/ 
unzip -o ~/.local/share/fonts/JetBrainsMono.zip -d ~/.local/share/fonts/ 
# Actualizar fuentes
fc-cache -f -v
```
## Instalar Drive de Audio, usando PipeWire
```shell
sudo pacman -S pipewire pipewire-audio gst-plugin-pipewire pipewire-alsa pipewire-jack pipewire-pulse pipewire-roc wireplumber realtime-privileges
```




## Instalacion de Repositorios
```shell
sudo pacman -S --needed base-devel
```

### Repositorio yay
```shell 
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```
### Repositorio Paru
```shell 
git clone https://aur.archlinux.org/paru.git
cd paru
makepkg -si
# para invertir el orden de busqueda, editar:
sudo nano /etc/paru.conf
# Descomentar: #BottomUp
# Usando vifm, para el PKGBUILD 
paru spotify --fm vifm
# tambien se puede agregar en el archivo de configuracion paru.conf
# Debajo de 
# [bin]
# FileManager = vifm <-- Agregar aqui: vifm
```

### Repositorio de BlackArch 
```shell
cd /tmp
curl -O https://blackarch.org/strap.sh
chmod +x strap.sh
./strap.sh

```


## Instalación de Maquina Virtual:

### Usando VirtualBox
```shell
sudo pacman -S virtualbox virtualbox-host-dkms virtualbox-ext-oracle
yay -S virtualbox virtualbox-host-dkms virtualbox-ext-oracle
```


### Instalando KVM, QUEMU y Virt Manager

```shell
sudo pacman -Syy
sudo pacman -S archlinux-keyring
sudo pacman -S qemu virt-manager virt-viewer dnsmasq vde2 bridge-utils openbsd-netcat
#
sudo pacman -S ebtables iptables
# libguestfs is a set of tools used to access and modify virtual machine (VM) disk images.
sudo pacman -S libguestfs
# Start KVM libvirt service
sudo systemctl enable libvirtd.service
sudo systemctl start libvirtd.service
```

## Crear un Dual-Boot(Linux-Windows)
```shell
# Creamos una particion, se puede usar gparted
sudo pacman -S gparted
# Para detectar la particion de Windows, modificar descomentando: #GRUB_DISABLE_OS_PROBER=false, desde la ruta:    
sudo nano /etc/default/grub
# Posteriormente actualizarlo
sudo grub-mkconfig -o /boot/grub/grub.cfg
```
## UFW (Uncomplicated Firewall)

```shell
#Instalar UFW: 
sudo pacman -S ufw
#Habilitar UFW en el arranque: 
sudo systemctl enable ufw  
sudo systemctl start ufw
#Configurar las reglas de firewall: 
sudo ufw default allow
#Para denegar todo el tráfico entrante y permitir todo el tráfico saliente: 
sudo ufw default deny incoming
sudo ufw default allow outgoing 
#Para permitir tráfico en un puerto específico, por ejemplo, el puerto 80 para HTTP, se puede utilizar el siguiente comando:
 
sudo ufw allow 80/tcp
#Para permitir el tráfico en un rango de puertos, por ejemplo, del puerto 1000 al 2000, se puede utilizar el siguiente comando:
 
sudo ufw allow 1000:2000/tcp
#Para permitir el tráfico desde una dirección IP específica, por ejemplo, la dirección IP 192.168.1.100, se puede utilizar el siguiente comando:
 
sudo ufw allow from 192.168.1.100
#Para permitir el tráfico de un protocolo específico, por ejemplo, el protocolo ICMP para ping, se puede utilizar el siguiente comando:
 
sudo ufw allow icmp
#Para denegar tráfico en un puerto específico, por ejemplo, el puerto 22 para SSH, se puede utilizar el siguiente comando:
 
sudo ufw deny 22/tcp
#Comprobar las reglas de firewall:
#Una vez definidas las reglas de firewall, es recomendable comprobarlas para asegurarse de que se han aplicado correctamente. Para comprobar las reglas de firewall, se puede utilizar el siguiente comando:
 
sudo ufw status verbose
#Este comando mostrará todas las reglas de firewall activas y su estado actual.

#Desactivar UFW:
#Si es necesario desactivar UFW, se puede utilizar el siguiente comando:
 
sudo ufw disable 
```
