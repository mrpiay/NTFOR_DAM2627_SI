# C2 · Cuestionario · semana del 9 al 13 de noviembre

Preguntas sobre el proyecto «El arranque de una máquina virtual» y sobre los apuntes. Puede que sufran modificaciones a lo largo de la semana. Responde poniendo el número de cada pregunta.

Responde con tus palabras y asegúrate de que lo entiendes: en las pruebas escritas tendrás que explicarlo sin ayuda de la IA.

Si en una pregunta aparece algo que no has visto, búscalo en «Dónde consultar», en el [README de `apuntes/`](apuntes/README.md).

---

## Cuestiones sobre el proyecto

**1.** En el proyecto, ¿quién es el anfitrión, quién el invitado y quién el hipervisor? ¿De qué tipo es VirtualBox y en qué se diferencia de uno de tipo 1? ¿Qué hay que activar en el firmware del ordenador para que una máquina virtual vaya rápida?

**2.** ¿En qué se diferencian las tablas de particiones MBR y GPT? ¿Por qué en un disco GPT no hay particiones lógicas? ¿Qué contiene la partición EFI y dónde está montada en Ubuntu?

**3.** Escribe en orden las fases del arranque. En el proyecto, ¿qué opciones ofrecía el *Boot Manager* de la máquina antes de instalar nada, y por qué no pudo arrancar con ninguna? Si al encender sale `grub>`, ¿en qué fase falla?

**4.** ¿Dónde se cambia la configuración de GRUB, qué orden la aplica y por qué no se edita `/boot/grub/grub.cfg`? En el modo de recuperación, ¿por qué hizo falta `mount -o remount,rw /` antes de cambiar la contraseña?

**5.** ¿Cómo se llama el gestor de arranque de Windows, dónde guarda su configuración y con qué orden se consulta? ¿Por qué Windows 11 no se instala en algunos ordenadores antiguos?

## Cuestiones sobre los apuntes

Estas preguntas se responden con los apuntes de cada unidad, en `apuntes/`.

**6.** ¿Cuáles son las dos funciones de un sistema operativo? ¿Qué es el kernel?

**7.** Clasifica Ubuntu Server según el número de usuarios, el número de tareas, su interfaz y la forma de ofrecer sus servicios. ¿Qué tipo de sistema necesita el airbag de un coche y por qué?

**8.** ¿En qué se diferencian un kernel monolítico y un microkernel? ¿De qué tipo es el de Linux? ¿Y el de Windows?

**9.** ¿Qué diferencia hay entre software libre, freeware y software propietario? VirtualBox tiene licencia GPL: ¿puedes publicar una versión modificada? ¿Con qué condición?

**10.** ¿Qué diferencia hay entre `sudo apt update` y `sudo apt upgrade`? ¿Con qué órdenes se instala y se quita un programa en Ubuntu? ¿Y desde el terminal de Windows?
