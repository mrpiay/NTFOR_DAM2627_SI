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
- Si en Windows está activo **Hyper-V** (lo usan WSL y algunas funciones de seguridad), VirtualBox funciona por encima de él (en VirtualBox, *native API*): funciona, pero más despacio.
- Una máquina son unos pocos archivos: su configuración (`.vbox`) y su **disco virtual** (`.vdi`), que puede ser **dinámico** (crece según se usa) o de **tamaño fijo** (más rápido).
- Una **instantánea** guarda el estado de la máquina para volver a él si algo sale mal. Mejor tomarla con la máquina apagada: guarda solo el disco y la configuración.
- Usos: probar sistemas y programas sin riesgo, aprender, aprovechar un servidor para muchos servicios, y copias de seguridad.
- Los **contenedores** (Docker) son otra forma de virtualizar, más ligera: comparten el kernel del anfitrión. Se ven en la UD6.

**Compara**

| | Tipo 1 | Tipo 2 |
|---|---|---|
| Dónde se instala | Directamente sobre el hardware | Dentro de un sistema operativo |
| Uso típico | Servidores | Ordenadores personales, aprendizaje |
| Ejemplos | VMware ESXi, Hyper-V, Proxmox | VirtualBox, VMware Workstation |

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

---

## 8. El arranque y los gestores de arranque

**En una frase:** el firmware busca un gestor de arranque, el gestor carga el kernel y el kernel arranca el resto del sistema.

**Lo que tienes que saber**

- Las fases: **firmware** (POST y búsqueda en el orden de arranque) → **gestor de arranque** → **kernel** → primeros servicios (en Linux, **systemd**) → **inicio de sesión**.
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

- En **Windows**, los programas se instalan desde la Microsoft Store, con su instalador o desde el terminal con `winget install`, y se quitan en *Configuración → Aplicaciones*.
