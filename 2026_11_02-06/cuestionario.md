# Autoevaluación · semana del 2 al 6 de noviembre

Preguntas sobre las órdenes de Linux y el proyecto «Ubuntu Linux, WSL, Java y VS Code», y sobre los apuntes. Puede que sufran modificaciones a lo largo de la semana. Responde poniendo el número de cada pregunta.

En las preguntas con órdenes, ejecútalas en un terminal de Linux (el de Ubuntu en WSL o, si tu ordenador tiene Linux, su terminal), copia en tu respuesta lo que sale por pantalla y asegúrate de que lo entiendes: en las pruebas escritas tendrás que explicarlo sin ayuda de la IA.

Las preguntas 1 a 7 se hacen seguidas, en el mismo terminal, dentro de una carpeta de prácticas en `/tmp`. Si cierras el terminal a mitad, vuelve a ella con `cd /tmp/prueba`.

Si en una pregunta aparece algo que no has visto, búscalo en «Dónde consultar», en el [README de `apuntes/`](apuntes/README.md).

---

## Cuestiones sobre el proyecto

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

## Cuestiones sobre los apuntes

Estas preguntas se responden con los apuntes de cada unidad, en `apuntes/`.

**11.** ¿En qué se diferencian el modelo de Von Neumann y el de Harvard? ¿Qué viaja por cada uno de los tres buses del sistema?

**12.** ¿Cuáles son las tres partes de la CPU y qué hace cada una? ¿Qué guarda el contador de programa?

**13.** Ordena de más rápida a más lenta: RAM, caché L3, SSD, registros, caché L1. ¿Cuáles se borran al apagar el equipo?

**14.** Un compañero quiere ampliar la RAM de su ordenador, que lleva DDR4. ¿Puede ponerle un módulo DDR5? ¿Qué cuatro características de un módulo de RAM tiene que mirar?

**15.** ¿Qué decide el chipset de una placa base? ¿Y el zócalo? Si un procesador nuevo no se puede montar en una placa, ¿qué no se comprobó?

**16.** Para el disco del sistema, ¿qué elegirías: un SSD NVMe, un SSD SATA o un disco duro? ¿Y para guardar copias de seguridad de mucha capacidad? ¿Por qué?

**17.** ¿Qué es un driver? ¿Qué significa Plug and Play? En Windows, ¿dónde se ve si a un dispositivo le falta el driver?

**18.** Di de qué tipo es cada uno de estos programas (de sistema, de programación o de aplicación): VirtualBox, un navegador web, el compilador `javac`, el firmware UEFI, LibreOffice y VS Code.

**19.** ¿Qué es el POST? Al encender un ordenador pita y no da imagen: ¿en qué momento de la puesta en marcha falla y dónde se mira qué significan esos pitidos?

**20.** Di tres normas de un puesto de trabajo con pantalla y dos precauciones antes de cambiar un componente dentro de un ordenador. ¿Qué norma regula los puestos con pantallas?
