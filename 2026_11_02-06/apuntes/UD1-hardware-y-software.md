# UD1 · Sistemas informáticos: hardware y software

Lo básico que hay que saber de la UD1. Cada apartado tiene la idea clave, lo que tienes que saber y, cuando hay conceptos que se confunden, una tabla para compararlos. Las preguntas para comprobar que lo entiendes están en el [cuestionario](../cuestionario.md) de la semana, en «Cuestiones sobre los apuntes».

---

## 1. El sistema informático

**En una frase:** un sistema informático recibe datos, los procesa y da resultados; su parte física es el hardware y su parte lógica, el software.

**Lo que tienes que saber**

- **Hardware:** lo que se puede tocar (procesador, memoria, discos, periféricos). **Software:** los programas y los datos.
- Casi todos los ordenadores siguen el **modelo de Von Neumann**: una CPU, una memoria donde están juntos los programas y los datos, y dispositivos de entrada/salida.
- Las piezas se comunican por el **bus del sistema**, que tiene tres partes: **datos**, **direcciones** (a qué posición de memoria se accede) y **control** (señales de lectura, escritura, reloj…).
- El **modelo Harvard** separa la memoria de instrucciones de la de datos, y así puede leer las dos a la vez. Los procesadores actuales lo usan dentro, en la caché.

**Compara**

| | Von Neumann | Harvard |
|---|---|---|
| Instrucciones y datos | En la misma memoria y por el mismo camino | En memorias y caminos separados |
| Ventaja | Más sencillo | Más rápido: lee instrucción y dato a la vez |

---

## 2. El procesador

**En una frase:** el procesador ejecuta las instrucciones de los programas; dentro, cada núcleo tiene su propia CPU.

**Lo que tienes que saber**

- La **CPU** tiene tres partes: la **unidad de control** (lee e interpreta cada instrucción y da las órdenes), la **unidad aritmético-lógica, ALU** (hace las cuentas y las comparaciones) y los **registros** (memorias diminutas y rapidísimas).
- Dos registros clave: el **contador de programa** (dónde está la siguiente instrucción) y el **registro de instrucción** (la que se está ejecutando).
- Un procesador actual tiene varios **núcleos**, que trabajan en paralelo, y cada uno puede llevar dos **hilos**.
- Sus características: **frecuencia** (GHz, ciclos por segundo), número de núcleos e hilos, **caché** (L1, L2 y L3), tamaño de fabricación (nm), consumo y **TDP** (el calor que hay que disipar).
- **Juego de instrucciones:** **CISC** (muchas instrucciones complejas: x86, de Intel y AMD) o **RISC** (pocas y simples, menos consumo: ARM, en móviles y en los Apple M).
- Una **interrupción** es un aviso (de un periférico o del sistema) que hace que el procesador pare lo que hace, lo atienda y después siga.

**Compara**

| | CISC | RISC |
|---|---|---|
| Instrucciones | Muchas y complejas | Pocas y simples |
| Consumo | Mayor | Menor |
| Dónde | La mayoría de PC (Intel, AMD) | Móviles, tabletas, Apple M |

---

## 3. La memoria

**En una frase:** la CPU solo trabaja con lo que está en memoria; cuanto más cerca de ella, más rápida y más pequeña.

**Lo que tienes que saber**

- De más rápida a más lenta: **registros → caché (L1, L2, L3) → RAM → almacenamiento** (SSD, disco duro). En la caché, la L1 es la más rápida y pequeña, y la L3, la más lenta y grande.
- La **RAM es volátil**: al apagar, se borra. El almacenamiento no.
- Las memorias **ROM** y sus variantes (**PROM**, **EPROM**, **EEPROM** y la **flash**, que es su sucesora) **no son volátiles**. Guardan el firmware de la placa.
- De la RAM importan la **capacidad** (GB), la **velocidad** (MT/s, como DDR5-5600), la **latencia** (CL: cuanto menor, mejor) y el **tipo**: **DDR5** en los equipos nuevos y DDR4 en muchos que aún se usan. No son intercambiables.
- **Doble canal:** con dos módulos iguales en las ranuras indicadas, la placa lee de los dos a la vez.
- Si falta RAM, el sistema usa el disco como **memoria virtual**, y todo va más lento.

**Compara**

| | RAM | ROM y flash |
|---|---|---|
| ¿Se borra al apagar? | Sí | No |
| ¿Para qué? | Los programas en uso y sus datos | El firmware y el almacenamiento |

---

## 4. La placa base

**En una frase:** la placa base conecta todos los componentes, y su chipset y su zócalo deciden qué se le puede poner.

**Lo que tienes que saber**

- El **factor de forma** fija su tamaño y la posición de las piezas: **ATX** (el más usado), **Micro-ATX** y **Mini-ITX** (más pequeños y con menos ranuras).
- El **chipset** coordina la comunicación entre el procesador, la memoria y el resto, y decide qué procesadores, cuánta RAM y qué puertos admite la placa.
- El **zócalo** (*socket*) es donde va el procesador: **LGA** (los contactos están en la placa) o **PGA** (las patillas están en el procesador).
- **Ranuras:** de **RAM** (DIMM; con colores para el doble canal) y de **expansión**, **PCI Express** (x1, x4, x16), para la tarjeta gráfica y otras.
- El **firmware** (BIOS o UEFI) está en una memoria flash de la placa. Una **pila** mantiene el reloj y la configuración.
- **Conectores internos:** **SATA** (discos), **M.2** (SSD, sobre todo **NVMe**), alimentación (24 pines para la placa, 4/8 para el procesador), ventiladores, USB y panel frontal. **Externos:** USB (A y C), HDMI y DisplayPort, red RJ45, audio, Thunderbolt (por USB-C).

**Compara**

| | SSD SATA | SSD NVMe (M.2) |
|---|---|---|
| Conexión | Bus SATA | PCI Express |
| Velocidad aproximada | Unos 550 MB/s | Varios GB/s |

---

## 5. Almacenamiento, fuente y periféricos

**En una frase:** el almacenamiento guarda los datos aunque se apague el equipo, la fuente da la energía y los periféricos comunican el equipo con el exterior.

**Lo que tienes que saber**

- **Almacenamiento:** **SSD** (flash, sin piezas móviles, rápido y resistente), **disco duro** magnético (más lento, pero barato por GB: copias de seguridad), **ópticos** (CD, DVD, Blu-ray, en desuso) y memorias **USB** y **SD**.
- La **fuente de alimentación** convierte la corriente alterna de la red (230 V) en continua de **3,3 V, 5 V y 12 V**, protege frente a picos y ayuda a sacar el calor.
- **Periféricos** de **entrada** (teclado, ratón, micrófono), de **salida** (pantalla, impresora, altavoces) y de **entrada/salida** (pantalla táctil, discos, tarjeta de red).
- Un **adaptador** conecta un periférico a un conector distinto (USB-C a HDMI, por ejemplo).

**Compara**

| | SSD | Disco duro (HDD) |
|---|---|---|
| Piezas móviles | No | Sí (platos y cabezal) |
| Velocidad | Mucho mayor | Menor |
| Precio por GB | Mayor | Menor |

---

## 6. Controladores (*drivers*)

**En una frase:** el driver es el programa que explica al sistema operativo cómo manejar un dispositivo.

**Lo que tienes que saber**

- Sin su driver, el sistema operativo no sabe usar un dispositivo, o lo usa a medias.
- Los sistemas actuales traen muchos drivers y los instalan solos al conectar el dispositivo (**Plug and Play**).
- Conviene instalar los del fabricante para la gráfica, la red y la placa, y siempre los de la versión del sistema y la arquitectura (64 bits) adecuadas.
- En **Windows**: el **Administrador de dispositivos** muestra cada dispositivo; un aviso amarillo indica que le falta el driver o falla. Desde ahí se actualiza, se desactiva o se desinstala.
- En **Linux**: la mayoría de drivers vienen con el kernel. `lspci`, `lsusb` y `sudo lshw` muestran el hardware detectado.

---

## 7. El software

**En una frase:** el software son los programas, y se clasifica según para qué sirve.

**Lo que tienes que saber**

- **De sistema:** hace funcionar el equipo (sistema operativo, firmware, drivers, utilidades, software de virtualización como VirtualBox).
- **De programación:** sirve para crear programas (editores, compiladores, IDE).
- **De aplicación:** lo que usa la persona para su trabajo (ofimática, como LibreOffice o Microsoft Office; navegador; juegos).
- Para ejecutarse, un programa pasa del almacenamiento a la **RAM**, y de ahí la CPU lee sus instrucciones.

---

## 8. La puesta en marcha

**En una frase:** al encender, el firmware comprueba el hardware (POST) y después busca desde dónde arrancar el sistema.

**Lo que tienes que saber**

- La fuente da tensión y el procesador empieza a ejecutar el **firmware** de la placa (BIOS o, hoy, UEFI).
- Lo primero es el **POST** (*Power-On Self Test*): comprueba procesador, memoria y gráfica.
- Si algo falla, avisa con **pitidos** o **códigos** en la pantalla o en la placa; su significado está en el manual del fabricante.
- Después inicializa el resto de dispositivos y busca el sistema en el **orden de arranque** configurado.
- Con una tecla al encender se entra en la **configuración del firmware** (Supr, F2…) o en su **menú de arranque** (F12, F8…), según el fabricante.

---

## 9. Seguridad y prevención de riesgos

**En una frase:** trabajar con ordenadores tiene riesgos (posturas, vista, electricidad) que se previenen con normas sencillas.

**Lo que tienes que saber**

- La norma general es la **Ley 31/1995 de Prevención de Riesgos Laborales**; para los puestos con ordenador, el **Real Decreto 488/1997** (pantallas de visualización).
- La empresa evalúa los riesgos, informa y forma; el trabajador usa bien los equipos y las protecciones y no anula los dispositivos de seguridad.
- **Puesto con pantalla:** pantalla sin reflejos, a la altura de los ojos o algo por debajo y a más de 40 cm; teclado separado, con espacio delante para apoyar las manos; silla regulable con apoyo lumbar; pies apoyados; buena luz.
- **Electricidad:** desconectar el equipo antes de abrirlo, descargarse de electricidad estática (pulsera antiestática) antes de tocar componentes, manos secas y no mover equipos encendidos.
