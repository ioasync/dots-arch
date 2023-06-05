<h2 align="center"> ━━━━━━  󰣇  ━━━━━━ </h2>
<!-- BADGES -->
<div align="center">
</div>  

## :loudspeaker: <samp>Contenido</samp>
- [Instalacion de Arch Linux](#instalacion-de-arch-linux)
  - [Tips para Linux](#space_invader-tips-para-linux)
  - [Servidor Gráfico](#rocket-servidor-gráfico)
  - [Instalación base de i3 (I)](#instalación-base-de-i3-i)
  - [Instalación base de BSPWM (II)](#instalación-base-de-bspwm-ii)
  - [Instalacion Gestor de Inicio de Sesión](#instalacion-gestor-de-inicio-de-sesión)
    - [Usando lightdm](#usando-lightdm)
  - [Paquetes Adicionales](#paquetes-adicionales)




# Instalacion de Arch Linux
Pasos para la instalacion manual de Arch-Linux: [`Ver Aqui`](Install.md)
## :space_invader: Tips para Linux 
Tips para Manejo y configuración de Linux y Arch: [`Ver Aqui`](Tips-Arch.md)
## :rocket: Servidor Gráfico 
| Paquete | Descripción   |
|---------|---------------|
| xorg    | Servidor X, un servidor gráfico que permite a las aplicaciones mostrar gráficos en la pantalla. |
| xorg-xinit| Script de inicio para el servidor X que se ejecuta al iniciar la sesión de un usuario. |
| xorg-xinput | Utilidad para configurar dispositivos de entrada como ratones y teclados. |

```bash
sudo pacman -S xorg xorg-xinit xorg-xinput
```
## Instalación base de i3 (I)
| Paquete | Descripción   |
|---------|---------------|
| i3-gaps | Gestor de ventanas muy ligero y altamente configurable.   |
| i3status | Programa de estado de sistema para el gestor de ventanas i3.   |

```bash
sudo pacman -S i3-gaps i3status # or i3blocks
```
## Instalación base de BSPWM (II)
| Paquete | Descripción   |
|---------|---------------|
| [`bspwm`](https://github.com/baskerville/bspwm) | Gestor de ventanas tipo mosaico que organiza las ventanas en un árbol binario completo   |
| [`sxhkd`](https://wiki.archlinux.org/title/Sxhkd_(Espa%C3%B1ol)) | Demonio simple de teclas de acceso directo para X, hecho por el desarrollador de bspwm, que reacciona a los eventos de entrada ejecutando comandos.   |
```bash
sudo pacman -S bspwm sxhkd 
```
## Instalacion Gestor de Inicio de Sesión
| Paquete |	Descripción |
|---------|-------------|
|lightdm  |	Un gestor de pantalla ligero y personalizable que soporta diferentes tecnologías de escritorio y de visualización|
|lightdm-gtk-greeter | Un greeter para lightdm basado en GTK que permite elegir el usuario, la sesión y el idioma|
|sddm  |	Un gestor de pantalla simple y moderno que usa Qt y QML para crear interfaces de inicio de sesión |
### Usando lightdm
```bash
sudo pacman -S lightdm lightdm-gtk-greeter
# para habilitarlo e iniciar
sudo systemctl enable lightdm
sudo systemctl start lightdm
```


## Paquetes Adicionales
|Paquete | Descripción|
|--------|------------|
|rofi | Selector de aplicaciones y lanzador de búsqueda.|
|feh | Visor de imágenes ligero. | 
|dunst | Sistema de notificación de escritorio. | 
|picom | Compositor de ventanas, que permite la transparencia y otros efectos visuales. | 
|dmenu | Selector de menús para el entorno de escritorio i3.  | 
|kitty | Emulador de terminal que permite la configuración avanzada. | 
| Alacritty | Emulador de terminal |
| lsd(lsDeluxe) | Alternativa a ls|
| bat | Alternativa moderna al comando clásico de Linux cat. |
| plocate | Herramienta de búsqueda de archivos en el sistema de archivos de Unix que utiliza una base de datos preconstruida de archivos generados (creada usando updatedb).|