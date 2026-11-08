# UD3 · Linux: el terminal

Lo básico del terminal de Linux que se usa desde esta semana. Cada apartado tiene la idea clave, lo que tienes que saber y, cuando hay conceptos que se confunden, una tabla para compararlos. Las preguntas para comprobar que lo entiendes están en el [cuestionario](../cuestionario.md) de la semana, en «Cuestiones sobre los apuntes».

---

## 1. Usuario normal y administrador: `sudo`

**En una frase:** tu usuario normal no puede cambiar el sistema; `sudo` ejecuta una orden como administrador.

**Lo que tienes que saber**

- En Linux, el administrador se llama **`root`**. Tu usuario normal puede trabajar con sus archivos, pero no cambiar el sistema (por ejemplo, instalar programas o tocar carpetas como `/etc` o `/usr`).
- **`sudo`** (*superuser do*) ejecuta **una sola orden** con permisos de administrador: se escribe delante, `sudo apt install zip`.
- Pide **tu contraseña de Linux** (la que creaste al instalar Ubuntu) y durante unos minutos no vuelve a pedirla. Al escribirla no se ve nada: es normal.
- Se usa solo cuando hace falta: para instalar o actualizar sí; para compilar, ejecutar o crear carpetas en tu carpeta personal (`~`) o en `/tmp`, no.

---

## 2. Instalar programas: `apt`

**En una frase:** `apt` es el gestor de paquetes de Ubuntu: descarga e instala programas desde los repositorios.

**Lo que tienes que saber**

| Orden | Qué hace |
| --- | --- |
| `sudo apt update` | Actualiza la lista de programas disponibles; no instala nada |
| `sudo apt upgrade` | Instala las versiones nuevas de lo que ya tienes |
| `sudo apt install <programa>` | Instala un programa |

- Si pregunta `Do you want to continue? [Y/n]`, **Intro** acepta (la mayúscula es la respuesta por defecto).
- **`&&`** une dos órdenes: la segunda solo se ejecuta si la primera termina bien. Por eso se escribe `sudo apt update && sudo apt upgrade`.

**Compara**

| | `apt update` | `apt upgrade` |
|---|---|---|
| Qué cambia | Solo la lista de lo que hay disponible | Los programas instalados |
| ¿Instala algo? | No | Sí, las versiones nuevas |
| Orden | Primero | Después |

---

## 3. El sistema de archivos

**En una frase:** en Linux todo cuelga de una sola carpeta raíz, `/`; tu trabajo va en tu carpeta personal.

**Lo que tienes que saber**

- **`/`** es la raíz: todas las carpetas cuelgan de ella (`/home`, `/etc`, `/tmp`, `/usr`…).
- **`~`** es tu carpeta personal (por ejemplo, `/home/ana`): ahí trabajas con tus archivos y tus proyectos, por ejemplo en `~/dam2627/prog`.
- **`/tmp`** es la carpeta de archivos temporales: cualquier usuario puede escribir en ella, y se vacía al reiniciar. Sirve para hacer pruebas.
- En WSL, **`/mnt/c`** es el disco `C:` de Windows visto desde Linux. Las herramientas de Linux trabajan más rápido con los archivos de `~` que con los de `/mnt/c`.
- Una ruta que empieza por `/` es **absoluta** (desde la raíz: `/tmp/prueba`); si no, es **relativa** a la carpeta en la que estás (`a/b`). `..` es la carpeta de arriba.

---

## 4. Órdenes básicas

**En una frase:** cada orden se escribe y se ejecuta con **Intro**; casi todas aceptan opciones, que empiezan por `-`.

**Lo que tienes que saber**

| Orden | Qué hace | Ejemplo |
|---|---|---|
| `pwd` | Dice en qué carpeta estás | `pwd` |
| `ls` | Lista lo que hay en la carpeta; `-R` también lo de dentro de cada subcarpeta | `ls`, `ls -R` |
| `cd` | Cambia de carpeta; `cd ..` sube una, y `cd` solo vuelve a tu carpeta personal | `cd /tmp/prueba` |
| `mkdir` | Crea una carpeta; `-p` crea también las intermedias que falten | `mkdir -p a/b` |
| `touch` | Crea un archivo vacío (o, si ya existe, solo actualiza su fecha) | `touch notas.txt` |
| `echo` | Escribe un texto en la pantalla | `echo "hola"` |
| `cat` | Muestra el contenido de un archivo | `cat notas.txt` |
| `sort` | Ordena las líneas alfabéticamente | `sort notas.txt` |
| `mv` | Mueve un archivo a otra carpeta o le cambia el nombre | `mv notas.txt a/`, `mv a.txt b.txt` |
| `cp` | Copia un archivo | `cp notas.txt copia.txt` |
| `rm` | Borra un archivo; una carpeta solo con `-r` (todo lo de dentro también, sin preguntar ni papelera) | `rm notas.txt`, `rm -r a` |
| `less` | Muestra un archivo largo página a página: flechas o **Espacio** para moverse, `/palabra` e **Intro** para buscar (`n`, la siguiente), `q` para salir | `less /etc/services` |
| `man` | El manual de una orden (se maneja como `less`) | `man ls` |

- `less` sirve para archivos largos, que con `cat` pasarían de golpe por la pantalla.

---

## 5. Redirección y tuberías

**En una frase:** lo que sale de una orden se puede mandar a un archivo o a otra orden.

**Lo que tienes que saber**

| Símbolo | Qué hace | Ejemplo |
|---|---|---|
| `>` | Manda lo que sale de una orden a un archivo, **sustituyendo** lo que tuviera | `echo "uno" > notas.txt` |
| `>>` | Lo mismo, pero **añadiendo** al final, sin borrar lo que había | `echo "dos" >> notas.txt` |
| `\|` (tubería) | Pasa lo que sale de una orden como entrada de la siguiente | `cat notas.txt \| sort` |

**Compara**

| | `>` | `>>` |
|---|---|---|
| Si el archivo no existe | Lo crea | Lo crea |
| Si ya existe | Borra lo que había y escribe | Añade al final |

---

## 6. Distribuciones de Linux

**En una frase:** una distribución es un Linux completo: el kernel Linux, los programas básicos, un gestor de paquetes y, normalmente, un escritorio.

**Lo que tienes que saber**

- Todas ejecutan los mismos programas; cambian sobre todo el **gestor de paquetes** y el **ritmo de actualizaciones**.

| Distribución | Descripción | Gestor de paquetes |
| --- | --- | --- |
| **Debian** | Una de las más antiguas y la base de muchas otras (Ubuntu, Linux Mint, Kali, Parrot). Muy estable: actualiza poco y con mucho cuidado. Uso típico: servidores y equipos que tienen que funcionar años sin sorpresas | `apt` |
| **Ubuntu** | Basada en Debian; la más usada en ordenadores personales y en la nube. Saca versiones LTS (de soporte largo) cada dos años, como la 24.04. Uso típico: escritorio para programar, servidores y WSL | `apt` |
| **Linux Mint** | Basada en Ubuntu, con un escritorio parecido al de Windows. Uso típico: quien viene de Windows o equipos con pocos recursos | `apt` |
| **Fedora** | Patrocinada por Red Hat; trae versiones recientes de los programas y saca una versión nueva cada seis meses. Uso típico: desarrollo de software y aprender el entorno de Red Hat, muy usado en empresas | `dnf` |
| **Arch** | Mínima: se instala casi pieza a pieza y se actualiza continuamente (*rolling release*). Uso típico: usuarios avanzados que quieren montar y controlar todo su sistema | `pacman` |
| **Manjaro** | Basada en Arch, pero con instalador y escritorio listos para usar. Uso típico: programas muy actualizados sin montar el sistema a mano | `pacman` |
| **Kali** y **Parrot** | Basadas en Debian y especializadas en ciberseguridad (auditorías, pruebas de penetración, análisis forense). No están pensadas para el uso diario; se suelen usar en una máquina virtual o desde un USB | `apt` |

- Para saber más: [Distribución Linux, en Wikipedia](https://es.wikipedia.org/wiki/Distribuci%C3%B3n_Linux) y el catálogo [DistroWatch](https://distrowatch.com/), en inglés.
