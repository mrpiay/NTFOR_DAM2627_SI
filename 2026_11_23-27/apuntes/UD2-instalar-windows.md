# UD2 · Instalar Windows en una máquina virtual

Continuación de los [apuntes de la UD2 de la semana del 9 al 13](../../2026_11_09-13/apuntes/UD2-sistemas-operativos.md), que tienen lo general: qué es una máquina virtual, cómo se planifica una instalación, las particiones y los sistemas de archivos. Aquí, lo propio de Windows: sus ediciones, sus requisitos y cómo se comprueban, la máquina virtual que necesita, el proceso de instalación, lo que se hace después y cómo se documenta. Todo sale del libro de Paraninfo, *Sistemas informáticos*, capítulo 2; cada apartado indica las páginas (en el lector, hay que sumar 12).

Hay dos tipos de contenido:

- Lo que no lleva marca es lo **imprescindible**: hay que entenderlo y saber explicarlo con tus palabras.
- > **Para saber más.** Lo que va en un recuadro como este ayuda a entender, pero no hay que aprenderlo de memoria.

---

## 1. Windows: versiones y ediciones

*Paraninfo 2.5.3, pp. 122–123.*

**En una frase:** Windows es el sistema operativo de Microsoft; la versión actual es Windows 11, y de cada versión hay varias **ediciones** con más o menos funciones.

**Lo que tienes que saber**

- Las primeras versiones (Windows 1.0 de 1985 a Windows 3.11) eran una aplicación gráfica que funcionaba sobre **MS-DOS** (*Microsoft Disk Operating System*). Desde **Windows 95** es un sistema operativo completo. Después vinieron 98, ME, XP, Vista, 8, 10 y 11.
- Para servidores hay una familia aparte: Windows NT, Windows 2000 y **Windows Server** (2003, 2008, 2012, 2016, 2019, 2022…).
- Windows 10 sigue muy extendido, y se va sustituyendo por Windows 11.

**Compara: las ediciones de Windows 11**

| Edición | Para quién | Qué añade |
|---|---|---|
| **Home** | Uso doméstico | Es la más básica |
| **Pro** | Profesionales y pequeñas empresas | Cifrado de unidades con BitLocker, escritorio remoto, unirse a un dominio o a Active Directory de Azure |
| **Pro for Workstations** | Empresas más grandes | Medidas especiales de seguridad y protección |
| **Enterprise** | Medianas y grandes empresas | Se vende con licencias por volumen |
| **Education** y **Pro for Education** | Centros educativos | Casi todo lo de Pro, con fines educativos |

> **Para saber más.** Las variantes **N** y **KN** de cada edición tienen lo mismo, pero sin algunos programas multimedia, como el Reproductor de Windows Media o la grabadora de voz (p. 128). Existe también **Windows 11 SE**, basado en la nube, para educación.

---

## 2. Los requisitos de Windows 11 y cómo se comprueban

*Paraninfo 2.5.1, pp. 103–104, y 2.5.3, pp. 123–125.*

**En una frase:** Windows 11 exige, además de procesador, memoria y disco, un firmware **UEFI con arranque seguro** y un chip **TPM 2.0**; antes de instalar se comprueba que el equipo los cumple.

**Lo que tienes que saber**

- **TPM** (*Trusted Platform Module*, módulo de plataforma segura): un chip de la placa base que guarda claves de cifrado y ayuda a comprobar que el equipo arranca sin manipulaciones. Windows 11 pide la **versión 2.0**. Si se instala en la placa, hay que **activarlo en el firmware** (BIOS UEFI).
- **Arranque seguro** (*Secure Boot*): una opción del firmware UEFI que solo deja arrancar programas de arranque firmados. También se activa en el firmware.
- Cómo se comprueba en un Windows ya instalado:

| Qué | Cómo |
|---|---|
| CPU, memoria, discos, red, GPU y si la virtualización está habilitada | **Administrador de tareas** (Ctrl+Mayús+Esc), pestaña **Rendimiento** |
| Todo el equipo en detalle | **Información del sistema**, ejecutada como administrador |
| Si hay chip TPM, si está listo y su versión | Windows+R y `tpm.msc`: «TPM está listo para usarse» y «Versión de la especificación: 2.0» |
| Versión de DirectX y del controlador gráfico (WDDM) | Windows+R y `dxdiag`: pestaña **Sistema** (versión de DirectX) y pestaña **Pantalla** (modelo de controlador) |

- Para instalar en una **máquina virtual** hace falta, además, la **virtualización asistida por hardware**, **HAV** (*Hardware Assisted Virtualization*): Intel VT o AMD-V. A veces viene desactivada aunque el procesador la tenga, y hay que activarla en el firmware. En el Administrador de tareas aparece como «Virtualización: Habilitado».

**Compara: requisitos mínimos de Windows 11 y de Windows 10**

| | Windows 11 | Windows 10 |
|---|---|---|
| Procesador | Doble núcleo de 64 bits, 1 GHz o más | 1 GHz |
| Memoria RAM | 4 GB | 1 GB (32 bits) o 2 GB (64 bits) |
| Disco | 64 GB (mejor más, para actualizaciones y aplicaciones) | 16 GB (32 bits) o 20 GB (64 bits) |
| Tarjeta gráfica | DirectX 12 y controlador WDDM 2.0 | DirectX 9 y controlador WDDM 1.0 |
| Pantalla | 720p (1280 × 720) | 800 × 600 |
| Firmware | UEFI con arranque seguro | — |
| TPM | Versión 2.0 | — |

En los dos hacen falta conexión a Internet, para las actualizaciones, y una unidad de DVD o un puerto USB para el medio de instalación; en una máquina virtual, un DVD virtual con el fichero ISO.

> **Para saber más.** **DirectX** es la interfaz de programación (API) de Windows con la que las aplicaciones usan directamente el hardware de vídeo y de audio. **WDDM** (*Windows Display Driver Model*) es el modelo de los controladores de las tarjetas gráficas (p. 125).

---

## 3. La máquina virtual para Windows 11 en VirtualBox

*Paraninfo 2.4.3, pp. 87–100 (actividad resuelta 2.4).*

**En una frase:** la máquina se crea con **Nueva**, con memoria, procesadores, EFI y un disco suficientes, y antes de arrancarla se comprueba que tiene **TPM 2.0**, **arranque seguro** y la ISO en la unidad óptica, que va primera en el orden de arranque.

**Lo que tienes que saber**

- **Crear la máquina:** **Máquina → Nueva…** (Ctrl+N). En **Modo experto** todo está en una ventana; en **Modo guiado**, en pantallas sucesivas. Se indican el nombre, la carpeta, la ISO (o después), el **Tipo** (Microsoft Windows) y la **Versión** (Windows 11, 64 bits).
- **Instalación desatendida.** Si se elige la ISO al crear la máquina y no se marca **Skip Unattended Installation**, VirtualBox instala Windows solo, con el usuario, la contraseña y el nombre del equipo que se le den. Si se marca, la instalación es **interactiva**: Windows va preguntando, como en el apartado 4.
- **Recursos:**

| Ajuste | Dónde | Valor del libro para Windows 11 |
|---|---|---|
| Memoria base | *Hardware*, o **Sistema → Placa base** | 4096 MB (sin pasar de la zona verde) |
| Procesadores | *Hardware*, o **Sistema → Procesador** | 2 |
| Arranque EFI | *Hardware*, o **Sistema → Placa base** | Marcado |
| Disco duro | *Hard Disk* | Nuevo, **VDI**, 80 GB, **reservado dinámicamente** (sin marcar *Pre-allocate Full Size*) |
| TPM | **Sistema → Placa base** | **v2.0** |
| Arranque seguro | **Sistema → Placa base** | **Enable Secure Boot** marcado |
| Orden de arranque | **Sistema → Placa base** | **Óptica** delante de **Disco duro** |
| Memoria de vídeo y 3D | **Pantalla** | 256 MB y aceleración 3D, si el anfitrión lo permite |
| ISO | **Almacenamiento**, en la unidad óptica vacía: icono del disco → **Seleccionar un archivo de disco…** | La ISO de Windows |

- **No hay que asignar más de lo que el anfitrión puede dar:** lo que se da a la máquina se quita al equipo real. VirtualBox lo marca en verde (bien) y en rojo (demasiado).
- **Tecla anfitrión** (*host*): por defecto, **Ctrl derecho**. Sirve para soltar el ratón de la máquina, y **tecla anfitrión + Supr** envía Ctrl+Alt+Supr a la máquina sin que lo capture Windows anfitrión.
- **Guest Additions:** programas que se instalan **en el sistema invitado** para integrarlo con el anfitrión: el ratón entra y sale sin tecla anfitrión, la pantalla se adapta a la ventana, se comparten carpetas y portapapeles, se puede arrastrar y soltar y se sincroniza la hora. Se instalan con **Dispositivos → Insertar imagen de CD de las «Guest Additions»…** y, si no arranca sola, ejecutándola desde el Explorador de archivos del invitado.

> **Para saber más.** Si el programa de virtualización no puede dar un TPM virtual, el libro explica cómo saltarse las comprobaciones de Windows 11 durante la instalación: en la primera pantalla, Mayúsculas+F10 abre una consola; con `regedit` se crea la clave `HKEY_LOCAL_MACHINE\SYSTEM\Setup\LabConfig` con valores DWORD a 1 llamados `BypassTPMCheck`, `BypassSecureBootCheck`, `BypassRAMCheck`, `BypassStorageCheck` y `BypassCPUCheck` (actividad resuelta 2.9, p. 134). Con VirtualBox 7 no hace falta, porque tiene TPM 2.0 y arranque seguro.

---

## 4. El proceso de instalación

*Paraninfo 2.5.3, pp. 125–133.*

**En una frase:** se arranca desde la ISO, se elige idioma y edición, se instala en el espacio sin asignar del disco y, tras reiniciar, se configuran región, red, usuario y privacidad.

**Lo que tienes que saber**

Las pantallas, en orden:

1. Si aparece el mensaje de **pulsar una tecla para arrancar desde el CD o DVD**, se pulsa: si no, la máquina intenta arrancar desde el disco, que está vacío.
2. **Idioma, formato de hora y moneda, y teclado:** Español (España).
3. **Instalar ahora.** (*Reparar el equipo* lleva a las opciones de recuperación.)
4. **Clave de producto**, o **No tengo la clave del producto** para ponerla después.
5. **Edición** que se instala (si la imagen trae varias). El libro recomienda Pro o Education si se tiene licencia.

   Con la **versión de evaluación de Windows 11 Enterprise** (la que se usa en clase: gratuita, 90 días), las pantallas 4 y 5 no aparecen: no pide clave y solo trae una edición.
6. **Términos de la licencia:** marcar **Acepto** y Siguiente.
7. **Tipo de instalación: Personalizada: instalar solo Windows (avanzado).** *Actualización* conserva lo que haya; aquí el disco está vacío.
8. **Dónde instalar:** **Espacio sin asignar en la unidad 0** y Siguiente. Desde esta pantalla se pueden crear, eliminar, formatear y extender particiones; si se deja el espacio sin asignar, Windows crea él solo las que necesita.
9. Windows **copia los archivos**, instala características y actualizaciones, y **se reinicia** solo.
10. Configuración inicial: **región**, **distribución de teclado** (y otra adicional, o *Omitir*), **red**.
11. **Cuenta:** con una cuenta de Microsoft, o **Unirse a un dominio**, que permite crear un **usuario local** con su contraseña y tres **preguntas de seguridad**. En clase, con la versión de evaluación, se elige **Unirse a un dominio** y se crea un usuario local. (Las ediciones Home y Pro de Windows 11 piden una cuenta de Microsoft y conexión a Internet.)
12. **Privacidad:** reconocimiento de voz, ubicación, encontrar el dispositivo, datos de diagnóstico, publicidad, historial de actividad. Todo se puede cambiar después.
13. Windows termina de configurarse (puede tardar varios minutos: no hay que apagar la máquina) y aparece el **escritorio**. Al conectarse a la red pregunta si el equipo puede ser **detectado por otros**: solo en redes conocidas, nunca en públicas.

En Windows 11, el menú Inicio y los iconos de la barra de tareas están por defecto **en el centro**, no a la izquierda (p. 133).

---

## 5. Después de instalar

*Paraninfo 2.5.3, pp. 134–138.*

**En una frase:** se actualiza el sistema con **Windows Update**, se comprueba en el **Administrador de dispositivos** que todos los dispositivos tienen controlador y se revisan las particiones que ha creado Windows.

**Lo que tienes que saber**

- **Windows Update** (**Configuración → Windows Update**): busca, descarga e instala las actualizaciones, que corrigen fallos, cierran agujeros de seguridad y añaden funciones. Permite pausarlas (no se aconseja), ver el **historial**, elegir en **Opciones avanzadas** cuándo y cómo se instalan y entrar en el **Programa Windows Insider** (versiones de prueba).
- **Controladores (drivers):** sin ellos el sistema no reconoce los dispositivos. En el **Administrador de dispositivos** (botón secundario sobre **Inicio**), un dispositivo mal reconocido lleva una **marca amarilla**. Con el botón secundario: **Actualizar controlador** (busca en Internet o en el equipo), deshabilitar o desinstalar. En **Propiedades**, la pestaña **General** dice si funciona bien y la pestaña **Controlador**, qué archivo y qué versión usa.
- En una máquina virtual recién instalada suele faltar el controlador de pantalla: aparece el **Adaptador de pantalla básico de Microsoft** hasta que se instalan las **Guest Additions**.
- **Las particiones que crea Windows** en un disco GPT, vistas en **Administración de discos** (en **Herramientas de Windows → Administración de equipos**):

| Partición | Tamaño aproximado | Para qué |
|---|---|---|
| Partición de sistema **EFI** | 100 MB, FAT32 | Los programas de arranque |
| **C:** | El resto, NTFS | Windows, programas y datos (arranque, archivo de paginación) |
| Partición de **recuperación** | Unos 600 MB, NTFS | Las herramientas para reparar Windows |

  (También crea una pequeña partición reservada, **MSR**, que Administración de discos no muestra.)
- **`diskpart`**, lo mismo desde la línea de comandos (como administrador):

| Orden | Qué hace |
|---|---|
| `list disk` | Lista los discos; un `*` en la columna Gpt indica que el disco es GPT |
| `select disk 0` | Selecciona el disco 0 |
| `list partition` | Lista las particiones del disco seleccionado |
| `list volume` | Lista los volúmenes, con su letra, sistema de archivos y tamaño |

- Si se añade un disco nuevo, Windows pide **inicializarlo** con un estilo de partición: **MBR** o **GPT**.

### MBR y GPT

*Paraninfo 2.6, p. 139. Más detalle en el [apartado 7 de los apuntes del 9 al 13](../../2026_11_09-13/apuntes/UD2-sistemas-operativos.md#7-discos-y-particiones).*

- La **tabla de particiones** es la lista de las particiones del disco: dónde empieza y acaba cada una y de qué tipo es. Va al principio del disco, y hay dos tipos (el **estilo de partición** de Windows):
  - **MBR** (*Master Boot Record*, registro de arranque principal): la tabla antigua. Va en el primer sector del disco, con el pequeño programa de arranque que ejecuta la BIOS. Admite como mucho **4 particiones principales** (más, con una **extendida** que contiene particiones **lógicas**) y discos de hasta **2 TB**.
  - **GPT** (*GUID Partition Table*, tabla de particiones con identificadores únicos): la actual, parte del estándar UEFI. Admite discos de más de 2 TB y muchas particiones (Windows, hasta 128) sin necesidad de extendidas, y guarda **una copia de la tabla al final del disco**: si se daña la del principio, se recupera. El libro resume sus ventajas: más tamaño de disco, más particiones, más seguridad en los datos y un arranque más rápido.
- **Cada tabla va con un firmware:** **BIOS con MBR** y **UEFI con GPT**. Windows 11 exige UEFI, así que se instala siempre en un disco GPT, con la partición **EFI** para el arranque. Si el modo de arranque y la tabla no coinciden, el firmware no encuentra el sistema.
- **Cómo se ve en Windows:**

| Qué | Dónde |
|---|---|
| El modo de arranque, UEFI o BIOS | **Información del sistema** (`msinfo32`) → **Resumen del sistema** → **Modo de BIOS**: *UEFI* o *Heredado* (BIOS) |
| La tabla del disco, MBR o GPT | En `diskpart`, `list disk`: un `*` en la columna **Gpt**. En PowerShell, `Get-Disk`: la columna **Partition Style**. En Administración de discos, botón secundario sobre el disco → **Propiedades** → **Volúmenes** → **Estilo de partición** |

**Ejemplo: un portátil real con Windows 11.** Administración de discos muestra el *Disco 0*, de 476,92 GB (un SSD de 512 GB: el fabricante cuenta 1 GB como 1000 MB y Windows, como 1024), con tres particiones: la **EFI** (260 MB), **C:** (475,78 GB, NTFS) y la de **recuperación** (905 MB). Es un disco GPT: tiene partición EFI. La numeración salta de la 1 a la 3 porque la 2 es la **MSR**, que no se muestra. Los tamaños de la EFI y de la recuperación no coinciden con los de la tabla de particiones de más arriba (100 MB y unos 600 MB): dependen de quién instaló Windows, el fabricante o el instalador de Microsoft; las particiones son las mismas.

### FAT32 y NTFS

*Más detalle en el [apartado 7 de los apuntes del 9 al 13](../../2026_11_09-13/apuntes/UD2-sistemas-operativos.md#sistemas-de-archivos-fat32-ext4-y-ntfs). Para ampliar: Síntesis, cap. 3, 3.2 «Sistemas de archivos» (FAT, exFAT y NTFS), pp. 93–95.*

- El **sistema de archivos** organiza el interior de una partición en archivos y carpetas. Windows usa dos: **NTFS** para el disco del sistema y **FAT32** (o exFAT) para lo que tiene que entender cualquier equipo.
- Windows 11 **solo se instala en NTFS**: `C:` y la partición de recuperación son NTFS. La partición **EFI** es **FAT32**, porque el firmware UEFI solo sabe leer FAT.
- Se ve en el **Explorador de archivos**: botón secundario sobre la unidad → **Propiedades** → pestaña **General** → **Sistema de archivos**. También en Administración de discos y con `list volume` en `diskpart`.

**Compara**

| | FAT32 (*File Allocation Table*, tabla de asignación de archivos, 32 bits) | NTFS (*New Technology File System*, sistema de archivos de nueva tecnología) |
|---|---|---|
| Origen | De los años 90 (Windows 95). Sencillo | De Windows NT (1993). El de Windows desde XP |
| Tamaño máximo de un archivo | **4 GB** | Prácticamente sin límite |
| Tamaño de la partición | Windows solo formatea en FAT32 hasta 32 GB | Prácticamente sin límite |
| Permisos | No: cualquiera que use el equipo puede leer y borrar todo | Sí: cada archivo y carpeta tiene una lista de usuarios y grupos con sus permisos (pestaña **Seguridad** de Propiedades, que en FAT32 no aparece) |
| Diario (*journaling*) | No: si se va la luz mientras escribe, se puede dañar | Sí: apunta lo que va a cambiar antes de hacerlo, y al arrancar se recupera |
| Otras funciones | Ninguna | Compresión, cifrado de archivos, cuotas de disco (cuánto puede ocupar cada usuario) |
| Quién lo entiende | Casi todos: Windows, Linux, macOS, televisores, cámaras… y el firmware UEFI | Windows. Linux lo lee y lo escribe; macOS solo lo lee |
| Dónde se usa | La partición EFI y las memorias USB pequeñas | `C:` y los discos internos de Windows |

- **exFAT** (*Extended FAT*) es un FAT moderno: sin el límite de 4 GB por archivo, pero tampoco tiene permisos ni diario. Es el de las memorias USB y tarjetas grandes, porque lo entienden Windows, macOS y Linux.

**Ejemplo.** La ISO de Windows 11 ocupa más de 5 GB. Si se copia a una memoria USB en FAT32, Windows responde *El archivo es demasiado grande para el sistema de archivos de destino*, aunque quede espacio libre: es el límite de 4 GB por archivo. En exFAT o NTFS se copia sin problema.

> **Para saber más.** En Windows, una **partición** es una división del disco, y un **volumen** puede ser una partición, varios discos o partes de varios discos, si los discos son **dinámicos** (p. 137).

---

## 6. Documentar la instalación

*Paraninfo 2.5.2, p. 122, y lo mismo para Windows al final de 2.5.3.*

**En una frase:** al terminar una instalación, se deja por escrito cómo se hizo, para poder mantener el equipo y actualizarlo después.

**Lo que tienes que saber**

- El libro lo dice así: «una vez realizado el proceso de instalación es importante documentarlo y guardarlo para un mejor mantenimiento y futuras actualizaciones». Quien tenga que reparar, actualizar o repetir la instalación (otra persona, o quien la hizo, meses después) sabe cómo está el equipo sin tener que adivinarlo.
- Lo básico que recoge el documento de una instalación:

| Qué | Por qué |
|---|---|
| El **equipo** (o la máquina virtual) y su **configuración** | Para saber en qué hardware funciona y con qué ajustes |
| Lo que se **eligió** en cada paso, con su **porqué** | Para repetir la instalación igual o entender una decisión |
| Las **incidencias** y cómo se resolvieron | Si vuelven a pasar, ya se sabe la solución |
| Las **comprobaciones** hechas después y su resultado | Para saber que el sistema quedó funcionando |
| Las **particiones** que se crearon | Para tocar el disco sin perder datos |

- Se escribe **mientras se instala**, no al final de memoria: los detalles (un mensaje de error, un valor) se olvidan enseguida.
