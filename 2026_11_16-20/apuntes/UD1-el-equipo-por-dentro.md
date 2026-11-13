# UD1 · El equipo por dentro

Continuación de los [apuntes de la UD1 de la semana del 2 al 6](../../2026_11_02-06/apuntes/UD1-hardware-y-software.md), que tienen lo general: el modelo de Von Neumann, las partes de la CPU, la jerarquía de memoria, la placa base, los drivers y la seguridad en el puesto de trabajo. Aquí, cada componente en detalle, cómo se averigua el de un equipo real y cómo se manipula con seguridad. Las preguntas para comprobar que lo entiendes están en el [cuestionario](../cuestionario.md) de la semana, en «Cuestiones sobre los apuntes». Lo de los apartados 2 a 8 se practica en el proyecto de la semana (`actividades/proyecto-SI.md`).

Hay tres tipos de contenido:

- Lo que no lleva marca es lo **imprescindible**: hay que entenderlo y saber explicarlo con tus palabras.
- > **Para saber más.** Lo que va en un recuadro como este ayuda a entender, pero no hay que aprenderlo de memoria.
- *Para la práctica: paso N del proyecto.* Los apartados que empiezan así recogen los detalles que se usan en ese paso. Se aprenden haciéndolo: vuelve a ellos cuando el proyecto te lo pida.

---

## 1. Caja, fuente y placa: que todo encaje

**En una frase:** la caja, la fuente y la placa base tienen que ser del mismo **factor de forma**, y la fuente tiene que dar la potencia y los conectores que piden los componentes.

**Lo que tienes que saber**

- El **factor de forma** de una placa fija sus medidas y dónde van los tornillos y los conectores. Los estándares hacen que cualquier caja y cualquier fuente del mismo formato sirvan para la placa. En los portátiles no hay estándar: cada fabricante hace sus propias placas.
- La **caja** se elige según la placa. De mayor a menor: torre, semitorre, minitorre, sobremesa, *slim* (formato pequeño), *barebone* (caja con placa y fuente ya montadas) y *all in one* (todo dentro de la pantalla).
- La **fuente de alimentación** convierte la corriente alterna de la red en continua. En los sobremesa va dentro de la caja (formatos **ATX**, **SFX** y **TFX**); en los portátiles y equipos pequeños es externa, el cargador.
- La fuente tiene que dar **potencia** (en vatios) suficiente para todo lo instalado: si se queda corta, el equipo no arranca o se apaga con carga. Una fuente **modular** solo lleva conectados los cables que se usan.

**Compara: los factores de forma de placa más usados**

| Factor de forma | Medidas | Uso |
|---|---|---|
| E-ATX | 30,5 × 33 cm | Servidores y equipos de alto rendimiento |
| ATX | 30,5 × 24,4 cm | El más usado en sobremesa |
| Micro-ATX | 24,4 × 24,4 cm | Compatible con cajas y fuentes ATX, con menos ranuras |
| Mini-ITX | 17 × 17 cm | Equipos pequeños |

**Compara: los conectores de la fuente**

| Conector | Qué alimenta |
|---|---|
| ATX de 24 pines | La placa base |
| ATX de 4 pines o EPS de 8 pines | El procesador |
| PCIe de 6 u 8 pines | La tarjeta gráfica |
| SATA | Discos y unidades ópticas |
| Molex de 4 pines | En desuso: discos y unidades IDE antiguos |

### El chipset hoy

- Antes la placa tenía dos chips: el **puente norte** (procesador con RAM y gráfica, lo más rápido) y el **puente sur** (discos, USB, audio, red, firmware).
- Hoy **el puente norte está dentro del procesador**: la RAM y la ranura PCIe x16 de la gráfica se conectan directamente a él. Lo que hacía el puente sur lo hace un único chip, el **chipset** (Intel lo llama PCH, *Platform Controller Hub*, y AMD, FCH).
- Por eso el chipset decide sobre todo cuántos USB, SATA, M.2 y ranuras PCIe tiene la placa.

---

## 2. El procesador en detalle

*Para la práctica: pasos 1 y 4 del proyecto.*

**En una frase:** de un procesador importan su zócalo, su arquitectura, sus núcleos e hilos, su frecuencia, su caché y lo que consume.

**Lo que tienes que saber**

| Característica | Qué es |
|---|---|
| **Zócalo** (*socket*) | Dónde se conecta a la placa: **LGA** (los contactos están en la placa; lo usa Intel) o **PGA** (las patillas están en el procesador). Placa y procesador tienen que tener el mismo |
| **Arquitectura** | **x86_64** (o x64, AMD64): Intel y AMD, en PC y servidores. **ARM**: móviles, tabletas y los Mac con Apple M. Un programa compilado para una no funciona en la otra sin traducción |
| **32 o 64 bits** | El tamaño de los datos y direcciones con los que trabaja. Con 32 bits solo se pueden usar 4 GB de RAM. Hoy casi todo es de 64 bits, y un sistema de 64 bits necesita un procesador de 64 bits |
| **Núcleos** (*cores*) | CPU completas dentro del mismo chip: cada una ejecuta su propio programa a la vez que las demás. De 2 a más de 64 |
| **Hilos** (*threads*) | Lo que un núcleo puede llevar a la vez. Con 2 hilos por núcleo, el sistema ve el doble de **procesadores lógicos** |
| **Frecuencia** | Ciclos de reloj por segundo, en GHz. Hay una **base** y una **turbo** (la máxima, durante poco tiempo). Más GHz no siempre es más rápido: cuentan también los núcleos, la caché y la generación |
| **Caché** | **L1** y **L2**, propias de cada núcleo; **L3**, compartida por todos |
| **TDP** | El calor que hay que sacar, en vatios. Decide qué refrigeración necesita: disipador con ventilador o refrigeración líquida |

- **Overclocking:** hacer que funcione por encima de su frecuencia: más rendimiento, más calor y menos vida útil. **Underclocking:** lo contrario, para consumir y calentarse menos.
- Fabricantes: **Intel** (Core i3, i5, i7 e i9, y Core Ultra; Xeon para servidores) y **AMD** (Ryzen; Epyc para servidores), con x86_64; **Qualcomm** (Snapdragon), **Apple** (M1, M2…) y **MediaTek**, con ARM.

> **Para saber más.** Un procesador tiene miles de millones de **transistores**, interruptores diminutos que solo tienen dos estados: por eso todo se guarda en binario. La **ley de Moore** (1965) predijo que su número se duplicaría cada dos años; hoy se acercan a los 3–5 nanómetros y el ritmo se frena por los límites de la física. El rendimiento también se mide en **MIPS** (millones de instrucciones por segundo) y **FLOPS** (operaciones con decimales por segundo).

---

## 3. La memoria RAM en detalle

*Para la práctica: pasos 1 y 4 del proyecto.*

**En una frase:** la RAM actual es DDR4 o DDR5, va en módulos DIMM (sobremesa) o SO-DIMM (portátil), y de ella importan la capacidad, la velocidad y la latencia.

**Lo que tienes que saber**

- La RAM es **DRAM** (dinámica): sus celdas pierden la carga y hay que refrescarlas continuamente. La **SRAM** (estática) no necesita refresco y es mucho más rápida, pero más grande y cara: se usa para la **caché**. Las tarjetas gráficas usan **GDDR**, una variante de DDR para mover muchos datos a la vez.
- **DDR** (*Double Data Rate*) hace **dos transferencias por ciclo** de reloj. Por eso una **DDR4-3200** hace 3200 millones de transferencias por segundo (**MT/s**) con un reloj de 1600 MHz: los MT/s son el doble de los MHz.
- Cada generación (DDR3, DDR4, DDR5) tiene distinto número de contactos y la **muesca** en otro sitio: **no son intercambiables**. Un módulo solo entra en la ranura de su generación y en una posición.
- **Módulos:** **DIMM** en sobremesa y **SO-DIMM**, más pequeño, en portátiles. En muchos portátiles la RAM va **soldada** a la placa y no se puede ampliar.
- **ECC:** RAM que detecta y corrige errores. Más cara: servidores y estaciones de trabajo.
- **Doble canal:** con dos módulos iguales en las ranuras indicadas por la placa (suelen ser del mismo color), el procesador lee de los dos a la vez y el ancho de banda se duplica. Algunas placas tienen cuatro canales.
- **Latencia CAS (CL):** los ciclos de reloj que pasan desde que se pide un dato hasta que empieza a llegar. Como se mide en ciclos, para comparar dos memorias hay que pasarla a nanosegundos (el cálculo está debajo).

**Compara: las generaciones de RAM**

| | DDR3 | DDR4 | DDR5 |
|---|---|---|---|
| Contactos (DIMM / SO-DIMM) | 240 / 204 | 288 / 260 | 288 / 262 |
| Voltaje | 1,5 V | 1,2 V | 1,1 V |
| Velocidad | 800–2400 MT/s | 1600–3200 MT/s | 4800 MT/s o más |

**Cómo se calcula la latencia en nanosegundos.** Una DDR4-3200 CL16:

1. Transferencias: 3200 MT/s. El reloj va a la mitad: **1600 MHz**.
2. Un ciclo dura 1 / 1600 MHz = **0,625 ns**.
3. La latencia son 16 ciclos: 16 × 0,625 ns = **10 ns**.

Una DDR4-2666 CL16 tarda 16 × 0,75 ns = 12 ns, y una DDR4-2133 CL15, 15 × 0,94 ns ≈ 14,1 ns: aunque tenga el CL más bajo, es la más lenta.

> **Para saber más.** La **NVRAM** combina RAM y memoria no volátil: es donde el firmware UEFI guarda sus entradas de arranque. El **bit de paridad** es la forma más sencilla de detectar errores: se añade un bit para que el número de unos sea par; detecta un error, pero no lo corrige.

---

## 4. El almacenamiento en detalle

*Para la práctica: pasos 2 y 4 del proyecto.*

**En una frase:** un disco duro guarda los datos magnéticamente en platos que giran; un SSD, en chips de memoria flash, sin piezas móviles; y los dos se conectan por SATA o, los SSD más rápidos, por NVMe.

**Lo que tienes que saber**

- **Disco duro (HDD):** **platos** metálicos que giran (de 5400 a 15 000 rpm) y un **cabezal** que lee y escribe en ellos. Por dentro se organiza en **pistas** (círculos), **sectores** (trozos de pista con una cantidad fija de datos), **cilindros** (la misma pista en todos los platos) y **clústeres** (grupos de sectores: lo mínimo que usa el sistema de archivos).
- **SSD:** memoria **flash**, sin piezas móviles: mucho más rápido, silencioso y resistente a golpes. Cada celda guarda 1 bit (**SLC**), 2 (**MLC**), 3 (**TLC**) o 4 (**QLC**): cuantos más bits, más capacidad y menos duración. Su vida útil se mide en **TBW** (terabytes que se pueden escribir).
- **Conexiones:** un SSD **SATA** va por cable o en formato **M.2** y llega a unos 550 MB/s. Un SSD **NVMe** va en formato **M.2** por **PCI Express** y llega a varios GB/s. Una ranura M.2 puede admitir SATA, NVMe o los dos: hay que mirar el manual de la placa.
- **Ópticos:** CD (700 MB), DVD (4,7–17 GB) y Blu-ray (25–128 GB), leídos con un láser. En desuso.
- **Almacenamiento en red:** **NAS** (un equipo con discos al que se accede por la red, con su sistema de archivos: típico para copias de seguridad en pequeñas empresas), **SAN** (una red de discos de alta velocidad, que los servidores usan como si fueran discos propios) y la **nube** (Google Drive, OneDrive, iCloud…).

**RAID: varios discos que trabajan juntos**

Un **RAID** (*Redundant Array of Independent Disks*) agrupa discos para ganar velocidad, tolerancia a fallos o las dos. La **redundancia** es guardar los datos más de una vez para no perderlos si un disco falla. **Un RAID no es una copia de seguridad:** si se borra un archivo, se borra en todos los discos.

| Nivel | Cómo funciona | Si falla un disco | Discos mínimos |
|---|---|---|---|
| RAID 0 | Reparte los datos entre los discos: más velocidad | Se pierde todo | 2 |
| RAID 1 | Copia los mismos datos en cada disco (espejo) | Sigue funcionando | 2 |
| RAID 5 | Reparte los datos y un cálculo de **paridad** que permite reconstruir lo perdido | Aguanta el fallo de 1 disco | 3 |
| RAID 6 | Como el 5, con doble paridad | Aguanta el fallo de 2 discos | 4 |
| RAID 10 | Un RAID 0 de varios RAID 1 | Aguanta un fallo en cada espejo | 4 |

---

## 5. Tarjetas de expansión

**En una frase:** las ranuras **PCI Express** permiten añadir tarjetas a la placa: gráfica, red, sonido o más puertos.

**Lo que tienes que saber**

- **PCI Express (PCIe)** es el bus de alta velocidad de las ranuras de expansión y de los SSD NVMe. Las ranuras son **x1, x4, x8 o x16** según cuántas líneas (carriles) tengan: más líneas, más velocidad y ranura más larga. Cada versión (PCIe 3.0, 4.0, 5.0) duplica la velocidad de la anterior. Las antiguas **PCI** y **AGP** ya no se usan.
- **Tarjeta gráfica.** Tiene su propio procesador, la **GPU**, y su propia memoria (GDDR). Puede ser **integrada** (dentro del procesador, compartiendo la RAM) o **dedicada** (una tarjeta en la ranura PCIe x16, mucho más potente). Salidas: HDMI, DisplayPort, USB-C y, en equipos antiguos, DVI y VGA. Fabricantes: NVIDIA, AMD e Intel.
- **Tarjeta de red** (*NIC*). Conecta el equipo a una red, por cable (RJ-45) o inalámbrica (wifi). Tiene una dirección física fija, la **MAC**: 48 bits escritos como 12 cifras hexadecimales, por ejemplo `A4-5E-60-12-34-56`.
- Otras: **sonido**, **capturadoras de vídeo** y **tarjetas de ampliación**, que añaden puertos USB, SATA o M.2.

---

## 6. Periféricos y conectores

*Para la práctica: pasos 3, 5 y 6 del proyecto.*

**En una frase:** los periféricos comunican el equipo con el exterior; se conectan por un puerto, casi siempre USB, o sin cables, y cada uno necesita su driver.

**Lo que tienes que saber**

- **Clasificación:**

  | De entrada | De salida | De entrada/salida (mixtos) |
  |---|---|---|
  | Teclado, ratón, *touchpad*, escáner, *webcam*, micrófono, *joystick* | Monitor, impresora, altavoces y auriculares | Pantalla táctil, impresora multifunción, discos externos, pendrive, auriculares con micrófono, el móvil conectado al equipo |

- **USB** (*Universal Serial Bus*) es el conector por excelencia: transmite datos y corriente, y admite conectar y desconectar en marcha. Los conectores son **tipo A** (el rectangular), **tipo C** (reversible, el actual), **micro-USB** y **mini-USB** (antiguos).
- **Otros conectores externos:** vídeo (**HDMI**, **DisplayPort**; antiguos, VGA y DVI), red (**RJ-45**, Ethernet), audio (**minijack** de 3,5 mm: verde salida, rosa micrófono, azul entrada de línea; **S/PDIF**, digital) y **Thunderbolt** (por USB-C: datos, vídeo y carga). **PS/2**, para teclado y ratón, ya no se usa.
- **Bluetooth:** conexión inalámbrica de corto alcance, para auriculares, teclados, ratones o el móvil.
- **Monitor:** **tamaño** (diagonal en pulgadas, 1″ = 2,54 cm), **resolución** (Full HD 1920 × 1080, 4K 3840 × 2160), **densidad** (píxeles por pulgada, ppp), **frecuencia de refresco** (Hz: veces por segundo que se redibuja la imagen) y **tecnología**: **LCD** con retroiluminación LED (asequible, pero no logra el negro puro) u **OLED** (cada píxel emite su luz: negro puro y más contraste, más caro).
- **Impresora:** de **inyección de tinta** (cartuchos) o **láser** (tóner: más rápida y más barata por página). La calidad se mide en **ppp** y la velocidad, en páginas por minuto (**ppm**).

**Compara: las versiones de USB**

| Versión | Velocidad máxima | Color del puerto (habitual) |
|---|---|---|
| USB 2.0 | 480 Mb/s | Negro o blanco |
| USB 3.2 Gen 1 (antes USB 3.0) | 5 Gb/s | Azul |
| USB 3.2 Gen 2 (antes USB 3.1) | 10 Gb/s | Azul claro o turquesa |
| USB 3.2 Gen 2x2 | 20 Gb/s | Solo USB-C |
| USB4 | 40 Gb/s | Solo USB-C |

Un puerto rojo o amarillo suele indicar que da carga aunque el equipo esté apagado. Un dispositivo USB funciona en cualquier puerto, pero a la velocidad del más lento de los dos. **Mb/s** son megabits por segundo; un byte son 8 bits.

### El móvil como periférico

- Un móvil tiene el mismo esquema que un ordenador (procesador, RAM, almacenamiento flash, pantalla), pensado para **gastar poco**: procesador **ARM**, todo integrado en un solo chip, batería y sin ventilador.
- Conectado por USB, **el móvil decide qué tipo de dispositivo es**, según el modo que se elija en su pantalla. Para el ordenador, cada modo es un dispositivo distinto, con su propio driver:

| Modo en Android | Qué es para el ordenador | Dónde aparece en Windows |
|---|---|---|
| Solo carga (*sin transferencia de datos*) | Ningún dispositivo de datos: solo toma corriente | En ningún sitio |
| **Transferencia de archivos** (MTP) | Un **dispositivo portátil**: se ven sus carpetas, pero no es un disco | *Dispositivos portátiles* |
| Fotos (PTP) | Una **cámara** | *Dispositivos portátiles* o *Cámaras* |
| **Compartir conexión por USB** | Una **tarjeta de red**: el ordenador sale a internet por el móvil | *Adaptadores de red* |

En un iPhone, al conectarlo pregunta **¿Confiar en este ordenador?**; sin aceptar, solo carga.

---

## 7. Ver el hardware de un equipo

*Para la práctica: pasos 1 a 6 del proyecto.*

**En una frase:** el sistema operativo sabe qué hardware tiene el equipo y lo muestra con sus herramientas; no hace falta abrirlo.

**En Windows**

| Herramienta | Cómo se abre | Qué muestra |
|---|---|---|
| **Administrador de tareas**, pestaña **Rendimiento** | `Ctrl + Mayús + Esc` | **CPU:** modelo, velocidad base, zócalos, núcleos, procesadores lógicos, caché y si la virtualización está activada. **Memoria:** capacidad, velocidad (MT/s), ranuras usadas y factor de forma (DIMM o SO-DIMM). **Disco:** capacidad y tipo (HDD, SSD o SSD NVMe). **GPU:** modelo y su memoria |
| **Información del sistema** | `Windows + R`, `msinfo32` | Fabricante y modelo del equipo, procesador, fabricante y modelo de la placa base, versión del firmware, modo de arranque (UEFI) y memoria instalada |
| **Administrador de dispositivos** | Clic derecho en Inicio, o `devmgmt.msc` | Todos los dispositivos, agrupados por tipo, con su driver. Un aviso amarillo: falta el driver o falla |
| **Administración de discos** | Clic derecho en Inicio, o `diskmgmt.msc` | Los discos y sus particiones |
| `ipconfig /all` | En el terminal | Las tarjetas de red, con su **dirección física** (la MAC) |
| `Get-CimInstance Win32_PhysicalMemory` | En el terminal (PowerShell) | Cada módulo de RAM: fabricante, referencia (*PartNumber*), velocidad y capacidad |

**En Linux**

| Orden | Qué muestra |
|---|---|
| `lscpu` | El procesador: arquitectura, modelo, núcleos, hilos por núcleo, caché y, si es una máquina virtual, el hipervisor |
| `free -h` | La memoria: total, usada y libre |
| `lsblk -d -o NAME,SIZE,ROTA,TRAN,MODEL` | Los discos: tamaño, si es de platos (`ROTA` 1) o no (0), cómo se conecta (`TRAN`: sata, nvme, usb) y su modelo |
| `lspci` | Los dispositivos conectados por PCI Express: chipset, gráfica, red, controladores de disco y de USB |
| `lsusb` | Los dispositivos USB conectados |
| `sudo dmesg` | Los mensajes del kernel: entre ellos, lo que pasa al conectar un dispositivo |
| `ip -br link` | Las tarjetas de red, con su MAC |

En una **máquina virtual**, estas herramientas muestran el hardware que **simula el hipervisor**, no el del ordenador real: un disco `VBOX HARDDISK`, una gráfica `VMware SVGA II`, un chipset de los años 90 (UD2, «El hardware de una máquina virtual»). El procesador sí es el real, aunque solo con los núcleos que se le han dado.

---

## 8. Mantenimiento y seguridad al manipular un equipo

*Para la práctica: paso 7 del proyecto.*

**En una frase:** antes de abrir un equipo se desconecta y se descarga la electricidad estática; los componentes se cogen por los bordes y no se fuerzan.

**Lo que tienes que saber**

- **Mantenimiento preventivo**, para evitar averías: limpiar por fuera, protegerlo del polvo, mantener una temperatura y una humedad adecuadas, y conectarlo a un **SAI** (*Sistema de Alimentación Ininterrumpida*), que da corriente durante un corte y protege de los picos de tensión.
- **Mantenimiento con el equipo abierto:** limpiar el polvo del interior con pincel o aire comprimido y cambiar la **pasta térmica** del procesador, que transmite el calor al disipador y se seca con los años.
- **Herramientas:** destornilladores de la medida de cada tornillo, pinzas, **multímetro** (mide tensión en voltios, corriente en amperios y resistencia en ohmios: por ejemplo, la pila de la placa debe dar unos 3 V), comprobador de fuentes y soldador.

**Antes de abrir y al manipular**

1. **Apagar** desde el sistema y **desconectar** el cable de corriente (y, en un portátil, la batería si se puede). Pulsar el botón de encendido unos segundos con el equipo desconectado descarga lo que queda.
2. **Descargar la electricidad estática** del cuerpo: pulsera antiestática conectada al chasis, o tocar una parte metálica sin pintar de la caja. Una descarga que no se nota puede estropear un chip.
3. Trabajar en una mesa **despejada, seca y bien iluminada**, sin alfombra, y guardar los tornillos ordenados.
4. Coger los componentes **por los bordes**, sin tocar los contactos ni los chips, y guardarlos en su **bolsa antiestática**.
5. **No forzar nada:** la RAM entra en una sola posición, por la muesca; las patillas de un procesador PGA se doblan con facilidad.
6. **No abrir nunca la fuente de alimentación:** sus condensadores guardan carga peligrosa aunque esté desconectada.
7. Antes de cerrar, comprobar que todos los cables están conectados y no tocan los ventiladores.

---

## Dónde consultar

- **Intel**: fichas de cada procesador en [Intel ARK](https://ark.intel.com/content/www/es/es/ark.html); **AMD**: [especificaciones de procesadores](https://www.amd.com/es/products/specifications/processors.html).
- **Android**: [usar el móvil para compartir conexión por USB](https://support.google.com/android/answer/9059108?hl=es).
- **Prevención de riesgos**: [Real Decreto 488/1997](https://www.boe.es/buscar/act.php?id=BOE-A-1997-8671) (pantallas de visualización), del apartado 9 de los apuntes de la semana del 2 al 6.
