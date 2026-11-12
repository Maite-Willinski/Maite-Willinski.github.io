<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&height=230&color=0:3B2470,55:7A4FC0,100:E7A3C3&text=Servidores%20web%20en%20AWS&fontColor=ffffff&fontSize=40&fontAlignY=36&desc=EC2%20%C2%B7%20Ubuntu%20%2B%20nginx%20%C2%B7%20Windows%20Server%20%2B%20IIS&descSize=16&descAlignY=56&animation=fadeIn" width="100%"/>

<img src="https://img.shields.io/badge/M%C3%B3dulo-Implantaci%C3%B3n%20de%20Sistemas%20Operativos-7A4FC0?style=for-the-badge&labelColor=3B2470" alt="Módulo: Implantación de Sistemas Operativos"/>
<img src="https://img.shields.io/badge/Curso-ASIR%20%C2%B7%201.%C2%BA-B5487A?style=for-the-badge&labelColor=3B2470" alt="Curso: ASIR · 1.º"/>
<img src="https://img.shields.io/badge/Fecha-Oct%20%E2%80%93%20Nov%202026-B9A3E3?style=for-the-badge&labelColor=3B2470" alt="Fecha: Oct – Nov 2026"/>

<sub><a href="https://maite-willinski.github.io">🌸 Volver al portafolio</a> · <a href="https://github.com/Maite-Willinski/Maite-Willinski.github.io">📂 Todos los proyectos</a></sub>

</div>

<br>

> **En una frase:** desplegué dos servidores en la nube con Amazon EC2, me conecté por SSH y RDP y publiqué una web en cada uno con nginx e IIS.

> [!NOTE]
> 🔒 Las IP públicas de las instancias y la huella de la clave SSH se han sustituido por valores de ejemplo. Las instancias de AWS Academy son temporales y ya no existen.


<p align="center"><img src="https://img.shields.io/badge/-%E2%9C%A6%20%E2%9C%A6%20%E2%9C%A6-E7A3C3?style=flat-square" alt="✦"/></p>

## 🎯 Objetivo
Crear dos máquinas virtuales en la nube con Amazon EC2, una con Ubuntu Server y otra con Windows Server,
conectarme a ellas de forma remota y publicar en cada una una página web propia.


<p align="center"><img src="https://img.shields.io/badge/-%E2%9C%A6%20%E2%9C%A6%20%E2%9C%A6-E7A3C3?style=flat-square" alt="✦"/></p>

## 🛠️ Qué he hecho

### <sub>01</sub> · Crear las instancias
Lancé las dos instancias desde EC2 con su **par de claves** y su **grupo de seguridad** (el firewall de
AWS). En la de Ubuntu añadí un script en **datos de usuario**, que se ejecuta solo al arrancar la máquina
por primera vez y deja nginx instalado:
<p align="center">
  <img src="img/userdata.png" alt="Script de datos de usuario para instalar nginx" width="88%"/>
  <br><sub><i>Script de datos de usuario para instalar nginx</i></sub>
</p>

### <sub>02</sub> · Acceso remoto
- **Ubuntu:** por **SSH** con la clave privada `.pem` (sin contraseña), abriendo el puerto 22 en el grupo de seguridad.
- **Windows Server:** por **Escritorio remoto (RDP)**.

<p align="center">
  <img src="img/ssh.png" alt="Conexión SSH a la instancia de Ubuntu" width="88%"/>
  <br><sub><i>Conexión SSH a la instancia de Ubuntu</i></sub>
</p>

### <sub>03</sub> · Servidor web en Ubuntu (nginx)
Comprobé que nginx estaba en marcha, abrí el puerto **80 (HTTP)** en el grupo de seguridad y modifiqué la
página de inicio en `/var/www/html`.
<p align="center">
  <img src="img/nginx.png" alt="Página servida por nginx" width="88%"/>
  <br><sub><i>Página servida por nginx</i></sub>
</p>

### <sub>04</sub> · Servidor web en Windows Server (IIS)
Instalé el rol **Internet Information Services (IIS)**, abrí el puerto 80 y creé mi propio `index.html` en
`C:\inetpub\wwwroot`, que sustituye a la página de bienvenida sin borrar `iisstart.htm` (IIS da prioridad
a `index.html`).
<p align="center">
  <img src="img/iis.png" alt="Página servida por IIS" width="88%"/>
  <br><sub><i>Página servida por IIS</i></sub>
</p>


<p align="center"><img src="https://img.shields.io/badge/-%E2%9C%A6%20%E2%9C%A6%20%E2%9C%A6-E7A3C3?style=flat-square" alt="✦"/></p>

## 🧩 Problemas y cómo los resolví
- **Puertos cerrados por defecto:** AWS bloquea todo el tráfico de entrada que no se haya permitido en el
  grupo de seguridad, así que para ver las webs hubo que abrir expresamente el puerto 80 (HTTP) en las dos
  instancias.
- **Aviso de "host desconocido" al conectar por SSH la primera vez:** es normal. El cliente guarda la
  huella del servidor en `known_hosts` para avisar si cambia en futuras conexiones (podría ser un ataque
  de intermediario).
<p align="center"><img src="https://img.shields.io/badge/-%E2%9C%A6%20%E2%9C%A6%20%E2%9C%A6-E7A3C3?style=flat-square" alt="✦"/></p>

## 🧰 Tecnologías

<p>
<img src="https://img.shields.io/badge/AWS%20EC2-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="AWS EC2"/>
<img src="https://img.shields.io/badge/Ubuntu%20Server-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="Ubuntu Server"/>
<img src="https://img.shields.io/badge/Windows%20Server-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="Windows Server"/>
<img src="https://img.shields.io/badge/nginx-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="nginx"/>
<img src="https://img.shields.io/badge/IIS-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="IIS"/>
<img src="https://img.shields.io/badge/SSH%20con%20claves-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="SSH con claves"/>
<img src="https://img.shields.io/badge/RDP-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="RDP"/>
<img src="https://img.shields.io/badge/Grupos%20de%20seguridad-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="Grupos de seguridad"/>
</p>


<p align="center"><img src="https://img.shields.io/badge/-%E2%9C%A6%20%E2%9C%A6%20%E2%9C%A6-E7A3C3?style=flat-square" alt="✦"/></p>

## 🌱 Qué he aprendido
- A desplegar y administrar servidores en la nube y a controlar el acceso con grupos de seguridad.
- La diferencia entre autenticarse por SSH con clave y por contraseña.
- A montar un servidor web básico tanto en Linux como en Windows.

<br>

<div align="center">

<a href="https://maite-willinski.github.io"><img src="https://img.shields.io/badge/Ver-portafolio-7A4FC0?style=for-the-badge&labelColor=3B2470" alt="Ver: portafolio"/></a>
<a href="https://www.linkedin.com/in/maite-willinski-gonz%C3%A1lez-b05706268/"><img src="https://img.shields.io/badge/Contacto-LinkedIn-B5487A?style=for-the-badge&labelColor=3B2470&logo=linkedin&logoColor=white" alt="Contacto: LinkedIn"/></a>

<sub>Hecho con 💜 por Maite Willinski · Técnica SMR y estudiante de ASIR</sub>

<img src="https://capsule-render.vercel.app/api?section=footer&type=waving&height=110&color=0:3B2470,55:7A4FC0,100:E7A3C3" width="100%"/>

</div>
