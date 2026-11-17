# Cuestionario C2 · semana del 9 al 13 de noviembre · soluciones

Entre paréntesis, dónde está la respuesta para repasarla.

## Cuestiones sobre el proyecto

**1.** *(UD2, apartado 5; proyecto, pasos 0–1)* El anfitrión es el ordenador real; el invitado, la máquina virtual con Ubuntu Server; el hipervisor, VirtualBox. VirtualBox es de **tipo 2**: funciona como un programa dentro de un sistema operativo, mientras que uno de tipo 1 funciona directamente sobre el hardware (en servidores). Hay que activar la **virtualización por hardware**, Intel VT-x o AMD-V.

**2.** *(UD2, apartado 7; proyecto, paso 4)* MBR admite 4 particiones principales y discos de hasta 2 TB, y va con BIOS; GPT admite hasta 128 particiones, discos mucho mayores y guarda una copia de la tabla al final del disco, y va con UEFI. En GPT no hay particiones lógicas porque no las necesita: las lógicas eran el truco de MBR para pasar de 4 particiones. La partición EFI contiene los programas de arranque (en Ubuntu, `EFI/ubuntu/shimx64.efi` y `grubx64.efi`) y está montada en `/boot/efi`.

**3.** *(UD2, apartado 8; proyecto, pasos 2 y 8)* Firmware (POST y búsqueda en el orden de arranque) → gestor de arranque (GRUB) → kernel → systemd → inicio de sesión. Antes de instalar, el *Boot Manager* ofrecía el disco (`UEFI VBOX HARDDISK`) y la red (`UEFI PXEv4` y `UEFI PXEv6`); el DVD no salía porque estaba vacío. El disco falló (`failed to load Boot0001 … Not Found`) porque estaba vacío, sin partición EFI ni programa de arranque, y por la red no había ningún servidor que ofreciera un sistema. `grub>` aparece cuando falla la fase del **gestor de arranque**: GRUB arranca, pero no encuentra su configuración.

**4.** *(UD2, apartado 8; proyecto, pasos 6 y 7)* Se cambia en `/etc/default/grub` y se aplica con `sudo update-grub`, que genera `/boot/grub/grub.cfg`. Ese archivo no se edita a mano porque se vuelve a generar en cada `update-grub` (y en las actualizaciones) y se perdería lo escrito. En el modo de recuperación la raíz está montada en **solo lectura** (el parámetro `ro`), así que `passwd` no podría guardar la contraseña nueva hasta volver a montarla en lectura y escritura.

**5.** *(UD2, apartados 6 y 8; proyecto, paso 10)* **Windows Boot Manager** (`bootmgfw.efi`, en la partición EFI). Guarda su configuración en el **BCD**, que se consulta con `bcdedit` (como administrador). Windows 11 pide **UEFI con Secure Boot** y un chip **TPM 2.0**, que muchos ordenadores antiguos no tienen.

## Cuestiones sobre los apuntes

**6.** *(UD2, apartado 1)* Ofrecer una **interfaz** para usar el equipo y **gestionar los recursos** (procesador, memoria, dispositivos, archivos) entre los programas. El **kernel** es la parte central: siempre está en memoria y es quien habla con el hardware.

**7.** *(UD2, apartado 2)* Ubuntu Server es **multiusuario**, **multitarea**, de interfaz **textual** (sin escritorio) y **en red** (da servicios a otros equipos). El airbag necesita un sistema **de tiempo real**, porque tiene que responder siempre dentro de un plazo garantizado.

**8.** *(UD2, apartado 3)* En el **monolítico**, todo el sistema (también los drivers) funciona dentro del kernel: es rápido, pero un fallo puede tirar todo el sistema. En el **microkernel**, el kernel hace lo mínimo y el resto funciona como programas aparte: más estable, pero más lento. Linux es **monolítico**; Windows, **híbrido**.

**9.** *(UD2, apartado 4)* El **libre** se puede usar, estudiar (el código está disponible), modificar y redistribuir. El **freeware** es gratis, pero sin código ni permiso para modificarlo. El **propietario** no da el código y limita el uso, y normalmente es de pago. Sí puedes publicar una versión modificada de VirtualBox, con la condición de que tu versión también sea **GPL** (*copyleft*).

**10.** *(UD2, apartado 9)* `apt update` solo descarga la lista actualizada de paquetes de los repositorios; `apt upgrade` actualiza los paquetes instalados. Se instala con `sudo apt install paquete` y se quita con `sudo apt remove paquete`. En Windows, con `winget install programa` y `winget uninstall programa`.
