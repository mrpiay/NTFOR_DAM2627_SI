# UD2 · Sistemas operativos: instalación

Lo básico que hay que saber de la UD2. Cada apartado tiene la idea clave, lo que tienes que saber y, cuando hay conceptos que se confunden, una tabla para compararlos. Las preguntas para comprobar que lo entiendes están en el [cuestionario](../cuestionario.md) de la semana, en «Cuestiones sobre los apuntes». Lo de los apartados 6 a 9 se practica en el proyecto de la semana (`actividades/proyecto-SI.md`).

---

## 1. Qué es un sistema operativo

**En una frase:** el sistema operativo hace de intermediario entre las personas y los programas y el hardware, y reparte los recursos del equipo.

**Lo que tienes que saber**

- Dos funciones: ofrecer una **interfaz** para usar el equipo sin saber cómo funciona por dentro, y **gestionar los recursos** (procesador, memoria, discos, periféricos) para que todos los programas los compartan bien.
- Lo que gestiona: **procesos** (qué programa usa el procesador en cada momento), **memoria** (y la memoria virtual), **entrada/salida** (los dispositivos), **archivos** (sistemas de archivos y carpetas) y **seguridad** (usuarios y permisos).
- Su parte central es el **kernel** (núcleo): siempre está en memoria y es quien habla con el hardware.
- Un sistema operativo también consume recursos y se actualiza para corregir fallos y admitir hardware nuevo.

---

## 2. Tipos de sistemas operativos

**En una frase:** los sistemas operativos se clasifican por cuántas tareas y usuarios atienden, por cómo responden, por su interfaz y por cómo ofrecen sus servicios.

**Lo que tienes que saber**

| Según | Tipos |
|---|---|
| Tareas a la vez | **Monotarea** / **multitarea** (todos los actuales) |
| Usuarios a la vez | **Monousuario** / **multiusuario** (Linux, Windows Server) |
| Forma de respuesta | **Interactivos** (responden a la persona: Windows, Ubuntu), **de tiempo real** (responden en un plazo garantizado: frenos, aviones, equipos médicos) y **por lotes** (procesan trabajos en serie sin intervención) |
| Interfaz | **Textual** (terminal: ligera y potente) / **gráfica** (ventanas: fácil, pero consume más) |
| Servicios | **De escritorio**, **en red** (un servidor da servicios a otros equipos) y **distribuidos** (varios equipos funcionan como uno) |

- Todo sistema multiusuario es multitarea; al revés, no siempre.

---

## 3. Arquitectura y familias

**En una frase:** el kernel puede ser monolítico, microkernel o híbrido, y hoy hay tres grandes familias: Windows, Linux y las de Apple.

**Lo que tienes que saber**

- **Monolítico:** todo el sistema funciona como un único programa con acceso total; rápido, pero un fallo puede afectar a todo. Ejemplo: **Linux**.
- **Microkernel:** el kernel hace lo mínimo y el resto funciona como programas aparte; más estable y seguro, pero más lento. Ejemplo: MINIX.
- **Híbrido:** mezcla los dos. Ejemplos: **Windows** y **macOS**.
- Versiones actuales: **Windows 11** (Home, Pro, Enterprise, Education) y **Windows Server 2025**; distribuciones **Linux** como Ubuntu, Debian, Fedora, Red Hat, Rocky o Arch; **macOS** e **iOS**. Android usa el kernel Linux.
- Ubuntu publica una **LTS** (soporte de 5 años) cada dos años: 24.04, 26.04…

**Compara**

| | Monolítico | Microkernel |
|---|---|---|
| Dónde funcionan los drivers y servicios | Dentro del kernel | Fuera, como programas aparte |
| Rendimiento | Mayor | Menor |
| Si falla un driver | Puede caer todo el sistema | Cae solo ese programa |

---

## 4. Licencias de software

**En una frase:** la licencia dice qué se puede hacer con un programa: usarlo, copiarlo, modificarlo o redistribuirlo.

**Lo que tienes que saber**

- **Software libre:** se puede usar, estudiar (el código está disponible), modificar y redistribuir. Ejemplos de licencias: **GPL** (las copias y versiones modificadas tienen que seguir siendo libres: *copyleft*) y **MIT** (casi sin condiciones).
- **Código abierto** (*open source*): el código es público. Casi siempre coincide con el software libre.
- **Propietario:** el código no está disponible y la licencia limita el uso (Windows, Microsoft Office).
- **Freeware:** gratis, pero no libre. **Shareware / prueba:** se prueba gratis un tiempo o con funciones limitadas.
- Gratis no es lo mismo que libre.

**Compara**

| | Libre | Freeware | Propietario de pago |
|---|---|---|---|
| ¿Gratis? | Normalmente | Sí | No |
| ¿Código disponible? | Sí | No | No |
| ¿Se puede modificar y redistribuir? | Sí | No | No |

---

## 5. Máquinas virtuales

**En una frase:** una máquina virtual es un ordenador simulado dentro de otro, con su propio sistema operativo.

**Lo que tienes que saber**

- **Anfitrión** (*host*): el ordenador real. **Invitado** (*guest*): la máquina virtual. **Hipervisor:** el programa que crea las máquinas y les reparte los recursos del anfitrión.
- **Tipo 1** (nativo): funciona directamente sobre el hardware; en servidores (VMware ESXi, Hyper-V, Proxmox). **Tipo 2** (alojado): funciona como un programa dentro de un sistema (VirtualBox, VMware Workstation).
- Para que vaya rápida, el procesador necesita la **virtualización por hardware** activada en el firmware (Intel VT-x o AMD-V).
- Si en Windows está activo **Hyper-V** (lo usan WSL y algunas funciones de seguridad), VirtualBox funciona por encima de él (en VirtualBox, *native API*): funciona, pero más despacio, porque, entre otras cosas, queda desactivada la traducción de memoria por hardware (*Nested Paging*).
- Una máquina son unos pocos archivos: su configuración (`.vbox`) y su **disco virtual** (`.vdi`), que puede ser **dinámico** (crece según se usa) o de **tamaño fijo** (más rápido).
- Una **instantánea** guarda el estado de la máquina para volver a él si algo sale mal. Mejor tomarla con la máquina apagada: guarda solo el disco y la configuración, ocupa menos y, al volver a ella, la máquina arranca limpia. Desde ese momento, el hipervisor escribe los cambios del disco en un archivo aparte, un **disco de diferencias** (*differencing*): así se puede volver atrás.
- Usos: probar sistemas y programas sin riesgo, aprender, aprovechar un servidor para muchos servicios, y copias de seguridad.
- Los **contenedores** (Docker) son otra forma de virtualizar, más ligera: comparten el kernel del anfitrión. Se ven en la UD6.

**Compara**

| | Tipo 1 | Tipo 2 |
|---|---|---|
| Dónde se instala | Directamente sobre el hardware | Dentro de un sistema operativo |
| Uso típico | Servidores | Ordenadores personales, aprendizaje |
| Ejemplos | VMware ESXi, Hyper-V, Proxmox | VirtualBox, VMware Workstation |

### El hardware de una máquina virtual

Cada ajuste de la máquina virtual es un componente de un ordenador. En VirtualBox se ven en *Settings*, en modo *Expert*:

| Dónde, en *Settings* | Qué hay | El componente real |
|---|---|---|
| *System → Motherboard* | *Base Memory* 2048 MB | La memoria RAM |
| *System → Motherboard* | *Chipset* PIIX3 | El chipset de la placa base |
| *System → Motherboard* | *Boot Device Order (BIOS only)* | El orden de arranque, solo para BIOS: con UEFI lo lleva el propio firmware |
| *System → Motherboard* | *TPM Version* None, *UEFI* marcado, *Secure Boot* sin marcar | El firmware y su seguridad. Sin TPM 2.0 ni Secure Boot, esta máquina no cumple los requisitos de Windows 11 |
| *System → Processor* | *Number of CPUs* 2 | El procesador. Aquí «CPU» es un **procesador virtual**, y cada uno usa un núcleo de tu procesador real: un portátil tiene un solo chip (*Sockets: 1* en el Administrador de tareas), pero con varios **núcleos** (*Cores*), y cada núcleo puede llevar dos hilos (*Logical processors*). La barra está en verde hasta tus núcleos: más que eso perjudica al anfitrión |
| *System → Acceleration* | *Paravirtualization Interface* Default, *Nested Paging* | Cómo usa la virtualización por hardware. Con *Default*, Ubuntu sabe que está en una máquina virtual (KVM) y colabora |
| *Display* | *Video Memory* 16 MB, *Graphics Controller* VMSVGA | La tarjeta gráfica |
| *Storage* | *Controller: IDE*, con el DVD | El controlador del DVD |
| *Storage* | *Controller: SATA*, tipo AHCI, con el disco en *SATA Port 0* | El controlador de disco y su puerto |
| *Storage* (clic en el `.vdi`) | *Virtual size* 25 GB, *Actual size* (lo que ocupa de verdad), *Dynamically allocated* | El disco, dinámico: crece según se usa |
| *Network → Adapter 1* | *Attached to* NAT, *Adapter Type* Intel PRO/1000 MT Desktop, *MAC Address* | La tarjeta de red y su dirección física (MAC). Hay hasta 4 |
| *USB* | USB 2.0 (OHCI + EHCI) | El controlador USB |

- En VirtualBox, una «CPU» es un **procesador virtual**, y cada uno usa un núcleo del procesador real. Un ordenador suele tener un solo chip (*Sockets: 1*), con varios **núcleos** (*Cores*), y cada núcleo puede llevar dos **hilos** (*Logical processors*). No conviene dar a la máquina más procesadores que núcleos tiene el anfitrión.
- **Paravirtualización:** el sistema invitado sabe que está en una máquina virtual y colabora con el hipervisor, para ir más rápido (en Linux, con la interfaz KVM).

### Instantáneas y estado actual

- Cada **instantánea** es una **foto fija** de la máquina en el momento de tomarla. No se enciende ni se cambia: queda tal cual para poder volver a ella.
- **Current State** (*Estado actual*) es la máquina **tal como está ahora**: la que se enciende y se usa. Cuelga de la última instantánea tomada o restaurada, y **todo lo que se hace con la máquina encendida se guarda aquí**, nunca en una instantánea.
- **Restaurar** una instantánea hace que el estado actual vuelva a ser una copia de esa foto: lo hecho desde entonces se pierde.

Lo que se puede hacer en VirtualBox depende de lo que esté seleccionado en la lista de *Snapshots*:

| Seleccionado | Qué se puede hacer |
|---|---|
| **Current State** | **Start**: encender la máquina; lo que se haga se guarda en el estado actual. **Take**: tomar una instantánea, una foto del estado actual. **Settings**: cambiar la configuración |
| Una **instantánea** | **Restore**: el estado actual pasa a ser una copia de esa foto, y lo hecho desde entonces se pierde (salvo que se marque *Create a snapshot of the current machine state*, que antes lo guarda en otra instantánea). **Delete**: borra la foto; el estado actual no cambia. **Clone**: crea otra máquina a partir de esa foto. Con una instantánea seleccionada, **Start** sale en gris |

### Los controladores de disco: IDE y SATA

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

- Con **NAT**, la máquina sale a Internet a través del anfitrión, pero desde fuera no se la ve. VirtualBox le da una dirección por DHCP.
- **`10.0.2.15/24`** es la dirección **IPv4 privada** que da el NAT de VirtualBox: todas las máquinas con NAT reciben esa misma. `/24` indica que la red son las direcciones `10.0.2.x`.
- La que empieza por **`fd`** es una dirección **IPv6 privada** de esa misma red.
- La tarjeta de red tiene además su dirección física, la **MAC**, que es fija: se ve en el instalador, en el menú de arranque del firmware (arranque por red, PXE) y en *Settings → Network*.

---

## 6. Instalar un sistema operativo

**En una frase:** antes de instalar se comprueban los requisitos y se planifica, sobre todo el disco y el modo de arranque.

**Lo que tienes que saber**

- **Requisitos mínimos** (para que funcione) y **recomendados** (para que vaya bien). Windows 11 pide además **UEFI con Secure Boot** y un chip **TPM 2.0**.
- **Planificar:** comprobar los requisitos, hacer copia de seguridad, decidir las particiones y el gestor de arranque si habrá varios sistemas, tener los drivers y el medio de instalación (ISO en un USB o, en una máquina virtual, en su DVD virtual).
- El **modo de arranque** y la **tabla de particiones** tienen que coincidir: **UEFI con GPT** (lo actual) o **BIOS/heredado con MBR** (lo antiguo).
- Después de instalar: actualizar el sistema e instalar los drivers que falten.
- Una **instalación desatendida** usa un archivo de respuestas para instalar sin preguntar; sirve para instalar muchos equipos iguales.

---

## 7. Discos y particiones

**En una frase:** un disco se divide en particiones, y su lista está en una tabla que puede ser MBR (antigua) o GPT (actual).

**Lo que tienes que saber**

- **MBR:** como mucho 4 particiones principales y discos de hasta 2 TB. Para tener más de 4, una de ellas se hace **extendida** y dentro se crean particiones **lógicas**: es un truco para saltarse ese límite. Va con BIOS.
- **GPT:** hasta 128 particiones (por eso no necesita particiones lógicas), discos enormes y una copia de seguridad de la tabla al final del disco. Va con UEFI.
- Con UEFI hace falta una **partición EFI**: pequeña, en FAT32, con los programas de arranque de cada sistema.
- **Windows con UEFI:** partición EFI, MSR (reservada), Windows (`C:`, NTFS) y recuperación.
- **Ubuntu con UEFI:** partición EFI (montada en `/boot/efi`) y la raíz `/` (ext4). En Linux no hay letras de unidad: cada partición se **monta** en una carpeta.
- Cada partición lleva un **sistema de archivos** (NTFS, ext4, FAT32, exFAT…), que se crea al **formatear**.

**Compara**

| | MBR | GPT |
|---|---|---|
| Firmware | BIOS (heredado) | UEFI |
| Particiones | 4 principales | Hasta 128 |
| Tamaño máximo | 2 TB | Prácticamente sin límite |
| Copia de la tabla | No | Sí, al final del disco |

### Sistemas de archivos: FAT32, ext4 y NTFS

- Un **sistema de archivos** es la forma de organizar los archivos y carpetas dentro de una partición: dónde está guardado cada archivo, su nombre, su tamaño, sus permisos… Una partición vacía no sirve hasta que se le crea uno: es lo que se llama **formatear**.
- La partición EFI tiene que ser **FAT32**, porque el estándar UEFI obliga al firmware a saber leer FAT, y no otros. Linux va en **ext4**, más seguro y con permisos. Windows usa **NTFS**, que también tiene permisos y diario.

**Compara**

| | FAT32 (*File Allocation Table*, 32 bits) | ext4 (*fourth extended filesystem*) |
|---|---|---|
| Qué es | Un sistema de archivos antiguo y sencillo, de los años 90 | El sistema de archivos habitual de Linux |
| Quién lo entiende | Casi todos: Windows, Linux, macOS… y el firmware UEFI | Linux. Windows no lo lee sin programas añadidos |
| Límites | Archivos de hasta 4 GB | Archivos y discos enormes |
| Permisos de usuarios | No | Sí: cada archivo tiene propietario y permisos |
| Si se va la luz | Se puede dañar | Tiene un **diario** (*journaling*): apunta lo que va a cambiar antes de hacerlo, y así se recupera |
| Dónde se usa | La partición EFI y las memorias USB | La raíz de Linux (`/`) |


---

## 8. El arranque y los gestores de arranque

**En una frase:** el firmware busca un gestor de arranque, el gestor carga el kernel y el kernel arranca el resto del sistema.

**Lo que tienes que saber**

- Las fases: **firmware** (POST y búsqueda en el orden de arranque) → **gestor de arranque** → **kernel** → primeros servicios (en Linux, **systemd**) → **inicio de sesión**. Entre el kernel y systemd, en Linux trabaja el **initrd**, un pequeño sistema en memoria que prepara lo necesario para montar la raíz.
- **UEFI** frente a BIOS: arranca más rápido, busca los cargadores en la partición EFI, tiene su propio menú de arranque y **Secure Boot** (solo arranca programas firmados).
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

Lo que se ve al arrancar dice en qué fase falla, y eso dice dónde mirar:

| Lo que ves | Dónde falla | Qué revisar |
|---|---|---|
| Un mensaje del firmware, como `No bootable option or device was found` | El firmware no encuentra nada que arrancar | El orden de arranque, el disco, la partición EFI |
| `grub>` o `grub rescue>` | GRUB arranca, pero no encuentra su configuración | `/boot/grub` y la configuración de GRUB |
| Mensajes del kernel y una consola de emergencia | El kernel no puede montar la raíz | Los parámetros del kernel, el disco |
| Un servicio que falla y se queda esperando | systemd | Los servicios |

### El firmware: BIOS y UEFI

- El **firmware** es un programa guardado en un chip de la placa base. Es lo primero que se ejecuta al encender: comprueba el hardware (el **POST**) y busca un sistema que arrancar.
- **EFI** (*Extensible Firmware Interface*, «interfaz de firmware extensible») es el nombre de la primera versión, creada por Intel: una interfaz entre el firmware y el sistema operativo, «extensible» porque se le pueden añadir programas, los `.efi`. **UEFI** (*Unified Extensible Firmware Interface*) es la misma, convertida en el estándar común de los fabricantes. Se usan como sinónimos: VirtualBox dice «EFI» y Ubuntu, «UEFI». Mucha gente sigue llamando «BIOS» a la configuración del firmware, aunque sea UEFI.

**Compara**

| | BIOS (heredada, *legacy*) | UEFI |
|---|---|---|
| Qué es | El firmware de los PC desde los años 80 | El que la sustituye: lo llevan los ordenadores actuales desde hace más de diez años |
| Cómo arranca | Lee el primer sector del disco y ejecuta el pequeño programa que hay allí | Lee una partición del disco, la **partición EFI** (en FAT32), y ejecuta un programa `.efi` que hay en ella: en Ubuntu, el de GRUB |
| Qué recuerda | Solo el orden de los dispositivos | Una lista de **entradas de arranque** con nombre (`Ubuntu`, `Windows Boot Manager`…) |
| Tabla de particiones | MBR | GPT |
| Además | — | Su propio menú de arranque (*Boot Manager*) y **Secure Boot**, que solo arranca programas firmados |

### GRUB, el gestor de arranque de Linux

- Sus siglas son *GRand Unified Bootloader*, «gran cargador de arranque unificado»: unificado porque sirve para arrancar sistemas muy distintos.
- Es el programa que el firmware ejecuta después de comprobar el hardware. Hace dos cosas: si hay varias opciones, muestra un **menú** para elegir una (con cuenta atrás: si no se toca nada, arranca la primera); y **carga en memoria el kernel** del sistema elegido, que pone en marcha todo lo demás.
- Una ISO de instalación trae **su propio GRUB**, con las opciones de la ISO (instalar, probar el sistema…). Al instalar, Ubuntu pone **otro GRUB en el disco**, con las entradas del sistema instalado.

---

## 9. Actualizaciones y aplicaciones

**En una frase:** el sistema y los programas se actualizan para corregir fallos y de seguridad; los programas se instalan desde fuentes de confianza.

**Lo que tienes que saber**

- **Windows Update:** una **actualización acumulativa** cada mes (incluye las anteriores) y una de características al año. Se gestiona en *Configuración → Windows Update*.
- **Ubuntu** instala programas de los **repositorios** (servidores con paquetes revisados) con `apt`:

| Orden | Qué hace |
|---|---|
| `sudo apt update` | Descarga la lista actualizada de paquetes |
| `sudo apt upgrade` | Actualiza los paquetes instalados |
| `sudo apt install paquete` | Instala un programa |
| `sudo apt remove paquete` | Lo desinstala |

- En **Windows**, los programas se instalan desde la Microsoft Store, con su instalador o desde el terminal con `winget install`; se quitan en *Configuración → Aplicaciones* o con `winget uninstall`.
