# SI · Ejercicio guiado «Entrar en GRUB con el menú oculto»

Se hace con la máquina `ubuntu-arranque` del [proyecto de la semana](proyecto-SI.md), después del paso 6.

## Qué es GRUB

Al encender un equipo, lo primero que se ejecuta es el **firmware** (BIOS o UEFI). El firmware busca un disco desde el que arrancar y carga un pequeño programa: el **gestor de arranque**. El gestor de arranque hace dos cosas:

- carga el **kernel** del sistema operativo, que pone en marcha todo lo demás;
- si hay varias opciones (varios sistemas, varios kernels, el modo de recuperación), muestra un **menú** para elegir.

En Linux, el gestor de arranque habitual es **GRUB** (*GRand Unified Bootloader*). Su configuración se escribe en `/etc/default/grub`, y la orden `update-grub` la pasa a `/boot/grub/grub.cfg`, que es lo que GRUB lee de verdad al arrancar ([apuntes de la UD2, apartado 8](../apuntes/UD2-sistemas-operativos.md#8-el-arranque-y-los-gestores-de-arranque)).

En el paso 6 del proyecto, GRUB quedó configurado para mostrar siempre el menú durante 10 segundos. En este ejercicio se vuelve a la configuración con la que se instala Ubuntu: **menú oculto y sin espera**. Después se **interrumpe el arranque** para hacer aparecer el menú igualmente, que es lo que se hace en un equipo real cuando hay que elegir otro kernel o entrar en el modo de recuperación.

## Paso 1 · Ver la configuración actual

Arranca la máquina, entra y muestra las dos líneas que controlan el menú:

```bash
grep GRUB_TIMEOUT /etc/default/grub
```

```
GRUB_TIMEOUT_STYLE=menu
GRUB_TIMEOUT=10
```

- **`GRUB_TIMEOUT_STYLE`**: `menu` muestra el menú; `hidden` lo oculta; `countdown` muestra solo una cuenta atrás.
- **`GRUB_TIMEOUT`**: los segundos que GRUB espera antes de arrancar la entrada por defecto.

Si sale `hidden` y `0`, la máquina está como antes del paso 6 (por ejemplo, porque se restauró la instantánea del paso 8): pasa directamente al paso 4 de este ejercicio.

## Paso 2 · Copia de seguridad

Antes de cambiar un archivo de configuración del sistema, se hace una copia:

```bash
sudo cp /etc/default/grub /etc/default/grub.bak
```

Para volver al original: `sudo cp /etc/default/grub.bak /etc/default/grub` y `sudo update-grub`.

## Paso 3 · Ocultar el menú y quitar la espera

Abre el archivo con **nano**:

```bash
sudo nano /etc/default/grub
```

Deja las dos líneas así:

```
GRUB_TIMEOUT_STYLE=hidden
GRUB_TIMEOUT=0
```

Si alguna empieza por `#`, borra el `#`: una línea que empieza por `#` es un comentario y no cuenta. Guarda (**Ctrl+O**, **Intro**) y sal (**Ctrl+X**). Comprueba el cambio con el `grep` del paso 1.

## Paso 4 · Aplicar la configuración

Lo escrito en `/etc/default/grub` no cambia nada hasta que se genera de nuevo `/boot/grub/grub.cfg`:

```bash
sudo update-grub
```

La salida termina en `done`.

## Paso 5 · Reiniciar sin tocar nada

```bash
sudo reboot
```

**Comprueba que…** la máquina arranca directamente, sin mostrar el menú de GRUB.

## Paso 6 · Interrumpir el arranque

1. Reinicia otra vez (`sudo reboot`) y haz clic dentro de la ventana de la máquina para que el teclado vaya a ella.
2. Justo cuando desaparece el logo de VirtualBox, **pulsa Esc una vez**. La máquina arranca con UEFI ([paso 1 del proyecto](proyecto-SI.md#paso-1--crear-la-máquina-virtual)); en una máquina con BIOS, se mantiene pulsada **Mayús**.
3. Aparece el menú de GRUB, sin cuenta atrás: espera a que se elija una entrada.

**Comprueba que…** sale el menú, con **Ubuntu** marcado con `*` y **Advanced options for Ubuntu** debajo. Entra en *Advanced options for Ubuntu*, mira qué kernels hay, vuelve con **Esc** y arranca **Ubuntu** con **Intro**.

**Si te falla…**

- *Arranca directamente, sin menú*: la tecla llegó tarde o la ventana no tenía el teclado. Reinicia, haz clic dentro antes de que salga el logo y pulsa **Esc** en cuanto desaparezca.
- *Sale `grub>` en lugar del menú*: se pulsó **Esc** más de una vez. Escribe `normal` e **Intro**.
- *Sale el menú aunque no se pulsa nada*:
  - si el menú dice **«Try or Install Ubuntu Server»**, es el GRUB de la ISO: está todavía en la unidad óptica. Quítala con **Devices → Optical Drives → Remove disk from virtual drive** (*Dispositivos → Unidades ópticas → Eliminar disco de la unidad virtual*) y reinicia;
  - si el menú es el de **Ubuntu**, el arranque anterior no terminó bien (por ejemplo, porque se cerró la ventana de la máquina) y GRUB lo muestra una vez con 30 segundos de espera. Arranca **Ubuntu**; en el siguiente arranque ya no sale;
  - si no es ninguno de los dos casos, no se ejecutó `sudo update-grub` o las líneas siguen con `#`. Repite los pasos 3 y 4.

## Cómo comprobarlo (lista final)

| Comprobación | Hecho |
|---|---|
| Sé qué es un gestor de arranque y qué hace GRUB |  |
| `grep GRUB_TIMEOUT /etc/default/grub` muestra `hidden` y `0` |  |
| Existe la copia `/etc/default/grub.bak` |  |
| Sé por qué hace falta `sudo update-grub` después de editar `/etc/default/grub` |  |
| Sin tocar nada, la máquina arranca sin menú |  |
| Pulsando **Esc** al desaparecer el logo de VirtualBox, aparece el menú de GRUB |  |
| Sé distinguir el GRUB de la ISO («Try or Install Ubuntu Server») del GRUB del sistema instalado («Ubuntu») |  |
