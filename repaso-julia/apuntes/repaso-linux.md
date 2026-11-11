# Repaso · gestión de archivos en Linux

Repaso de la práctica de Julia «Gestión de archivos» (Teams): las órdenes que no están en los apuntes de la semana del 2 al 6. Es una introducción a la UD3, que se evalúa en la 2ª evaluación. Lo que se explica en esos apuntes solo se menciona aquí, con su enlace.

---

## 1. Copiar, mover y borrar carpetas

**En una frase:** las carpetas se copian y se borran con las mismas órdenes que los archivos, añadiendo la opción que recorre todo su contenido.

**Lo que tienes que saber**

- **`cp -r origen destino`** copia una carpeta **con todo lo que tiene dentro** (`-r`: recursivo). Sin `-r`, `cp` no copia carpetas.
- **`mv`** mueve **o renombra** archivos y carpetas, sin opciones especiales.
- **`rmdir carpeta`** borra una carpeta **solo si está vacía**.
- **`rm -r carpeta`** borra una carpeta **y todo su contenido**, sin pasar por la papelera. Antes de usarlo, conviene comprobar la ruta con `ls`.

**Compara**

| | `rmdir carpeta` | `rm -r carpeta` |
|---|---|---|
| Carpeta vacía | La borra | La borra |
| Carpeta con contenido | Da error y no borra nada | Lo borra todo |

---

## 2. Editar un archivo desde el terminal

**En una frase:** `nano` es el editor más sencillo del terminal; `vim` es más potente, pero tiene modos.

**Lo que tienes que saber**

- **`nano archivo.txt`** abre (o crea) el archivo. **Ctrl+O** e Intro guarda; **Ctrl+X** sale. Los atajos se ven abajo (`^` es Ctrl).
- **`vim archivo.txt`** empieza en **modo normal**, donde las teclas son órdenes:
  - **`i`** pasa al **modo inserción**, para escribir;
  - **Esc** vuelve al modo normal;
  - **`:w`** guarda, **`:q`** sale, **`:wq`** guarda y sale, **`:q!`** sale sin guardar.

---

## 3. Consultar y buscar dentro de los archivos

**En una frase:** varias órdenes pequeñas muestran, cuentan o filtran el contenido de un archivo, y se combinan con `|`.

**Lo que tienes que saber**

- **`head archivo`** muestra las **10 primeras** líneas; **`tail archivo`**, las **10 últimas**. Con `-n 3`, las 3.
- **`wc -l archivo`** cuenta las **líneas**.
- **`grep texto archivo`** muestra las líneas que **contienen** ese texto. `-i` no distingue mayúsculas; `-c` cuenta las líneas que coinciden.
- **`sort`** ordena las líneas; **`uniq`** quita las líneas **repetidas seguidas**, por eso casi siempre va después de `sort`.
- Ejemplo: `sort empleados.txt | uniq | wc -l` cuenta los nombres distintos.

**Compara**

| Orden | Resultado |
|---|---|
| `grep Vigo clientes.txt` | Las líneas que contienen «Vigo» |
| `grep -c Vigo clientes.txt` | Cuántas líneas contienen «Vigo» |
| `sort clientes.txt \| uniq` | Las líneas ordenadas y sin repetir |

---

## 4. Comprimir y hacer copias de seguridad

**En una frase:** `gzip` comprime un archivo; `tar` junta una carpeta entera en un solo archivo y, con `-z`, además lo comprime.

**Lo que tienes que saber**

- **`gzip informe.txt`** lo comprime en `informe.txt.gz` (el original desaparece); **`gunzip informe.txt.gz`** lo descomprime.
- **`tar`** con sus opciones:
  - **`tar -czf copia.tar.gz carpeta`**: **c**rea la copia, comprimida (**z**), en el archivo (**f**) `copia.tar.gz`;
  - **`tar -tzf copia.tar.gz`**: lis**t**a lo que hay dentro sin extraerlo;
  - **`tar -xzf copia.tar.gz`**: e**x**trae el contenido en la carpeta actual.

---

## 5. Lo demás, en los apuntes de la semana del 2 al 6

| Tema | Dónde |
|---|---|
| El sistema de archivos, rutas absolutas y relativas | [UD3 · Linux, apartado 3](../../2026_11_02-06/apuntes/UD3-linux.md#3-el-sistema-de-archivos) |
| `pwd`, `ls`, `cd`, `mkdir`, `touch`, `cp`, `mv`, `rm`, `cat`, `less`, `man` | [UD3 · Linux, apartado 4](../../2026_11_02-06/apuntes/UD3-linux.md#4-órdenes-básicas) |
| `>`, `>>` y `\|` | [UD3 · Linux, apartado 5](../../2026_11_02-06/apuntes/UD3-linux.md#5-redirección-y-tuberías) |
