# UD1 · Ampliación: las tarjetas de red con una máquina virtual

Al comparar la red del equipo real con la de la máquina virtual (paso 4 del proyecto), `ipconfig` y Ubuntu muestran MAC e IP distintas. Es lo esperado: este apartado explica qué es cada dato, dónde se mira y qué tiene que coincidir. Continúa el [apartado 5 de los apuntes de la UD1](UD1-el-equipo-por-dentro.md#5-tarjetas-de-expansión) (la tarjeta de red y la MAC).

---

## 1. Dos equipos, dos tarjetas

Con la máquina virtual encendida hay **dos ordenadores**, y cada uno tiene su tarjeta de red:

- **El equipo real** (Windows), con su tarjeta de verdad: la Wi-Fi o la Ethernet de la placa.
- **La máquina virtual** (Ubuntu), con una tarjeta **inventada por VirtualBox**, que se presenta como una Intel `82540EM`.

De cada tarjeta interesan dos datos:

| Dato | Qué es | ¿Cambia? |
|---|---|---|
| **MAC** | El número que identifica a la tarjeta: 48 bits, escritos como 12 cifras hexadecimales | No: es de la tarjeta, esté donde esté |
| **IP** | La dirección que la red da a esa tarjeta para comunicarse | Sí: depende de la red a la que se conecte |

Como son dos tarjetas distintas, hay **dos MAC distintas** y **dos IP distintas**.

## 2. Dónde se mira cada cosa

| Dónde | Qué se ve | De qué tarjeta |
|---|---|---|
| `ipconfig /all`, en el terminal de Windows | La MAC (*Dirección física*) y la IP de cada adaptador | De las tarjetas **del equipo real** |
| VirtualBox: **Settings → Network → Adapter 1 → Advanced → MAC Address** (*Configuración → Red → Adaptador 1 → Avanzadas → Dirección MAC*) | La MAC que VirtualBox **ha dado** a la tarjeta de la máquina | De la tarjeta **de la máquina virtual** |
| `ip -br link` (MAC) e `ip -br addr` (IP), en el terminal de Ubuntu | La MAC y la IP que Ubuntu **ve** en su tarjeta | De la tarjeta **de la máquina virtual** |

De ahí sale qué se compara:

- **VirtualBox y `ip -br link` tienen que coincidir**: miran la misma tarjeta. VirtualBox dice qué MAC le ha puesto y Ubuntu confirma que es esa.
- **`ipconfig` y la máquina virtual no tienen que coincidir**: son tarjetas distintas.

## 3. Un ejemplo

**En Windows, `ipconfig /all`:**

```
Adaptador de LAN inalámbrica Wi-Fi:
   Descripción . . . . . . : Intel(R) Wi-Fi 6 AX201
   Dirección física. . . . : A4-5E-60-12-34-56      ← MAC de la tarjeta real
   Dirección IPv4. . . . . : 192.168.1.35           ← IP del equipo real en la red del aula o de casa
```

**En VirtualBox, Adapter 1 → Advanced:**

```
MAC Address: 080027A1B2C3                           ← MAC que VirtualBox dio a la tarjeta de la máquina
```

**En Ubuntu:**

```
$ ip -br link
lo       UNKNOWN  00:00:00:00:00:00
enp0s3   UP       08:00:27:a1:b2:c3                 ← la misma MAC que en VirtualBox

$ ip -br addr
lo       UNKNOWN  127.0.0.1/8
enp0s3   UP       10.0.2.15/24                      ← IP de la máquina virtual
```

- `080027A1B2C3` y `08:00:27:a1:b2:c3` son **el mismo número**, escrito de otra forma: VirtualBox, sin separadores; Linux, con dos puntos; Windows, con guiones (`08-00-27-A1-B2-C3`).
- Los **tres primeros bytes** de una MAC identifican al **fabricante** de la tarjeta: `08:00:27` es VirtualBox; `A4-5E-60`, el fabricante de la tarjeta real.
- `lo` (*loopback*) no es una tarjeta: es la conexión del equipo consigo mismo, siempre con `127.0.0.1`. Se ignora.

## 4. Por qué la IP de la máquina es `10.0.2.15`: los modos de red

La IP de la máquina depende del modo de red elegido en VirtualBox: **Adapter 1 → Attached to** (*Adaptador 1 → Conectado a*). La máquina del curso usa **NAT**, como se vio al instalarla («[La red de la máquina: NAT](../../2026_11_09-13/apuntes/UD2-sistemas-operativos.md#la-red-de-la-máquina-nat)», en los apuntes de la UD2).

| Modo | Cómo funciona | IP de la máquina | ¿Se parece a la de `ipconfig`? |
|---|---|---|---|
| **NAT** (el que viene por defecto) | VirtualBox monta una **red privada pequeña** solo para la máquina, que sale a Internet **a través del equipo real**, como un móvil que usa la conexión compartida de otro | Siempre `10.0.2.15` | No: está en otra red |
| **Bridged Adapter** (*Adaptador puente*) | La máquina se conecta **directamente a la misma red** que el equipo real, como otro ordenador enchufado al mismo router | Una de la misma red, por ejemplo `192.168.1.40` | Sí, la misma red, pero otra IP y otra MAC: es otro equipo |
| **Host-only Adapter** (*Adaptador solo anfitrión*) | Una red privada **solo entre el equipo real y sus máquinas**, sin Internet (apartado 6) | Una de la red `192.168.56.x`, por ejemplo `192.168.56.101` | Se parece a la del adaptador «VirtualBox Host-Only» de `ipconfig` (`192.168.56.1`): es la misma red |

## 5. Cómo sale la máquina a Internet

### Con NAT: VirtualBox sale por la máquina

La clave: **para Windows, VirtualBox es un programa más que usa Internet, como el navegador.** La máquina no sale directamente: le pide a VirtualBox que salga por ella. Así, paso a paso, cuando la máquina abre `www.google.com`:

1. **La máquina envía su petición a la puerta de enlace.** Ubuntu no sabe llegar a Google, así que hace lo que hace cualquier equipo: envía el paquete a su **puerta de enlace** (el router de su red), `10.0.2.2`:

   ```
   De: 10.0.2.15 (la máquina)   →   Para: 142.250.x.x (Google)
   ```

2. **VirtualBox lo recoge.** `10.0.2.2` no es ningún aparato: la tarjeta de la máquina es inventada, así que todo lo que envía llega a VirtualBox, un programa que se ejecuta en Windows.
3. **VirtualBox hace la petición desde Windows, como un programa normal.** Abre él mismo una conexión con Google, igual que la abriría Chrome, y Windows la envía por la Wi-Fi o la Ethernet de verdad, con su IP:

   ```
   De: 192.168.1.35 (el equipo real)   →   Para: 142.250.x.x (Google)
   ```

   Antes, VirtualBox **apunta** de quién es esa conexión:

   | Conexión que abrió VirtualBox en Windows | Es de… |
   |---|---|
   | hacia Google, desde el puerto 51234 | la máquina `10.0.2.15` |

4. **Google responde al equipo real.** Solo ve a `192.168.1.35`; no sabe que hay una máquina virtual.
5. **VirtualBox mira su nota y se lo pasa a la máquina**, como si viniera de Google:

   ```
   De: 142.250.x.x (Google)   →   Para: 10.0.2.15 (la máquina)
   ```

   La máquina recibe su web sin enterarse de que hubo un intermediario.

Esto es **NAT** (*Network Address Translation*, traducción de direcciones de red): cambiar la dirección de quien envía y recordar el cambio para devolver la respuesta.

**Después, el router del aula hace lo mismo.** El paquete de Windows tampoco sale tal cual: el router cambia `192.168.1.35` por la IP pública del centro, lo apunta y devuelve la respuesta al equipo. Hay **dos NAT seguidos**:

```
Máquina 10.0.2.15 → VirtualBox (NAT 1) → Windows 192.168.1.35 → router del aula (NAT 2) → Internet
```

**Por qué desde fuera no se llega a la máquina.** VirtualBox solo tiene en su nota las conexiones que **empezó la máquina**. Si alguien (incluso el propio Windows) intenta conectarse a la máquina, no hay ninguna nota que diga «esto es para `10.0.2.15`», y se descarta. Con NAT, **la máquina puede salir, pero nadie puede entrar**.

Se ve en Ubuntu (salidas resumidas):

```
$ ip route
default via 10.0.2.2 dev enp0s3      ← la puerta de enlace: el «router» de VirtualBox
10.0.2.0/24 dev enp0s3               ← la red privada de la máquina

$ resolvectl status
...
Current DNS Server: 10.0.2.3         ← también es VirtualBox, que pregunta al DNS del equipo real
```

### Con adaptador puente: sale por su cuenta

En modo **puente**, VirtualBox no traduce nada: los paquetes de la máquina salen por la tarjeta real **con la MAC y la IP de la máquina**. El router del aula la ve como un equipo más, le da IP (`192.168.1.40`) y la máquina sale a Internet a través de él, igual que el equipo real.

### Con solo anfitrión: no sale

En modo **Host-only** no hay router ni traducción: la máquina solo llega al equipo real y a las otras máquinas de esa red. Para que además tenga Internet, se le pone un **segundo adaptador** en NAT (**Adapter 2**), y entonces tiene dos tarjetas, una en cada red.

## 6. Lo que despista: el adaptador «VirtualBox Host-Only»

En `ipconfig /all` puede aparecer un adaptador que no es ni la Wi-Fi ni la Ethernet:

```
Adaptador de Ethernet VirtualBox Host-Only Network:
   Dirección física. . . . : 0A-00-27-00-00-0B
   Dirección IPv4. . . . . : 192.168.56.1
```

Por el nombre parece la tarjeta de la máquina virtual, pero **no lo es**. Es una tarjeta virtual que VirtualBox **añade a Windows** al instalarse, esté encendida o no alguna máquina, y la usen o no. Por eso sale en `ipconfig` aunque la máquina esté en modo NAT.

**Para qué sirve.** VirtualBox tiene un tercer modo de red, **Host-only Adapter** (*Adaptador solo anfitrión*): una **red privada solo entre el equipo real y sus máquinas virtuales**, sin salida a Internet. Es como un cable que une el ordenador con las máquinas y con nada más. En esa red:

- el equipo real es `192.168.56.1`, a través de este adaptador de Windows;
- cada máquina conectada en ese modo recibe una IP de la misma red, como `192.168.56.101`, en su propia tarjeta (que en Ubuntu se ve con `ip -br addr`, como siempre).

Se usa cuando el equipo real tiene que **llegar a la máquina**: entrar en ella desde el terminal de Windows o abrir en el navegador una web que se sirve dentro de la máquina. En modo NAT eso no se puede, porque la red de NAT es solo de la máquina y el equipo real no la ve.

**Con el modo NAT**, que es el de la máquina de este curso, este adaptador **no interviene**: la máquina no está conectada a esa red. Su IP y su MAC no tienen que coincidir con nada de lo que se ve dentro de la máquina.

---

## En resumen

- `ipconfig` muestra la red **del equipo real**.
- La red **de la máquina virtual** se mira en **VirtualBox** y con **`ip -br link` / `ip -br addr` en Ubuntu**, y esos dos sí coinciden.
- En modo NAT, la máquina tiene siempre `10.0.2.15`, en una red propia, y sale a Internet porque VirtualBox, un programa de Windows, hace cada petición por ella con la IP del equipo real y le devuelve la respuesta; en modo puente, tiene una IP de la misma red que el equipo y sale por su cuenta.
