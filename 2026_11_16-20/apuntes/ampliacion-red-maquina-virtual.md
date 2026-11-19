# UD1 · Ampliación: las tarjetas de red con una máquina virtual

Al comparar la red del equipo real con la de la máquina virtual (paso 4 del proyecto), `ipconfig` y Ubuntu muestran MAC e IP distintas. Es lo esperado: este documento explica qué es cada dato, dónde se mira y qué tiene que coincidir, y después cómo se conecta la máquina, con un dispositivo de red en cada extremo de cada conexión, y los dos modos de red de VirtualBox que interesan, **NAT** y **Host-only**: qué es cada uno, dónde está cada adaptador, qué se puede hacer y para qué se usa. Continúa el [apartado 5 de los apuntes de la UD1](UD1-el-equipo-por-dentro.md#5-tarjetas-de-expansión) (la tarjeta de red y la MAC).

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

```
            ANFITRIÓN (Windows o Linux)                          INVITADO (Ubuntu)

  Internet ── tarjeta real (Wi-Fi) 192.168.1.35
                    ▲
                    │ VirtualBox sale por ella, como cualquier programa
  router virtual de VirtualBox 10.0.2.2       ◄────►  tarjeta 1 (NAT)        10.0.2.15
  adaptador VirtualBox Host-Only 192.168.56.1 ◄────►  tarjeta 2 (Host-only)  192.168.56.101
```

- En **NAT**, el otro extremo también es un dispositivo de red, aunque no sale en `ipconfig`: VirtualBox lo crea dentro del propio programa y hace de router.
- En **Host-only**, el otro extremo sí sale en `ipconfig`: es el adaptador *VirtualBox Host-Only*, que existe desde que se instala VirtualBox.
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
| **Windows → máquina** | **No** (solo con reenvío de puertos, apartado 5) | **Sí** |
| **Máquina → Windows** | Solo como salida a Internet | **Sí** |
| **Entre varias máquinas** | No: cada una tiene su NAT, aislado | Sí, las que estén en esa misma red |
| **Para qué se usa** | Lo habitual: una máquina que solo necesita Internet (instalar paquetes, navegar) | Entrar en la máquina desde Windows (un terminal remoto, una web que se sirve dentro) sin exponerla a la red |

## 5. NAT por dentro: cómo sale la máquina a Internet

La clave: **para Windows, VirtualBox es un programa más que usa Internet, como el navegador.** La máquina no sale directamente: le pide a VirtualBox que salga por ella. Así, paso a paso, cuando la máquina abre `www.google.com`:

1. **La máquina envía su petición a la puerta de enlace.** Ubuntu no sabe llegar a Google, así que hace lo que hace cualquier equipo: envía el paquete a su **puerta de enlace** (el router de su red), `10.0.2.2`:

   ```
   De: 10.0.2.15 (la máquina)   →   Para: 142.250.x.x (Google)
   ```

2. **VirtualBox lo recoge.** `10.0.2.2` es el otro extremo de la conexión: el router virtual que VirtualBox crea dentro del propio programa. No es ningún aparato físico; todo lo que envía la máquina llega a VirtualBox, un programa que se ejecuta en Windows.
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

### Ejemplo de uso: instalar un programa

Es lo que se hizo en el paso 6 del proyecto: `sudo apt install usbutils`. La máquina pide el paquete a los servidores de Ubuntu, en Internet, y VirtualBox hace la petición por ella. No hace falta que nadie entre en la máquina: solo sale.

### Cómo se ve

| Dónde | Qué mirar | Qué sale |
|---|---|---|
| **cmd** (Windows) | `ipconfig` | Solo las tarjetas de Windows: la Wi-Fi o la Ethernet, con `192.168.1.35`. De la máquina, **nada**: con NAT no hay adaptador en Windows |
| | `ping 10.0.2.15` | **No responde**: Windows no conoce esa red, que es solo de la máquina |
| **VirtualBox** | **Settings → Network → Adapter 1** | **Attached to: NAT**. En **Advanced**, la **MAC Address** (`080027…`) y el botón **Port Forwarding** |
| **Ubuntu** | `ip -br addr` | `enp0s3` con `10.0.2.15/24` |
| | `ip route` | `default via 10.0.2.2`: hay puerta de enlace, y por eso hay Internet |
| | `ping -c 3 8.8.8.8` | Responde: la máquina llega a Internet (`8.8.8.8` es un servidor de Google) |

### Entrar a pesar del NAT: el reenvío de puertos

Para que Windows llegue a un servicio de la máquina, se le da a VirtualBox una nota fija: **Adapter 1 → Advanced → Port Forwarding** (*Avanzadas → Reenvío de puertos*), con una regla «lo que llegue al puerto `8080` del equipo real, pásalo al puerto `8000` de la máquina». Con el servidor web del ejemplo del apartado 6 en marcha en la máquina, el navegador de Windows lo abre en `http://127.0.0.1:8080`. Solo se abre ese puerto; lo demás sigue cerrado.

## 6. Host-only por dentro: un cable entre Windows y la máquina

En Host-only no hay intermediario ni traducción: hay **una red pequeña con dos extremos**, como un cable.

```
Windows                                          Máquina virtual (Ubuntu)
VirtualBox Host-Only Ethernet Adapter   ←──→   su tarjeta enp0s3
192.168.56.1 · MAC 0A-00-27-…                   192.168.56.101 · MAC 08:00:27:…
(se ve con ipconfig)                            (se ve con ip -br addr)
```

- **El extremo de Windows** es el adaptador *VirtualBox Host-Only*. Existe siempre, desde que se instala VirtualBox, haya o no una máquina al otro lado.
- **El extremo de la máquina** es su tarjeta, que solo se conecta a esta red si en **Attached to** se elige **Host-only Adapter**. Su IP se la da VirtualBox, que en esta red reparte direcciones desde `192.168.56.101`.

**Por qué no hay Internet:** en `ip route`, la máquina solo conoce la red `192.168.56.0/24`; no hay línea `default`. Sin línea `default` no hay puerta de enlace, y sin puerta de enlace no hay a quién mandar lo que va a Internet.

### Ejemplo de uso: abrir desde Windows una web que está en la máquina

1. En Ubuntu, en el terminal, se pone en marcha un servidor web pequeño, que trae Python, y se deja abierto:

   ```bash
   python3 -m http.server 8000
   ```

   Sirve la lista de archivos de la carpeta en la que está el terminal.
2. En Windows, en el navegador, se abre `http://192.168.56.101:8000`. Sale esa lista de archivos: **Windows ha llegado a la máquina** por el cable de la red solo anfitrión.

Con la máquina en NAT, esa dirección no abre nada: Windows no puede entrar en la máquina.

### Cómo se ve

| Dónde | Qué mirar | Qué sale |
|---|---|---|
| **cmd** (Windows) | `ipconfig` | El adaptador **VirtualBox Host-Only Ethernet Adapter**, con `192.168.56.1`: el extremo de Windows |
| | `ping 192.168.56.101` | **Responde**: Windows llega a la máquina |
| **VirtualBox** | **Settings → Network → Adapter 1** | **Attached to: Host-only Adapter** y, en **Name**, *VirtualBox Host-Only Ethernet Adapter*: el **mismo nombre** que en `ipconfig`, porque es el otro extremo del cable |
| | **File → Tools → Network Manager → Host-only Networks** | La red, con `192.168.56.1/24` (el extremo de Windows) y el reparto de IP (**DHCP Server**) activado |
| **Ubuntu** | `ip -br addr` | `enp0s3` con `192.168.56.101/24`: el extremo de la máquina |
| | `ip route` | Solo `192.168.56.0/24 dev enp0s3`, **sin** `default`: sin puerta de enlace, no hay Internet |
| | `ping -c 3 192.168.56.1` | Llega a Windows, aunque puede que no responda: el cortafuegos de Windows bloquea el `ping` por defecto. No es que falte la conexión |
| | `ping -c 3 8.8.8.8` | `Network is unreachable`: no hay Internet |

## 7. Los dos a la vez: Internet y acceso desde Windows

Cuando la máquina necesita **las dos cosas**, se le ponen **dos tarjetas**:

- **Adapter 1** en **NAT**: para salir a Internet.
- **Adapter 2** en **Host-only Adapter**: para que Windows llegue a ella.

En Ubuntu salen dos tarjetas, cada una en su red:

```
$ ip -br addr
enp0s3   UP   10.0.2.15/24          ← Adapter 1: NAT, para Internet
enp0s8   UP   192.168.56.101/24     ← Adapter 2: Host-only, para hablar con Windows
```

Lo que va a Internet sale por `enp0s3` (la única con puerta de enlace) y lo que va a `192.168.56.x`, por `enp0s8`.

### Ejemplo de uso: las dos cosas en la misma máquina

En la máquina, `sudo apt install usbutils` funciona (sale por NAT) y, con `python3 -m http.server 8000` en marcha, Windows abre `http://192.168.56.101:8000` (entra por Host-only).

### Cómo se ve

| Dónde | Qué mirar | Qué sale |
|---|---|---|
| **cmd** (Windows) | `ipconfig` | La Wi-Fi o la Ethernet y el adaptador **VirtualBox Host-Only**, con `192.168.56.1`. La parte NAT, como siempre, no se ve |
| | `ping 192.168.56.101` | **Responde**: Windows llega a la máquina por la tarjeta Host-only |
| **VirtualBox** | **Settings → Network** | **Adapter 1**: **Attached to: NAT**. **Adapter 2**: **Enable Network Adapter** marcado y **Attached to: Host-only Adapter**. Cada uno con su MAC (`080027…`), distinta. La segunda tarjeta se añade con la máquina apagada |
| **Ubuntu** | `ip -br addr` | Dos tarjetas: `enp0s3` con `10.0.2.15` y `enp0s8` con `192.168.56.101` |
| | `ip route` | `default via 10.0.2.2 dev enp0s3` (Internet, por NAT) y `192.168.56.0/24 dev enp0s8` (la red con Windows) |
| | `ping -c 3 8.8.8.8` | Responde: hay Internet |

## 8. Qué se ve en `ipconfig`

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
- **NAT:** la máquina tiene `10.0.2.15` y sale a Internet porque VirtualBox, un programa de Windows, hace cada petición por ella con la IP del equipo real. Desde fuera no se puede entrar, salvo con reenvío de puertos.
- **Host-only:** un cable entre Windows (`192.168.56.1`, el adaptador *VirtualBox Host-Only* de `ipconfig`) y la máquina (`192.168.56.101`). Se comunican entre ellos, pero no hay Internet.
- **Las dos cosas a la vez:** dos tarjetas, una en NAT y otra en Host-only.
