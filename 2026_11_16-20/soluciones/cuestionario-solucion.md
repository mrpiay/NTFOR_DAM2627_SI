# Autoevaluación · semana del 16 al 20 de noviembre · soluciones

Entre paréntesis, dónde está la respuesta para repasarla.

## Cuestiones sobre el proyecto

**1.** En el Administrador de tareas, un procesador muestra 8 núcleos y 16 procesadores lógicos. ¿Qué es un núcleo y qué es un procesador lógico? ¿Cuántos hilos lleva cada núcleo? ¿Qué muestra tu equipo?

**Respuesta.** *(UD1 esta semana, apartado 2; proyecto, paso 1)* Un **núcleo** es una CPU completa dentro del chip, que ejecuta su propio programa a la vez que las demás. Un **procesador lógico** es cada unidad de procesamiento que el sistema operativo reconoce y puede utilizar para ejecutar hilos de software: con 2 hilos por núcleo, el sistema reconoce el doble de procesadores lógicos que núcleos. Con 8 núcleos y 16 procesadores lógicos, cada núcleo lleva **2 hilos**. La última parte depende de cada equipo: los datos son los de *Rendimiento → CPU* del propio ordenador.

**2.** La memoria de un portátil aparece así: DDR4, 3200 MT/s, ranuras usadas 1 de 2, factor de forma SODIMM. ¿A cuántos MHz va su reloj, y por qué? ¿Se puede ampliar? ¿Qué módulo habría que comprar? ¿Qué querría decir que el factor de forma fuera *Row of chips*?

**Respuesta.** *(UD1 esta semana, apartado 3; proyecto, pasos 1 y 7)* El reloj va a **1600 MHz**: la DDR hace dos transferencias por ciclo, así que los MT/s son el doble de los MHz (3200 / 2). **Se puede ampliar**: hay una ranura libre. Habría que comprar un módulo **DDR4 SO-DIMM** (SO-DIMM porque es un portátil), de **3200 MT/s**, y mejor de la misma capacidad que el que tiene, para que funcionen en doble canal. *Row of chips* querría decir que la memoria va **soldada** a la placa: no hay módulos ni ranuras, y no se puede ampliar.

**3.** ¿Con qué herramienta de Windows se ven el fabricante y el modelo de la placa base y la versión del firmware? ¿Y si el disco es HDD, SSD o SSD NVMe? ¿Qué diferencia hay entre un SSD SATA y uno NVMe?

**Respuesta.** *(UD1 esta semana, apartados 4 y 7; proyecto, paso 2)* La placa base y el firmware se ven en **Información del sistema** (`msinfo32`): *Fabricante* y *Producto de placa base*, y *Versión y fecha de BIOS*. El tipo de disco, en el **Administrador de tareas**, *Rendimiento → Disco*: el campo *Tipo*. Un SSD **SATA** usa el bus SATA y llega a unos 550 MB/s; un SSD **NVMe** va por **PCI Express**, en formato M.2, y llega a varios GB/s.

**4.** En la máquina virtual, `lscpu` muestra el mismo modelo de procesador que tu ordenador, pero `lspci` muestra una gráfica `VMware SVGA II` y un chipset `440FX`, y `lsblk` un disco `VBOX HARDDISK`. ¿Por qué coincide el procesador y lo demás no?

**Respuesta.** *(UD1 esta semana, apartado 7; UD2, apartado 5; proyecto, paso 4)* El **procesador** de la máquina virtual es el real: el hipervisor deja que la máquina ejecute sus instrucciones directamente en él (virtualización por hardware), aunque solo con los procesadores que se le dieron. El resto del hardware lo **simula** VirtualBox: la gráfica, el chipset y el disco son dispositivos virtuales, que no existen en el ordenador. El disco, por ejemplo, es el archivo `.vdi`.

**5.** Un móvil Android aparece en Windows en *Dispositivos portátiles* en el modo de transferencia de archivos, y en *Adaptadores de red* en el de compartir conexión. ¿Por qué? En la máquina virtual, ¿con qué órdenes lo viste, y qué cambió al cambiar de modo?

**Respuesta.** *(UD1 esta semana, apartado 6; proyecto, pasos 5 y 6)* Porque, según el modo que se elige en el móvil, **el móvil se presenta como un dispositivo distinto**: en transferencia de archivos, como un dispositivo portátil (MTP); al compartir conexión, como una **tarjeta de red**. Para el sistema son dispositivos distintos, cada uno con su driver. En la máquina virtual se ve con `lsusb` (el fabricante y el producto, con sus números `ID fabricante:producto`) y `sudo dmesg` (lo que vio el kernel al conectarlo). Al cambiar a compartir conexión, cambia el **número de producto** de `lsusb` y aparece una **tarjeta de red nueva** en `ip -br link`.

## Cuestiones sobre los apuntes

**6.** Escribe en orden los pasos para cambiar un módulo de RAM de un ordenador de sobremesa con seguridad. ¿Por qué no se debe abrir nunca la fuente de alimentación?

**Respuesta.** *(UD1 esta semana, apartado 8; UD1 semana del 2 al 6, apartado 9)* Apagar desde el sistema y **desconectar** el cable de corriente; pulsar unos segundos el botón de encendido para descargar lo que queda; **descargarse de electricidad estática** (pulsera antiestática al chasis o tocar una parte metálica sin pintar); abrir la caja en una mesa despejada y seca, guardando los tornillos; abrir las pestañas de la ranura y sacar el módulo **cogiéndolo por los bordes**; colocar el nuevo con la **muesca** alineada, sin forzar, hasta que cierren las pestañas; cerrar y comprobar en el sistema (Administrador de tareas o `msinfo32`) que reconoce la memoria. La fuente no se abre porque sus **condensadores** guardan una carga peligrosa aunque esté desconectada.

**7.** ¿Se puede montar una placa Mini-ITX en una caja ATX? ¿Y una ATX en una caja para Mini-ITX? ¿Qué conector de la fuente alimenta la placa base y cuál el procesador? ¿Qué pasa si la fuente no tiene potencia suficiente?

**Respuesta.** *(UD1 esta semana, apartado 1)* **Sí**: una caja ATX admite placas más pequeñas del mismo estándar (Micro-ATX, Mini-ITX), porque coinciden los tornillos. **No** al revés: una placa ATX no cabe en una caja para Mini-ITX. La placa se alimenta con el conector **ATX de 24 pines** y el procesador, con el de **4 u 8 pines** (EPS). Si la fuente no tiene potencia suficiente, el equipo no arranca o se apaga cuando trabaja con carga.

**8.** Calcula la latencia en nanosegundos de una DDR5-6000 CL30 y de una DDR4-3200 CL16. ¿Cuál responde antes? ¿Por qué no basta con comparar el CL?

**Respuesta.** *(UD1 esta semana, apartado 3)* DDR5-6000: el reloj va a 3000 MHz, un ciclo dura 1 / 3000 MHz ≈ 0,333 ns, y 30 ciclos son **10 ns**. DDR4-3200: 1600 MHz, 0,625 ns por ciclo, y 16 ciclos son **10 ns**. **Responden igual de rápido.** No basta con el CL porque es un número de **ciclos**, y lo que dura un ciclo depende de la frecuencia: una memoria más rápida tiene ciclos más cortos, y un CL más alto puede ser el mismo tiempo.

**9.** Una pequeña empresa quiere que, si se estropea un disco de su servidor, no se pierda nada. ¿Qué RAID usaría con 2 discos? ¿Y con 3? ¿Por qué un RAID no sustituye a las copias de seguridad?

**Respuesta.** *(UD1 esta semana, apartado 4)* Con 2 discos, **RAID 1** (espejo): los dos tienen los mismos datos y, si uno falla, el otro sigue. Con 3 discos, **RAID 5**: reparte los datos y la paridad y aguanta el fallo de un disco, con más capacidad útil que un espejo. Un RAID no es una copia de seguridad porque protege del fallo de un disco, no de los errores: si se borra o se estropea un archivo, se borra o se estropea en todos los discos a la vez.

**10.** Un pendrive USB 3.2 Gen 1 se conecta a un puerto USB 2.0: ¿a qué velocidad máxima funciona? ¿Cómo se distinguen esos puertos a simple vista? Clasifica como de entrada, de salida o de entrada/salida: una pantalla táctil, una *webcam*, una impresora multifunción, unos altavoces y un móvil conectado al ordenador.

**Respuesta.** *(UD1 esta semana, apartado 6)* A la velocidad del más lento: **480 Mb/s**, la de USB 2.0. Por fuera, el puerto USB 2.0 suele ser **negro** (o blanco) y el USB 3.2 Gen 1, **azul**. **Entrada:** la *webcam*. **Salida:** los altavoces. **Entrada/salida:** la pantalla táctil (muestra y recibe), la impresora multifunción (imprime y escanea) y el móvil conectado (envía y recibe datos).

