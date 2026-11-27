# Sistemas Informáticos · 1º DAM · Examen parcial (P1) · Simulacro

- **Duración:** 1 hora y 30 minutos.
- **Verdadero o falso** (1 punto): se marca V o F. Cada acierto suma 1 punto, cada error resta 0,5 y una pregunta en blanco vale 0. Los errores solo restan dentro de esta parte, que nunca baja de 0: no quitan puntos de unir pares. Conviene contestar aunque haya dudas: compensa en cuanto se acierta más de una de cada tres veces.
- **Unir pares** (1 punto): cada elemento de la izquierda va con uno de la derecha. La derecha tiene una opción de más, que no va con ninguno. Cada pareja bien unida vale 0,25, y las mal unidas no restan.
- En total, 27 preguntas y 27 puntos; la nota, de 0 a 10, es proporcional: puntos obtenidos × 10 / 27.
- **Preguntas adicionales:** al final hay 11 preguntas optativas, con las mismas reglas, para sustituir preguntas del examen que no se sepan. Sus puntos se suman a los demás, pero la nota no pasa de 27 puntos, es decir, de un 10.
- Debajo de cada pregunta, la respuesta correcta marcada y su porqué.

---

## UD1 · Sistemas informáticos. Hardware y software

### Componentes, memorias, sistemas de numeración y seguridad

**1.** Une cada parte del equipo con lo que hace.

| | Parte | | Qué hace |
|---|---|---|---|
| 1 | Unidad de control | a | Hace las operaciones aritméticas y lógicas |
| 2 | ALU | b | Lee e interpreta cada instrucción y da las órdenes para ejecutarla |
| 3 | Registros | c | Guarda el firmware de la placa y no se borra al apagar |
| 4 | RAM | d | Memorias diminutas y muy rápidas dentro de la CPU, con los datos con los que trabaja en cada momento |
| | | e | Guarda los programas que se están ejecutando, que pasan a ella desde el almacenamiento |

1 → **b** &nbsp;&nbsp;&nbsp; 2 → **a** &nbsp;&nbsp;&nbsp; 3 → **d** &nbsp;&nbsp;&nbsp; 4 → **e**

*Por qué:* La unidad de control, la ALU y los registros son las tres partes de la CPU. Para ejecutarse, un programa pasa del almacenamiento a la **RAM**, y de ahí la CPU lee sus instrucciones. La c es la **ROM** o la **flash**, que no son volátiles.

**2.** De más rápida a más lenta, el orden es: registros, caché L1, caché L3, RAM y SSD.

**V** ☒ &nbsp;&nbsp;&nbsp; **F** ☐

*Por qué:* Registros → caché (L1 la más rápida, L3 la más lenta de las tres) → RAM → almacenamiento.

**3.** Al apagar el equipo se borran la RAM y el SSD, porque los dos son memorias.

**V** ☐ &nbsp;&nbsp;&nbsp; **F** ☒

*Por qué:* Se borran los registros, las cachés y la RAM, porque son **volátiles**. El SSD es almacenamiento, y lo que guarda sigue ahí al apagar.

**4.** Una memoria DDR4-3600 tiene un reloj de 3600 MHz.

**V** ☐ &nbsp;&nbsp;&nbsp; **F** ☒

*Por qué:* Va a **1800 MHz**. La DDR hace dos transferencias por ciclo, así que los MT/s son el doble de los MHz: 3600 / 2.

**5.** Una memoria DDR4-3600 CL18 tiene una latencia de unos 10 ns.

**V** ☒ &nbsp;&nbsp;&nbsp; **F** ☐

*Por qué:* El reloj va a 1800 MHz, así que un ciclo dura 1 / 1800 MHz ≈ 0,556 ns, y 18 ciclos son **10 ns**.

**6.** La memoria de un equipo aparece así en el Administrador de tareas: DDR4, 3200 MT/s, ranuras usadas 1 de 2, factor de forma SODIMM. Es la memoria de un portátil, y se puede ampliar.

**V** ☒ &nbsp;&nbsp;&nbsp; **F** ☐

*Por qué:* **SODIMM** es el módulo pequeño de los portátiles; los de sobremesa usan **DIMM**. Se puede ampliar porque hay una ranura libre.

**7.** Los dos discos de un servidor están en RAID 1. Si alguien borra un archivo por error, se puede recuperar del otro disco.

**V** ☐ &nbsp;&nbsp;&nbsp; **F** ☒

*Por qué:* En **RAID 1** (espejo), los dos discos tienen los mismos datos: el archivo se borra en los dos a la vez. Un RAID protege del fallo de un disco, no de los errores, y por eso no sustituye a las copias de seguridad.

**8.** Una fuente de alimentación se puede abrir sin peligro si está desconectada.

**V** ☐ &nbsp;&nbsp;&nbsp; **F** ☒

*Por qué:* Sus **condensadores** guardan una carga eléctrica peligrosa aunque esté desconectada. No se abre nunca.

### Puesta en marcha de un equipo

**9.** Un ordenador pita al encenderlo y no da imagen. Falla en el POST, y lo que significan los pitidos se mira en el manual del fabricante de la placa base.

**V** ☒ &nbsp;&nbsp;&nbsp; **F** ☐

*Por qué:* El **POST** es la comprobación del hardware (procesador, memoria, gráfica) que hace el firmware al encender, antes de buscar el sistema. Los códigos de pitidos dependen del fabricante de la placa.

### Periféricos: clasificar, instalar y configurar

**10.** En Windows, un dispositivo al que le falta el driver aparece con una marca amarilla en el Administrador de dispositivos.

**V** ☒ &nbsp;&nbsp;&nbsp; **F** ☐

*Por qué:* El **driver** es el programa que explica al sistema operativo cómo manejar un dispositivo; sin él, el **Administrador de dispositivos** lo marca en amarillo.

**11.** Una impresora con escáner es un periférico de salida.

**V** ☐ &nbsp;&nbsp;&nbsp; **F** ☒

*Por qué:* Es de **entrada/salida**: imprime (salida) y escanea (entrada).

**12.** Una pantalla táctil es un periférico de entrada/salida.

**V** ☒ &nbsp;&nbsp;&nbsp; **F** ☐

*Por qué:* Muestra la imagen (salida) y recibe los toques (entrada).

## UD2 · Sistemas operativos. Instalación

### Funciones, tipos, arquitectura, licencias y comparación de sistemas operativos

**13.** La única función de un sistema operativo es ofrecer una interfaz para usar el equipo.

**V** ☐ &nbsp;&nbsp;&nbsp; **F** ☒

*Por qué:* Tiene dos: ofrecer una **interfaz** para usar el equipo y **gestionar los recursos** (procesador, memoria, dispositivos, archivos) entre los programas.

**14.** El kernel es la parte del sistema operativo que siempre está en memoria y que habla con el hardware.

**V** ☒ &nbsp;&nbsp;&nbsp; **F** ☐

*Por qué:* Es la parte central del sistema operativo.

**15.** Une cada término con lo que es.

| | Término | | Qué es |
|---|---|---|---|
| 1 | Kernel monolítico | a | Un driver que el kernel carga solo cuando hace falta |
| 2 | Microkernel | b | Todo el sistema, también los drivers, funciona dentro del kernel: rápido, pero un fallo puede tirarlo todo |
| 3 | Kernel de Linux | c | El kernel hace lo mínimo y el resto son programas aparte: más estable, pero más lento |
| 4 | Módulo del kernel | d | Monolítico, pero modular |
| | | e | Un hipervisor que funciona directamente sobre el hardware |

1 → **b** &nbsp;&nbsp;&nbsp; 2 → **c** &nbsp;&nbsp;&nbsp; 3 → **d** &nbsp;&nbsp;&nbsp; 4 → **a**

*Por qué:* Linux es monolítico, pero muchos de sus drivers son **módulos** que el kernel carga solo cuando hacen falta. La e es un hipervisor de tipo 1, no una parte del kernel.

**16.** El software libre se puede usar, estudiar, modificar y redistribuir.

**V** ☒ &nbsp;&nbsp;&nbsp; **F** ☐

*Por qué:* Para poder estudiarlo, su código está disponible. El **propietario** no da el código y limita el uso.

**17.** La versión base de VirtualBox tiene licencia GPL. Una versión modificada se puede publicar como software propietario, sin dar su código.

**V** ☐ &nbsp;&nbsp;&nbsp; **F** ☒

*Por qué:* La GPL obliga a que la versión modificada también sea **GPL** y se distribuya con su código fuente: es el *copyleft*.

### Planificar, virtualizar, actualizar, recuperar e instalar aplicaciones

**18.** VirtualBox es un hipervisor de tipo 1, porque funciona directamente sobre el hardware.

**V** ☐ &nbsp;&nbsp;&nbsp; **F** ☒

*Por qué:* Es de **tipo 2**: funciona como un programa dentro de un sistema operativo. El de **tipo 1** funciona directamente sobre el hardware, sin sistema operativo debajo, y se usa en servidores.

**19.** Un disco con tabla MBR admite como máximo 4 particiones principales.

**V** ☒ &nbsp;&nbsp;&nbsp; **F** ☐

*Por qué:* MBR admite **4**; GPT, hasta **128** en Windows.

**20.** En un disco GPT, para tener más de 4 particiones hay que crear particiones lógicas.

**V** ☐ &nbsp;&nbsp;&nbsp; **F** ☒

*Por qué:* GPT no las necesita: admite hasta 128 particiones. Las lógicas eran el truco de MBR para pasar de 4.

**21.** Las fases del arranque de Ubuntu, en orden, son: firmware, gestor de arranque (GRUB), kernel, systemd e inicio de sesión.

**V** ☒ &nbsp;&nbsp;&nbsp; **F** ☐

*Por qué:* El firmware hace el POST y busca en el orden de arranque; después vienen GRUB, el kernel, systemd y el inicio de sesión.

**22.** Si al encender sale `grub>`, el fallo está en la fase del kernel.

**V** ☐ &nbsp;&nbsp;&nbsp; **F** ☒

*Por qué:* Falla la fase del **gestor de arranque**: GRUB arranca, pero no encuentra su configuración.

**23.** Para cambiar la configuración de GRUB, se edita `/boot/grub/grub.cfg` y después se ejecuta `sudo update-grub`.

**V** ☐ &nbsp;&nbsp;&nbsp; **F** ☒

*Por qué:* Se edita **`/etc/default/grub`**. `update-grub` vuelve a generar `grub.cfg` (también en las actualizaciones), así que lo escrito a mano en él se perdería.

**24.** Une cada orden con lo que hace.

| | Orden | | Qué hace |
|---|---|---|---|
| 1 | `sudo apt update` | a | Ejecuta la orden con permisos de administrador (`root`) |
| 2 | `sudo apt upgrade` | b | Vuelve a generar la configuración de arranque a partir de `/etc/default/grub` |
| 3 | `sudo` | c | Descarga la lista actualizada de paquetes de los repositorios |
| 4 | `sudo update-grub` | d | Actualiza los paquetes instalados |
| | | e | Borra los paquetes que ya no hacen falta |

1 → **c** &nbsp;&nbsp;&nbsp; 2 → **d** &nbsp;&nbsp;&nbsp; 3 → **a** &nbsp;&nbsp;&nbsp; 4 → **b**

*Por qué:* `update` solo descarga la lista; `upgrade` es la que actualiza. Las dos necesitan `sudo` porque instalar y actualizar cambia el sistema.

### Instalar y actualizar sistemas libres y propietarios

**25.** Windows 11 pide un TPM 2.0, y con `tpm.msc` se comprueba si está listo para usarse.

**V** ☒ &nbsp;&nbsp;&nbsp; **F** ☐

*Por qué:* El **TPM** es un chip de la placa base que guarda claves de cifrado y ayuda a comprobar que el equipo arranca sin manipulaciones.

**26.** Un equipo tiene un procesador compatible con Windows 11 de cuatro núcleos a 2,5 GHz, 8 GB de RAM, un SSD de 256 GB y firmware UEFI con arranque seguro, pero no tiene TPM. Puede instalar Windows 11.

**V** ☐ &nbsp;&nbsp;&nbsp; **F** ☒

*Por qué:* Cumple el procesador, la memoria, el disco y UEFI con arranque seguro, pero le falta el **TPM 2.0**.

**27.** La partición EFI que crea Windows 11 tiene las herramientas para reparar Windows.

**V** ☐ &nbsp;&nbsp;&nbsp; **F** ☒

*Por qué:* La **EFI** guarda los programas de arranque. Las herramientas para reparar Windows están en la partición de **recuperación**.

## Preguntas adicionales

Optativas, con las mismas reglas, para sustituir preguntas del examen que no se sepan.

**28.** WSL ejecuta un Linux dentro de Windows sin crear un ordenador virtual completo, con su firmware, su disco y su arranque, como hace VirtualBox.

**V** ☒ &nbsp;&nbsp;&nbsp; **F** ☐

*Por qué:* **WSL** (*Windows Subsystem for Linux*) ejecuta un Linux de verdad dentro de Windows, sin máquina virtual aparte ni arranque dual. Con VirtualBox se crea un ordenador virtual completo y en él se instala el sistema.

**29.** Al ejecutar estas órdenes, la última muestra las frutas en el orden en que se escribieron: pera, manzana y kiwi.

```bash
echo "pera" > frutas.txt
echo "manzana" >> frutas.txt
echo "kiwi" >> frutas.txt
cat frutas.txt | sort
```

**V** ☐ &nbsp;&nbsp;&nbsp; **F** ☒

*Por qué:* El `|` es una **tubería**: pasa lo que sale de `cat` (el contenido del archivo) como entrada de `sort`, que ordena las líneas. Sale `kiwi`, `manzana` y `pera`, cada una en una línea.

**30.** En VirtualBox, la máquina virtual se comunica con Windows en el modo de red NAT, a través del adaptador *VirtualBox Host-Only*.

**V** ☐ &nbsp;&nbsp;&nbsp; **F** ☒

*Por qué:* Ese es el modo **Host-only**. En **NAT**, la máquina tiene Internet: un router virtual de VirtualBox la saca a Internet por la tarjeta real de Windows.

**31.** Con firmware UEFI se usa la tabla de particiones GPT, y con BIOS, MBR.

**V** ☒ &nbsp;&nbsp;&nbsp; **F** ☐

*Por qué:* Cada firmware va con su tabla: BIOS con **MBR** y UEFI con **GPT**.

**32.** Un archivo de 6 GB se puede guardar en un pendrive formateado en FAT32.

**V** ☐ &nbsp;&nbsp;&nbsp; **F** ☒

*Por qué:* En FAT32, un archivo puede ocupar como máximo **4 GB**. NTFS no tiene ese límite y, además, permite poner permisos a archivos y carpetas.

**33.** Un procesador tiene 8 núcleos y 16 procesadores lógicos: cada núcleo lleva 2 hilos.

**V** ☒ &nbsp;&nbsp;&nbsp; **F** ☐

*Por qué:* Un **procesador lógico** es cada unidad de procesamiento que el sistema operativo reconoce y puede usar para ejecutar hilos. Con 2 hilos por núcleo, reconoce 8 × 2 = 16.

**34.** Una distribución de Linux es el kernel Linux solo, sin programas ni gestor de paquetes.

**V** ☐ &nbsp;&nbsp;&nbsp; **F** ☒

*Por qué:* Una **distribución** es un sistema operativo basado en el kernel Linux que incluye programas, herramientas, un sistema de gestión de paquetes y, normalmente, un entorno de escritorio: Debian, Ubuntu, Linux Mint, Fedora, Arch, Manjaro, Kali o Parrot.

**35.** Una empresa quiere cifrar los discos de sus portátiles con BitLocker. Le sirve Windows 11 Home.

**V** ☐ &nbsp;&nbsp;&nbsp; **F** ☒

*Por qué:* Home no tiene BitLocker. Le sirve **Pro** (o Enterprise, si es una empresa mediana o grande).

**36.** Una máquina virtual con Ubuntu tiene la IP `10.0.2.15` en NAT, y `192.168.56.101` en Host-only. Une cada `ping` con lo que pasa.

| | `ping` | | Qué pasa |
|---|---|---|---|
| 1 | En NAT, desde Ubuntu: `ping -c 4 8.8.8.8` | a | Responde: el router virtual de VirtualBox saca la máquina a Internet por la tarjeta real de Windows |
| 2 | En NAT, desde Windows: `ping 10.0.2.15` | b | No responde: Windows no tiene ninguna tarjeta en la red `10.0.2.0/24` |
| 3 | En Host-only, desde Windows: `ping 192.168.56.101` | c | Responde: el adaptador *VirtualBox Host-Only* de Windows y la máquina están en la misma red, `192.168.56.0/24` |
| 4 | En Host-only, desde Ubuntu: `ping -c 4 8.8.8.8` | d | `Network is unreachable`: sin puerta de enlace, Ubuntu no sabe por dónde enviar lo que no es de su red |
| | | e | Responde: el adaptador *VirtualBox Host-Only* de Windows está conectado con la máquina en cualquier modo de red |

1 → **a** &nbsp;&nbsp;&nbsp; 2 → **b** &nbsp;&nbsp;&nbsp; 3 → **c** &nbsp;&nbsp;&nbsp; 4 → **d**

*Por qué:* En **NAT**, el otro extremo es un router virtual de VirtualBox (`10.0.2.2`), que saca la máquina a Internet, pero Windows no está en esa red. En **Host-only**, el otro extremo es el adaptador *VirtualBox Host-Only* de Windows (`192.168.56.1`): Windows y la máquina se ven, pero no hay salida a Internet. La e es falsa: ese adaptador sale siempre en `ipconfig`, pero con la máquina en NAT no hay nadie al otro extremo.

**37.** Con la máquina en Host-only, `ping -c 4 192.168.56.1` desde Ubuntu no responde. Eso quiere decir que Ubuntu y Windows no están conectados.

**V** ☐ &nbsp;&nbsp;&nbsp; **F** ☒

*Por qué:* La conexión existe: desde Windows, `ping 192.168.56.101` sí responde. Lo normal es que el **cortafuegos de Windows** no conteste a los `ping` que le llegan, porque suele tratar el adaptador Host-Only como una red pública.

**38.** Con la máquina en NAT, `ping -c 4 10.0.2.2` desde Ubuntu responde.

**V** ☒ &nbsp;&nbsp;&nbsp; **F** ☐

*Por qué:* `10.0.2.2` es el **router virtual de VirtualBox**, la puerta de enlace de la máquina en NAT (la línea `default via 10.0.2.2` de `ip route`). Por él sale todo lo que Ubuntu envía fuera de su red.
