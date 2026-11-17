# Cuestionario C1 · semana del 2 al 6 de noviembre · soluciones

Las salidas son las que da un terminal de Ubuntu. Alguna puede cambiar según el ordenador (las versiones de Java): lo que importa es su forma.

## Cuestiones sobre el proyecto

**1.**

```
.:
a

./a:
b

./a/b:
```

`mkdir -p` crea `/tmp/prueba`, `a` y `b` de una vez: `-p` crea también las carpetas intermedias que falten (sin él, `mkdir` daría error porque `/tmp/prueba/a` no existe). `cd` entra en la carpeta. `ls -R` lista la carpeta y, de forma recursiva, todas las de dentro: `.` es la carpeta actual, que tiene `a`; `a` tiene `b`; y `b` está vacía.

**2.**

```
a  datos.txt  notas.txt
```

`touch` crea los archivos vacíos (si ya existieran, solo actualizaría su fecha). `ls` lista lo que hay en la carpeta, por orden alfabético.

**3.**

```
dos
```

`>` manda la salida de `echo` a un archivo y **sustituye** lo que tuviera: el segundo `echo` borra el `uno` y deja solo `dos`. `cat` muestra el contenido del archivo.

**4.**

```
uno
dos
tres
```

`>` crea `lista.txt` con `uno`; `>>` **añade** al final sin borrar lo que había.

**5.**

```
dos
tres
uno
```

`|` (tubería) manda la salida de la primera orden a la entrada de la segunda: `cat` saca las tres líneas y `sort` las ordena alfabéticamente.

**6.**

```
a  datos.txt  notas.txt
numeros.txt
```

`mv` sirve para cambiar el nombre (`lista.txt` pasa a ser `numeros.txt`) y para mover a otra carpeta (`numeros.txt` va a `a/b/`). Por eso `ls` ya no lo muestra en `/tmp/prueba` y `ls a/b` sí.

**7.**

```
rm: cannot remove 'a': Is a directory
datos.txt  notas.txt
```

`rm` solo borra archivos: con una carpeta da error. `rm -r` borra de forma recursiva la carpeta y todo lo que contiene (`b` y `numeros.txt`). Lo que se borra con `rm` no va a ninguna papelera.

**8.** Con las flechas (o `Espacio` para bajar una pantalla y `b` para subirla). Se busca con `/` seguido de la palabra e `Intro` (`n` va a la siguiente coincidencia). Se sale con `q`. `cat` saca todo el archivo de golpe; con uno largo, el principio se pierde por arriba. `less` lo muestra pantalla a pantalla, sin cambiarlo.

**9.** `sudo` ejecuta una sola orden con permisos de administrador (`root`); pide tu contraseña de Linux. Instalar programas cambia el sistema, y eso solo lo puede hacer el administrador. Crear carpetas en `/tmp` (o en tu carpeta personal, `~`) no cambia el sistema: tu usuario ya tiene permiso.

**10.** Algo así:

```
javac 21.0.x
openjdk version "21.0.x" …
```

Los dos tienen que mostrar la versión 21. El JRE solo ejecuta programas Java ya compilados (`java`); el JDK incluye el JRE y añade las herramientas para programar, como el compilador `javac`. Por eso, si `java -version` funciona y `javac` no, solo está instalado el JRE.

## Cuestiones sobre los apuntes

**11.** *(UD1, apartado 1)* En Von Neumann, las instrucciones y los datos están en la misma memoria y van por el mismo camino; en Harvard, en memorias y caminos separados, así que puede leer una instrucción y un dato a la vez. Por el bus de **datos** viajan los datos (y, en Von Neumann, también las instrucciones); por el de **direcciones**, la posición de memoria a la que se quiere acceder; por el de **control**, las señales que coordinan (leer, escribir, reloj, interrupciones…).

**12.** *(UD1, apartado 2)* La **unidad de control** lee e interpreta cada instrucción y da las órdenes; la **ALU** hace las operaciones aritméticas y lógicas; los **registros** son memorias diminutas y muy rápidas dentro de la CPU. El contador de programa guarda la dirección de la **siguiente instrucción** que hay que ejecutar.

**13.** *(UD1, apartado 3)* Registros → caché L1 → caché L3 → RAM → SSD. Se borran al apagar los registros, las cachés y la RAM (son volátiles); el SSD no.

**14.** *(UD1, apartado 3)* No: DDR4 y DDR5 no son intercambiables (la muesca está en distinto sitio y la placa solo admite un tipo). Tiene que mirar el **tipo** (DDR4), la **capacidad** (GB), la **velocidad** (MT/s) y la **latencia** (CL), además de que sea del formato adecuado (DIMM en sobremesa, SO-DIMM en portátil). Para el doble canal, mejor módulos iguales.

**15.** *(UD1, apartado 4)* El **chipset** decide qué procesadores, cuánta RAM y qué puertos y ranuras admite la placa. El **zócalo** es el conector físico del procesador (LGA o PGA). Si no se puede montar, no se comprobó que el zócalo y el chipset de la placa admiten ese procesador.

**16.** *(UD1, apartados 4 y 5)* Para el sistema, un **SSD NVMe**: es el más rápido (varios GB/s frente a unos 550 MB/s del SATA), y el sistema arranca y abre los programas antes. Para copias de seguridad grandes, un **disco duro**: es más lento, pero mucho más barato por GB.

**17.** *(UD1, apartado 6)* Un driver es el programa que explica al sistema operativo cómo manejar un dispositivo. **Plug and Play** significa que, al conectarlo, el sistema lo reconoce e instala su driver solo. En Windows se ve en el **Administrador de dispositivos**: un aviso amarillo indica que falta el driver o que falla.

**18.** *(UD1, apartado 7)* De sistema: VirtualBox y el firmware UEFI. De programación: el compilador `javac` y VS Code. De aplicación: el navegador y LibreOffice.

**19.** *(UD1, apartado 8)* El POST (*Power-On Self Test*) es la comprobación del hardware que hace el firmware al encender (procesador, memoria, gráfica). Si pita y no da imagen, falla en el **POST**, antes de buscar el sistema. El significado de los pitidos está en el **manual del fabricante** de la placa; suelen indicar fallo de la memoria o de la gráfica.

**20.** *(UD1, apartado 9)* Por ejemplo: pantalla sin reflejos, a la altura de los ojos o algo por debajo y a más de 40 cm; teclado con espacio delante para apoyar las manos; silla regulable con apoyo lumbar y pies apoyados. Antes de cambiar un componente: apagar y desenchufar el equipo, y descargarse de electricidad estática (pulsera antiestática). Los puestos con pantallas los regula el **Real Decreto 488/1997**, dentro de la Ley 31/1995 de Prevención de Riesgos Laborales.
