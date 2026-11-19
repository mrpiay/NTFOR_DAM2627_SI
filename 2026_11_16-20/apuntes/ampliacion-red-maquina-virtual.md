# UD1 · Ampliación: las tarjetas de red con una máquina virtual

Al comparar la red del equipo real con la de la máquina virtual (paso 4 del proyecto), `ipconfig` y Ubuntu muestran MAC e IP distintas. Es lo esperado: este documento explica qué es cada dato, dónde se mira y qué tiene que coincidir, y después cómo se conecta la máquina, con un dispositivo de red en cada extremo de cada conexión, en los dos modos de red de VirtualBox que interesan, **NAT** y **Host-only**. Continúa el [apartado 5 de los apuntes de la UD1](UD1-el-equipo-por-dentro.md#5-tarjetas-de-expansión) (la tarjeta de red y la MAC).

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

## 4. Cómo se conecta la máquina: dos extremos en cada conexión

Para que dos dispositivos se comuniquen hace falta una conexión entre ellos, como un cable, y una conexión tiene **un dispositivo de red en cada extremo**.

Con una máquina virtual hay dos equipos:

- **El anfitrión** (*host*): el equipo real, con Windows o con Linux. Tiene su tarjeta real, la Wi-Fi o la Ethernet, para salir a Internet. En los ejemplos de este documento, el anfitrión es Windows.
- **El invitado** (*guest*): la máquina virtual. Tiene **una o más tarjetas virtuales**, hasta cuatro (**Adapter 1** a **Adapter 4** en **Settings → Network**, *Configuración → Red*). La máquina del curso tiene una.

Cada tarjeta del invitado es **el extremo del invitado** de una conexión. Lo que se elige en **Attached to** (*Conectado a*) es **qué dispositivo hay en el otro extremo**, y eso depende de lo que se quiera hacer:

| Se quiere… | Modo | Extremo del invitado | Otro extremo | Por eso… |
|---|---|---|---|---|
| Salir a Internet desde el invitado | **NAT** | Su tarjeta, con `10.0.2.15` | El **router virtual de VirtualBox**, con `10.0.2.2`, que sale a Internet por la tarjeta real del anfitrión | Hay Internet, pero desde el anfitrión no se llega al invitado |
| Entrar en el invitado desde el anfitrión | **Host-only** (*Adaptador solo anfitrión*) | Su tarjeta, con `192.168.56.101` | El adaptador ***VirtualBox Host-Only*** del anfitrión, con `192.168.56.1` | El anfitrión y el invitado se comunican, pero no hay Internet: la conexión acaba en el anfitrión |
| Las dos cosas | **NAT** y **Host-only** | Dos tarjetas | Una conecta con el router de VirtualBox y la otra, con el adaptador Host-Only | Hay las dos cosas |

En el anfitrión hay dos partes: **Windows**, el sistema, y **VirtualBox**, un programa que se ejecuta en él. Cada uno de los dos «otros extremos» está en una de ellas:

```
   WINDOWS (el sistema)               VIRTUALBOX (el programa)          INVITADO (Ubuntu)

 tarjeta real (Wi-Fi) 192.168.1.35 ◄── sale por ella, como
   └── Internet                        cualquier programa
                                      router NAT 10.0.2.2  ◄─────────►  tarjeta 1 (NAT)        10.0.2.15

 adaptador Host-Only 192.168.56.1 ◄──────────────────────────────────►  tarjeta 2 (Host-only)  192.168.56.101
   (sale en ipconfig)                 (VirtualBox solo instaló
                                       este adaptador)
```

| | Router de VirtualBox (NAT) | Adaptador *VirtualBox Host-Only* |
|---|---|---|
| **De quién es** | **Del programa VirtualBox.** Lo crea dentro de sí mismo, uno por cada máquina en NAT | **De Windows.** Es una tarjeta de red virtual que el instalador de VirtualBox añade a Windows con su controlador |
| **¿Lo ve Windows?** | **No.** Para Windows no existe: solo ve un programa, VirtualBox, que usa Internet | **Sí.** Para Windows es una tarjeta más, con su IP `192.168.56.1` |
| **Dónde se ve** | En ninguna parte de Windows: solo lo conoce el invitado, como su puerta de enlace | En `ipconfig` y en el Administrador de dispositivos de Windows |
| **¿Existe con la máquina apagada?** | No: existe mientras la máquina está encendida en NAT | Sí: desde que se instala VirtualBox |

Por eso, en Host-only, Windows llega a la máquina por su propia tarjeta, el adaptador Host-Only. En NAT no puede: Windows no tiene ninguna tarjeta en esa red, porque el router NAT está dentro de un programa.

- La tarjeta del invitado es siempre la inventada por VirtualBox (MAC `08:00:27:…`). Al cambiar el modo, cambia lo que hay en el otro extremo y, con ello, la IP que recibe y con quién se puede comunicar.

### NAT y Host-only, comparados

La máquina del curso usa **NAT**, como se vio al instalarla («[La red de la máquina: NAT](../../2026_11_09-13/apuntes/UD2-sistemas-operativos.md#la-red-de-la-máquina-nat)», en los apuntes de la UD2). VirtualBox tiene otros modos (puente, red interna…) que no se usan en este módulo.

| | **NAT** | **Host-only** (*Adaptador solo anfitrión*) |
|---|---|---|
| **Qué es** | Una red privada pequeña **solo para esa máquina**, por la que VirtualBox la saca a Internet | Una red privada **entre el anfitrión y sus máquinas**, sin Internet |
| **Otro extremo** | El router virtual de VirtualBox (`10.0.2.2`). No sale en `ipconfig` | El adaptador *VirtualBox Host-Only* del anfitrión (`192.168.56.1`). Sale en `ipconfig` |
| **Extremo del invitado** | Su tarjeta, con `10.0.2.15` | Su tarjeta, con una IP de `192.168.56.x`, por ejemplo `192.168.56.101` |
| **Puerta de enlace** | `10.0.2.2` (es VirtualBox) | Ninguna |
| **Internet** | **Sí** | **No** |
| **Windows → máquina** | **No** | **Sí** |
| **Máquina → Windows** | Solo como salida a Internet | **Sí** |
| **Entre varias máquinas** | No: cada una tiene su NAT, aislado | Sí, las que estén en esa misma red |
| **Para qué se usa** | Lo habitual: una máquina que solo necesita Internet (instalar paquetes, navegar) | Entrar en la máquina desde Windows (un terminal remoto, una web que se sirve dentro) sin exponerla a la red |

## 5. Qué se ve en `ipconfig`

`ipconfig /all` solo muestra **las tarjetas de Windows**. La de la máquina virtual no aparece nunca. Lo que puede aparecer:

| Adaptador | Qué es | IP | MAC |
|---|---|---|---|
| **Wi-Fi** o **Ethernet** | La tarjeta real del equipo | La que da el router del aula, por ejemplo `192.168.1.35` | La de la tarjeta, con el código de su fabricante |
| **VirtualBox Host-Only Ethernet Adapter** | El extremo de Windows de la red solo anfitrión | `192.168.56.1` | Empieza por `0A-00-27` |

```
Adaptador de Ethernet VirtualBox Host-Only Network:
   Dirección física. . . . : 0A-00-27-00-00-0B
   Dirección IPv4. . . . . : 192.168.56.1
```

Por el nombre parece la tarjeta de la máquina virtual, pero **no lo es**: es la punta de Windows del cable de la red solo anfitrión. Sale siempre en `ipconfig`, esté la máquina en el modo que esté. Con la máquina en **Host-only**, al otro extremo está la máquina (`192.168.56.101`); con la máquina en **NAT**, como la del curso, **no hay nadie al otro extremo** y ese adaptador no interviene.

---

## En resumen

- Cada conexión tiene **un dispositivo de red en cada extremo**. Uno es la tarjeta del invitado; el modo de red decide cuál es el otro.
- `ipconfig` muestra la red **del equipo real**. La red **de la máquina** se mira en **VirtualBox** y con **`ip -br link` / `ip -br addr` en Ubuntu**, y esos dos sí coinciden.
- **NAT:** el otro extremo es el router de VirtualBox, que está dentro del programa y Windows no ve. La máquina sale a Internet, pero desde Windows no se llega a ella.
- **Host-only:** el otro extremo es el adaptador *VirtualBox Host-Only*, que es de Windows y sale en `ipconfig`. Se comunican entre ellos, pero no hay Internet.
- **Las dos cosas a la vez:** dos tarjetas, una en NAT y otra en Host-only.
