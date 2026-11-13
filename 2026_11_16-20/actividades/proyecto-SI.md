# SI · Proyecto guiado «Mi equipo por dentro»

## Punto de partida

Antes de comprar, ampliar o reparar un ordenador hay que saber qué tiene dentro: qué procesador, cuánta memoria y de qué tipo, qué disco, qué se le puede añadir. Este proyecto lo averigua **sin abrir el equipo**, con las herramientas del sistema operativo, sobre tu propio ordenador. Después lo compara con el hardware de la máquina virtual de la semana pasada y conecta un periférico, el móvil, para ver cómo lo reconocen Windows y Linux.

Es la **UD1 · Sistemas informáticos. Hardware y software**: componentes, memorias, periféricos y seguridad, en un equipo real.

**Usa la IA como guía, no para que lo haga por ti.** Pídele que te explique lo que no entiendas; **lo que se mira en el equipo lo miras tú**, y los datos de la ficha son **los de tu ordenador**. El objetivo es que lo que hagas **cumpla los requisitos** de cada paso («Comprueba que…») y que sepas **qué significa cada dato** de tu equipo.

**El objetivo es entender cada paso:** es lo que necesitas para responder el cuestionario y preparar los exámenes.

**Evaluación.** Esta actividad guiada (**A3**) se evalúa con su lista de cotejo: cada «Comprueba que…» se cumple o no. El cuestionario de la semana (**C3**) se entrega hasta el lunes 23 de noviembre. El **viernes 4 de diciembre** hay un examen parcial, **P1**, en papel, con todo lo de la 1ª evaluación, también esta actividad: los componentes de un equipo y sus características, cómo se averiguan, los periféricos y sus drivers, y la seguridad al manipular un equipo. Qué entra y cuánto vale cada parte: [1ª evaluación](../../programacion/1a-evaluacion.md).

---

## Antes de empezar

La teoría está en los [apuntes de esta semana](../apuntes/UD1-el-equipo-por-dentro.md), que continúan los [apuntes de la UD1 de la semana del 2 al 6](../../2026_11_02-06/apuntes/UD1-hardware-y-software.md). Antes de cada paso, lee el apartado que le corresponde:

| Pasos | Apartado de los apuntes de esta semana |
|---|---|
| 1 | 2 · El procesador en detalle, y 3 · La memoria RAM en detalle |
| 2 | 1 · Caja, fuente y placa, y 4 · El almacenamiento en detalle |
| 3 | 5 · Tarjetas de expansión, y 6 · Periféricos y conectores |
| 4 | 7 · Ver el hardware de un equipo, la parte de Linux |
| 5 y 6 | 6 · Periféricos y conectores: «El móvil como periférico» |
| 7 | 8 · Mantenimiento y seguridad al manipular un equipo |

Las herramientas de cada paso están resumidas en el apartado 7 de los apuntes.

---

## Las herramientas

| Herramienta | Qué es | Pasos |
|---|---|---|
| **Las herramientas de Windows** | Administrador de tareas, Información del sistema (`msinfo32`), Administrador de dispositivos y el terminal | 1, 2, 3 y 5 |
| **La máquina virtual `ubuntu-arranque`** | La del proyecto de la semana del 9 al 13, en VirtualBox | 4 y 6 |
| **Tu móvil y su cable USB** | El periférico. Sirve Android o iPhone; el cable tiene que ser de datos (el de la caja del móvil lo es) | 5 y 6 |
| **`mi-equipo.md`** | Un archivo de texto donde apuntas la ficha de tu equipo. Se crea en el paso 0 | Todos |

En este proyecto **solo se mira**: no se cambia ninguna opción de Windows, del firmware ni de los dispositivos, y no se abre el ordenador.

La guía está probada con **Windows 11** y **VirtualBox 7.2**, los dos en inglés: los nombres de menús y botones van en inglés y, entre paréntesis, en español.

## Qué se trabaja

| Qué | Pasos |
|---|---|
| El procesador y la memoria de un equipo real, y qué significa cada dato | 1 |
| La placa base, el firmware y los discos | 2 |
| La gráfica, la red y los dispositivos con su driver | 3 |
| El hardware de una máquina virtual, comparado con el real | 4 |
| Un periférico USB: cómo cambia el dispositivo y el driver según su modo, en Windows y en Linux | 5 y 6 |
| Qué se puede ampliar en un equipo y cómo se manipula con seguridad | 7 |

## Plan de la semana

Cada sesión dura 50 minutos.

| Día | Sesión | Qué se hace |
|---|---|---|
| Martes 17 | 13:00 | Leer los apartados 2 y 3 de los apuntes. **Paso 0** (preparar la ficha) y **paso 1** (procesador y memoria). |
| Martes 17 | 13:50 | **Paso 2** (placa, firmware y discos) y **paso 3** (gráfica, red y dispositivos). |
| Jueves 19 | 10:10 | **Paso 4** (el mismo inventario en la máquina virtual). |
| Jueves 19 | 11:00 | **Paso 5** (el móvil en Windows). |
| Viernes 20 | 08:30 | **Paso 6** (el móvil en la máquina virtual). |
| Viernes 20 | 09:20 | **Paso 7** (qué se puede ampliar y cómo se haría con seguridad). Repasar con la lista final («Cómo comprobarlo»). |

**Los pasos se hacen en orden**, cada uno en la sesión que le toca según el plan de la semana.

---

## Paso 0 · Preparar la ficha

**Objetivo.** Un archivo `mi-equipo.md` con la ficha vacía de tu ordenador, para rellenarla en los pasos siguientes.

**Pista.** Crea una carpeta `C:\dam2627\si\mi-equipo`, ábrela en VS Code (*File > Open Folder…*) y crea dentro el archivo `mi-equipo.md` con este contenido:

```markdown
# Mi equipo

Equipo: (fabricante y modelo)

| Componente | Modelo | Características | Dónde lo he visto |
|---|---|---|---|
| Procesador | | | |
| Memoria RAM | | | |
| Placa base | | | |
| Firmware | | | |
| Disco | | | |
| Gráfica | | | |
| Red | | | |

## La máquina virtual

## El móvil como periférico

## Qué se le puede ampliar
```

**Comprueba que…** tienes `mi-equipo.md` abierto en VS Code, con la tabla vacía.

---

## Paso 1 · El procesador y la memoria

**Objetivo.** Apuntar en la ficha el procesador y la memoria de tu equipo, y saber qué significa cada dato.

**Pista.**

1. Abre el **Administrador de tareas** (*Task Manager*): `Ctrl + Mayús + Esc`. Ve a la pestaña **Performance** (*Rendimiento*), el segundo icono de la izquierda.
2. Pulsa **CPU**. Arriba a la derecha está el **modelo** del procesador. Abajo, apunta:
   - **Base speed** (*Velocidad base*): su frecuencia, en GHz;
   - **Sockets** (*Sockets*): cuántos procesadores físicos tiene la placa, casi siempre 1;
   - **Cores** (*Núcleos*) y **Logical processors** (*Procesadores lógicos*): si los lógicos son el doble que los núcleos, cada núcleo lleva dos hilos;
   - **L1, L2 y L3 cache** (*Caché L1, L2 y L3*);
   - **Virtualization** (*Virtualización*): `Enabled` (*Habilitado*), como se comprobó para la máquina virtual.
3. Pulsa **Memory** (*Memoria*). Apunta la capacidad (arriba a la derecha) y, abajo:
   - **Speed** (*Velocidad*), en MT/s;
   - **Slots used** (*Ranuras usadas*), por ejemplo `2 of 2` (*2 de 2*): cuántos módulos hay y cuántas ranuras tiene la placa;
   - **Form factor** (*Factor de forma*): `DIMM` en un sobremesa, `SODIMM` en un portátil. Si no sale, o sale `Row of chips`, la memoria va **soldada** a la placa.
4. Para saber el **tipo y la referencia** de cada módulo, abre el terminal (clic derecho en Inicio → **Terminal**) y escribe:

   ```powershell
   Get-CimInstance Win32_PhysicalMemory | Format-Table Manufacturer, PartNumber, Speed, Capacity
   ```

   Sale una línea por módulo: fabricante, referencia (*PartNumber*), velocidad y capacidad en bytes (8589934592 bytes son 8 GB). Busca la referencia en internet: la ficha del fabricante dice si es **DDR4 o DDR5** y su **latencia CL**.
5. Rellena las filas **Procesador** y **Memoria RAM** de la ficha. En «Características», escribe los datos y, para el procesador, si es **x86_64 o ARM** (Intel y AMD son x86_64) y **cuántos hilos por núcleo**.

**Comprueba que…**

- en la ficha están el modelo del procesador, su frecuencia base, sus núcleos, sus procesadores lógicos y su caché, y sabes explicar la diferencia entre núcleo y procesador lógico;
- en la ficha están la capacidad, el tipo (DDR4 o DDR5), la velocidad en MT/s, los módulos y las ranuras de la memoria, y sabes calcular a cuántos MHz va su reloj ([apuntes, apartado 3](../apuntes/UD1-el-equipo-por-dentro.md#3-la-memoria-ram-en-detalle)).

**Si te falla…**

- *En `PartNumber` sale vacío o un texto genérico*: algunos fabricantes no lo rellenan, sobre todo con la memoria soldada. Apunta lo que sale en el Administrador de tareas y busca la ficha del modelo del portátil en la web de su fabricante: dice el tipo de memoria.
- *El Administrador de tareas se abre pequeño, sin pestañas*: pulsa **More details** (*Más detalles*).

---

## Paso 2 · La placa base, el firmware y los discos

**Objetivo.** Apuntar en la ficha la placa base, el firmware y los discos.

**Pista.**

1. Pulsa `Windows + R`, escribe `msinfo32` e **Intro**. En **System Summary** (*Resumen del sistema*), apunta:
   - **System Manufacturer** y **System Model** (*Fabricante* y *Modelo del sistema*): el equipo, en la primera línea de la ficha;
   - **BaseBoard Manufacturer** y **BaseBoard Product** (*Fabricante* y *Producto de placa base*): la placa;
   - **BIOS Version/Date** (*Versión y fecha de BIOS*) y **BIOS Mode** (*Modo de BIOS*): el firmware y si arranca con UEFI;
   - **Installed Physical Memory (RAM)** (*Memoria física instalada*): tiene que coincidir con el paso 1.
2. En el Administrador de tareas, pestaña **Performance** (*Rendimiento*), pulsa **Disk 0** (*Disco 0*). Arriba a la derecha está el modelo; abajo, la **Capacity** (*Capacidad*) y el **Type** (*Tipo*): `HDD`, `SSD` o `SSD (NVMe)`. Si tienes más discos, salen como *Disk 1*, *Disk 2*…
3. Busca en internet el modelo de la placa (o, en un portátil, el del equipo) y abre su **ficha técnica** o su manual en la web del fabricante. Apunta su **factor de forma** (en un sobremesa) y cuántas **ranuras de RAM** y **ranuras M.2** tiene.
4. Rellena las filas **Placa base**, **Firmware** y **Disco**.

**Comprueba que…**

- en la ficha están el fabricante y modelo del equipo y de la placa, la versión del firmware y su modo (UEFI), y el disco con su capacidad y su tipo;
- sabes decir si tu disco va por SATA o por NVMe y qué diferencia hay ([apuntes, apartado 4](../apuntes/UD1-el-equipo-por-dentro.md#4-el-almacenamiento-en-detalle)).

**Si te falla…**

- *En `BaseBoard Product` sale «Not Available» o un código*: es habitual en portátiles. Usa el modelo del equipo (`System Model`) para buscar su ficha.

---

## Paso 3 · La gráfica, la red y los dispositivos

**Objetivo.** Apuntar la gráfica y la tarjeta de red, y ver cómo organiza Windows los dispositivos y sus drivers.

**Pista.**

1. En el Administrador de tareas, pestaña **Performance** (*Rendimiento*), pulsa **GPU 0**. Arriba a la derecha está el modelo. Si sale **Dedicated GPU memory** (*Memoria de GPU dedicada*) con varios GB, es una gráfica **dedicada**; si solo tiene **Shared GPU memory** (*Memoria de GPU compartida*), es **integrada** en el procesador. Si hay una *GPU 1*, el equipo tiene las dos.
2. Abre el terminal y escribe:

   ```
   ipconfig /all
   ```

   Busca el adaptador **Wi-Fi** y, si lo tiene, el **Ethernet**. En cada uno, **Description** (*Descripción*) es el modelo de la tarjeta y **Physical Address** (*Dirección física*), su **MAC**. Apunta las dos tarjetas en la fila **Red**.
3. Abre el **Administrador de dispositivos** (*Device Manager*): clic derecho en Inicio. Despliega **Processors** (*Procesadores*), **Disk drives** (*Unidades de disco*), **Display adapters** (*Adaptadores de pantalla*) y **Network adapters** (*Adaptadores de red*): son los mismos componentes de la ficha.
4. Haz doble clic en la gráfica → pestaña **Driver** (*Controlador*). Apunta el **proveedor** y la **versión** del driver. Cierra con **Cancel** (*Cancelar*), sin pulsar ningún botón de la pestaña.
5. Comprueba si algún dispositivo tiene un **aviso amarillo**: a ese le falta el driver o le falla.
6. Rellena las filas **Gráfica** y **Red**, y en «Dónde lo he visto» la herramienta de cada dato.

**Comprueba que…**

- en la ficha están la gráfica, si es integrada o dedicada, y las tarjetas de red con su MAC;
- sabes explicar qué es la MAC y cuántos bits tiene, y qué indica un aviso amarillo en el Administrador de dispositivos.

**Si te falla…**

- *Ves `Media disconnected` en el adaptador Ethernet*: no tiene cable conectado. La MAC se ve igual.
- *Hay varios adaptadores que no conoces* (*Bluetooth*, *Hyper-V*, *VirtualBox Host-Only*…): son tarjetas de red virtuales, creadas por programas. Apunta solo las físicas: Wi-Fi y Ethernet.

---

## Paso 4 · El mismo inventario en la máquina virtual

**Objetivo.** Ver el hardware de la máquina `ubuntu-arranque` con las órdenes de Linux y compararlo con el real.

**Pista.** Arranca la máquina `ubuntu-arranque` (desde **Current State**) y entra. Escribe estas órdenes, una a una:

1. **El procesador:**

   ```bash
   lscpu
   ```

   Mira **Architecture** (`x86_64`), **Model name** (el modelo: ¡es el de tu procesador real!), **CPU(s)** (los procesadores que tiene la máquina: 2, los que le diste en VirtualBox), **Thread(s) per core**, **Hypervisor vendor** (`KVM`: Linux sabe que está en una máquina virtual) y las cachés.
2. **La memoria y el disco:**

   ```bash
   free -h
   lsblk -d -o NAME,SIZE,ROTA,TRAN,MODEL
   ```

   `free -h`: unos 2 GB (`Mem: total`). `lsblk`: el disco `sda`, de 25 GB, por `sata` y con modelo `VBOX HARDDISK`.
3. **El resto del hardware:**

   ```bash
   lspci
   ```

   El chipset (`440FX`, `PIIX3`), la gráfica (`VMware SVGA II`), la red (`82540EM`), los controladores IDE y SATA, los de USB y uno propio de VirtualBox.
4. Completa el apartado **La máquina virtual** de la ficha con una tabla que compare las dos:

   ```markdown
   | Componente | Equipo real | Máquina virtual |
   |---|---|---|
   | Procesador | | |
   | Núcleos o procesadores | | |
   | Memoria | | |
   | Disco | | |
   | Gráfica | | |
   | Red | | |
   ```

**Comprueba que…**

- la tabla de la ficha compara los seis componentes del equipo real y de la máquina virtual;
- sabes explicar qué componente es el mismo en los dos (el modelo del procesador) y por qué los demás son distintos ([apuntes, apartado 7](../apuntes/UD1-el-equipo-por-dentro.md#7-ver-el-hardware-de-un-equipo)).

**Si te falla…**

- *`lsblk` no conoce alguna de las columnas*: escribe `lsblk -d` sin el resto; sale el tamaño. El modelo se ve con `lsblk -d -o NAME,MODEL`.

---

## Paso 5 · El móvil en Windows

**Objetivo.** Ver que un mismo periférico, el móvil, es para Windows un dispositivo distinto, con otro driver, según el modo USB que se elija.

**Pista.** Conecta el móvil al ordenador con su cable USB y desbloquéalo. Abre el **Administrador de dispositivos** y déjalo a la vista.

1. **Solo carga.** En Android, despliega las notificaciones y pulsa la de **USB** (algo como *Cargando este dispositivo por USB*). Elige **Sin transferencia de datos** (o *Solo carga*). En el Administrador de dispositivos no aparece nada nuevo: el móvil solo toma corriente.
2. **Transferencia de archivos.** Elige **Transferencia de archivos** (*File transfer*, MTP). Aparece en **Portable Devices** (*Dispositivos portátiles*) con el nombre del móvil. Haz doble clic → pestaña **Driver** (*Controlador*) y apunta el **proveedor** del driver. Abre el **Explorador de archivos**: el móvil sale en *Este equipo* y se ven sus carpetas, pero sin letra de unidad: no es un disco.
3. **Compartir conexión.** Elige **Compartir conexión por USB** (*USB tethering*; en algunos móviles está en *Ajustes → Red → Zona Wi-Fi/compartir conexión*). Ahora aparece en **Network adapters** (*Adaptadores de red*), con un nombre como *Remote NDIS based Internet Sharing Device*: para Windows, el móvil es una tarjeta de red. Desactívalo después.
4. **Con un iPhone:** al conectarlo, en el iPhone pulsa **Confiar** (*Trust*) y escribe el código. Aparece en **Portable Devices** como *Apple iPhone*. Haz el punto 2 y, en lugar del punto 3, apunta solo que en un iPhone el modo no se elige en una notificación.
5. En el apartado **El móvil como periférico** de la ficha, apunta en una tabla, para cada modo: dónde aparece en el Administrador de dispositivos y con qué nombre.

**Comprueba que…**

- la ficha tiene, para cada modo que has probado, dónde aparece el móvil en el Administrador de dispositivos;
- sabes explicar por qué el mismo móvil aparece como dispositivos distintos y qué tiene que ver con los drivers ([apuntes, apartado 6](../apuntes/UD1-el-equipo-por-dentro.md#el-móvil-como-periférico)).

**Si te falla…**

- *No sale la notificación de USB, o no aparece nada en ningún modo*: el cable solo sirve para cargar. Prueba con el de la caja del móvil, u otro de datos.
- *Al elegir transferencia de archivos, el Explorador no muestra carpetas*: desbloquea el móvil; con la pantalla bloqueada no deja ver sus archivos.

---

## Paso 6 · El móvil en la máquina virtual

**Objetivo.** Pasar el móvil a la máquina virtual y ver cómo lo reconoce Linux.

**Pista.** VirtualBox puede **pasar** un dispositivo USB del ordenador a la máquina virtual: mientras lo tiene la máquina, Windows deja de verlo.

1. En el móvil, elige **Transferencia de archivos**. Con la máquina `ubuntu-arranque` encendida y dentro de ella, mira primero qué USB tiene:

   ```bash
   lsusb
   ```

   Solo salen los controladores USB de la máquina (`Linux Foundation … root hub`) y, quizá, la tableta de VirtualBox.
2. Pasa el móvil a la máquina: en el menú de la ventana, **Devices → USB** (*Dispositivos → USB*) y marca el nombre de tu móvil. En el Administrador de dispositivos de Windows, el móvil desaparece.
3. En la máquina:

   ```bash
   lsusb
   sudo dmesg | tail -20
   ```

   `lsusb` muestra una línea nueva: el fabricante y el móvil, con dos números, por ejemplo `ID 18d1:4ee1`. El primero identifica al **fabricante** y el segundo, al **producto** (en este modo). `dmesg` muestra lo que vio el kernel al conectarlo: `New USB device found`, el fabricante (*Manufacturer*), el producto (*Product*) y la velocidad.
4. Con un **Android**, cambia el modo a **Compartir conexión por USB** (el móvil se desconecta y se vuelve a conectar solo) y repite:

   ```bash
   lsusb
   ip -br link
   ```

   El número de producto de `lsusb` ha cambiado, y `ip -br link` muestra una **tarjeta de red nueva** (con un nombre como `usb0` o `enx…`): Linux también lo ve ahora como una tarjeta de red. Vuelve a dejar el móvil en **Sin transferencia de datos**.
5. **Devuelve el móvil a Windows:** **Devices → USB** y desmarca el móvil.
6. Apunta en la ficha la línea de `lsusb` de cada modo y la tarjeta de red nueva.

**Comprueba que…**

- la ficha tiene la línea de `lsusb` del móvil y lo que mostró `dmesg` al conectarlo;
- con un Android, en la ficha están los dos números de `lsusb` de cada modo y la tarjeta de red de `ip -br link`, y sabes explicar por qué cambia el número de producto;
- el móvil ha vuelto a Windows.

**Si te falla…**

- *En **Devices → USB** no sale el móvil, o sale en gris*: en **Settings → USB** (*Configuración → USB*) de la máquina tiene que estar marcado **Enable USB Controller** (*Habilitar controlador USB*). Apaga la máquina para cambiarlo.
- *Sale `Failed to attach the USB device`*: otro programa de Windows está usando el móvil (el Explorador de archivos, un programa del fabricante). Ciérralos y repite.
- *`lsusb: command not found`*: instálalo con `sudo apt install usbutils`.

---

## Paso 7 · Qué se puede ampliar, y cómo se haría con seguridad

**Objetivo.** Decidir, con la ficha, qué se le podría ampliar a tu equipo y escribir cómo se haría con seguridad, **sin abrirlo**.

**Pista.**

1. Con lo apuntado en los pasos 1 y 2, responde en el apartado **Qué se le puede ampliar** de la ficha:
   - **Memoria:** ¿hay ranuras libres? ¿De qué tipo tendría que ser el módulo nuevo (DDR4 o DDR5, DIMM o SO-DIMM) y a qué velocidad? Si va soldada, no se puede ampliar.
   - **Disco:** ¿hay una ranura M.2 libre o una bahía para un disco SATA?
   - **Gráfica** (en un sobremesa): ¿hay una ranura PCIe x16 libre? ¿Tiene la fuente el conector de 6 u 8 pines?
2. Elige **una** de esas ampliaciones (si tu equipo no admite ninguna, la de la RAM) y escribe, en orden, los pasos para hacerla **con seguridad**, desde apagar el equipo hasta comprobar que el sistema la reconoce. Usa el apartado 8 de los apuntes.
3. Escribe con qué herramienta y en qué dato de los pasos 1 o 2 comprobarías después que la ampliación funciona.

**Comprueba que…**

- la ficha dice qué se puede ampliar en tu equipo, con el tipo exacto de componente que admitiría;
- los pasos de la ampliación elegida empiezan por apagar y desconectar, incluyen descargarse de electricidad estática y coger el componente por los bordes, y terminan comprobando con una herramienta del sistema que funciona.

---

## Entrega

Qué se entrega y cuándo: [`entrega.md`](entrega.md).

## Cómo comprobarlo (lista final)

| Comprobación | Hecho |
|---|---|
| Mi ficha tiene el procesador con su frecuencia, núcleos, procesadores lógicos y caché, y sé qué significa cada dato |  |
| Mi ficha tiene la memoria con su capacidad, tipo, velocidad, módulos y ranuras, y sé pasar de MT/s a MHz |  |
| Mi ficha tiene el equipo, la placa, el firmware y el disco con su tipo, y sé diferenciar SATA de NVMe |  |
| Mi ficha tiene la gráfica (integrada o dedicada) y las tarjetas de red con su MAC |  |
| Sé ver los dispositivos y sus drivers en el Administrador de dispositivos y qué significa un aviso amarillo |  |
| Comparé el hardware de mi equipo con el de la máquina virtual y sé por qué solo coincide el procesador |  |
| Vi el móvil en Windows en varios modos USB y sé por qué cada uno es un dispositivo distinto |  |
| Pasé el móvil a la máquina virtual, lo vi con `lsusb` y `dmesg`, y lo devolví a Windows |  |
| Sé qué se le puede ampliar a mi equipo y los pasos para hacerlo con seguridad |  |
