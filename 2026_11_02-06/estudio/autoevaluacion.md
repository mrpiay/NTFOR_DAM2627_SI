# Autoevaluación · semana del 2 al 6 de noviembre

Preguntas sobre «Ubuntu Linux, WSL, Java y VS Code». Puede que sufran modificaciones a lo largo de la semana. Responde poniendo el número de cada pregunta.

En las preguntas con órdenes, ejecútalas en un terminal de Linux (el de Ubuntu en WSL o, si tu ordenador tiene Linux, su terminal), copia en tu respuesta lo que sale por pantalla y asegúrate de que lo entiendes: en las pruebas escritas tendrás que explicarlo sin ayuda de la IA.

Las preguntas sobre WSL y Windows hay que responderlas aunque tu ordenador tenga Linux y no los uses: no piden ejecutar nada, y lo que preguntan está en la guía.

Si en una pregunta aparece algo que no has visto, búscalo en «Dónde consultar», en el [README de `estudio/`](README.md).

---

**1.** ¿Qué es WSL? ¿En qué se diferencia de una máquina virtual de VirtualBox?

**2.** ¿Qué muestra `wsl --list --verbose`, en PowerShell? ¿Qué significan `NAME`, `STATE` y `VERSION 2`?

**3.** Ejecuta estas cuatro órdenes. Copia lo que sale por pantalla.

```bash
cd /tmp
pwd
cd ..
pwd
```

**4.** ¿Qué es `sudo`? ¿Por qué `sudo apt install zip` lo necesita y `mkdir ~/prueba` no?

**5.** ¿Qué diferencia hay entre `sudo apt update`, `sudo apt upgrade` y `sudo apt install unzip`?

**6.** Ejecuta estas dos órdenes. Copia lo que sale por pantalla.

```bash
ls /noexiste && echo hola
ls -d /tmp && echo hola
```

**7.** Con WSL, ¿qué es `/mnt/c`? ¿Cómo se llega desde Ubuntu a los archivos de Windows? ¿Y desde el Explorador de Windows a los archivos de Ubuntu?

**8.** Ejecuta estas dos órdenes. Copia lo que sale por pantalla. ¿Qué diferencia hay entre el JDK y el JRE?

```bash
javac -version
java -version
```

**9.** Ejecuta `which javac`. Copia lo que sale por pantalla.

**10.** Con WSL, ¿qué indica **WSL: Ubuntu-24.04** abajo a la izquierda de VS Code? ¿Para qué sirve la extensión **WSL**?
