# Sistemas Informáticos · 1º DAM · Examen parcial (P1) · Simulacro

- **Duración:** 1 hora y 30 minutos.
- **Tiempo medio de respuesta a cada apartado:** minuto y medio.
- Cada pregunta indica los puntos que vale: cada dato que se pide vale 0,5, y 0,25 cuando es un elemento de una lista. En total, 26 puntos; la nota, de 0 a 10, es proporcional: puntos obtenidos × 10 / 26.
- **Preguntas adicionales:** al final hay 8 preguntas optativas, de 1 punto cada una, para sustituir preguntas del examen que no se sepan. Sus puntos se suman a los demás, pero la nota no pasa de 26 puntos, es decir, de un 10.
- Debajo de cada pregunta, su respuesta: cada dato en una línea que empieza por lo que vale, entre corchetes.

---

## UD1 · Sistemas informáticos. Hardware y software (10,5 puntos)

### Componentes, memorias, sistemas de numeración y seguridad (7 puntos)

**1.** *(1,5 puntos)* ¿Cuáles son las tres partes de la CPU y qué hace cada una?

- **[0,25]** La **unidad de control**.
- **[0,25]** Lee e interpreta cada instrucción y da las órdenes para ejecutarla.
- **[0,25]** La **ALU**.
- **[0,25]** Hace las operaciones aritméticas y lógicas.
- **[0,25]** Los **registros**.
- **[0,25]** Son memorias diminutas y muy rápidas dentro de la CPU, con los datos con los que trabaja en cada momento.

**2.** *(1 punto)* Ordena de más rápida a más lenta: RAM, SSD, caché L1, registros y caché L3. ¿Cuáles se borran al apagar el equipo?

- **[0,5]** Registros → caché L1 → caché L3 → RAM → SSD.
- **[0,5]** Se borran los registros, las cachés y la RAM, porque son volátiles.

**3.** *(1,5 puntos)* Una memoria es DDR4-3600 CL18. ¿A cuántos MHz va su reloj, y por qué? Calcula su latencia en nanosegundos.

- **[0,5]** A **1800 MHz**.
- **[0,5]** Porque la DDR hace dos transferencias por ciclo: los MT/s son el doble de los MHz (3600 / 2).
- **[0,5]** Un ciclo dura 1 / 1800 MHz ≈ 0,556 ns, y 18 ciclos son **10 ns**.

**4.** *(1,5 puntos)* La memoria de un equipo aparece así en el Administrador de tareas: DDR4, 3200 MT/s, ranuras usadas 1 de 2, factor de forma SODIMM. ¿Para qué tipo de equipo es esa memoria, y por qué? ¿Se puede ampliar?

- **[0,5]** Para un **portátil**.
- **[0,5]** Porque el factor de forma es **SODIMM**, el módulo pequeño de los portátiles; los de sobremesa usan **DIMM**.
- **[0,5]** **Sí**, porque hay una ranura libre.

**5.** *(1 punto)* Una pequeña empresa quiere que, si se estropea uno de los 2 discos de su servidor, no se pierda nada. ¿Qué RAID usaría? ¿Por qué un RAID no sustituye a las copias de seguridad?

- **[0,5]** **RAID 1** (espejo): los dos discos tienen los mismos datos.
- **[0,5]** Un RAID protege del fallo de un disco, no de los errores: si se borra o se estropea un archivo, pasa en los dos discos a la vez.

**6.** *(0,5 puntos)* ¿Por qué no se debe abrir nunca la fuente de alimentación de un ordenador, aunque esté desconectada?

- **[0,5]** Porque sus **condensadores** guardan una carga eléctrica peligrosa aunque esté desconectada.

### Puesta en marcha de un equipo (1,5 puntos)

**7.** *(1,5 puntos)* ¿Qué es el POST? Si un ordenador pita al encenderlo y no da imagen, ¿en qué fase falla y dónde se mira qué significan los pitidos?

- **[0,5]** La comprobación del hardware (procesador, memoria, gráfica) que hace el firmware al encender, antes de buscar el sistema.
- **[0,5]** Falla en el **POST**.
- **[0,5]** Los pitidos se miran en el **manual del fabricante** de la placa base.

### Periféricos: clasificar, instalar y configurar (2 puntos)

**8.** *(1 punto)* ¿Qué es un driver? En Windows, ¿dónde se ve si a un dispositivo le falta el driver?

- **[0,5]** El programa que explica al sistema operativo cómo manejar un dispositivo.
- **[0,5]** En el **Administrador de dispositivos**, con una marca amarilla.

**9.** *(1 punto)* Clasifica como de entrada, de salida o de entrada/salida: un micrófono, una impresora con escáner, un proyector y una pantalla táctil.

- **[0,25]** Micrófono: **entrada**.
- **[0,25]** Impresora con escáner: **entrada/salida**, porque imprime y escanea.
- **[0,25]** Proyector: **salida**.
- **[0,25]** Pantalla táctil: **entrada/salida**, porque muestra y recibe.

## UD2 · Sistemas operativos. Instalación (15,5 puntos)

### Funciones, tipos, arquitectura, licencias y comparación de sistemas operativos (4,5 puntos)

**10.** *(1,5 puntos)* ¿Cuáles son las dos funciones de un sistema operativo? ¿Qué es el kernel?

- **[0,5]** Ofrecer una **interfaz** para usar el equipo.
- **[0,5]** **Gestionar los recursos** (procesador, memoria, dispositivos, archivos) entre los programas.
- **[0,5]** El kernel es la parte central: siempre está en memoria y es quien habla con el hardware.

**11.** *(1,5 puntos)* ¿En qué se diferencian un kernel monolítico y un microkernel? ¿De qué tipo es el de Linux?

- **[0,5]** En el **monolítico**, todo el sistema, también los drivers, funciona dentro del kernel: rápido, pero un fallo puede tirarlo todo.
- **[0,5]** En el **microkernel**, el kernel hace lo mínimo y el resto son programas aparte: más estable, pero más lento.
- **[0,5]** Linux es **monolítico, pero modular**: muchos drivers son módulos que el kernel carga solo cuando hacen falta.

**12.** *(1,5 puntos)* ¿Qué diferencia hay entre software libre y software propietario? La versión base de VirtualBox tiene licencia GPL: ¿con qué condición se puede publicar una versión modificada?

- **[0,5]** El **libre** se puede usar, estudiar (el código está disponible), modificar y redistribuir.
- **[0,5]** El **propietario** no da el código y limita el uso.
- **[0,5]** Que la versión modificada también sea **GPL** y se distribuya con su código fuente (*copyleft*).

### Planificar, virtualizar, actualizar, recuperar e instalar aplicaciones (7,5 puntos)

**13.** *(1,5 puntos)* ¿Qué tipos de hipervisores hay y en qué se diferencian? ¿De qué tipo es VirtualBox?

- **[0,5]** **Tipo 1**: funciona directamente sobre el hardware, sin sistema operativo debajo; se usa en servidores.
- **[0,5]** **Tipo 2**: funciona como un programa dentro de un sistema operativo.
- **[0,5]** VirtualBox es de **tipo 2**.

**14.** *(1,5 puntos)* ¿Cuántas particiones principales admiten las tablas MBR y GPT? ¿Por qué en un disco GPT no hay particiones lógicas?

- **[0,5]** MBR, **4**.
- **[0,5]** GPT, hasta **128** en Windows.
- **[0,5]** Porque no las necesita: las lógicas eran el truco de MBR para pasar de 4 particiones.

**15.** *(1,5 puntos)* Escribe en orden las fases del arranque de Ubuntu. Si al encender sale `grub>`, ¿en qué fase falla?

- **[0,25]** **Firmware** (POST y búsqueda en el orden de arranque).
- **[0,25]** **Gestor de arranque** (GRUB).
- **[0,25]** **Kernel**.
- **[0,25]** **systemd**.
- **[0,25]** **Inicio de sesión**.
- **[0,25]** `grub>` sale cuando falla la fase del **gestor de arranque**: GRUB arranca, pero no encuentra su configuración.

**16.** *(1,5 puntos)* ¿En qué archivo se cambia la configuración de GRUB y con qué orden se aplica? ¿Por qué no se edita `/boot/grub/grub.cfg` a mano?

- **[0,5]** En **`/etc/default/grub`**.
- **[0,5]** Se aplica con **`sudo update-grub`**.
- **[0,5]** Porque `update-grub` lo vuelve a generar, también en las actualizaciones, y se perdería lo escrito.

**17.** *(1,5 puntos)* ¿Qué hacen `sudo apt update` y `sudo apt upgrade`? ¿Para qué hace falta `sudo`?

- **[0,5]** `apt update` descarga la lista actualizada de paquetes de los repositorios.
- **[0,5]** `apt upgrade` actualiza los paquetes instalados.
- **[0,5]** `sudo` ejecuta la orden con permisos de administrador (`root`), porque instalar y actualizar cambia el sistema.

### Instalar y actualizar sistemas libres y propietarios (3,5 puntos)

**18.** *(1,5 puntos)* ¿Qué es el TPM y qué versión pide Windows 11? ¿Con qué herramienta de Windows se comprueba si está listo para usarse?

- **[0,5]** Un chip de la placa base que guarda claves de cifrado y ayuda a comprobar que el equipo arranca sin manipulaciones.
- **[0,5]** Windows 11 pide la **2.0**.
- **[0,5]** Con **`tpm.msc`**.

**19.** *(1 punto)* Un equipo tiene un procesador compatible con Windows 11 de cuatro núcleos a 2,5 GHz, 8 GB de RAM, un SSD de 256 GB y firmware UEFI con arranque seguro, pero no tiene TPM. ¿Puede instalar Windows 11? ¿Por qué?

- **[0,5]** **No**.
- **[0,5]** Cumple el procesador, la memoria, el disco y UEFI con arranque seguro, pero le falta el **TPM 2.0**.

**20.** *(1 punto)* ¿Para qué sirven la partición EFI y la partición de recuperación que crea Windows 11?

- **[0,5]** La **EFI** guarda los programas de arranque.
- **[0,5]** La de **recuperación** tiene las herramientas para reparar Windows.

## Preguntas adicionales

Optativas, para sustituir preguntas del examen que no se sepan.

**21.** *(1 punto)* ¿Qué es WSL? ¿En qué se diferencia de una máquina virtual de VirtualBox?

- **[0,5]** WSL (*Windows Subsystem for Linux*) ejecuta un Linux de verdad dentro de Windows, sin máquina virtual aparte ni arranque dual.
- **[0,5]** Con VirtualBox se crea un ordenador virtual completo, con su firmware, su disco y su arranque, y en él se instala el sistema.

**22.** *(1 punto)* ¿Qué sale por pantalla al ejecutar estas órdenes? ¿Qué hace el `|` de la última?

```bash
echo "pera" > frutas.txt
echo "manzana" >> frutas.txt
echo "kiwi" >> frutas.txt
cat frutas.txt | sort
```

- **[0,5]** Las tres frutas ordenadas: `kiwi`, `manzana` y `pera`, cada una en una línea.
- **[0,5]** Es una tubería: pasa lo que sale de `cat` (el contenido del archivo) como entrada de `sort`, que ordena las líneas.

**23.** *(1 punto)* En VirtualBox, ¿en qué modo de red tiene Internet la máquina, y en cuál se puede comunicar con Windows?

- **[0,5]** En **NAT** tiene Internet: un router virtual de VirtualBox la saca a Internet por la tarjeta real de Windows.
- **[0,5]** En **Host-only** se comunica con Windows, a través del adaptador *VirtualBox Host-Only*.

**24.** *(1 punto)* ¿Qué tabla de particiones va con BIOS y cuál con UEFI?

- **[0,5]** Con BIOS, **MBR**.
- **[0,5]** Con UEFI, **GPT**.

**25.** *(1 punto)* ¿Cuál es el tamaño máximo de un archivo en FAT32? ¿Cuál de los dos, FAT32 o NTFS, permite poner permisos a archivos y carpetas?

- **[0,5]** **4 GB**.
- **[0,5]** **NTFS**.

**26.** *(1 punto)* Un procesador tiene 8 núcleos y 16 procesadores lógicos. ¿Qué es un procesador lógico? ¿Cuántos hilos lleva cada núcleo?

- **[0,5]** Cada unidad de procesamiento que el sistema operativo reconoce y puede utilizar para ejecutar hilos de software.
- **[0,5]** **2 hilos**: con 2 hilos por núcleo, el sistema reconoce 16 procesadores lógicos (8 × 2).

**27.** *(1 punto)* ¿Qué es una distribución de Linux? Pon dos ejemplos.

- **[0,5]** Un sistema operativo basado en el kernel Linux que incluye programas, herramientas, un sistema de gestión de paquetes y, normalmente, un entorno de escritorio.
- **[0,25]** Una distribución, por ejemplo **Kali**.
- **[0,25]** Otra distinta, por ejemplo **Arch**.

Vale cualquiera de los apuntes: Debian, Ubuntu, Linux Mint, Fedora, Arch, Manjaro, Kali o Parrot.

**28.** *(1 punto)* Una empresa quiere cifrar los discos de sus portátiles con BitLocker. ¿Qué edición de Windows 11 no le sirve y cuál sí?

- **[0,5]** No le sirve **Home**: no tiene BitLocker.
- **[0,5]** Le sirve **Pro** (o Enterprise, si es una empresa mediana o grande).
