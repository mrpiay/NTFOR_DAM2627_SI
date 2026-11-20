# C4 · Cuestionario · semana del 23 al 27 de noviembre

Preguntas sobre la actividad «Windows en una máquina virtual» y sobre los apuntes. Puede que sufran modificaciones a lo largo de la semana. Responde poniendo el número de cada pregunta.

Responde con tus palabras y asegúrate de que lo entiendes: en las pruebas escritas tendrás que explicarlo sin ayuda de la IA.

Si en una pregunta aparece algo que no has visto, búscalo en «Dónde consultar», en el [README de `apuntes/`](apuntes/README.md).

---

## Cuestiones sobre la actividad

**1.** ¿Qué ajustes de la máquina `windows11` son obligatorios para que se pueda instalar Windows 11, y cuáles se eligen para que funcione mejor? ¿Por qué el disco es dinámico y no de tamaño fijo?

**2.** ¿Para qué se marca *Skip Unattended Installation*? ¿Qué haría VirtualBox si no se marcara?

**3.** En la pantalla «¿Qué tipo de instalación quieres?», ¿por qué se elige *Personalizada* y no *Actualización*? En «¿Dónde quieres instalar Windows?», ¿por qué no hace falta crear particiones?

**4.** ¿Qué cambia en la máquina después de instalar las Guest Additions? ¿En qué sistema se instalan, en el anfitrión o en el invitado?

**5.** ¿Qué particiones creó Windows en el disco de la máquina, para qué sirve cada una y en qué sistema de archivos está? ¿Por qué el disco es GPT?

## Cuestiones sobre los apuntes

Estas preguntas se responden con los apuntes de esta semana y de la semana del 9 al 13, en `apuntes/`.

**6.** ¿Qué es el TPM y qué versión pide Windows 11? ¿Con qué herramienta se comprueba si un equipo lo tiene y está listo? ¿Qué otro requisito del firmware pide Windows 11?

**7.** Un equipo tiene un procesador de doble núcleo a 2 GHz, 4 GB de RAM, un disco de 128 GB, firmware UEFI con arranque seguro y sin TPM. ¿Puede instalar Windows 11? ¿Y Windows 10? Justifica la respuesta con los requisitos mínimos.

**8.** Una empresa necesita cifrar los discos de sus portátiles con BitLocker y unirlos a un dominio. ¿Qué edición de Windows 11 no le sirve y cuál sí? ¿Qué edición usan los centros educativos?

**9.** ¿Qué indica una marca amarilla en el Administrador de dispositivos? ¿Qué se puede hacer desde el botón secundario sobre ese dispositivo?

**10.** ¿Qué hacen las órdenes `list disk`, `select disk 0`, `list partition` y `list volume` de `diskpart`? ¿Cómo se sabe con `list disk` si un disco es GPT?
