# UD2 · Sistemas operativos: instalación

Lo básico que hay que saber de la UD2. Cada apartado tiene la idea clave (**En una frase**), lo que tienes que saber y, cuando hay conceptos que se confunden, una tabla para compararlos (**Compara**). Las preguntas para comprobar que lo entiendes están en el [cuestionario](../cuestionario.md) de la semana, en «Cuestiones sobre los apuntes». Lo de los apartados 5 a 9 se practica en el proyecto de la semana (`actividades/proyecto-SI.md`).

Hay tres tipos de contenido:

- Lo que no lleva marca es lo **imprescindible**: hay que entenderlo y saber explicarlo con tus palabras.
- > **Para saber más.** Lo que va en un recuadro como este ayuda a entender, pero no hay que aprenderlo de memoria.
- *Para la práctica: paso N del proyecto.* Los apartados que empiezan así recogen los detalles que se usan en ese paso. Se aprenden haciéndolo: vuelve a ellos cuando el proyecto te lo pida.

---

## 1. Qué es un sistema operativo

**En una frase:** el sistema operativo hace de intermediario entre las personas y los programas y el hardware, y reparte los recursos del equipo.

**Lo que tienes que saber**

- Dos funciones: ofrecer una **interfaz** para usar el equipo sin saber cómo funciona por dentro, y **gestionar los recursos** (procesador, memoria, discos, periféricos) para que todos los programas los compartan bien.
- Lo que gestiona: **procesos** (qué programa usa el procesador en cada momento), **memoria** (y la memoria virtual), **entrada/salida** (los dispositivos), **archivos** (sistemas de archivos y carpetas) y **seguridad** (usuarios y permisos).
- Su parte central es el **kernel** (núcleo): siempre está en memoria y es quien habla con el hardware. Funciona en **modo núcleo**, con acceso total al equipo. Los programas funcionan en **modo usuario**, sin acceso directo al hardware: cuando necesitan algo (abrir un archivo, enviar datos por la red), se lo piden al kernel con una **llamada al sistema**.
- Un sistema operativo también consume recursos y se actualiza para corregir fallos y admitir hardware nuevo.

**Ejemplo.** Al guardar un documento, el procesador de textos no escribe en el disco: se lo pide al sistema operativo. El kernel comprueba que tienes permiso para escribir en esa carpeta (seguridad), decide dónde se guarda dentro de la partición (archivos) y usa el driver del disco para escribirlo (entrada/salida).

---

## 2. Tipos de sistemas operativos

**En una frase:** los sistemas operativos se clasifican por cuántas tareas y usuarios atienden, por cómo responden, por su interfaz y por cómo ofrecen sus servicios.

**Lo que tienes que saber**

| Según | Tipos | Ejemplos |
|---|---|---|
| Tareas a la vez | **Monotarea**: un programa cada vez. **Multitarea**: varios a la vez; el sistema reparte el procesador entre ellos tan rápido que parecen simultáneos | MS-DOS era monotarea. Todos los actuales son multitarea: escuchas música mientras navegas |
| Usuarios a la vez | **Monousuario**: lo usa una persona cada vez. **Multiusuario**: varias personas a la vez, cada una con su sesión | Un servidor Linux o Windows Server con muchos usuarios conectados por la red. Windows 11 admite varias cuentas, pero está pensado para que lo use una persona cada vez |
| Forma de respuesta | **Interactivos**: responden a la persona. **De tiempo real**: responden en un plazo garantizado. **Por lotes**: procesan trabajos en serie, sin intervención | Windows y Ubuntu son interactivos. El ABS de un coche, un avión o un equipo médico necesitan tiempo real. Las nóminas de una empresa se procesan por lotes, de noche |
| Interfaz | **Textual** (terminal: ligera y potente) / **gráfica** (ventanas: fácil, pero consume más) | Ubuntu Server, el del proyecto, es textual. Windows 11 y Ubuntu Desktop son gráficos |
| Servicios | **De escritorio**, **en red** (un servidor da servicios a otros equipos) y **distribuidos** (varios equipos funcionan como uno) | Windows 11 en un portátil; un Windows Server que comparte carpetas en una empresa; un clúster de servidores que atiende una web como si fuera uno solo |

- Todo sistema multiusuario es multitarea; al revés, no siempre.
- Un mismo sistema se clasifica a la vez con todos los criterios. Por ejemplo, Ubuntu Server es multitarea, multiusuario, interactivo, de interfaz textual y en red.

---

## 3. Arquitectura y familias

**En una frase:** el kernel puede ser monolítico, microkernel o híbrido, y hoy hay tres grandes familias: Windows, Linux y las de Apple.

### El kernel: monolítico, microkernel o híbrido

**Lo que tienes que saber**

- La diferencia está en **qué funciona dentro del kernel**, en modo núcleo y con acceso total (apartado 1), y qué funciona fuera, como programas normales.
- **Monolítico:** el kernel lo incluye casi todo: la gestión de procesos y de memoria, los sistemas de archivos y los drivers. Todo eso funciona como un único programa en modo núcleo. Es rápido, porque las partes se comunican directamente, pero un fallo en un driver puede tumbar todo el sistema. Ejemplo: **Linux**.
- **Linux es monolítico, pero modular:** muchos drivers son **módulos** que el kernel carga solo cuando hacen falta (por ejemplo, al conectar un dispositivo). Una vez cargados, funcionan dentro del kernel, como el resto.
- **Microkernel:** el kernel hace lo mínimo (procesos, memoria y comunicación entre programas); los drivers y los sistemas de archivos funcionan fuera, como programas aparte. Es más estable y seguro, pero más lento, porque las partes tienen que comunicarse con mensajes. Ejemplo: MINIX.
- **Híbrido:** mezcla los dos. Ejemplos: **Windows** y **macOS**.

**Compara**

| | Monolítico | Microkernel |
|---|---|---|
| Dónde funcionan los drivers y servicios | Dentro del kernel | Fuera, como programas aparte |
| Rendimiento | Mayor | Menor |
| Si falla un driver | Puede caer todo el sistema | Cae solo ese programa |
| Ejemplo | Linux (modular) | MINIX |

### Las familias actuales

- **Windows**, de Microsoft: **Windows 11** (Home, Pro, Enterprise, Education) para equipos personales y **Windows Server 2025** para servidores.
- **Linux**: Linux es solo el kernel. Lo que se instala es una **distribución**: el kernel más los programas, un instalador y un gestor de paquetes. Distribuciones: Ubuntu, Debian, Fedora, Red Hat, Rocky o Arch.
- Ubuntu publica una **LTS** (*Long Term Support*, soporte de 5 años) cada dos años, en abril: 24.04, **26.04** (la del proyecto)…
- **Apple**: **macOS** e **iOS**.
- **Android** usa el kernel Linux, aunque no es una distribución como las demás.

---

## 4. Licencias de software

**En una frase:** la licencia dice qué se puede hacer con un programa: usarlo, copiarlo, modificarlo o redistribuirlo.

**Lo que tienes que saber**

- Al instalar un programa no lo compras: aceptas una **licencia**, un contrato que dice qué puedes hacer con él.
- **Software libre:** la licencia te da cuatro libertades: **usarlo** para lo que quieras, **estudiar** cómo funciona (por eso el código tiene que estar disponible), **modificarlo** y **redistribuirlo**, con cambios o sin ellos. Habla de libertad, no de precio: el software libre también se puede vender. Por ejemplo, Red Hat Enterprise Linux es libre, pero se paga una suscripción.
- Dos licencias libres muy usadas: **GPL**, la de Linux y VirtualBox (las copias y versiones modificadas tienen que seguir siendo libres: *copyleft*), y **MIT** (casi sin condiciones: se puede usar incluso dentro de un programa propietario).
- **Código abierto** (*open source*): el código es público y se puede modificar y redistribuir. En la práctica, casi todo el software libre es de código abierto y al revés. Cambia el enfoque: el software libre lo defiende como un derecho de los usuarios; el código abierto, por sus ventajas prácticas (mucha gente revisa y mejora el código).
- **Propietario:** el código no está disponible y la licencia limita el uso: en cuántos equipos se instala, si se puede modificar… Puede ser de pago (Windows, Microsoft Office) o gratis.
- **Freeware:** propietario, pero gratis (Google Chrome). **Shareware / prueba:** se prueba gratis un tiempo o con funciones limitadas, y después se paga (WinRAR).
- **Gratis no es lo mismo que libre:** Chrome es gratis y no es libre; Red Hat Enterprise Linux es libre y es de pago.

**Compara**

| | Libre | Freeware | Propietario de pago |
|---|---|---|---|
| ¿Gratis? | Casi siempre, pero se puede cobrar | Sí | No |
| ¿Código disponible? | Sí | No | No |
| ¿Se puede modificar y redistribuir? | Sí | No | No |
| Ejemplos | Linux, Ubuntu, VirtualBox | Google Chrome | Windows 11, Microsoft Office |

---

## 5. Máquinas virtuales

**En una frase:** una máquina virtual es un ordenador simulado dentro de otro, con su propio sistema operativo.

**Lo que tienes que saber**

- **Anfitrión** (*host*): el ordenador real. **Invitado** (*guest*): la máquina virtual. **Hipervisor:** el programa que crea las máquinas y les reparte los recursos del anfitrión.
- **Tipo 1** (nativo): funciona directamente sobre el hardware; en servidores (VMware ESXi, Hyper-V, Proxmox). **Tipo 2** (alojado): funciona como un programa dentro de un sistema operativo (VirtualBox, VMware Workstation).
- Para que vaya rápida, el procesador necesita la **virtualización por hardware** activada en el firmware (Intel VT-x o AMD-V).
- Una máquina son unos pocos archivos: su configuración (`.vbox`) y su **disco virtual** (`.vdi`), que puede ser **dinámico** (crece según se usa) o de **tamaño fijo** (ocupa todo desde el principio, pero es más rápido).
- Una **instantánea** guarda el estado de la máquina para volver a él si algo sale mal. Cómo funciona: desde que se toma, el disco original ya no se toca, y los cambios se escriben en un archivo aparte, un **disco de diferencias** (*differencing*). Volver a la instantánea es tirar esas diferencias.
- Mejor tomar las instantáneas con la máquina **apagada**: guardan solo el disco y la configuración, ocupan menos y, al volver a ellas, la máquina arranca limpia.
- **Una instantánea no es una copia de seguridad:** depende del disco original, en el mismo ordenador. Si se borra o se estropea el `.vdi`, se pierden la máquina y sus instantáneas. Una copia de seguridad es copiar los archivos de la máquina a otro sitio, o exportarla (*File → Export Appliance*, un archivo `.ova`).
- Usos: probar sistemas y programas sin riesgo, aprender, aprovechar un servidor para muchos servicios y mover o copiar máquinas enteras de un equipo a otro.
- Los **contenedores** (Docker) son otra forma de virtualizar, más ligera: comparten el kernel del anfitrión. Se ven en la UD6.

**Compara**

| | Tipo 1 | Tipo 2 |
|---|---|---|
| Dónde se instala | Directamente sobre el hardware | Dentro de un sistema operativo |
| Uso típico | Servidores | Ordenadores personales, aprendizaje |
| Ejemplos | VMware ESXi, Hyper-V, Proxmox | VirtualBox, VMware Workstation |

**VirtualBox con Hyper-V activo.** *Para la práctica: pasos 2 y 3 del proyecto.* Si en Windows está activo **Hyper-V**, el hipervisor de Windows (lo usan WSL y algunas funciones de seguridad), VirtualBox no puede usar la virtualización por hardware directamente y funciona por encima de Hyper-V (en VirtualBox, *Execution Engine: native API*). Funciona, pero más despacio, porque, entre otras cosas, queda desactivada la traducción de memoria por hardware (*Nested Paging*). Por eso la instalación tarda más y pueden salir avisos como `soft lockup`.

### El hardware de una máquina virtual

*Para la práctica: paso 1 del proyecto.*

Cada ajuste de la máquina virtual es un componente de un ordenador. En VirtualBox se ven en *Settings*, en modo *Expert*:

| Dónde, en *Settings* | Qué hay | El componente real |
|---|---|---|
| *System → Motherboard* | *Base Memory* 2048 MB | La memoria RAM |
| *System → Motherboard* | *Chipset* PIIX3 | El chipset de la placa base |
| *System → Motherboard* | *Boot Device Order (BIOS only)* | El orden de arranque, solo para BIOS: con UEFI lo lleva el propio firmware |
| *System → Motherboard* | *TPM Version* None, *UEFI* marcado, *Secure Boot* sin marcar | El firmware y su seguridad. Sin TPM 2.0 ni Secure Boot, esta máquina no cumple los requisitos de Windows 11 |
| *System → Processor* | *Number of CPUs* 2 | El procesador: 2 procesadores virtuales (lee debajo de la tabla) |
| *System → Acceleration* | *Paravirtualization Interface* Default, *Nested Paging* | Cómo usa la virtualización por hardware |
| *Display* | *Video Memory* 16 MB, *Graphics Controller* VMSVGA | La tarjeta gráfica |
| *Storage* | *Controller: IDE*, con el DVD | El controlador del DVD |
| *Storage* | *Controller: SATA*, tipo AHCI, con el disco en *SATA Port 0* | El controlador de disco y su puerto |
| *Storage* (clic en el `.vdi`) | *Virtual size* 25 GB, *Actual size* (lo que ocupa de verdad), *Dynamically allocated* | El disco, dinámico: crece según se usa |
| *Network → Adapter 1* | *Attached to* NAT, *Adapter Type* Intel PRO/1000 MT Desktop, *MAC Address* | La tarjeta de red y su dirección física (MAC). Hay hasta 4 |
| *USB* | USB 2.0 (OHCI + EHCI) | El controlador USB |

- **Procesadores virtuales.** En VirtualBox, una «CPU» es un **procesador virtual**, y cada uno usa un núcleo del procesador real. Un ordenador suele tener un solo chip (*Sockets: 1* en el Administrador de tareas), con varios **núcleos** (*Cores*), y cada núcleo puede llevar dos **hilos** (*Logical processors*). En *Settings*, la barra está en verde hasta el número de núcleos del anfitrión: dar a la máquina más que eso perjudica al anfitrión.

> **Para saber más.** **Paravirtualización:** el sistema invitado sabe que está en una máquina virtual y colabora con el hipervisor, para ir más rápido. Con *Paravirtualization Interface: Default*, Ubuntu lo hace con la interfaz KVM. **PIIX3** es un chipset de Intel de los años 90: VirtualBox lo simula porque todos los sistemas lo reconocen.

### Instantáneas y estado actual

*Para la práctica: pasos 5 y 8 del proyecto.*

- Cada **instantánea** es una **foto fija** de la máquina en el momento de tomarla. No se enciende ni se cambia: queda tal cual para poder volver a ella.
- **Current State** (*Estado actual*) es la máquina **tal como está ahora**: la que se enciende y se usa. Cuelga de la última instantánea tomada o restaurada, y **todo lo que se hace con la máquina encendida se guarda aquí**, nunca en una instantánea.
- **Restaurar** una instantánea hace que el estado actual vuelva a ser una copia de esa foto: lo hecho desde entonces se pierde.

Lo que se puede hacer en VirtualBox depende de lo que esté seleccionado en la lista de *Snapshots*:

| Seleccionado | Qué se puede hacer |
|---|---|
| **Current State** | **Start**: encender la máquina; lo que se haga se guarda en el estado actual. **Take**: tomar una instantánea, una foto del estado actual. **Settings**: cambiar la configuración |
| Una **instantánea** | **Restore**: el estado actual pasa a ser una copia de esa foto, y lo hecho desde entonces se pierde (salvo que se marque *Create a snapshot of the current machine state*, que antes lo guarda en otra instantánea). **Delete**: borra la foto; el estado actual no cambia. **Clone**: crea otra máquina a partir de esa foto. Con una instantánea seleccionada, **Start** sale en gris |

### Los controladores de disco: IDE y SATA

*Para la práctica: pasos 1 y 3 del proyecto.*

- Los discos y las unidades de DVD se conectan a la placa base a través de un **controlador de almacenamiento**, y cada controlador usa una **interfaz**: el tipo de conexión (cable y forma de comunicarse).
- VirtualBox simula los dos controladores. En una máquina nueva, en el **IDE** está la **unidad de DVD**, donde se mete la **ISO** (un archivo que VirtualBox presenta como un disco metido en el lector), y en el **SATA**, el **disco duro**, el archivo `.vdi`. La máquina cree que tiene un lector de DVD y un disco; en el anfitrión solo son dos archivos.
- Dentro de Linux, el disco SATA aparece como `/dev/sda` y el DVD como `/dev/sr0`.

**Compara**

| | IDE (o PATA, *Parallel ATA*) | SATA (*Serial ATA*) |
|---|---|---|
| Qué es | La interfaz antigua, de los años 80 hasta mediados de los 2000 | La que la sustituyó; la de los discos y DVD actuales (los SSD más rápidos usan NVMe) |
| Cable | Ancho y plano, con dos dispositivos por cable (*maestro* y *esclavo*) | Fino, con un dispositivo por puerto |
| Velocidad | Hasta 133 MB/s | Hasta 600 MB/s |

### La red de la máquina: NAT

*Para la práctica: pasos 3 y 5 del proyecto.*

- Con **NAT**, la máquina sale a Internet a través del anfitrión, pero desde fuera no se la ve. VirtualBox le da una dirección por DHCP.
- **`10.0.2.15/24`** es la dirección **IPv4 privada** que da el NAT de VirtualBox. Cada máquina tiene su propio NAT, aislado de los demás: por eso todas reciben la misma sin que choquen. `/24` indica que la red son las direcciones `10.0.2.x`.
- La que empieza por **`fd`** es una dirección **IPv6 privada** de esa misma red.
- La tarjeta de red tiene además su dirección física, la **MAC**: se ve en el instalador, en el menú de arranque del firmware (arranque por red, PXE) y en *Settings → Network*.

---

## 6. Instalar un sistema operativo

**En una frase:** antes de instalar se comprueban los requisitos y se planifica, sobre todo el disco y el modo de arranque.

**Lo que tienes que saber**

- **Requisitos mínimos** (para que funcione) y **recomendados** (para que vaya bien). Windows 11 pide, por ejemplo, 4 GB de memoria, 64 GB de disco, firmware **UEFI compatible con Secure Boot** y un chip **TPM 2.0**.
- **Planificar** es responder unas preguntas antes de empezar:
  1. ¿El equipo cumple los requisitos?
  2. ¿Hay datos que conservar? Entonces, **copia de seguridad**: al particionar se puede borrar el disco.
  3. ¿Cómo arranca el equipo, con **UEFI** o con **BIOS**? De eso depende la tabla de particiones: lo normal es **UEFI con GPT** (lo actual) y **BIOS con MBR** (lo antiguo). Windows lo exige así; Linux es más flexible, pero lo habitual es lo mismo.
  4. ¿Cómo se reparte el disco? Qué **particiones** hacen falta y, si habrá varios sistemas, cuál se instala primero: normalmente Windows, porque el instalador de Linux detecta Windows y añade su entrada en GRUB, y el de Windows no hace lo mismo con Linux.
  5. ¿Hay **drivers** para todo el hardware, sobre todo la red y el disco?
  6. ¿Cuál es el **medio de instalación**? La ISO, grabada en un USB o, en una máquina virtual, metida en su DVD virtual.
- **El proceso**, en casi todos los sistemas:
  1. Arrancar desde el medio de instalación (con el menú de arranque del firmware o cambiando el orden de arranque).
  2. Elegir idioma y teclado.
  3. Configurar la red.
  4. **Particionar el disco.** Es el paso delicado: aquí se borran datos.
  5. Crear el usuario y su contraseña, y dar nombre al equipo.
  6. Esperar a que se copie el sistema y se instale el gestor de arranque.
  7. Reiniciar, quitando antes el medio de instalación.
- Después de instalar: actualizar el sistema, instalar los drivers que falten y comprobar que todo funciona.
- Una **instalación desatendida** usa un archivo de respuestas para instalar sin preguntar; sirve para instalar muchos equipos iguales.

**Ejemplo.** En el paso 3 del proyecto: la máquina tiene UEFI, así que el instalador hace una tabla GPT con dos particiones, la EFI y la raíz; el particionado guiado borra el disco entero, que es el virtual y está vacío; y, antes de reiniciar, se quita la ISO.

---

## 7. Discos y particiones

**En una frase:** un disco se divide en particiones, y su lista está en una tabla que puede ser MBR (antigua) o GPT (actual).

**Antes de empezar: disco, partición, tabla y sistema de archivos**

- **Disco:** donde se guardan los datos (un disco duro o un SSD). Para el disco no hay archivos: solo bloques numerados, uno detrás de otro.
- **Partición:** un trozo del disco, de un bloque a otro, que el sistema trata como si fuera un disco independiente. Sirve para separar sistemas, o el sistema de los datos.
- **Tabla de particiones:** la lista de las particiones del disco (dónde empieza y dónde acaba cada una, y de qué tipo es). Está al principio del disco. Hay dos tipos: **MBR** y **GPT**.
- **Sistema de archivos:** organiza el interior de cada partición en archivos y carpetas. Se crea al **formatear** la partición.

Van en ese orden: el disco tiene una tabla, la tabla dice qué particiones hay, y cada partición lleva su sistema de archivos, que guarda los archivos. En el paso 4 del proyecto, `lsblk` lo muestra: `sda` es el disco, con una tabla GPT; `sda1` es una partición con FAT32, y `sda2`, otra con ext4.

**Lo que tienes que saber**

- **MBR** (*Master Boot Record*): la tabla está en el primer sector del disco, junto con un pequeño programa de arranque, el que ejecuta la BIOS. Como mucho 4 particiones principales y discos de hasta 2 TB. Para tener más de 4, una de ellas se hace **extendida** y dentro se crean particiones **lógicas**: es un truco para saltarse ese límite.
- **GPT** (*GUID Partition Table*): forma parte del estándar UEFI. Hasta 128 particiones (por eso no necesita particiones lógicas), discos enormes y una copia de seguridad de la tabla al final del disco: si se daña la del principio, se recupera.
- Con UEFI hace falta una **partición EFI**: pequeña, en FAT32, con los programas de arranque de cada sistema.
- **Windows con UEFI:** partición EFI, MSR (reservada), Windows (`C:`, NTFS) y recuperación.
- **Ubuntu con UEFI:** partición EFI (montada en `/boot/efi`) y la raíz `/` (ext4).
- **Letras y carpetas:** en Windows, cada partición tiene una letra (`C:`, `D:`…). En Linux no hay letras: todo cuelga de una única carpeta, la raíz `/`, y cada partición se **monta** en una carpeta de ese árbol. Por ejemplo, la partición EFI se ve dentro de `/boot/efi`.

**Compara**

| | MBR | GPT |
|---|---|---|
| Firmware | BIOS (heredado) | UEFI |
| Particiones | 4 principales | Hasta 128 |
| Tamaño máximo | 2 TB | Prácticamente sin límite |
| Copia de la tabla | No | Sí, al final del disco |

### Sistemas de archivos: FAT32, ext4 y NTFS

- Un **sistema de archivos** es la forma de organizar los archivos y carpetas dentro de una partición: dónde está guardado cada archivo, su nombre, su tamaño, sus permisos… Una partición vacía no sirve hasta que se le crea uno: es lo que se llama **formatear**.
- La partición EFI tiene que ser **FAT32**, porque el estándar UEFI obliga al firmware a saber leer FAT, y no otros. Linux va en **ext4** y Windows, en **NTFS**: los dos tienen permisos y diario.
- **exFAT** es un FAT moderno, sin el límite de 4 GB por archivo: el de las memorias USB y tarjetas grandes.

**Compara**

| | FAT32 (*File Allocation Table*, 32 bits) | ext4 (*fourth extended filesystem*) | NTFS (*New Technology File System*) |
|---|---|---|---|
| Qué es | Un sistema de archivos antiguo y sencillo, de los años 90 | El sistema de archivos habitual de Linux | El sistema de archivos de Windows |
| Quién lo entiende | Casi todos: Windows, Linux, macOS… y el firmware UEFI | Linux. Windows no lo lee sin programas añadidos | Windows. Linux lo lee y lo escribe; macOS solo lo lee |
| Límites | Archivos de hasta 4 GB | Archivos y discos enormes | Archivos y discos enormes |
| Permisos de usuarios | No | Sí: cada archivo tiene propietario y permisos | Sí: cada archivo tiene una lista de usuarios y grupos con sus permisos |
| Si se va la luz | Se puede dañar | Tiene un **diario** (*journaling*): apunta lo que va a cambiar antes de hacerlo, y así se recupera | También tiene diario |
| Dónde se usa | La partición EFI y las memorias USB | La raíz de Linux (`/`) | `C:` en Windows |

---

## 8. El arranque y los gestores de arranque

**En una frase:** el firmware busca un gestor de arranque, el gestor carga el kernel y el kernel arranca el resto del sistema.

**Las fases, paso a paso**

1. **Firmware.** Al encender, se ejecuta el firmware de la placa base. Comprueba el hardware (el **POST**) y busca algo que arrancar, siguiendo el orden de arranque. Si no encuentra nada, se para con un mensaje.
2. **Gestor de arranque.** El firmware ejecuta el gestor de arranque: **GRUB** en Linux, **Windows Boot Manager** en Windows. Si hay varios sistemas, muestra un menú. Después carga en memoria el kernel del sistema elegido.
3. **Kernel.** Se pone en marcha, reconoce el hardware y carga sus drivers. En Linux lo ayuda el **initrd**, un pequeño sistema en memoria que prepara lo necesario para **montar la raíz**, la partición donde está el resto del sistema.
4. **Primeros servicios.** El kernel arranca el primer programa, que arranca todos los demás: la red, el registro de mensajes, el inicio de sesión… En Linux es **systemd**, el proceso número 1.
5. **Inicio de sesión.** El `login:` en un sistema textual o la pantalla de inicio en uno gráfico.

**Lo que tienes que saber**

- **UEFI** frente a BIOS: arranca más rápido, busca los cargadores en la partición EFI, tiene su propio menú de arranque y **Secure Boot** (solo arranca programas firmados). Más abajo, en «El firmware: BIOS y UEFI».
- **GRUB** (Linux): su configuración se cambia en `/etc/default/grub` (menú, tiempo de espera, entrada por defecto) y se aplica con `sudo update-grub`, que genera `/boot/grub/grub.cfg`. Ese archivo no se edita a mano.
- **Windows Boot Manager** (Windows): su configuración es el **BCD**, que se consulta y cambia con `bcdedit`. Carga `winload.efi`, que carga el kernel de Windows.
- Con varios sistemas (**arranque dual**), GRUB muestra un menú y, si se elige Windows, le pasa el control a su gestor de arranque (**arranque en cadena**).
- **Recuperación:** en Linux, el **modo de recuperación** del menú de GRUB; en Windows, el **entorno de recuperación** (WinRE).

**Compara**

| | Linux (Ubuntu) | Windows |
|---|---|---|
| Gestor de arranque | GRUB | Windows Boot Manager |
| Su configuración | `/etc/default/grub` → `update-grub` → `grub.cfg` | El BCD, con `bcdedit` |
| Recuperación | Modo de recuperación de GRUB | WinRE |

**Compara: qué se ve cuando falla cada fase.** Lo que aparece en pantalla dice en qué fase falla el arranque, y eso dice dónde mirar:

| Lo que ves | Fase | Qué pasa | Qué revisar |
|---|---|---|---|
| Un mensaje del firmware, como `No bootable option or device was found` | 1 · Firmware | No encuentra nada que arrancar | El orden de arranque, el disco, la partición EFI |
| `grub>` | 2 · Gestor de arranque | GRUB arranca, pero no encuentra su configuración (`grub.cfg`) | `/boot/grub/grub.cfg` |
| `grub rescue>` | 2 · Gestor de arranque | GRUB ni siquiera encuentra sus propios archivos | La partición donde está `/boot/grub` |
| Mensajes del kernel y una consola de emergencia (`(initramfs)`) | 3 · Kernel | El kernel no puede montar la raíz | Los parámetros del kernel, el disco |
| Un servicio que falla y se queda esperando | 4 · Servicios | systemd no puede arrancar un servicio | Los servicios |

### El firmware: BIOS y UEFI

- El **firmware** es un programa guardado en un chip de la placa base. Es lo primero que se ejecuta al encender: comprueba el hardware (el **POST**) y busca un sistema que arrancar.
- **UEFI** es el firmware actual; **BIOS**, el antiguo. Mucha gente sigue llamando «BIOS» a la configuración del firmware, aunque sea UEFI.

**Compara**

| | BIOS (heredada, *legacy*) | UEFI |
|---|---|---|
| Qué es | El firmware de los PC desde los años 80 | El que la sustituye: lo llevan los ordenadores actuales desde hace más de diez años |
| Cómo arranca | Lee el primer sector del disco y ejecuta el pequeño programa que hay allí | Lee una partición del disco, la **partición EFI** (en FAT32), y ejecuta un programa `.efi` que hay en ella: en Ubuntu, el de GRUB |
| Qué recuerda | Solo el orden de los dispositivos | Una lista de **entradas de arranque** con nombre (`Ubuntu`, `Windows Boot Manager`…) |
| Tabla de particiones | MBR | GPT |
| Además | — | Su propio menú de arranque (*Boot Manager*) y **Secure Boot**, que solo arranca programas firmados |

> **Para saber más.** **EFI** (*Extensible Firmware Interface*, «interfaz de firmware extensible») es el nombre de la primera versión, creada por Intel: «extensible» porque se le pueden añadir programas, los `.efi`. **UEFI** (*Unified Extensible Firmware Interface*) es la misma, convertida en el estándar común de los fabricantes. Se usan como sinónimos: VirtualBox dice «EFI» y Ubuntu, «UEFI».

### GRUB, el gestor de arranque de Linux

- Sus siglas son *GRand Unified Bootloader*, «gran cargador de arranque unificado»: unificado porque sirve para arrancar sistemas muy distintos.
- Es el programa que el firmware ejecuta después de comprobar el hardware. Hace dos cosas: si hay varias opciones, muestra un **menú** para elegir una (con cuenta atrás: si no se toca nada, arranca la primera); y **carga en memoria el kernel** del sistema elegido, que pone en marcha todo lo demás.
- Una ISO de instalación trae **su propio GRUB**, con las opciones de la ISO (instalar, probar el sistema…). Al instalar, Ubuntu pone **otro GRUB en el disco**, con las entradas del sistema instalado.

### Las piezas del arranque de Ubuntu con UEFI

*Para la práctica: pasos 4, 6 y 8 del proyecto.*

| Pieza | Qué es | Dónde está | Para qué sirve |
|---|---|---|---|
| **Partición EFI** | Una partición pequeña, en FAT32 | La primera del disco (`sda1`); Linux la monta en `/boot/efi` | Guarda los programas de arranque de cada sistema instalado. Es lo que lee el firmware |
| **Entrada de arranque `Ubuntu`** | Un registro con un nombre y la ruta de un archivo | En la memoria del firmware, en la placa base (no en el disco). Se ve con `sudo efibootmgr` | Le dice al firmware qué archivo arrancar: `\EFI\ubuntu\shimx64.efi`, en la partición EFI |
| **`shimx64.efi`** | Un programa pequeño, firmado | `/boot/efi/EFI/ubuntu/` | Es lo primero que ejecuta el firmware. Como está firmado, pasa el control de **Secure Boot**, y arranca GRUB |
| **`grubx64.efi`** | El programa **GRUB** | `/boot/efi/EFI/ubuntu/` | Muestra el menú y carga el kernel y el initrd |
| **`grub.cfg`** de la partición EFI | Un archivo de texto de pocas líneas | `/boot/efi/EFI/ubuntu/` | Le dice a GRUB dónde está su configuración de verdad |
| **`/boot/grub/grub.cfg`** | La configuración de GRUB: el menú y sus entradas | En la raíz, en `/boot/grub/` | Lo lee GRUB al arrancar. Lo genera `sudo update-grub`: no se edita a mano |
| **`/etc/default/grub`** | Los ajustes de GRUB: menú, tiempo de espera, entrada por defecto | En la raíz, en `/etc/default/` | Es donde se cambia GRUB. Los cambios se aplican con `sudo update-grub` |
| **`vmlinuz-…`** | El **kernel** | En la raíz, en `/boot/` | El núcleo del sistema operativo. Lo carga GRUB |
| **`initrd.img-…`** | El **initrd**: un pequeño sistema en memoria | En la raíz, en `/boot/` | Prepara lo necesario para montar la raíz; después deja paso al sistema |
| **`systemd`** | El primer programa, el proceso 1 | `/usr/lib/systemd/systemd` | Lo arranca el kernel, y él arranca todos los servicios |

Por orden: el firmware lee su **entrada de arranque** → ejecuta **`shimx64.efi`** de la **partición EFI** → que arranca **GRUB** (`grubx64.efi`) → que lee **`/boot/grub/grub.cfg`** y carga el **kernel** y el **initrd** → que arrancan **systemd**.

### Las piezas del arranque de Windows con UEFI

*Para la práctica: paso 10 del proyecto.*

| Pieza | Dónde está | Cómo se ve | Su equivalente en Ubuntu |
|---|---|---|---|
| **Partición EFI** | La primera del disco, de 100 a 300 MB | `msinfo32` (*Boot Device*) y Administración de discos | La partición EFI (`/boot/efi`) |
| **Entrada de arranque `Windows Boot Manager`** | En la memoria del firmware | `bcdedit /enum firmware` | La entrada `Ubuntu` (`efibootmgr`) |
| **`bootmgfw.efi`**, el Windows Boot Manager | `\EFI\Microsoft\Boot\`, en la partición EFI | `bcdedit` (su `path`) | GRUB (`grubx64.efi`) |
| **El BCD**, su configuración | `\EFI\Microsoft\Boot\BCD`, en la partición EFI | `bcdedit` | `grub.cfg` |
| **`winload.efi`** | `C:\Windows\System32\` | `bcdedit` (el `path` del *Windows Boot Loader*) | La línea `linux` de GRUB, que carga el kernel |
| **WinRE**, el entorno de recuperación | La partición de recuperación | `bcdedit` (`recoverysequence`) | El modo de recuperación de GRUB |

---

## 9. Actualizaciones y aplicaciones

**En una frase:** el sistema y los programas se actualizan para corregir fallos y de seguridad; los programas se instalan desde fuentes de confianza.

**Lo que tienes que saber**

- **Por qué actualizar:** sobre todo por **seguridad**. Cuando se descubre un fallo, el fabricante publica un **parche**; un equipo sin actualizar sigue teniendo el fallo, y es una de las vías de ataque más habituales. Además, las actualizaciones corrigen errores y añaden drivers y funciones.
- **Fuentes de confianza:** los repositorios del sistema, la tienda oficial o la web del fabricante. Un instalador descargado de cualquier web puede traer programas maliciosos.
- **Windows Update:** una **actualización acumulativa** cada mes (incluye todas las anteriores, así que basta con la última) y una de características al año. También instala drivers. Se gestiona en *Configuración → Windows Update*.
- En **Windows**, los programas se instalan desde la Microsoft Store, con su instalador o desde el terminal con `winget install`; se quitan en *Configuración → Aplicaciones* o con `winget uninstall`.

**Ubuntu: paquetes y repositorios**

- Un **paquete** es un archivo con un programa listo para instalar (en Ubuntu, `.deb`) y la lista de los otros paquetes que necesita para funcionar: sus **dependencias**.
- Un **repositorio** es un servidor con miles de paquetes revisados y firmados.
- **`apt`** es el gestor de paquetes: busca el programa en los repositorios, lo descarga con sus dependencias y lo instala. Para actualizar, compara lo instalado con la lista de los repositorios.

| Orden | Qué hace |
|---|---|
| `sudo apt update` | Descarga la lista actualizada de paquetes. No instala nada |
| `sudo apt upgrade` | Actualiza los paquetes instalados |
| `sudo apt install paquete` | Instala un programa, con sus dependencias |
| `sudo apt remove paquete` | Lo desinstala |
| `sudo apt autoremove` | Quita los paquetes que ya no hacen falta, como los kernels antiguos |

- `update` va siempre antes que `upgrade`: sin la lista nueva, `apt` no sabe que hay versiones nuevas.

> **Para saber más.** Ubuntu tiene otro formato de paquetes, **snap**, que lleva el programa con todo lo que necesita dentro. Cada snap instalado aparece en `lsblk` como un disco `loop`.

**Compara**

| | Ubuntu | Windows |
|---|---|---|
| Actualizar el sistema | `sudo apt update` y `sudo apt upgrade` | Windows Update |
| De dónde salen los programas | Los repositorios | Microsoft Store, la web del fabricante |
| Instalar desde el terminal | `sudo apt install` | `winget install` |
