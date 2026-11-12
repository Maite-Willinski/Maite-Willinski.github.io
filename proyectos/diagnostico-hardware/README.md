<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&height=230&color=0:3B2470,55:7A4FC0,100:E7A3C3&text=Diagn%C3%B3stico%20de%20hardware&fontColor=ffffff&fontSize=40&fontAlignY=36&desc=UEFI%20%C2%B7%20S.M.A.R.T.%20%C2%B7%20Test%20de%20RAM%20%C2%B7%20Aver%C3%ADas%20de%20arranque&descSize=16&descAlignY=56&animation=fadeIn" width="100%"/>

<img src="https://img.shields.io/badge/M%C3%B3dulo-Fundamentos%20de%20Hardware-7A4FC0?style=for-the-badge&labelColor=3B2470" alt="Módulo: Fundamentos de Hardware"/>
<img src="https://img.shields.io/badge/Curso-ASIR%20%C2%B7%201.%C2%BA-B5487A?style=for-the-badge&labelColor=3B2470" alt="Curso: ASIR · 1.º"/>
<img src="https://img.shields.io/badge/Fecha-Octubre%202026-B9A3E3?style=for-the-badge&labelColor=3B2470" alt="Fecha: Octubre 2026"/>

<sub><a href="https://maite-willinski.github.io">🌸 Volver al portafolio</a> · <a href="https://github.com/Maite-Willinski/Maite-Willinski.github.io">📂 Todos los proyectos</a></sub>

</div>

<br>

> **En una frase:** revisé un equipo real con las herramientas de soporte técnico (UEFI, CrystalDiskInfo, MemTest64, Cinebench) y planteé el diagnóstico de averías de arranque.

> [!NOTE]
> 🔒 En la captura de CrystalDiskInfo se ha ocultado el número de serie del disco.


<p align="center"><img src="https://img.shields.io/badge/-%E2%9C%A6%20%E2%9C%A6%20%E2%9C%A6-E7A3C3?style=flat-square" alt="✦"/></p>

## 🎯 Objetivo
Revisar el estado de un equipo real (el mío) con las herramientas que se usan en soporte técnico:
configuración en la UEFI, salud del disco, test de memoria y rendimiento de la CPU. También diagnosticar
averías típicas de arranque.


<p align="center"><img src="https://img.shields.io/badge/-%E2%9C%A6%20%E2%9C%A6%20%E2%9C%A6-E7A3C3?style=flat-square" alt="✦"/></p>

## 🛠️ Qué he hecho

### <sub>01</sub> · Información desde la UEFI
Comprobé la memoria instalada (32 GB DDR5 a 4800 MHz en dos módulos de 16 GB, en las ranuras A2 y B2 para
trabajar en **Dual Channel**) y el orden de arranque, con Windows Boot Manager en el SSD NVMe.
<p align="center">
  <img src="img/bios.jpg" alt="UEFI de la placa base" width="88%"/>
  <br><sub><i>UEFI de la placa base</i></sub>
</p>

### <sub>02</sub> · Salud del disco con CrystalDiskInfo
Analicé los valores **S.M.A.R.T.** del SSD: estado "Bueno" al 100 %, 42 °C, interfaz **PCIe 4.0 x4** con NVMe
2.0, horas de uso y datos escritos (desgaste muy bajo) y **TRIM** activo, que ayuda a que el SSD mantenga
su rendimiento con el tiempo.
<p align="center">
  <img src="img/crystaldisk.png" alt="CrystalDiskInfo" width="88%"/>
  <br><sub><i>CrystalDiskInfo</i></sub>
</p>

### <sub>03</sub> · Test de memoria RAM
Pasé TechPowerUp MemTest64 en modo máximo con 12 hilos. Detectó los dos módulos en canales distintos y la
prueba terminó **sin errores**.
<p align="center">
  <img src="img/memtest.png" alt="MemTest64" width="88%"/>
  <br><sub><i>MemTest64</i></sub>
</p>

### <sub>04</sub> · Rendimiento de la CPU
Con Cinebench medí la CPU en un núcleo y en todos los hilos (Ryzen 5 7600X, 6 núcleos y 12 hilos). La
relación entre los dos resultados (7,29×) indica lo bien que escala el procesador en tareas en paralelo,
como la virtualización.

### <sub>05</sub> · Diagnóstico de averías de arranque
- **No pita y no responde:** lo más probable es la fuente de alimentación (no envía la señal *Power Good*) o
  una avería grave en la placa base. Ojo: muchos equipos modernos no traen el altavoz interno, así que
  "no pita" no siempre significa que el POST haya fallado. **Me pasó en mis prácticas de SMR.**
- **Pitidos cortos continuos:** problema de alimentación de la placa base, conector ATX de 24 pines mal
  conectado o, según la BIOS, memoria RAM mal insertada o dañada.


<p align="center"><img src="https://img.shields.io/badge/-%E2%9C%A6%20%E2%9C%A6%20%E2%9C%A6-E7A3C3?style=flat-square" alt="✦"/></p>

## 🧩 Problemas y cómo los resolví
- **Aviso "Memory locking failed" en el test de RAM:** al principio parece un error, pero no lo es. El
  test se ejecuta dentro de Windows y el sistema tiene reservada parte de la memoria, así que el programa
  solo pudo probar 17 GB de los 32 GB. El resultado es fiable para esa parte, y la prueba terminó sin errores.
<p align="center"><img src="https://img.shields.io/badge/-%E2%9C%A6%20%E2%9C%A6%20%E2%9C%A6-E7A3C3?style=flat-square" alt="✦"/></p>

## 🧰 Tecnologías

<p>
<img src="https://img.shields.io/badge/UEFI-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="UEFI"/>
<img src="https://img.shields.io/badge/CrystalDiskInfo%20%28S.M.A.R.T.%29-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="CrystalDiskInfo (S.M.A.R.T.)"/>
<img src="https://img.shields.io/badge/MemTest64-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="MemTest64"/>
<img src="https://img.shields.io/badge/Cinebench-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="Cinebench"/>
<img src="https://img.shields.io/badge/NVMe-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="NVMe"/>
<img src="https://img.shields.io/badge/DDR5-B9A3E3?style=flat-square&labelColor=B9A3E3" alt="DDR5"/>
</p>


<p align="center"><img src="https://img.shields.io/badge/-%E2%9C%A6%20%E2%9C%A6%20%E2%9C%A6-E7A3C3?style=flat-square" alt="✦"/></p>

## 🌱 Qué he aprendido
- A comprobar el estado de un disco y de la memoria antes de dar un equipo por bueno.
- A interpretar Dual Channel, TRIM y los datos S.M.A.R.T.
- A plantear un diagnóstico de arranque por pasos, de lo más probable a lo menos probable.

<br>

<div align="center">

<a href="https://maite-willinski.github.io"><img src="https://img.shields.io/badge/Ver-portafolio-7A4FC0?style=for-the-badge&labelColor=3B2470" alt="Ver: portafolio"/></a>
<a href="https://www.linkedin.com/in/maite-willinski-gonz%C3%A1lez-b05706268/"><img src="https://img.shields.io/badge/Contacto-LinkedIn-B5487A?style=for-the-badge&labelColor=3B2470&logo=linkedin&logoColor=white" alt="Contacto: LinkedIn"/></a>

<sub>Hecho con 💜 por Maite Willinski · Técnica SMR y estudiante de ASIR</sub>

<img src="https://capsule-render.vercel.app/api?section=footer&type=waving&height=110&color=0:3B2470,55:7A4FC0,100:E7A3C3" width="100%"/>

</div>
