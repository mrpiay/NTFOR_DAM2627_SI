# Autoevaluación · semana del 2 al 6 de noviembre

Preguntas sobre «Linux con WSL, Java y VS Code». Puede que sufran modificaciones a lo largo de la semana. Responde poniendo el número de cada pregunta.

En las preguntas con órdenes, ejecútalas donde se indica (PowerShell o el terminal de Ubuntu), copia en tu respuesta lo que sale por pantalla y asegúrate de que lo entiendes: en las pruebas escritas tendrás que explicarlo sin ayuda de la IA.

Si en una pregunta aparece algo que no has visto, búscalo en «Dónde consultar», en el [README de `estudio/`](README.md).

---

**1.** ¿Qué es WSL? ¿En qué se diferencia de una máquina virtual de VirtualBox?

**2.** En PowerShell, ejecuta `wsl --list --verbose`. Copia lo que sale por pantalla.

**3.** En el terminal de Ubuntu, ejecuta estas tres órdenes. Copia lo que sale por pantalla.

```bash
whoami
cd ~
pwd
```

**4.** ¿Qué es `sudo`? ¿Por qué `sudo apt install zip` lo necesita y `mkdir ~/prueba` no?

**5.** ¿Qué diferencia hay entre `sudo apt update`, `sudo apt upgrade` y `sudo apt install unzip`?

**6.** En el terminal de Ubuntu, ejecuta estas dos órdenes. Copia lo que sale por pantalla.

```bash
ls /noexiste && echo hola
ls -d /mnt && echo hola
```

**7.** En el terminal de Ubuntu, ejecuta `ls /mnt/c`. Copia lo que sale por pantalla.

**8.** En el terminal de Ubuntu, ejecuta estas dos órdenes. Copia lo que sale por pantalla. ¿Qué diferencia hay entre el JDK y el JRE?

```bash
javac -version
java -version
```

**9.** En el terminal de Ubuntu, ejecuta `which javac`. Copia lo que sale por pantalla.

**10.** Desde el terminal de Ubuntu, en tu carpeta personal, ejecuta `code .`. ¿Qué pone abajo a la izquierda de VS Code? ¿Para qué sirve la extensión **WSL**?
