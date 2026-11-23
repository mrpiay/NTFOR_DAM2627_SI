# SI · Actividad guiada «Windows en una máquina virtual»

## Punto de partida

En la semana del 9 al 13 instalaste un sistema libre, Ubuntu Server, en una máquina virtual. Ahora toca un sistema **propietario**: Windows 11, el que exige más al equipo (TPM 2.0 y arranque seguro). Lo instalas en una máquina virtual nueva y **documentas la instalación** mientras la haces: cómo es la máquina, qué se decide en cada pantalla, qué incidencias salen y cómo se comprueba que todo funciona.

Es la **UD2 · Sistemas operativos. Instalación**: planificar, instalar y actualizar un sistema propietario, y documentar el proceso.

**Usa la IA como guía, no para que lo haga por ti.** Pídele que te explique lo que no entiendas; **lo que se hace en la máquina lo haces tú**, y el documento cuenta **tu instalación**, con sus incidencias. El objetivo es que lo que hagas **cumpla los requisitos** de cada paso («Comprueba que…») y que sepas **por qué** se hace cada cosa.

**El objetivo es entender cada paso:** es lo que necesitas para responder el cuestionario y preparar los exámenes.

**Evaluación.** Esta actividad guiada (**A4**) comprende los pasos 0 a 6. Se califica, una vez terminada, por su resultado (cuántas de sus 12 comprobaciones salen bien) y por 4 preguntas sobre su diseño y su arquitectura, al 50 %. Qué se muestra en cada nivel, en las [rúbricas](../../programacion/1a-evaluacion.md#rúbricas). El cuestionario de la semana (**C4**) se entrega hasta el lunes 30 de noviembre. El **viernes 4 de diciembre** hay un examen parcial, **P1**, en papel, con todo lo de la 1ª evaluación, también esta actividad. Qué entra y cuánto vale cada parte: [1ª evaluación](../../programacion/1a-evaluacion.md).

---

## Antes de empezar

La teoría está en los [apuntes de esta semana](../apuntes/UD2-instalar-windows.md), que continúan los [apuntes de la UD2 de la semana del 9 al 13](../../2026_11_09-13/apuntes/UD2-sistemas-operativos.md). Antes de cada paso, lee el apartado que le corresponde:

| Pasos | Apartado de los apuntes de esta semana |
|---|---|
| 0 | 2 · Los requisitos de Windows 11 y cómo se comprueban |
| 1 | 3 · La máquina virtual para Windows 11 en VirtualBox |
| 2 y 3 | 4 · El proceso de instalación |
| 4 y 5 | 5 · Después de instalar |
| 6, y el documento en todos | 6 · Documentar la instalación; la instantánea, en el apartado 5 de los [apuntes del 9 al 13](../../2026_11_09-13/apuntes/UD2-sistemas-operativos.md#5-máquinas-virtuales) |

---

## Lo que necesitas

| Qué | Para qué | Pasos |
|---|---|---|
| **La ISO de Windows 11 Enterprise de evaluación**, en español (unos 5–6 GB) | El medio de instalación. Es gratuita y funciona 90 días. Se facilita en clase: no la descargues en el aula | 1 |
| **VirtualBox 7** | El hipervisor, el de la semana del 9 al 13 | 1 a 6 |
| **Unos 30 GB libres** en el disco de tu ordenador y **8 GB de RAM** o más | El disco virtual es dinámico: crece hasta unos 20 GB con Windows instalado | 0 y 1 |
| **`instalacion-windows.md`** | El documento de la instalación. Se crea en el paso 0 y se rellena en todos | Todos |

La guía está probada con **Windows 11** como anfitrión y **VirtualBox 7.2**, en inglés: los nombres de menús y botones de VirtualBox van en inglés y, entre paréntesis, en español. Windows 11 de la máquina virtual se instala en español.

## Qué se trabaja

| Qué | Pasos |
|---|---|
| Comprobar que el equipo puede con Windows 11 en una máquina virtual | 0 |
| Crear una máquina virtual que cumpla los requisitos de Windows 11 | 1 |
| Instalar Windows: las pantallas y lo que se decide en cada una | 2 y 3 |
| Integrar la máquina y comprobar controladores, TPM, versión y actualizaciones | 4 |
| Las particiones que crea Windows | 5 |
| Documentar el proceso | Todos, y 6 |

## Plan de la semana

Cada sesión dura 50 minutos. La instalación se hace en las dos sesiones seguidas del martes; el jueves y el viernes son de repaso.

| Día | Sesión | Qué se hace |
|---|---|---|
| Martes 24 | 13:00 | **Paso 0** (comprobar el equipo y preparar el documento), **paso 1** (crear la máquina) y **paso 2** (instalar). Mientras Windows copia archivos, rellenar el documento. |
| Martes 24 | 13:50 | **Paso 3** (configuración inicial), **paso 4** (después de instalar), **paso 5** (particiones) y **paso 6** (cerrar el documento). Repasar con la lista final («Cómo comprobarlo»). |

**Los pasos se hacen en orden**, cada uno en la sesión que le toca según el plan de la semana.

---

## Paso 0 · Comprobar el equipo y preparar el documento

**Objetivo.** Saber si tu ordenador puede con una máquina virtual de Windows 11 y tener el documento de la instalación listo para rellenar.

**Pista.**

1. Abre el **Administrador de tareas** (`Ctrl + Mayús + Esc`), pestaña **Rendimiento**:
   - en **CPU**, comprueba que **Virtualización** dice **Habilitado** y apunta los núcleos y los procesadores lógicos;
   - en **Memoria**, apunta la memoria total y la que está **en uso**: a la máquina se le darán 4 GB, que tienen que quedar libres;
   - en **Disco**, comprueba en el Explorador de archivos que `C:` tiene **30 GB libres** o más.
2. Crea la carpeta `C:\dam2627\si\windows`, ábrela en VS Code (*File > Open Folder…*) y crea dentro el archivo `instalacion-windows.md` con este contenido:

```markdown
# Instalación de Windows 11 en una máquina virtual

Fecha:
Autor o autora:

## 1. El equipo anfitrión

| Dato | Valor |
|---|---|
| Procesador (núcleos / procesadores lógicos) | |
| Virtualización | |
| Memoria total / en uso | |
| Espacio libre en C: | |
| VirtualBox (versión) | |

## 2. La máquina virtual

| Ajuste | Valor | Por qué |
|---|---|---|
| Nombre | | |
| Sistema operativo | | |
| Memoria base | | |
| Procesadores | | |
| EFI | | |
| TPM | | |
| Arranque seguro | | |
| Disco | | |
| Orden de arranque | | |
| ISO | | |

## 3. La instalación, pantalla a pantalla

| Pantalla | Qué se eligió | Por qué |
|---|---|---|

## 4. Incidencias

| Qué pasó | Cómo se resolvió |
|---|---|

## 5. Comprobaciones después de instalar

| Qué | Cómo se comprobó | Resultado |
|---|---|---|

## 6. Las particiones de Windows

| Partición | Tamaño | Sistema de archivos | Para qué |
|---|---|---|---|
```

3. Rellena el apartado **1. El equipo anfitrión**. La versión de VirtualBox está en su menú **Help → About VirtualBox…** (*Ayuda → Acerca de VirtualBox…*).

**Comprueba que…**

- la virtualización está habilitada y tu equipo tiene 4 GB de RAM y 30 GB de disco libres para la máquina;
- el apartado 1 del documento está completo.

**Si te falla…**

- *Virtualización: Deshabilitado*: hay que activarla en el firmware (Intel VT-x o AMD-V) antes de seguir, porque sin ella la máquina no arranca ([apuntes, apartado 2](../apuntes/UD2-instalar-windows.md#2-los-requisitos-de-windows-11-y-cómo-se-comprueban)).
- *Hay menos de 4 GB de RAM libres*: cierra los programas que no uses (el navegador con muchas pestañas consume mucho) y vuelve a mirar.

---

## Paso 1 · Crear la máquina virtual

**Objetivo.** Una máquina `windows11` que cumpla los requisitos de Windows 11, con la ISO en su unidad óptica.

**Pista.**

1. En VirtualBox, **Machine → New…** (*Máquina → Nueva…*, `Ctrl + N`) y, si no lo está, pulsa **Expert Mode** (*Modo experto*).
2. En **Name and Operating System** (*Nombre y sistema operativo*):
   - **Name** (*Nombre*): `windows11`;
   - **ISO Image** (*Imagen ISO*): la ISO de Windows 11;
   - **Type** (*Tipo*): `Microsoft Windows`; **Version** (*Versión*): `Windows 11 (64-bit)`;
   - marca **Skip Unattended Installation** (*Omitir la instalación desatendida*): la instalación será **interactiva**, para ver y documentar cada pantalla.
3. En **Hardware**: **Base Memory** (*Memoria base*) `4096 MB`, **Processors** (*Procesadores*) `2` y **Enable EFI** (*Habilitar EFI*) marcado.
4. En **Hard Disk** (*Disco duro*): **Create a Virtual Hard Disk Now** (*Crear un disco duro virtual ahora*), `80 GB`, tipo **VDI**, con **Pre-allocate Full Size** (*Reservar el tamaño completo*) **sin marcar**: disco dinámico.
5. Pulsa **Finish** (*Terminar*). Con la máquina seleccionada, **Settings** (*Configuración*):
   - **System → Motherboard** (*Sistema → Placa base*): **TPM** `v2.0`, **Enable Secure Boot** (*Habilitar arranque seguro*) marcado y, en **Boot Order** (*Orden de arranque*), **Optical** (*Óptica*) delante de **Hard Disk** (*Disco duro*);
   - **Storage** (*Almacenamiento*): la unidad óptica tiene la ISO de Windows.
6. Rellena el apartado **2. La máquina virtual** del documento: cada ajuste, su valor y por qué (por ejemplo, «TPM v2.0: lo exige Windows 11»).

**Comprueba que…**

- la máquina `windows11` tiene 4096 MB, 2 procesadores, EFI, TPM 2.0, arranque seguro y un disco VDI dinámico de 80 GB, y la ISO en la unidad óptica, que va primera en el orden de arranque;
- el apartado 2 del documento tiene todos los ajustes con su porqué.

**Si te falla…**

- *VirtualBox marca la memoria o los procesadores en rojo*: el anfitrión no puede darlos. Baja la memoria a la zona verde (mínimo 4096 MB para Windows 11) o cierra programas.
- *No aparece la opción TPM*: tu VirtualBox es anterior a la versión 7. Actualízalo antes de seguir.

---

## Paso 2 · Instalar Windows

**Objetivo.** Windows 11 copiado en el disco de la máquina, con cada decisión apuntada en el documento.

**Pista.**

1. Pulsa **Start** (*Iniciar*). Si sale **Press any key to boot from CD or DVD…**, pulsa una tecla enseguida: si no, la máquina intenta arrancar desde el disco vacío.
2. Sigue las pantallas del [apartado 4 de los apuntes](../apuntes/UD2-instalar-windows.md#4-el-proceso-de-instalación):
   - **idioma, formato de hora y moneda, y teclado**: Español (España);
   - **Instalar ahora**;
   - **términos de la licencia**: acéptalos;
   - **tipo de instalación**: **Personalizada: instalar solo Windows (avanzado)**;
   - **dónde instalar**: **Espacio sin asignar en la unidad 0** y **Siguiente**, sin crear particiones: Windows crea las que necesita.
3. Windows copia los archivos y se reinicia solo. **Mientras copia** (tarda entre 10 y 20 minutos), apunta en el apartado **3. La instalación, pantalla a pantalla** cada pantalla, qué elegiste y por qué, y en **4. Incidencias**, cualquier cosa que no saliera a la primera.

**Comprueba que…**

- la instalación avanza por «Copiando archivos de Windows» e «Instalando características»;
- el apartado 3 del documento tiene las pantallas, de la del idioma a la de dónde instalar, con lo elegido y su porqué.

**Si te falla…**

- *Sale «Este equipo no puede ejecutar Windows 11»*: falta TPM 2.0 o arranque seguro. Apaga la máquina (**File → Close… → Power off the machine**, *Archivo → Cerrar… → Apagar la máquina*), revisa **System → Motherboard** y vuelve a empezar. Apúntalo en Incidencias.
- *Sale la consola de UEFI (`Shell>`) o «No bootable medium found»*: no se pulsó una tecla a tiempo o la ISO no está en la unidad óptica. Reinicia la máquina (**Machine → Reset**, *Máquina → Reiniciar*) y pulsa una tecla en cuanto salga el mensaje.
- *El ratón se queda dentro de la máquina*: suéltalo con la **tecla anfitrión**, `Ctrl` derecho.

---

## Paso 3 · La configuración inicial

**Objetivo.** Entrar en el escritorio de Windows 11 con un **usuario local**, sin cuenta de Microsoft.

**Pista.**

1. Tras el reinicio, Windows pregunta la **región** (España), la **distribución de teclado** (Español) y si quieres otra (**Omitir**). Después configura la red: la máquina tiene Internet por NAT.
2. En la pantalla de la cuenta, pulsa **Opciones de inicio de sesión** y elige **Unirse a un dominio** (o **Unirse al dominio en su lugar**). Así se crea un **usuario local**: escribe `dam` como nombre, una contraseña que recuerdes y las tres **preguntas de seguridad**.
3. En las pantallas de **privacidad** (ubicación, encontrar mi dispositivo, datos de diagnóstico, publicidad…), elige **No** en todas: se pueden cambiar después.
4. Espera a que Windows termine de configurarse, sin apagar la máquina. Cuando salga el escritorio, si pregunta si el equipo puede ser **detectable en la red**, responde **No**: la red de la máquina es NAT, no una red de confianza.
5. **Quita la ISO** de la unidad óptica: en la ventana de la máquina, **Devices → Optical Drives → Remove disk from virtual drive** (*Dispositivos → Unidades ópticas → Quitar disco de la unidad virtual*).
6. Sigue apuntando en el documento: las pantallas de este paso en el apartado 3 y lo que no salió a la primera en el 4.

**Comprueba que…**

- estás en el escritorio de Windows 11, con el menú Inicio en el centro de la barra de tareas, y has entrado con el usuario local `dam`;
- la ISO ya no está en la unidad óptica;
- el apartado 3 del documento llega hasta el escritorio.

**Si te falla…**

- *No sale «Opciones de inicio de sesión» y pide una cuenta de Microsoft*: no es la ISO de evaluación de Enterprise, sino una de Home o Pro, que no permiten crear un usuario local. Apúntalo en Incidencias y repite la instalación desde el paso 1 con la ISO de evaluación.

---

## Paso 4 · Después de instalar

**Objetivo.** Integrar la máquina con el anfitrión y comprobar que Windows funciona: controladores, TPM, versión y actualizaciones.

**Pista.**

1. **Guest Additions:** en la ventana de la máquina, **Devices → Insert Guest Additions CD image…** (*Dispositivos → Insertar imagen de CD de las «Guest Additions»…*). En el Explorador de archivos de Windows, abre la unidad de CD y ejecuta **`VBoxWindowsAdditions.exe`**, acepta las preguntas y **reinicia** la máquina. Después, la pantalla se ajusta al tamaño de la ventana y el ratón entra y sale sin la tecla anfitrión.
2. **Controladores:** botón secundario sobre **Inicio → Administrador de dispositivos**. Comprueba que ningún dispositivo tiene **marca amarilla** y, en **Adaptadores de pantalla**, que ya no sale el **Adaptador de pantalla básico de Microsoft**, sino el de VirtualBox.
3. **TPM:** `Windows + R`, escribe `tpm.msc` e Intro: tiene que decir **«TPM está listo para usarse»** y **«Versión de la especificación: 2.0»**.
4. **Versión:** `Windows + R`, escribe `dxdiag` e Intro. En la pestaña **Sistema**, apunta el **Sistema operativo** (edición y compilación) y la **Versión de DirectX**.
5. **Actualizaciones:** **Configuración → Windows Update → Buscar actualizaciones**. No hace falta esperar a que se instalen todas: apunta qué encuentra y su estado.
6. Rellena el apartado **5. Comprobaciones después de instalar**: qué comprobaste, cómo y el resultado de cada una.

**Comprueba que…**

- la pantalla se adapta a la ventana y el Administrador de dispositivos no tiene avisos amarillos;
- `tpm.msc` muestra el TPM listo, versión 2.0;
- el apartado 5 del documento tiene las cinco comprobaciones con su resultado.

**Si te falla…**

- *Al insertar el CD de las Guest Additions no aparece nada*: abre el Explorador de archivos y entra en la unidad de CD (`D:`) a mano.
- *Windows Update tarda mucho*: déjalo trabajando y sigue con el paso 5; apunta en qué estado lo dejaste.

---

## Paso 5 · Las particiones de Windows

**Objetivo.** Ver qué particiones creó Windows en el disco vacío y para qué sirve cada una.

**Pista.**

1. Botón secundario sobre **Inicio → Administración de discos**. En el **Disco 0** salen las particiones: la **partición de sistema EFI**, **`C:`** y la **partición de recuperación**. Apunta el tamaño y el sistema de archivos de cada una.
2. Abre el **Terminal** como administrador (botón secundario sobre **Inicio → Terminal (Administrador)**) y escribe:

   ```text
   diskpart
   list disk
   select disk 0
   list partition
   list volume
   exit
   ```

   `list disk` marca el disco con `*` en la columna **Gpt**: el disco es GPT. `list partition` muestra además la partición **reservada** (MSR), que Administración de discos no enseña.
3. Rellena el apartado **6. Las particiones de Windows** del documento, con todas las particiones de `list partition`, su tamaño, su sistema de archivos y para qué sirve cada una.

**Comprueba que…**

- el apartado 6 del documento tiene las particiones EFI, reservada, `C:` y recuperación, con su tamaño y su uso;
- sabes decir por qué el disco es GPT y no MBR.

---

## Paso 6 · Cerrar el documento y la instantánea

**Objetivo.** El documento de la instalación completo y la máquina guardada en un estado limpio.

**Pista.**

1. Repasa `instalacion-windows.md` de arriba abajo: que cada apartado esté completo y que el apartado **4. Incidencias** recoja lo que pasó de verdad (si no hubo ninguna, escríbelo).
2. Apaga Windows desde **Inicio → Apagar**.
3. Con la máquina apagada, toma una **instantánea** llamada `windows-instalado` (**Snapshots → Take**, *Instantáneas → Tomar*): es el punto al que volver en las prácticas de Windows de la 2ª evaluación.

**Comprueba que…**

- los seis apartados del documento están completos;
- la máquina `windows11` tiene la instantánea `windows-instalado`.

---

## Entrega

Qué se entrega y cuándo: [`entrega.md`](entrega.md).

## Cómo comprobarlo (lista final)

| Comprobación | Hecho |
|---|---|
| Comprobé que mi equipo tiene la virtualización habilitada y memoria y disco suficientes |  |
| La máquina `windows11` tiene 4096 MB, 2 procesadores, EFI, TPM 2.0, arranque seguro y un disco VDI dinámico de 80 GB |  |
| Windows 11 está instalado y arranca sin la ISO hasta el escritorio, con el usuario local `dam` |  |
| Las Guest Additions están instaladas y el Administrador de dispositivos no tiene avisos amarillos |  |
| `tpm.msc` muestra el TPM listo, versión 2.0, y apunté la versión de Windows con `dxdiag` |  |
| Sé qué particiones creó Windows, para qué sirve cada una y por qué el disco es GPT |  |
| `instalacion-windows.md` tiene la máquina, las pantallas con lo elegido y su porqué, las incidencias, las comprobaciones y las particiones |  |
| La máquina tiene la instantánea `windows-instalado` |  |
