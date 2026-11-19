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

La IP de la máquina depende del modo de red elegido en VirtualBox: **Adapter 1 → Attached to** (*Adaptador 1 → Conectado a*).

| Modo | Cómo funciona | IP de la máquina | ¿Se parece a la de `ipconfig`? |
|---|---|---|---|
| **NAT** (el que viene por defecto) | VirtualBox monta una **red privada pequeña** solo para la máquina, que sale a Internet **a través del equipo real**, como un móvil que usa la conexión compartida de otro | Siempre `10.0.2.15` | No: está en otra red |
| **Bridged Adapter** (*Adaptador puente*) | La máquina se conecta **directamente a la misma red** que el equipo real, como otro ordenador enchufado al mismo router | Una de la misma red, por ejemplo `192.168.1.40` | Sí, la misma red, pero otra IP y otra MAC: es otro equipo |

## 5. Lo que despista: el adaptador «VirtualBox Host-Only»

En `ipconfig /all` puede aparecer un adaptador que no es ni la Wi-Fi ni la Ethernet:

```
Adaptador de Ethernet VirtualBox Host-Only Network:
   Dirección física. . . . : 0A-00-27-00-00-0B
   Dirección IPv4. . . . . : 192.168.56.1
```

Por el nombre parece la tarjeta de la máquina virtual, pero **no lo es**. Es una tarjeta virtual que VirtualBox crea **en Windows** para una red interna entre el equipo y sus máquinas, y solo se usa con el modo **Host-only Adapter** (*Adaptador solo anfitrión*). En modo NAT no interviene, y no tiene que coincidir con nada de lo que se ve dentro de la máquina.

---

## En resumen

- `ipconfig` muestra la red **del equipo real**.
- La red **de la máquina virtual** se mira en **VirtualBox** y con **`ip -br link` / `ip -br addr` en Ubuntu**, y esos dos sí coinciden.
- En modo NAT, la máquina tiene siempre `10.0.2.15`, en una red propia; en modo puente, una IP de la misma red que el equipo.
