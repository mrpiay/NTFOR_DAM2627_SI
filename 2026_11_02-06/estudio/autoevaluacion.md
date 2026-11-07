# Autoevaluación · semana del 2 al 6 de noviembre

Preguntas sobre las órdenes de Linux y sobre «Ubuntu Linux, WSL, Java y VS Code». Puede que sufran modificaciones a lo largo de la semana. Responde poniendo el número de cada pregunta.

En las preguntas con órdenes, ejecútalas en un terminal de Linux (el de Ubuntu en WSL o, si tu ordenador tiene Linux, su terminal), copia en tu respuesta lo que sale por pantalla y asegúrate de que lo entiendes: en las pruebas escritas tendrás que explicarlo sin ayuda de la IA.

Las preguntas 1 a 7 se hacen seguidas, en el mismo terminal, dentro de una carpeta de prácticas en `/tmp`. Si cierras el terminal a mitad, vuelve a ella con `cd /tmp/prueba`.

Si en una pregunta aparece algo que no has visto, búscalo en «Dónde consultar», en el [README de `estudio/`](README.md).

---

**1.** Ejecuta estas órdenes. Copia lo que sale por pantalla.

```bash
mkdir -p /tmp/prueba/a/b
cd /tmp/prueba
ls -R
```

**2.** Ejecuta estas órdenes. Copia lo que sale por pantalla.

```bash
touch notas.txt datos.txt
ls
```

**3.** Ejecuta estas órdenes. Copia lo que sale por pantalla.

```bash
echo "uno" > notas.txt
echo "dos" > notas.txt
cat notas.txt
```

**4.** Ejecuta estas órdenes. Copia lo que sale por pantalla.

```bash
echo "uno" > lista.txt
echo "dos" >> lista.txt
echo "tres" >> lista.txt
cat lista.txt
```

**5.** Ejecuta esta orden. Copia lo que sale por pantalla.

```bash
cat lista.txt | sort
```

**6.** Ejecuta estas órdenes. Copia lo que sale por pantalla.

```bash
mv lista.txt numeros.txt
mv numeros.txt a/b/
ls
ls a/b
```

**7.** Ejecuta estas órdenes. Copia lo que sale por pantalla.

```bash
rm a
rm -r a
ls
```

**8.** Abre un archivo largo con `less /etc/services`. ¿Cómo bajas y subes por el archivo? ¿Cómo buscas una palabra? ¿Cómo sales? ¿Para qué sirve `less` si ya existe `cat`?

**9.** ¿Qué es `sudo`? ¿Por qué `sudo apt install zip` lo necesita y `mkdir -p /tmp/prueba` no?

**10.** Ejecuta estas dos órdenes. Copia lo que sale por pantalla. ¿Qué diferencia hay entre el JDK y el JRE?

```bash
javac -version
java -version
```
