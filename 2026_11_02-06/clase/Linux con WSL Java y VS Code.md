# Linux con WSL, Java y VS Code

**Preparando el entorno de desarrollo para el módulo de Programación**

Vamos a empezar a programar en Java preparando un entorno de desarrollo con tres piezas, instaladas en este orden:

1. **WSL con Ubuntu:** un Linux dentro de Windows, donde viven tus proyectos y tu terminal.
2. **JDK:** las herramientas de Java (`javac` y `java`), instaladas dentro de Ubuntu.
3. **VS Code:** el editor, instalado en Windows y conectado a Ubuntu con la extensión WSL.

Al final, escribes el código en VS Code y compilas y ejecutas desde su terminal, que es un terminal de Ubuntu.

> **Si tu ordenador tiene Linux en lugar de Windows**, no necesitas WSL: tu Linux ya es el entorno.
> - Sáltate el apartado 1.
> - Haz el apartado 2 en tu terminal.
> - En el apartado 3, descarga VS Code para Linux desde [code.visualstudio.com](https://code.visualstudio.com) (en Ubuntu, el paquete `.deb`) e instálalo con `sudo apt install ./code_*.deb`, desde la carpeta de la descarga. No instales la extensión WSL: `code .` abre VS Code directamente y su terminal (**Ctrl+ñ**) ya es el de tu Linux.
> - Si tu Linux no es Ubuntu, las órdenes equivalentes están en «Otras distribuciones de Linux», al final.

Para Java también hay IDE (entornos de desarrollo integrados) como Eclipse, IntelliJ IDEA o NetBeans, que compilan y ejecutan con un botón. VS Code es un editor, pero con extensiones se acerca a un IDE. Empezamos con VS Code y el terminal para ver qué hace cada paso, y lo aprendido te servirá después en cualquier IDE.

## 1. WSL: Linux dentro de Windows

WSL (Windows Subsystem for Linux) ejecuta un Linux de verdad dentro de Windows, sin máquina virtual aparte ni arranque dual. Usamos Ubuntu 24.04, que tiene su propio terminal (bash), sus propios programas y sus propios archivos.

Requisitos: Windows 10 versión 2004 o superior (build 19041 o superior) o Windows 11.

**Instalación**

1. Abre PowerShell como administrador: escribe *PowerShell* en el menú Inicio, clic derecho > **Ejecutar como administrador** y acepta el aviso de Windows.
2. Ejecuta:

   ```powershell
   wsl --install -d Ubuntu-24.04
   ```

   `-d Ubuntu-24.04` elige la versión de Ubuntu: así todos tenemos la misma y con ella Java 21.

3. Reinicia el ordenador. Al volver, a veces Ubuntu se abre solo para terminar la instalación: si es así, sigue con el paso 4 en esa ventana.
4. Abre **Ubuntu** desde el menú Inicio. La primera vez te pide un nombre de usuario y una contraseña de Linux. Son independientes de los de Windows, y la contraseña es la que te pedirá `sudo`. Al escribirla no se ve nada en pantalla: es normal.
5. Actualiza los paquetes de Ubuntu:

   ```bash
   sudo apt update && sudo apt upgrade
   ```

   Si pregunta `Do you want to continue? [Y/n]`, pulsa Intro para aceptar.

**Qué es sudo**

En Linux, tu usuario normal no puede cambiar el sistema, por ejemplo instalar programas. `sudo` ("superuser do") ejecuta un solo comando con permisos de administrador, llamado `root` en Linux.

- Escribe `sudo` delante del comando: `sudo apt install zip`.
- Te pide tu contraseña de Linux, la que creaste al instalar Ubuntu, y durante unos minutos no vuelve a pedirla.
- Úsalo solo cuando haga falta, como al instalar o actualizar. Para compilar, ejecutar o crear carpetas en tu `~` no se necesita.

En los comandos de instalación también aparece `apt`, el gestor de paquetes de Ubuntu, que descarga e instala programas:

| Comando | Qué hace |
| --- | --- |
| `sudo apt update` | Actualiza la lista de programas disponibles; no instala nada |
| `sudo apt upgrade` | Instala las versiones nuevas de lo que ya tienes |
| `sudo apt install <programa>` | Instala un programa |

`&&` une dos comandos: el segundo solo se ejecuta si el primero termina bien.

Para comprobar la instalación, en PowerShell:

```powershell
wsl --list --verbose
```

Debe aparecer `Ubuntu-24.04` con `VERSION 2`.

**WSL2 y VirtualBox.** Con WSL2 activo, VirtualBox funciona sobre la virtualización de Windows (Hyper-V) y las máquinas virtuales van más lentas. Es normal: siguen funcionando igual.

**Dónde viven tus archivos**

- `~` (por ejemplo `/home/ana`) es tu carpeta personal en Linux. Guarda aquí tus proyectos, por ejemplo en `~/dam2627/prog`. Las herramientas de Linux trabajan más rápido con estos archivos.
- `/mnt/c` es el disco C: de Windows visto desde Linux.
- Desde el Explorador de Windows puedes ver tus archivos de Linux en **Linux > Ubuntu**, en el panel izquierdo, o escribiendo `explorer.exe .` en el terminal de Ubuntu.

## 2. JDK: las herramientas para programar en Java

El JDK (Java Development Kit) es lo que necesitas para programar en Java. Incluye el JRE, que solo sirve para ejecutar programas, y le añade las herramientas de desarrollo.

| Herramienta | Para qué sirve |
| --- | --- |
| `javac` | Compilador: convierte los `.java` en bytecode (`.class`) |
| `java` | Arranca la máquina virtual (JVM) y ejecuta el bytecode |
| JRE | Máquina virtual y librerías para ejecutar programas; viene dentro del JDK |

Con el JRE solo podrías ejecutar programas ya compilados. Para compilar los tuyos necesitas el JDK.

**Instalación en Ubuntu**

En el terminal de Ubuntu, no en PowerShell:

```bash
sudo apt update
sudo apt install openjdk-21-jdk zip unzip
```

- `openjdk-21-jdk` instala el JDK de Java 21, una versión de soporte largo (LTS).
- `zip` y `unzip` no son parte de Java, pero los necesitarás para entregar los proyectos.

Comprueba la instalación:

```bash
javac -version
java -version
```

Los dos comandos deben mostrar la versión 21: `javac 21.0.x` y `openjdk version "21.0.x"`. Si `apt install` pregunta `[Y/n]`, pulsa Intro para aceptar.

## 3. VS Code: el editor, conectado a Linux

VS Code (Visual Studio Code) es un editor de código gratuito de Microsoft. Se instala en Windows, y con la extensión WSL edita los archivos de Ubuntu y abre un terminal de Ubuntu dentro del propio editor.

**Instalación**

1. Descarga VS Code para Windows desde [code.visualstudio.com](https://code.visualstudio.com) e instálalo en Windows, no dentro de Ubuntu.
2. Durante la instalación, deja marcada la opción **Add to PATH**. Es la que permite abrir VS Code con `code` desde el terminal de Ubuntu.
3. En VS Code, abre Extensiones (**Ctrl+Shift+X**) e instala **WSL**, de Microsoft (`ms-vscode-remote.remote-wsl`).

**Uso desde Linux**

1. Abre el terminal de Ubuntu y entra en la carpeta del proyecto:

   ```bash
   mkdir -p ~/dam2627/prog/java-pr0
   cd ~/dam2627/prog/java-pr0
   code .
   ```

2. La primera vez, VS Code descarga lo que necesita dentro de Ubuntu (el servidor de VS Code). Tarda unos segundos.
3. Abajo a la izquierda debe aparecer **WSL: Ubuntu-24.04**. Si no aparece, estás editando como si fueran archivos de Windows: cierra y vuelve a abrir con `code .` desde Ubuntu.
4. Abre el terminal integrado con **Terminal > New Terminal** (en español, **Terminal > Nuevo terminal**) o **Ctrl+ñ** (en teclado inglés, ``Ctrl+` ``). Es un bash de Ubuntu: desde ahí compilas con `javac` y ejecutas con `java`.

**Extensiones**

Con la conexión WSL, la mayoría de las extensiones se instalan dentro de Ubuntu. En la vista de Extensiones salen en dos grupos: **Local - Installed** (Windows) y **WSL: Ubuntu-24.04**. Si una extensión sale atenuada, pulsa **Install in WSL: Ubuntu-24.04**.

> **Nota:** mientras aprendes, conviene no instalar extensiones que escriben código por ti (autocompletado, asistentes) ni que marcan los errores mientras escribes. Así te encuentras los errores al compilar, lees lo que dice `javac` y aprendes de cada fallo.

## Otras distribuciones de Linux

Una **distribución** es un Linux completo: el núcleo (el kernel Linux), los programas básicos, un gestor de paquetes para instalar más y, normalmente, un escritorio. Todas ejecutan los mismos programas; cambian sobre todo el gestor de paquetes y el ritmo de actualizaciones.

| Distribución | Descripción | Gestor de paquetes |
| --- | --- | --- |
| **Debian** | Una de las más antiguas y la base de muchas otras (Ubuntu, Linux Mint, Kali, Parrot).<br>Muy estable: actualiza poco y con mucho cuidado.<br>Uso típico: servidores y equipos que tienen que funcionar años sin sorpresas. | `apt` |
| **Ubuntu** | Basada en Debian; la más usada en ordenadores personales y en la nube.<br>Saca versiones LTS (de soporte largo) cada dos años, como la 24.04.<br>Uso típico: escritorio para programar, servidores y WSL. | `apt` |
| **Linux Mint** | Basada en Ubuntu, con un escritorio parecido al de Windows.<br>Uso típico: ordenadores personales de quien viene de Windows o de equipos con pocos recursos. | `apt` |
| **Fedora** | Patrocinada por Red Hat; trae versiones recientes de los programas y saca una versión nueva cada seis meses.<br>Uso típico: desarrollo de software y para aprender el entorno de Red Hat, muy usado en empresas. | `dnf` |
| **Arch** | Mínima: se instala casi pieza a pieza y se actualiza continuamente (*rolling release*).<br>Uso típico: usuarios avanzados que quieren montar y controlar todo su sistema. | `pacman` |
| **Manjaro** | Basada en Arch, pero con instalador y escritorio listos para usar.<br>Uso típico: tener programas muy actualizados sin montar el sistema a mano. | `pacman` |
| **Kali** y **Parrot** | Basadas en Debian y especializadas en ciberseguridad: traen cientos de herramientas para auditorías de seguridad, pruebas de penetración y análisis forense.<br>No están pensadas para el uso diario; normalmente se usan en una máquina virtual o arrancando desde un USB.<br>Para esta guía, sus órdenes son las de Ubuntu (`apt`). | `apt` |

Esta guía usa las órdenes de Ubuntu (`apt`). Si tu ordenador tiene otra distribución, estas son las equivalentes:

| Para… | Ubuntu, Debian y Linux Mint | Fedora | Arch (y Manjaro) |
| --- | --- | --- | --- |
| Actualizar la lista de programas | `sudo apt update` | `sudo dnf check-update` | Se hace junto con la fila siguiente |
| Instalar las versiones nuevas | `sudo apt upgrade` | `sudo dnf upgrade` | `sudo pacman -Syu` |
| Instalar el JDK 21 | `sudo apt install openjdk-21-jdk` | `sudo dnf install java-21-openjdk-devel` | `sudo pacman -S jdk21-openjdk` |
| Instalar `zip` y `unzip` | `sudo apt install zip unzip` | `sudo dnf install zip unzip` | `sudo pacman -S zip unzip` |
| Instalar VS Code | Paquete `.deb` de code.visualstudio.com: `sudo apt install ./code_*.deb` | Paquete `.rpm`: `sudo dnf install ./code-*.rpm` | `sudo pacman -S code` (la versión libre, «Code - OSS») |

Lo demás es igual en todas: `javac -version`, `java -version`, `code .` y el terminal de VS Code.

## Si algo falla

| Qué pasa | Qué hacer |
| --- | --- |
| `wsl --install` se queda parado en 0.0 % | Cancela con **Ctrl+C** y ejecuta `wsl --install --web-download -d Ubuntu-24.04` |
| `wsl --list --verbose` muestra Ubuntu con `VERSION 1` | En PowerShell: `wsl --set-version Ubuntu-24.04 2` |
| `javac` dice `command not found` | Falta el JDK: `sudo apt install openjdk-21-jdk` |
| `E: Unable to locate package openjdk-21-jdk` | Falta actualizar la lista: `sudo apt update` y repite la instalación |
| `code .` dice `command not found` | Cierra el terminal de Ubuntu y ábrelo de nuevo después de instalar VS Code. Si sigue, en PowerShell `wsl --shutdown` y vuelve a abrir Ubuntu |
| `wsl --install` da el error `0x80370102` | La virtualización está desactivada: actívala en la BIOS/UEFI (Intel VT-x, AMD-V o SVM) y repite |
| Abajo a la izquierda de VS Code no pone **WSL: Ubuntu-24.04** | Cierra VS Code y vuelve a abrirlo con `code .` desde el terminal de Ubuntu |
