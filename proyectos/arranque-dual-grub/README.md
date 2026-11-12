<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&height=220&color=0:E7A3C3,50:B9A3E3,100:7A4FC0&text=Arranque%20dual%20y%20GRUB&fontColor=3B2470&fontSize=42&fontAlignY=38&desc=Windows%2011%20%2B%20Ubuntu%20%C2%B7%20UEFI%20%C2%B7%20Secure%20Boot%20%C2%B7%20Recuperaci%C3%B3n&descSize=16&descAlignY=58&animation=fadeIn" width="100%"/>

<img src="https://img.shields.io/badge/M%C3%B3dulo-Implantaci%C3%B3n%20de%20Sistemas%20Operativos-B9A3E3?style=for-the-badge&labelColor=F1ECFA" alt="Módulo: Implantación de Sistemas Operativos"/>
<img src="https://img.shields.io/badge/ASIR-1.%C2%BA%20curso-E7A3C3?style=for-the-badge&labelColor=F1ECFA" alt="ASIR: 1.º curso"/>
<img src="https://img.shields.io/badge/Fecha-Octubre%202026-B9A3E3?style=for-the-badge&labelColor=F1ECFA" alt="Fecha: Octubre 2026"/>

<sub><a href="https://maite-willinski.github.io">♡ Volver al portafolio</a> &nbsp;·&nbsp; <a href="https://github.com/Maite-Willinski/Maite-Willinski.github.io">❀ Ver todos los proyectos</a></sub>

</div>

<br>

<table align="center"><tr><td align="center">
<br>
<i>Instalé Windows 11 y Ubuntu en la misma máquina, borré a propósito la partición EFI y recuperé el arranque de los dos sistemas desde la línea de comandos.</i>
<br><br>
</td></tr></table>

<p align="center">˚ ༘ ♡ ⋆｡˚ ❀ ˚｡⋆ ♡ ༘ ˚</p>

## ❀ Objetivo
Instalar Windows 11 y Ubuntu en la misma máquina virtual con UEFI y Secure Boot, personalizar el gestor
de arranque GRUB y, después, provocar a propósito un fallo de arranque borrando la partición EFI para
recuperar los dos sistemas solo con la línea de comandos.


<p align="center">˚ ༘ ♡ ⋆｡˚ ❀ ˚｡⋆ ♡ ༘ ˚</p>

## ✿ Qué he hecho

### ✿ Paso 1 · Máquina virtual con UEFI y Secure Boot
Creé la VM en VirtualBox con 8 GB de RAM, 2 CPU, firmware EFI y Secure Boot activado, y lo comprobé con
`VBoxManage`.
<p align="center">
  <img src="img/vboxmanage.png" alt="Configuración de la VM con VBoxManage" width="86%"/>
  <br><sub>⋆ Configuración de la VM con VBoxManage ⋆</sub>
</p>

### ✿ Paso 2 · Instalación de los dos sistemas y particionado
Instalé primero Windows 11 y después Ubuntu en el mismo disco. Con `lsblk` se ve el resultado: la
partición **EFI** (FAT32, montada en `/boot/efi`), las particiones de Windows (NTFS / BitLocker) y las de
Ubuntu (ext4).
<p align="center">
  <img src="img/lsblk.png" alt="Particiones del disco con lsblk" width="86%"/>
  <br><sub>⋆ Particiones del disco con lsblk ⋆</sub>
</p>

También instalé las **Guest Additions** en los dos sistemas. En Ubuntu tuve que instalar antes las
dependencias (`gcc`, `make`, `perl`…) y registrar la clave con **MOK Management** al reiniciar, porque
Secure Boot no deja cargar módulos del kernel sin firmar.

### ✿ Paso 3 · Personalización de GRUB
Edité `/etc/default/grub` y la entrada de Windows en `grub.cfg` para que aparezca con mis iniciales.
<p align="center">
  <img src="img/grub_menu.png" alt="Menú de GRUB con la entrada de Windows personalizada" width="86%"/>
  <br><sub>⋆ Menú de GRUB con la entrada de Windows personalizada ⋆</sub>
</p>

### ✿ Paso 4 · Simulación de avería y recuperación
Desmonté y formateé la partición EFI (`umount /boot/efi` y `mkfs.fat -F32 /dev/sda1`), así que ninguno de
los dos sistemas podía arrancar. Después:

- **Windows:** arranqué desde el disco de instalación, abrí la consola y regeneré los archivos de arranque
  con `bcdboot`.
- **Ubuntu:** arranqué en modo live, monté el sistema instalado en `/mnt` (también `/boot/efi`, `/dev`,
  `/proc` y `/sys`), entré con `chroot`, reinstalé GRUB y regeneré su configuración.
- Por último cambié el orden de arranque en la UEFI para que GRUB volviera a ser el primero.

<p align="center">
  <img src="img/grubinstall.png" alt="Recuperación de GRUB con chroot y grub-install" width="86%"/>
  <br><sub>⋆ Recuperación de GRUB con chroot y grub-install ⋆</sub>
</p>


<p align="center">˚ ༘ ♡ ⋆｡˚ ❀ ˚｡⋆ ♡ ༘ ˚</p>

## ♡ Problemas y cómo los resolví
- **`grub-install /dev/sda` daba error** (`/usr/lib/grub/i386-pc/modinfo.sh doesn't exist`): sin indicar
  nada, intentaba instalar la versión para BIOS clásica (i386-pc). Me di cuenta de que el sistema arranca
  en **UEFI** y lo arreglé indicando la plataforma: `grub-install --target=x86_64-efi /dev/sda`, y después
  `update-grub`.
- **El teclado estaba en inglés** en el entorno live y escribía `/` en lugar de `-` (se ve en
  `grub/install` en la captura). Lo detecté por el error "No such file or directory" y corregí los comandos.

<p align="center">˚ ༘ ♡ ⋆｡˚ ❀ ˚｡⋆ ♡ ༘ ˚</p>

## ✦ Tecnologías

<p>
<img src="https://img.shields.io/badge/VirtualBox-B9A3E3?style=flat-square" alt="VirtualBox"/>
<img src="https://img.shields.io/badge/Windows%2011-E7A3C3?style=flat-square" alt="Windows 11"/>
<img src="https://img.shields.io/badge/Ubuntu-B9A3E3?style=flat-square" alt="Ubuntu"/>
<img src="https://img.shields.io/badge/UEFI-E7A3C3?style=flat-square" alt="UEFI"/>
<img src="https://img.shields.io/badge/Secure%20Boot-B9A3E3?style=flat-square" alt="Secure Boot"/>
<img src="https://img.shields.io/badge/GRUB-E7A3C3?style=flat-square" alt="GRUB"/>
<img src="https://img.shields.io/badge/bcdboot-B9A3E3?style=flat-square" alt="bcdboot"/>
<img src="https://img.shields.io/badge/chroot-E7A3C3?style=flat-square" alt="chroot"/>
<img src="https://img.shields.io/badge/lsblk-B9A3E3?style=flat-square" alt="lsblk"/>
</p>


<p align="center">˚ ༘ ♡ ⋆｡˚ ❀ ˚｡⋆ ♡ ༘ ˚</p>

## ❁ Qué he aprendido
- Cómo arranca un equipo UEFI: firmware → partición EFI → gestor de arranque → sistema operativo.
- A recuperar un sistema que no arranca sin herramientas automáticas como Boot Repair.
- A leer los mensajes de error para saber qué está fallando de verdad (BIOS frente a UEFI).

<p align="center">˚ ༘ ♡ ⋆｡˚ ❀ ˚｡⋆ ♡ ༘ ˚</p>

<div align="center">

<a href="https://maite-willinski.github.io"><img src="https://img.shields.io/badge/Ver-portafolio-E7A3C3?style=for-the-badge&labelColor=F1ECFA" alt="Ver: portafolio"/></a>
<a href="https://www.linkedin.com/in/maite-willinski-gonz%C3%A1lez-b05706268/"><img src="https://img.shields.io/badge/Hablemos-LinkedIn-B9A3E3?style=for-the-badge&labelColor=F1ECFA&logo=linkedin&logoColor=3B2470" alt="Hablemos: LinkedIn"/></a>

<sub>Hecho con ♡ por Maite Willinski · Técnica SMR y estudiante de ASIR</sub>

<img src="https://capsule-render.vercel.app/api?section=footer&type=waving&height=100&color=0:E7A3C3,50:B9A3E3,100:7A4FC0" width="100%"/>

</div>
