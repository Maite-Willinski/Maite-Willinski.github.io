<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&height=230&color=0:3B2470,55:7A4FC0,100:E7A3C3&text=Redes%20y%20Wireshark&fontColor=ffffff&fontSize=40&fontAlignY=36&desc=Direccionamiento%20IP%20%C2%B7%20Subnetting%20%C2%B7%20ARP%20%C2%B7%20DNS%20%C2%B7%20HTTP&descSize=16&descAlignY=56&animation=fadeIn" width="100%"/>

<img src="https://img.shields.io/badge/M%C3%B3dulo-Planificaci%C3%B3n%20y%20Administraci%C3%B3n%20de%20Redes-7A4FC0?style=for-the-badge&labelColor=3B2470" alt="Módulo: Planificación y Administración de Redes"/>
<img src="https://img.shields.io/badge/Curso-ASIR%20%C2%B7%201.%C2%BA-B5487A?style=for-the-badge&labelColor=3B2470" alt="Curso: ASIR · 1.º"/>
<img src="https://img.shields.io/badge/Fecha-Octubre%202026-B9A3E3?style=for-the-badge&labelColor=3B2470" alt="Fecha: Octubre 2026"/>

<sub><a href="https://maite-willinski.github.io">🌸 Volver al portafolio</a> · <a href="https://github.com/Maite-Willinski/Maite-Willinski.github.io">📂 Todos los proyectos</a></sub>

</div>

<br>

> **En una frase:** calculé subredes y cuellos de botella de una red con dos LAN y comprobé con capturas reales cómo viajan ARP, DNS y HTTP por las capas TCP/IP.

> [!NOTE]
> 🔒 Las IP públicas y las direcciones MAC de las capturas se han sustituido por valores de ejemplo (rangos reservados para documentación, como 198.51.100.0/24 y 203.0.113.0/24). Aparecen marcados en lavanda.


<p align="center"><img src="https://img.shields.io/badge/-%E2%9C%A6%20%E2%9C%A6%20%E2%9C%A6-E7A3C3?style=flat-square" alt="✦"/></p>

## 🎯 Objetivo
Analizar una red con dos LAN y salida a Internet: distinguir la parte pública de la privada, calcular
subredes y el ancho de banda real, y comprobar con capturas reales cómo viaja un paquete por las capas
TCP/IP (ARP, DNS y HTTP).


<p align="center"><img src="https://img.shields.io/badge/-%E2%9C%A6%20%E2%9C%A6%20%E2%9C%A6-E7A3C3?style=flat-square" alt="✦"/></p>

## 🛠️ Qué he hecho

### <sub>01</sub> · Análisis de una topología (Packet Tracer)
<p align="center">
  <img src="img/topologia.png" alt="Topología con dos LAN y enlace al ISP" width="88%"/>
  <br><sub><i>Topología con dos LAN y enlace al ISP</i></sub>
</p>

- Separé la **parte privada (LAN)**, con los dos switches, los PC y los servidores, de la **parte pública (WAN)**:
  router del ISP, nube de Internet y enlace serie.
- Clasifiqué cada IP por tipo (pública o privada) y clase, y calculé su dirección de red y de difusión:

| Enlace | Máscara | Red | Difusión |
| --- | --- | --- | --- |
| WAN (router – ISP) | /30 · 255.255.255.252 | 26.17.1.0 | 26.17.1.3 |
| LAN 2 (PC) | /24 · 255.255.255.0 | 10.17.1.0 | 10.17.1.255 |
| LAN 1 (servidores) | /23 · 255.255.254.0 | 10.17.2.0 | 10.17.3.255 |

- Calculé tiempos de descarga buscando el **cuello de botella**: un fichero de 500 MB son 4000 Mb; con una
  tarjeta GigabitEthernet (1000 Mbps) tarda 4 s, y con FastEthernet (100 Mbps), 40 s.
- Con salida a Internet de 500 Mbps y equipos FastEthernet, pueden descargar a la vez a máxima velocidad
  500 / 100 = **5 equipos**.

### <sub>02</sub> · Subnetting (VLSM básico)
Partiendo de un rango /25 de ejemplo (172.16.50.0/25), calculé la máscara para 30 equipos por subred:
2⁵ − 2 = 30 → 5 bits de host → **/27 (255.255.255.224)**, con 2 bits prestados → **4 subredes**.

| Subred | Red | Hosts | Difusión |
| --- | --- | --- | --- |
| 1 | 172.16.50.0/27 | .1 – .30 | .31 |
| 2 | 172.16.50.32/27 | .33 – .62 | .63 |
| 3 | 172.16.50.64/27 | .65 – .94 | .95 |
| 4 | 172.16.50.96/27 | .97 – .126 | .127 |

### <sub>03</sub> · Capturas reales con Wireshark (ARP, DNS y HTTP)
Antes de capturar vacié la caché ARP (`arp -d *`) y la DNS (`ipconfig /flushdns`) para obligar al
equipo a generar todo el tráfico desde cero. Después abrí una web HTTP y filtré por protocolo.

**ARP:** el router (192.168.1.1) pregunta qué MAC tiene la IP de mi PC (192.168.1.29). ARP no usa puertos:
trabaja entre la capa de enlace y la de red.
<p align="center">
  <img src="img/wireshark_arp.png" alt="Captura ARP en Wireshark" width="88%"/>
  <br><sub><i>Captura ARP en Wireshark</i></sub>
</p>

**DNS:** mi PC envía la consulta por **UDP** desde un puerto aleatorio (62968) al **puerto 53** del router,
que hace de servidor DNS, para traducir el nombre de la web a una IP.
<p align="center">
  <img src="img/wireshark_dns.png" alt="Captura DNS en Wireshark" width="88%"/>
  <br><sub><i>Captura DNS en Wireshark</i></sub>
</p>

**HTTP:** el navegador abre una conexión **TCP** desde un puerto efímero (65104) al **puerto 80** del
servidor y envía un `GET`. La IP de destino es la del servidor web, pero la **MAC de destino es la de mi
router**, porque las MAC solo sirven dentro de la red local y cambian en cada salto.
<p align="center">
  <img src="img/wireshark_http.png" alt="Captura HTTP en Wireshark" width="88%"/>
  <br><sub><i>Captura HTTP en Wireshark</i></sub>
</p>

### <sub>04</sub> · Comprobación con comandos (HTTPS)
Identifiqué los datos de una respuesta HTTPS que llega a mi PC con `netstat -ano`, `ping` y `arp -a`:
puertos (443 en el servidor y un puerto efímero en mi equipo), IP de origen y MAC del router.
<p align="center">
  <img src="img/netstat.png" alt="netstat filtrando el puerto 443" width="88%"/>
  <br><sub><i>netstat filtrando el puerto 443</i></sub>
</p>
<p align="center">
  <img src="img/arp.png" alt="Tabla ARP con la MAC del router" width="88%"/>
  <br><sub><i>Tabla ARP con la MAC del router</i></sub>
</p>


<p align="center"><img src="https://img.shields.io/badge/-%E2%9C%A6%20%E2%9C%A6%20%E2%9C%A6-E7A3C3?style=flat-square" alt="✦"/></p>

## 🧩 Problemas y cómo los resolví
- **Vaciado de cachés:** si las cachés ARP y DNS tienen datos, el equipo no genera las peticiones iniciales
  y no aparecen en la captura. Tuve que vaciarlas con los comandos adecuados antes de capturar y, como hay
  muchísimo tráfico, usar filtros para encontrar los paquetes (`arp`, `dns`, `http.request.method == "GET"`).
- **La MAC de origen no era la del servidor:** entendí que en un paquete que viene de Internet la MAC de
  origen es la del último salto (mi router), no la del servidor, mientras que las IP de origen y destino
  se mantienen (salvo el cambio que hace el NAT en el router).
<p align="center"><img src="https://img.shields.io/badge/-%E2%9C%A6%20%E2%9C%A6%20%E2%9C%A6-E7A3C3?style=flat-square" alt="✦"/></p>

## 🧰 Tecnologías

<p>
<img src="https://img.shields.io/badge/Wireshark-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="Wireshark"/>
<img src="https://img.shields.io/badge/Packet%20Tracer-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="Packet Tracer"/>
<img src="https://img.shields.io/badge/TCP%2FIP-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="TCP/IP"/>
<img src="https://img.shields.io/badge/ARP-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="ARP"/>
<img src="https://img.shields.io/badge/DNS-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="DNS"/>
<img src="https://img.shields.io/badge/HTTP%2FHTTPS-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="HTTP/HTTPS"/>
<img src="https://img.shields.io/badge/Subnetting-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="Subnetting"/>
<img src="https://img.shields.io/badge/netstat-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="netstat"/>
<img src="https://img.shields.io/badge/arp-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="arp"/>
<img src="https://img.shields.io/badge/ping-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="ping"/>
<img src="https://img.shields.io/badge/ipconfig-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="ipconfig"/>
</p>


<p align="center"><img src="https://img.shields.io/badge/-%E2%9C%A6%20%E2%9C%A6%20%E2%9C%A6-E7A3C3?style=flat-square" alt="✦"/></p>

## 🌱 Qué he aprendido
- A leer una captura capa a capa: MAC (enlace), IP (red) y puertos (transporte).
- A calcular subredes y a localizar el cuello de botella real de una red.
- La diferencia entre puertos conocidos (53, 80, 443) y puertos efímeros del cliente.

<br>

<div align="center">

<a href="https://maite-willinski.github.io"><img src="https://img.shields.io/badge/Ver-portafolio-7A4FC0?style=for-the-badge&labelColor=3B2470" alt="Ver: portafolio"/></a>
<a href="https://www.linkedin.com/in/maite-willinski-gonz%C3%A1lez-b05706268/"><img src="https://img.shields.io/badge/Contacto-LinkedIn-B5487A?style=for-the-badge&labelColor=3B2470&logo=linkedin&logoColor=white" alt="Contacto: LinkedIn"/></a>

<sub>Hecho con 💜 por Maite Willinski · Técnica SMR y estudiante de ASIR</sub>

<img src="https://capsule-render.vercel.app/api?section=footer&type=waving&height=110&color=0:3B2470,55:7A4FC0,100:E7A3C3" width="100%"/>

</div>
