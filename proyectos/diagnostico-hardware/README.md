<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&height=220&color=0:E7A3C3,50:B9A3E3,100:7A4FC0&text=Diagn%C3%B3stico%20de%20hardware&fontColor=3B2470&fontSize=42&fontAlignY=38&desc=UEFI%20%C2%B7%20S.M.A.R.T.%20%C2%B7%20Test%20de%20RAM%20%C2%B7%20Aver%C3%ADas%20de%20arranque&descSize=16&descAlignY=58&animation=fadeIn" width="100%"/>

<img src="https://img.shields.io/badge/M%C3%B3dulo-Fundamentos%20de%20Hardware-B9A3E3?style=for-the-badge&labelColor=F1ECFA" alt="Módulo: Fundamentos de Hardware"/>
<img src="https://img.shields.io/badge/ASIR-1.%C2%BA%20curso-E7A3C3?style=for-the-badge&labelColor=F1ECFA" alt="ASIR: 1.º curso"/>
<img src="https://img.shields.io/badge/Fecha-Octubre%202026-B9A3E3?style=for-the-badge&labelColor=F1ECFA" alt="Fecha: Octubre 2026"/>

<sub><a href="https://maite-willinski.github.io">♡ Volver al portafolio</a> &nbsp;·&nbsp; <a href="https://github.com/Maite-Willinski/Maite-Willinski.github.io">❀ Ver todos los proyectos</a></sub>

</div>

<br>

<table align="center"><tr><td align="center">
<br>
<i>Revisé un equipo real con herramientas de soporte técnico (UEFI, CrystalDiskInfo, MemTest64, Cinebench) y planteé el diagnóstico de averías de arranque.</i>
<br><br>
</td></tr></table>

> [!NOTE]
> **Privacidad ♡** En la captura de CrystalDiskInfo se ha ocultado el número de serie del disco.


<p align="center">˚ ༘ ♡ ⋆｡˚ ❀ ˚｡⋆ ♡ ༘ ˚</p>

## ❀ Objetivo
Revisar el estado de un equipo real (el mío) con las herramientas que se usan en soporte técnico:
configuración en la UEFI, salud del disco, test de memoria y rendimiento de la CPU. También diagnosticar
averías típicas de arranque.


<p align="center">˚ ༘ ♡ ⋆｡˚ ❀ ˚｡⋆ ♡ ༘ ˚</p>

## ✿ Qué he hecho

### ✿ Paso 1 · Información desde la UEFI
Comprobé la memoria instalada (32 GB DDR5 a 4800 MHz en dos módulos de 16 GB, en las ranuras A2 y B2 para
trabajar en **Dual Channel**) y el orden de arranque, con Windows Boot Manager en el SSD NVMe.
<p align="center">
  <img src="img/bios.jpg" alt="UEFI de la placa base" width="86%"/>
  <br><sub>⋆ UEFI de la placa base ⋆</sub>
</p>

### ✿ Paso 2 · Salud del disco con CrystalDiskInfo
Analicé los valores **S.M.A.R.T.** del SSD: estado "Bueno" al 100 %, 42 °C, interfaz **PCIe 4.0 x4** con NVMe
2.0, horas de uso y datos escritos (desgaste muy bajo) y **TRIM** activo, que ayuda a que el SSD mantenga
su rendimiento con el tiempo.
<p align="center">
  <img src="img/crystaldisk.png" alt="CrystalDiskInfo" width="86%"/>
  <br><sub>⋆ CrystalDiskInfo ⋆</sub>
</p>

### ✿ Paso 3 · Test de memoria RAM
Pasé TechPowerUp MemTest64 en modo máximo con 12 hilos. Detectó los dos módulos en canales distintos y la
prueba terminó **sin errores**.
<p align="center">
  <img src="img/memtest.png" alt="MemTest64" width="86%"/>
  <br><sub>⋆ MemTest64 ⋆</sub>
</p>

### ✿ Paso 4 · Rendimiento de la CPU
Con Cinebench medí la CPU en un núcleo y en todos los hilos (Ryzen 5 7600X, 6 núcleos y 12 hilos). La
relación entre los dos resultados (7,29×) indica lo bien que escala el procesador en tareas en paralelo,
como la virtualización.

### ✿ Paso 5 · Diagnóstico de averías de arranque
- **No pita y no responde:** lo más probable es la fuente de alimentación (no envía la señal *Power Good*) o
  una avería grave en la placa base. Ojo: muchos equipos modernos no traen el altavoz interno, así que
  "no pita" no siempre significa que el POST haya fallado. **Me pasó en mis prácticas de SMR.**
- **Pitidos cortos continuos:** problema de alimentación de la placa base, conector ATX de 24 pines mal
  conectado o, según la BIOS, memoria RAM mal insertada o dañada.


<p align="center">˚ ༘ ♡ ⋆｡˚ ❀ ˚｡⋆ ♡ ༘ ˚</p>

## ♡ Problemas y cómo los resolví
- **Aviso "Memory locking failed" en el test de RAM:** al principio parece un error, pero no lo es. El
  test se ejecuta dentro de Windows y el sistema tiene reservada parte de la memoria, así que el programa
  solo pudo probar 17 GB de los 32 GB. El resultado es fiable para esa parte, y la prueba terminó sin errores.

<p align="center">˚ ༘ ♡ ⋆｡˚ ❀ ˚｡⋆ ♡ ༘ ˚</p>

## ✦ Tecnologías

<p>
<img src="https://img.shields.io/badge/UEFI-B9A3E3?style=flat-square" alt="UEFI"/>
<img src="https://img.shields.io/badge/CrystalDiskInfo%20%28S.M.A.R.T.%29-E7A3C3?style=flat-square" alt="CrystalDiskInfo (S.M.A.R.T.)"/>
<img src="https://img.shields.io/badge/MemTest64-B9A3E3?style=flat-square" alt="MemTest64"/>
<img src="https://img.shields.io/badge/Cinebench-E7A3C3?style=flat-square" alt="Cinebench"/>
<img src="https://img.shields.io/badge/NVMe-B9A3E3?style=flat-square" alt="NVMe"/>
<img src="https://img.shields.io/badge/DDR5-E7A3C3?style=flat-square" alt="DDR5"/>
</p>


<p align="center">˚ ༘ ♡ ⋆｡˚ ❀ ˚｡⋆ ♡ ༘ ˚</p>

## ❁ Qué he aprendido
- A comprobar el estado de un disco y de la memoria antes de dar un equipo por bueno.
- A interpretar Dual Channel, TRIM y los datos S.M.A.R.T.
- A plantear un diagnóstico de arranque por pasos, de lo más probable a lo menos probable.

<p align="center">˚ ༘ ♡ ⋆｡˚ ❀ ˚｡⋆ ♡ ༘ ˚</p>

<div align="center">

<a href="https://maite-willinski.github.io"><img src="https://img.shields.io/badge/Ver-portafolio-E7A3C3?style=for-the-badge&labelColor=F1ECFA" alt="Ver: portafolio"/></a>
<a href="https://www.linkedin.com/in/maite-willinski-gonz%C3%A1lez-b05706268/"><img src="https://img.shields.io/badge/Hablemos-LinkedIn-B9A3E3?style=for-the-badge&labelColor=F1ECFA&logo=linkedin&logoColor=3B2470" alt="Hablemos: LinkedIn"/></a>

<sub>Hecho con ♡ por Maite Willinski · Técnica SMR y estudiante de ASIR</sub>

<img src="https://capsule-render.vercel.app/api?section=footer&type=waving&height=100&color=0:E7A3C3,50:B9A3E3,100:7A4FC0" width="100%"/>

</div>
