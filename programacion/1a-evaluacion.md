# 1ª evaluación · SI

[← Programación](README.md)

Cómo se calcula la nota de la 1ª evaluación, qué contenidos entran en los exámenes y planificación semanal. La planificación empieza el 2 de noviembre; lo que ya evaluó Julia (exámenes y tareas de Teams) está en la fila «Antes del 2 nov».

**En este documento:** [Cómo se evalúa](#cómo-se-evalúa-de-dónde-sale-la-nota) · [Qué entra en los exámenes](#qué-entra-en-los-exámenes) · [Rúbricas](#rúbricas) · [Planificación semanal](#planificación-semanal) · [Notas](#notas)

## Cómo se evalúa: de dónde sale la nota

Porcentajes sobre la nota de la evaluación: entre todas las partes suman 100 %.

| Parte | Peso | Qué incluye |
|---|---|---|
| **P** · exámenes parciales | 40 % | P1 · vie 4 dic: 40 % |
| **A** · actividades guiadas | 20 % | 4 actividades, 5 % cada una. Nivel de implementación (50 %) y de comprensión (50 %) |
| **F** · examen final | 30 % | vie 11 dic |
| **R** · autoevaluación | 10 % | Una sola, la semana del examen final: una tarea de Teams con la [plantilla de autoevaluación](autoevaluacion-1a.xlsx) |
| **C** · cuestionarios | — | 4 cuestionarios. No tienen nota propia, pero su entrega es obligatoria: sin todos ellos entregados, la R es un 0 |

## Qué entra en los exámenes

Los porcentajes de esta sección no son partes de la nota: dicen cuánto pesa cada unidad y cada contenido **dentro de los exámenes**. Con ellos se reparte el 40 % de los exámenes parciales (P) entre lo que evaluó Julia y el examen parcial, y valen igual para el examen final (F), que pregunta todas las unidades: los contenidos con más porcentaje tienen preguntas que valen más. Cada porcentaje es la suma de los pesos de sus criterios de evaluación en la programación oficial. Las actividades guiadas (A) y la autoevaluación (R) cuentan aparte, como se indica en «Cómo se evalúa».

### UD1 · Sistemas informáticos. Hardware y software

Pesa un 42,9 % en los exámenes (15 % del módulo).

| Contenido | Peso en la unidad |
|---|---|
| Componentes, memorias, sistemas de numeración y seguridad | 60 % |
| Puesta en marcha de un equipo | 15 % |
| Periféricos: clasificar, instalar y configurar | 25 % |

### UD2 · Sistemas operativos. Instalación

Pesa un 57,1 % en los exámenes (20 % del módulo).

| Contenido | Peso en la unidad |
|---|---|
| Funciones, tipos, arquitectura, licencias y comparación de sistemas operativos (también las distribuciones de Linux) | 25 % |
| Planificar, virtualizar, actualizar, recuperar e instalar aplicaciones (también WSL, apt, el JDK y VS Code) | 50 % |
| Instalar y actualizar sistemas libres y propietarios | 20 % |
| Documentar los procesos | 5 % |

## Rúbricas

Cómo se califica cada parte de la evaluación.

### Exámenes parciales (P) y examen final (F)

En papel, con preguntas de dos tipos, de 1 punto cada una: verdadero o falso (cada acierto suma 1, cada error resta 0,5 y una pregunta en blanco vale 0; esta parte nunca baja de 0) y unir pares (0,25 por cada pareja bien unida; las mal unidas no restan). Los contenidos con más porcentaje tienen más preguntas, y la nota es proporcional a los puntos obtenidos. La rúbrica de cada examen se publica aquí antes del examen. Para practicar, hay un [simulacro del examen parcial (P1)](simulacro-P1-SI.md), con las respuestas debajo de cada pregunta.

### Actividades guiadas (A)

Se califican una vez terminadas, por su **nivel de implementación y comprensión**, y cómo depende del tipo de actividad:

- **Proyecto de progresión continuada** (un mismo proyecto que avanza de una actividad a la siguiente): se califica **hasta dónde se ha implementado la solución final del proyecto**, no cada actividad por separado. Todas sus actividades tienen la misma nota.
- **Actividad independiente:** se califica su propio resultado.

La nota tiene dos mitades:

- **Implementación (50 %):** con el proyecto propio, en el ordenador, se muestran, por orden, las comprobaciones de las tablas de abajo: 12 por proyecto o actividad, 3 en cada nivel (del 1, lo más básico, al 4). Cada comprobación que sale bien suma por sí misma, aunque falle alguna de un nivel anterior: la nota de implementación es las que salen bien entre 12, por 10.
- **Comprensión (50 %):** cuánto se sabe explicar. Se hacen 4 preguntas sobre el diseño y la arquitectura, una por nivel, sobre lo que se muestra en ese nivel; se hacen las cuatro aunque no se haya alcanzado el nivel. Cada respuesta bien dada vale 2,5. De qué trata cada pregunta, en las tablas de abajo.

#### A1 · Ubuntu Linux, WSL, Java y VS Code

**Implementación** (12 comprobaciones; cada una que sale bien suma 10/12)

| Nivel | Muestra que… |
|---|---|
| **1** | • Ubuntu se abre en WSL<br>• su terminal funciona (por ejemplo, `pwd` y `ls`)<br>• `sudo apt update` termina sin errores |
| **2** | • el JDK está instalado con `apt`<br>• `javac -version` da la versión 21<br>• `java -version` da la versión 21 |
| **3** | • VS Code se abre desde Ubuntu con `code .`<br>• abajo a la izquierda pone **WSL: Ubuntu**<br>• las extensiones están instaladas en **WSL: Ubuntu** |
| **4** | • el terminal de VS Code es el de Ubuntu<br>• se compila un programa con `javac`<br>• se ejecuta con `java` |

**Comprensión** (una pregunta por nivel; se hacen las cuatro)

| Nivel | La pregunta trata sobre… |
|---|---|
| 1 | Qué es WSL |
| 2 | Qué es el JDK |
| 3 | Por qué VS Code se conecta a WSL |
| 4 | El terminal de Ubuntu y el de Windows |

#### A2 · Arranque y GRUB en una máquina virtual

**Implementación** (12 comprobaciones; cada una que sale bien suma 10/12)

| Nivel | Muestra que… |
|---|---|
| **1** | • la máquina virtual está creada, con EFI<br>• tiene la memoria y el disco que pide la actividad<br>• arrancada sin sistema, sale «No bootable option or device was found» |
| **2** | • Ubuntu Server está instalado<br>• arranca sin la ISO hasta el `login:`<br>• se entra con el usuario creado en la instalación |
| **3** | • hay una instantánea tomada<br>• al arrancar sale el menú de GRUB<br>• se entra en sus opciones avanzadas |
| **4** | • se ha visto el arranque roto: sale `grub>`<br>• se ha recuperado<br>• vuelve a arrancar hasta el `login:` |

**Comprensión** (una pregunta por nivel; se hacen las cuatro)

| Nivel | La pregunta trata sobre… |
|---|---|
| 1 | Qué es un hipervisor |
| 2 | Qué hace el firmware al arrancar |
| 3 | Para qué sirve GRUB |
| 4 | Qué indica `grub>` y cómo se recupera el arranque |

#### A3 · Mi equipo por dentro

**Implementación** (12 comprobaciones; cada una que sale bien suma 10/12)

| Nivel | Muestra que… |
|---|---|
| **1** | • la ficha `mi-equipo.md` tiene el procesador de tu equipo<br>• tiene su memoria<br>• dice de dónde sale cada dato (qué herramienta u orden) |
| **2** | • tiene la placa base y el firmware<br>• tiene los discos<br>• tiene la gráfica y la red |
| **3** | • tiene los componentes de la máquina virtual<br>• la tabla compara los seis componentes con los del equipo real<br>• marca cuál es el mismo en los dos |
| **4** | • dice en qué modos de conexión se ha probado el móvil en Windows<br>• dice dónde aparece en el Administrador de dispositivos en cada uno<br>• tiene la línea de `lsusb` del móvil en la máquina virtual |

**Comprensión** (una pregunta por nivel; se hacen las cuatro)

| Nivel | La pregunta trata sobre… |
|---|---|
| 1 | Núcleos y procesadores lógicos |
| 2 | SATA y NVMe |
| 3 | Por qué la máquina virtual tiene otros componentes |
| 4 | Por qué el móvil aparece como dispositivos distintos |

#### A4 · Windows en una máquina virtual

**Implementación** (12 comprobaciones; cada una que sale bien suma 10/12)

| Nivel | Muestra que… |
|---|---|
| **1** | • la máquina `windows11` tiene 4096 MB, 2 procesadores y EFI<br>• tiene TPM 2.0 y arranque seguro<br>• tiene un disco VDI dinámico de 80 GB |
| **2** | • Windows 11 arranca sin la ISO hasta el escritorio<br>• se entra con el usuario local `dam`<br>• la ISO se ha quitado de la unidad óptica |
| **3** | • las Guest Additions están instaladas: la pantalla se adapta a la ventana<br>• el Administrador de dispositivos no tiene avisos amarillos<br>• `tpm.msc` muestra el TPM listo, versión 2.0 |
| **4** | • `instalacion-windows.md` tiene la máquina, con el porqué de cada ajuste<br>• tiene las pantallas de la instalación con lo elegido, y las incidencias<br>• tiene las particiones que creó Windows y para qué sirve cada una |

**Comprensión** (una pregunta por nivel; se hacen las cuatro)

| Nivel | La pregunta trata sobre… |
|---|---|
| 1 | Por qué Windows 11 pide TPM 2.0 y arranque seguro |
| 2 | La instalación personalizada en el espacio sin asignar |
| 3 | Para qué sirven las Guest Additions |
| 4 | Las particiones que crea Windows |

| Comprensión | Nota |
|---|---|
| Las 4 preguntas, bien respondidas | 10 |
| 3 preguntas | 7,5 |
| 2 preguntas | 5 |
| 1 pregunta | 2,5 |
| Ninguna | 0 |

La nota es la media de las dos. El mínimo de 4 se aplica a la media de las actividades de la evaluación.

### Cuestionarios (C) y autoevaluación (R)

Hay un cuestionario cada semana en la que se facilitan apuntes o actividades guiadas nuevas, con preguntas sobre ellos. Su entrega es obligatoria, hasta el lunes siguiente a su semana, salvo que se indique otra fecha (ver las notas de la [1ª evaluación](#cómo-se-evalúa-de-dónde-sale-la-nota)). No tienen nota propia, pero son un requisito de la autoevaluación: sin todos los cuestionarios entregados, la autoevaluación (R) es un 0.

La autoevaluación (R) se hace una sola vez, la semana del examen final, con la [plantilla de autoevaluación](autoevaluacion-1a.xlsx) en una tarea de Teams. Forma el 10 % de la nota. La mitad es la hoja completa: un nivel en cada tema, un tipo de fallo donde corresponde y una frecuencia en cada hábito de estudio. La otra mitad es la reflexión final, si es concreta: nombra los temas o los hábitos que más fallan y qué se va a hacer, en concreto, para mejorarlos. Requisito: tener entregados todos los cuestionarios (C); si falta alguno, la R es un 0. Lo marcado en cada tema y en cada hábito no cambia la nota.

## Planificación semanal

| Semana | Qué se trabaja | Cómo se evalúa | Exámenes |
|---|---|---|---|
| Antes del 2 nov<br>[repaso Julia](../repaso-julia/apuntes) | Lo evaluado por Julia | Nada evaluado | — |
| [2–6 nov](../2026_11_02-06)<br>[apuntes](../2026_11_02-06/apuntes) · [actividades](../2026_11_02-06/actividades) | UD1 · Componentes, memorias y seguridad: la teoría<br>UD1 · Puesta en marcha: firmware, POST y orden de arranque<br>UD1 · Periféricos: tipos, conectores y drivers<br>UD2 · Las distribuciones de Linux<br>UD2 · Virtualizar e instalar aplicaciones: WSL, apt, el JDK y VS Code<br>UD2 · Instalar un sistema libre: Ubuntu en WSL<br>UD3 · Introducción: sistema de archivos, órdenes básicas y redirección (cuentan en la 2ª evaluación) | A1 (5 %), C1 | — |
| [9–13 nov](../2026_11_09-13)<br>[apuntes](../2026_11_09-13/apuntes) · [actividades](../2026_11_09-13/actividades) | UD1 · Puesta en marcha: el arranque de una máquina virtual<br>UD2 · Funciones, tipos, arquitectura y licencias de los sistemas operativos<br>UD2 · Planificar, virtualizar, actualizar y recuperar: VirtualBox, instantáneas y GRUB<br>UD2 · Instalar un sistema libre: Ubuntu Server en una máquina virtual | A2 (5 %), C2 | — |
| [16–20 nov](../2026_11_16-20)<br>[apuntes](../2026_11_16-20/apuntes) · [actividades](../2026_11_16-20/actividades) | UD1 · Componentes, memorias y seguridad, en el propio equipo<br>UD1 · Periféricos: el móvil, en Windows y en Linux | A3 (5 %), C3 | — |
| [23–27 nov](../2026_11_23-27)<br>[apuntes](../2026_11_23-27/apuntes) · [actividades](../2026_11_23-27/actividades) | UD2 · Instalar un sistema propietario: Windows en una máquina virtual (mar 24)<br>UD2 · Documentar la instalación de Windows<br>Repaso de toda la evaluación (jue 26 y vie 27) | A4 (5 %), C4 | — |
| 30 nov–4 dic | Repaso (mar 1 y jue 3) | — | **P1** (40 %), vie 4 dic |
| 7–11 dic | Repaso (jue 10) | R (10 %) | **F** (30 %), vie 11 dic |
| 14–18 dic | UD3 · Linux | Cierre de la 1ª evaluación · jue 17 | — |

## Notas

- **Cuestionarios (C).** Hay uno cada semana en la que se facilitan apuntes o actividades guiadas nuevas, con preguntas sobre ellos. Su entrega es obligatoria, hasta el lunes siguiente a su semana, salvo que se indique otra fecha (ver las notas). No tienen nota propia, pero sin todos los cuestionarios entregados, la autoevaluación (R) es un 0.
- **Autoevaluación (R).** La R es de reflexión. Una sola, la semana del examen final, en una tarea de Teams: la [plantilla de autoevaluación](autoevaluacion-1a.xlsx), que cada estudiante rellena en su propia copia. Por cada tema de cada unidad, el nivel de comprensión y el tipo de fallo principal; la frecuencia de 15 hábitos de estudio, y una reflexión general sobre qué hacer para mejorar en la 2ª evaluación. Forma el 10 % de autoevaluación del apartado 6.1 de la programación oficial. La mitad de su nota es la hoja completa; la otra mitad, la reflexión, si es concreta. Requisito: tener entregados todos los cuestionarios (C); si falta alguno, la R es un 0. Lo marcado en cada tema y en cada hábito no cambia la nota.
- **Exámenes escritos** (parciales, **P**, y final, **F**). Son en papel, sobre los mismos contenidos que los cuestionarios, con preguntas de dos tipos, de 1 punto cada una: verdadero o falso (cada acierto suma 1, cada error resta 0,5 y una pregunta en blanco vale 0; esta parte nunca baja de 0) y unir pares (0,25 por cada pareja bien unida; las mal unidas no restan). Los contenidos con más porcentaje tienen más preguntas, y la nota es proporcional a los puntos obtenidos.
- **Actividades guiadas (A).** Se califican, una vez terminadas, por su nivel de implementación y comprensión, al 50 %. Si son partes de un proyecto de progresión continuada, se califica hasta dónde se ha implementado la solución final del proyecto, con la misma nota para todas; si son independientes, cada una por su resultado. Implementación: 12 comprobaciones ordenadas en 4 niveles; cada una que sale bien suma 10/12. Comprensión: 4 preguntas sobre el diseño y la arquitectura, una por nivel (2,5 cada una); qué pide cada nivel, en las [rúbricas](#rúbricas). Detalle, en las [rúbricas](#rúbricas). El mínimo de 4 se aplica a la media de las actividades de la evaluación.
- La semana del 23 al 27: el martes 24, instalar Windows en una máquina virtual y documentar la instalación (A4); el jueves 26 y el viernes 27, repaso de toda la evaluación (decisión del 20 de noviembre). Los sistemas de numeración ya se dieron: se repasan en una hora.
- Antes del 2 de noviembre no hay nada evaluado en SI: ni exámenes ni tareas entregadas.
- El C1 se entrega junto con el C2, el lunes 16 de noviembre.
- WSL, apt, el JDK, VS Code y las distribuciones de Linux son de la UD2. El sistema de archivos, las órdenes básicas y la redirección son una introducción a la UD3: la P1 puede preguntarlos, pero esas preguntas cuentan para la UD3 en la 2ª evaluación.
- Mínimo de 4 en cada examen parcial, en la media de las actividades guiadas y en el final para aplicar la media (apartado 6.1 de la programación oficial).
