# UD1 · Ampliación: las tarjetas de red con una máquina virtual

Al comparar la red del equipo real con la de la máquina virtual (paso 4 del proyecto), `ipconfig` y Ubuntu muestran MAC e IP distintas. Es lo esperado: este documento explica qué es cada dato, dónde se mira y qué tiene que coincidir, y después los modos de red de VirtualBox: qué significa cada uno, dónde está cada adaptador, qué se puede hacer con él y para qué se usa. Continúa el [apartado 5 de los apuntes de la UD1](UD1-el-equipo-por-dentro.md#5-tarjetas-de-expansión) (la tarjeta de red y la MAC).

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

## 4. Los modos de red de VirtualBox

Cada máquina puede tener hasta **cuatro tarjetas de red** (**Adapter 1** a **Adapter 4** en **Settings → Network**, *Configuración → Red*). Para cada una se elige a qué está conectada en **Attached to** (*Conectado a*): es como decidir **a qué enchufe va el cable** de esa tarjeta. La máquina del curso tiene una sola, en **NAT**, como se vio al instalarla («[La red de la máquina: NAT](../../2026_11_09-13/apuntes/UD2-sistemas-operativos.md#la-red-de-la-máquina-nat)», en los apuntes de la UD2).

En todos los modos, **la tarjeta de la máquina es la misma**: la inventada por VirtualBox, con MAC `08:00:27:…`, que en Ubuntu se ve con `ip -br addr`. Lo que cambia es **a qué red está conectada** y, con ello, qué IP recibe y con quién puede hablar.

### Not attached (*No conectado*)

- **Qué es:** la tarjeta existe, pero **sin cable**.
- **Dónde está cada extremo:** en la máquina, la tarjeta, sin conexión; en Windows, nada.
- **IP de la máquina:** ninguna.
- **Qué se puede hacer:** nada por red.
- **Para qué se usa:** para dejar una máquina sin red a propósito, o para probar qué hace un sistema cuando pierde la conexión.

### NAT

- **Qué es:** VirtualBox monta una **red privada pequeña solo para esa máquina** y sale a Internet por ella con la IP del equipo real (cómo, en el apartado 6). Es el modo por defecto.
- **Dónde está cada extremo:** en la máquina, su tarjeta; en Windows, **ningún adaptador nuevo**: VirtualBox usa la conexión de Windows como cualquier programa.
- **IP de la máquina:** siempre `10.0.2.15`. La puerta de enlace es `10.0.2.2` y el DNS, `10.0.2.3`: los dos son VirtualBox.
- **Qué se puede hacer:** salir a Internet. Desde fuera **no se puede entrar**: ni el equipo real, ni otras máquinas, ni otros equipos del aula (salvo con reenvío de puertos, en el apartado 6). Cada máquina tiene su propio NAT, aislado: dos máquinas en NAT no se ven entre sí.
- **Para qué se usa:** para lo habitual, una máquina que solo necesita Internet (instalar paquetes, navegar).

### NAT Network (*Red NAT*)

- **Qué es:** como NAT, pero la red privada es **compartida por varias máquinas**. Se crea antes en **File → Tools → Network Manager → NAT Networks** (*Archivo → Herramientas → Administrador de red → Redes NAT*) y luego se elige en cada máquina.
- **Dónde está cada extremo:** en cada máquina, su tarjeta; en Windows, **ningún adaptador nuevo**.
- **IP de la máquina:** una de la red de esa Red NAT (por defecto, `10.0.2.x`), distinta en cada máquina. La puerta de enlace es `10.0.2.1`.
- **Qué se puede hacer:** salir a Internet y **hablar entre las máquinas** de esa red. El equipo real y el resto del aula no pueden entrar (salvo con reenvío de puertos).
- **Para qué se usa:** para montar una red de varias máquinas con Internet, por ejemplo un servidor y un cliente que se conectan entre sí.

### Bridged Adapter (*Adaptador puente*)

- **Qué es:** la máquina se conecta **directamente a la red real** (la del aula o la de casa) a través de la tarjeta del equipo, como **otro ordenador enchufado al mismo router**. En **Name** (*Nombre*) se elige qué tarjeta real usar: la Wi-Fi o la Ethernet.
- **Dónde está cada extremo:** en la máquina, su tarjeta; en Windows, **ningún adaptador nuevo**: se usa la tarjeta real. VirtualBox solo le añade un componente, *VirtualBox NDIS6 Bridged Networking Driver*, que se ve en las propiedades de esa tarjeta (`ncpa.cpl` → la tarjeta → **Propiedades**).
- **IP de la máquina:** la que le da **el router de la red real**, de la misma red que el equipo (por ejemplo `192.168.1.40` si el equipo tiene `192.168.1.35`). Su MAC sigue siendo `08:00:27:…`: para el router es un equipo distinto.
- **Qué se puede hacer:** todo, como un equipo más: salir a Internet, y que **el equipo real, otras máquinas y otros equipos del aula** lleguen a ella.
- **Para qué se usa:** para que la máquina sea un servidor visible en la red (una web, una carpeta compartida) o para probar algo que necesita estar en la red real. En algunas redes (las de centros con control de equipos, algunas Wi-Fi) la máquina puede no recibir IP.

### Internal Network (*Red interna*)

- **Qué es:** una red **solo entre máquinas virtuales**: se conectan las que tienen el mismo nombre de red (por defecto, `intnet`). Ni el equipo real ni Internet están en ella.
- **Dónde está cada extremo:** en cada máquina, su tarjeta; en Windows, **nada**.
- **IP de la máquina:** ninguna automática, porque nadie las reparte (no hay servidor DHCP): se ponen a mano, por ejemplo `192.168.100.1` y `192.168.100.2`.
- **Qué se puede hacer:** que las máquinas hablen **solo entre ellas**.
- **Para qué se usa:** para practicar redes de forma aislada: montar un servidor DHCP propio, un cortafuegos entre dos redes, o probar algo que no debe salir de ahí.

### Host-only Adapter (*Adaptador solo anfitrión*)

- **Qué es:** una red privada **entre el equipo real y sus máquinas**, sin Internet: como un cable que une el ordenador con las máquinas y con nada más. Se gestiona en **File → Tools → Network Manager → Host-only Networks**.
- **Dónde está cada extremo:** en la máquina, su tarjeta; en Windows, **sí hay un adaptador**: el **VirtualBox Host-Only Ethernet Adapter** que aparece en `ipconfig` (apartado 7). Son **las dos puntas del mismo cable**.
- **IP de la máquina:** una de la red `192.168.56.x`, que reparte VirtualBox, por ejemplo `192.168.56.101`. El extremo de Windows es `192.168.56.1`.
- **Qué se puede hacer:** que **el equipo real llegue a la máquina** y la máquina al equipo, y que las máquinas de esa red se hablen. **No hay Internet**, ni llegan otros equipos del aula.
- **Para qué se usa:** para entrar en la máquina desde Windows (un terminal remoto, una web que se sirve dentro) sin exponerla a la red. Si además necesita Internet, se le pone una **segunda tarjeta** en NAT (**Adapter 2**): una sale a Internet y la otra habla con el equipo.

Hay otros dos modos, **Generic Driver** y **Cloud Network**, para usos avanzados que no aparecen en este módulo.

## 5. Todos los modos de un vistazo

| Modo | Adaptador en `ipconfig` (Windows) | IP de la máquina | Internet | Equipo real → máquina | Entre máquinas | Otros equipos del aula → máquina |
|---|---|---|---|---|---|---|
| **Not attached** | No | Ninguna | No | No | No | No |
| **NAT** | No | `10.0.2.15` | Sí | No (solo con reenvío de puertos) | No | No |
| **NAT Network** | No | `10.0.2.x`, una por máquina | Sí | No (solo con reenvío de puertos) | Sí | No |
| **Bridged** | No (usa la tarjeta real) | De la red real, `192.168.1.x` | Sí | Sí | Sí | Sí |
| **Internal Network** | No | A mano | No | No | Sí | No |
| **Host-only** | Sí: *VirtualBox Host-Only*, `192.168.56.1` | `192.168.56.x` | No | Sí | Sí | No |

## 6. Cómo sale la máquina a Internet con NAT

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

### Entrar en una máquina en NAT: el reenvío de puertos

Para que el equipo real llegue a un servicio de una máquina en NAT, se le da a VirtualBox una nota fija: **Adapter 1 → Advanced → Port Forwarding** (*Avanzadas → Reenvío de puertos*). Por ejemplo: «lo que llegue al puerto `2222` del equipo real, pásalo al puerto `22` de la máquina». Si la máquina tiene un servidor SSH, `ssh -p 2222 usuario@127.0.0.1` en el terminal de Windows entra en ella. Solo se abre ese puerto; lo demás sigue cerrado.

## 7. Qué se ve en `ipconfig`

`ipconfig /all` solo muestra **las tarjetas de Windows**. La de la máquina virtual no aparece nunca, en ningún modo. Lo que puede aparecer:

| Adaptador | Qué es | IP | MAC |
|---|---|---|---|
| **Wi-Fi** o **Ethernet** | La tarjeta real del equipo | La que da el router del aula, por ejemplo `192.168.1.35` | La de la tarjeta, con el código de su fabricante |
| **VirtualBox Host-Only Ethernet Adapter** | El extremo de Windows de la red solo anfitrión | `192.168.56.1` | Empieza por `0A-00-27` |

```
Adaptador de Ethernet VirtualBox Host-Only Network:
   Dirección física. . . . : 0A-00-27-00-00-0B
   Dirección IPv4. . . . . : 192.168.56.1
```

Por el nombre parece la tarjeta de la máquina virtual, pero **no lo es**: es una tarjeta que VirtualBox **añade a Windows** al instalarse. Aparece siempre, haya o no máquinas encendidas y estén en el modo que estén. Solo tiene una máquina al otro lado si esa máquina usa el modo **Host-only**; con NAT, como la del curso, **no interviene**, y su IP y su MAC no tienen que coincidir con nada de lo que se ve dentro de la máquina.

---

## En resumen

- `ipconfig` muestra la red **del equipo real**. La red **de la máquina** se mira en **VirtualBox** y con **`ip -br link` / `ip -br addr` en Ubuntu**, y esos dos sí coinciden.
- El modo de red decide **a qué está conectada** la tarjeta de la máquina: a Internet a través de VirtualBox (**NAT**), a una red de máquinas con Internet (**NAT Network**), a la red real (**Bridged**), solo a otras máquinas (**Internal Network**) o solo al equipo real y sus máquinas (**Host-only**).
- Con NAT, la máquina tiene siempre `10.0.2.15` y sale a Internet porque VirtualBox, un programa de Windows, hace cada petición por ella con la IP del equipo real; desde fuera no se puede entrar, salvo con reenvío de puertos.
- El adaptador **VirtualBox Host-Only** de `ipconfig` es el extremo de Windows de la red solo anfitrión, no la tarjeta de la máquina.
