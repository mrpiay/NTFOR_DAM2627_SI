# UD1 · Ampliación: las tarjetas de red con una máquina virtual

Al comparar la red del equipo real con la de la máquina virtual (paso 4 del proyecto), `ipconfig` y Ubuntu muestran MAC e IP distintas. Es lo esperado: este documento explica qué es cada dato y dónde se mira, y después los **modos de red** de VirtualBox, cada uno con una explicación breve y una **comprobación** para hacer en la propia máquina. Continúa el [apartado 5 de los apuntes de la UD1](UD1-el-equipo-por-dentro.md#5-tarjetas-de-expansión) (la tarjeta de red y la MAC).

---

## 1. Dos equipos, dos tarjetas

Con la máquina virtual encendida hay **dos ordenadores**, y cada uno tiene su tarjeta de red:

- **El anfitrión** (*host*): el equipo real, con Windows, y su tarjeta de verdad, la Wi-Fi o la Ethernet de la placa.
- **El invitado** (*guest*): la máquina virtual, con Ubuntu, y una tarjeta **inventada por VirtualBox**, que se presenta como una Intel `82540EM`.

De cada tarjeta interesan dos datos:

| Dato | Qué es | ¿Cambia? |
|---|---|---|
| **MAC** | El número que identifica a la tarjeta: 48 bits, escritos como 12 cifras hexadecimales | No: es de la tarjeta, esté donde esté |
| **IP** | La dirección que la red da a esa tarjeta para comunicarse | Sí: depende de la red a la que se conecte |

Como son dos tarjetas distintas, hay **dos MAC distintas** y **dos IP distintas**.

## 2. Dónde se mira cada cosa, con un ejemplo

| Dónde | Qué se ve | De qué tarjeta |
|---|---|---|
| `ipconfig /all`, en el terminal de Windows | La MAC (*Dirección física*) y la IP de cada adaptador | De las tarjetas **del equipo real** |
| VirtualBox: **Settings → Network → Adapter 1 → Advanced → MAC Address** (*Configuración → Red → Adaptador 1 → Avanzadas → Dirección MAC*) | La MAC que VirtualBox **ha dado** a la tarjeta de la máquina | De la tarjeta **de la máquina virtual** |
| `ip -br link` (MAC) e `ip -br addr` (IP), en el terminal de Ubuntu | La MAC y la IP que Ubuntu **ve** en su tarjeta | De la tarjeta **de la máquina virtual** |

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

- **VirtualBox y `ip -br link` coinciden**: miran la misma tarjeta. `080027A1B2C3` y `08:00:27:a1:b2:c3` son el mismo número, escrito de otra forma (Windows lo escribiría con guiones: `08-00-27-A1-B2-C3`).
- **`ipconfig` y la máquina virtual no coinciden**: son tarjetas distintas.
- Los **tres primeros bytes** de una MAC identifican al **fabricante**: `08:00:27` es VirtualBox; `A4-5E-60`, el de la tarjeta real.
- `lo` (*loopback*) no es una tarjeta: es la conexión del equipo consigo mismo, siempre con `127.0.0.1`. Se ignora.

## 3. Los modos de red: qué hay en el otro extremo

Para que dos dispositivos se comuniquen hace falta una conexión entre ellos, como un cable, y una conexión tiene **un dispositivo de red en cada extremo**. La tarjeta del invitado es siempre uno de los dos. Lo que se elige en VirtualBox, en **Settings → Network → Adapter 1 → Attached to** (*Configuración → Red → Adaptador 1 → Conectado a*), es el **modo de red**: **qué dispositivo hay en el otro extremo**. De eso depende la IP que recibe la máquina y con quién se puede comunicar. Una máquina puede tener hasta cuatro tarjetas (Adapter 1 a 4); la del curso tiene una.

El modo solo se puede cambiar con la máquina **apagada** (`sudo poweroff`). Para comprobar cada modo se usan estos comandos:

| Comando | Dónde | Qué muestra o hace |
|---|---|---|
| `ip -br addr` | Ubuntu | La IP de cada tarjeta |
| `ip route` | Ubuntu | La **tabla de rutas**: a qué red pertenece la tarjeta (`10.0.2.0/24 …`) y por dónde salen los paquetes que van a otras redes. La línea `default via …` es la **puerta de enlace** |
| `ping -c 4 <IP>` | Ubuntu | Envía 4 paquetes a esa IP y espera respuesta. Si llegan (`64 bytes from …`), hay comunicación; si no, `100% packet loss` |
| `ipconfig` y `ping <IP>` | Windows (CMD o PowerShell) | Las IP de las tarjetas de Windows, y lo mismo que `ping` en Ubuntu |

Las IP de los ejemplos son las de este documento: la de Windows cambia de un equipo a otro, pero las de VirtualBox (`10.0.2.x` y `192.168.56.x`) salen casi siempre iguales.

## 4. NAT

Es el modo de la máquina del curso, como se vio al instalarla («[La red de la máquina: NAT](../../2026_11_09-13/apuntes/UD2-sistemas-operativos.md#la-red-de-la-máquina-nat)», en los apuntes de la UD2).

- **El otro extremo** es un **router virtual que crea VirtualBox**, con la IP `10.0.2.2`. Le da a la máquina la IP `10.0.2.15` y la saca a Internet por la tarjeta real de Windows, como a cualquier otro programa.
- Ese router **está dentro del programa VirtualBox**: Windows no lo ve ni tiene ninguna tarjeta en esa red. Por eso **la máquina tiene Internet, pero desde Windows no se llega a ella**.
- Cada máquina en NAT tiene su propio router, aislado: dos máquinas en NAT no se ven entre sí.
- **Para qué se usa:** lo habitual, una máquina que solo necesita Internet (instalar paquetes, navegar).

### Comprobación

1. Con la máquina apagada, en **Adapter 1**: **Enable Network Adapter** (*Habilitar adaptador de red*) marcado y **Attached to: NAT**. Arranca la máquina.
2. **En Windows**, `ipconfig`: la IP y la puerta de enlace de la tarjeta real, por ejemplo:

   ```
   Adaptador de LAN inalámbrica Wi-Fi:
      Dirección IPv4. . . . . . . . . . . . . . : 192.168.1.35
      Máscara de subred . . . . . . . . . . . . : 255.255.255.0
      Puerta de enlace predeterminada . . . . . : 192.168.1.1
   ```

3. **En Ubuntu:**

   ```
   $ ip -br addr
   lo       UNKNOWN  127.0.0.1/8 ::1/128
   enp0s3   UP       10.0.2.15/24 …
   $ ip route
   default via 10.0.2.2 dev enp0s3 proto dhcp …
   10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15 …
   ```

4. **Desde Ubuntu:** `ping -c 4 10.0.2.2` responde (es el router de VirtualBox), y `ping -c 4 8.8.8.8` también (es un servidor de Internet, el DNS de Google).
5. **Desde Windows:** `ping 10.0.2.15` **no responde**.

**Comprueba que lo entiendes.** Contesta antes de abrir las respuestas:

1. ¿Cuál es la IP de Windows, y cuál la de Ubuntu?
2. ¿Cuál es la puerta de enlace de Ubuntu, y qué es en realidad?
3. ¿Qué quiere decir `10.0.2.0/24` en la salida de `ip route`?
4. ¿Por qué Ubuntu llega a `8.8.8.8`, y Windows no llega a Ubuntu?

<details>
<summary>Respuestas</summary>

1. Windows, la de su tarjeta real: `192.168.1.35` en el ejemplo. Ubuntu, `10.0.2.15`. Son de redes distintas.
2. `10.0.2.2`, la de la línea `default via`. Es el router virtual de VirtualBox, que está dentro del programa: por él sale todo lo que Ubuntu envía fuera de su red.
3. Es **la red** a la que pertenece la tarjeta de Ubuntu: todas las IP que empiezan por `10.0.2.` (`/24` quiere decir que los tres primeros números son los de la red). No es la IP de ningún equipo.
4. Ubuntu envía todo lo que no es de su red a su puerta de enlace, el router de VirtualBox, que lo saca a Internet por la tarjeta real de Windows. Windows, en cambio, no tiene ninguna tarjeta en la red `10.0.2.0/24`: el router NAT no es una tarjeta de Windows, sino una parte del programa VirtualBox.

</details>

## 5. Host-only (adaptador solo anfitrión)

- **El otro extremo** es el **adaptador *VirtualBox Host-Only*** de Windows, con la IP `192.168.56.1`: una tarjeta de red virtual que el instalador de VirtualBox añade a Windows. La máquina recibe una IP de esa red, por ejemplo `192.168.56.101`.
- **Windows y la máquina se comunican**, porque cada uno tiene su tarjeta en la misma red. Pero **no hay Internet**: la conexión acaba en Windows, y la máquina no tiene puerta de enlace.
- Las máquinas que estén en Host-only se ven entre sí.
- **Para qué se usa:** entrar en la máquina desde Windows (un terminal remoto, una web que se sirve dentro) sin exponerla al resto de la red.

**El adaptador Host-Only en `ipconfig`.** Sale **siempre** en `ipconfig`, desde que se instala VirtualBox, esté la máquina en el modo que esté:

```
Adaptador de Ethernet VirtualBox Host-Only Network:
   Dirección física. . . . : 0A-00-27-00-00-0B
   Dirección IPv4. . . . . : 192.168.56.1
```

Por el nombre parece la tarjeta de la máquina virtual, pero **no lo es**: es la punta de Windows del cable de la red solo anfitrión. Con la máquina en Host-only, al otro extremo está la máquina; con la máquina en NAT, **no hay nadie al otro extremo** y ese adaptador no interviene.

### Comprobación

1. Apaga la máquina. En **Adapter 1**, **Attached to: Host-only Adapter** (*Adaptador solo anfitrión*), con **Name** (*Nombre*) **VirtualBox Host-Only Ethernet Adapter**. Arranca la máquina.
2. **En Windows**, `ipconfig`: la tarjeta real sigue con su IP, y el adaptador Host-Only tiene `192.168.56.1`, sin puerta de enlace.
3. **En Ubuntu:**

   ```
   $ ip -br addr
   enp0s3   UP       192.168.56.101/24 …
   $ ip route
   192.168.56.0/24 dev enp0s3 proto kernel scope link src 192.168.56.101 …
   ```

   La IP ha cambiado, y **ya no hay línea `default via`**.
4. **Desde Windows:** `ping 192.168.56.101` **responde**.
5. **Desde Ubuntu:** `ping -c 4 8.8.8.8` da `Network is unreachable` (la red no se puede alcanzar): sin puerta de enlace, Ubuntu no sabe por dónde enviar lo que no es de su red.
6. **Desde Ubuntu:** `ping -c 4 192.168.56.1` lo normal es que **no responda**, aunque la conexión exista. El **cortafuegos de Windows** no contesta a los `ping` que le llegan, y suele tratar el adaptador Host-Only como una red pública. No es un fallo: la prueba fiable es la del paso 4.

**Comprueba que lo entiendes.** Contesta antes de abrir las respuestas:

1. ¿Cuál es la IP del adaptador Host-Only de Windows, y cuál la de Ubuntu?
2. ¿Cuál es la red, y por qué las dos IP están en ella?
3. ¿Por qué Ubuntu no tiene Internet en Host-only?
4. Si `ping 192.168.56.1` desde Ubuntu no responde, ¿quiere decir que Ubuntu y Windows no están conectados?

<details>
<summary>Respuestas</summary>

1. Windows, `192.168.56.1`, en su adaptador *VirtualBox Host-Only*. Ubuntu, `192.168.56.101`. La tarjeta real de Windows sigue con su IP de siempre.
2. `192.168.56.0/24`: todas las IP que empiezan por `192.168.56.`. Las dos tarjetas son los dos extremos de la misma conexión, la red solo anfitrión, y por eso están en la misma red y se comunican directamente.
3. Porque la conexión acaba en el adaptador Host-Only de Windows, y no hay puerta de enlace: `ip route` no tiene línea `default via`. Para Ubuntu, fuera de `192.168.56.0/24` no hay nada.
4. No. El `ping` de Windows a Ubuntu responde, así que la conexión funciona. Lo que pasa es que el cortafuegos de Windows no contesta a los `ping`.

</details>

## 6. NAT y Host-only a la vez

Con **dos tarjetas** en la máquina, una en NAT y otra en Host-only, se tienen las dos cosas: Internet por la primera y comunicación con Windows por la segunda. Cada tarjeta tiene su otro extremo, y cada uno está en una parte distinta del anfitrión:

```
   WINDOWS (el sistema)               VIRTUALBOX (el programa)          INVITADO (Ubuntu)

 tarjeta real (Wi-Fi) 192.168.1.35 ◄── sale por ella, como
   └── Internet                        cualquier programa
                                      router NAT 10.0.2.2  ◄─────────►  tarjeta 1 (NAT)        10.0.2.15

 adaptador Host-Only 192.168.56.1 ◄──────────────────────────────────►  tarjeta 2 (Host-only)  192.168.56.101
   (sale en ipconfig)                 (VirtualBox solo instaló
                                       este adaptador)
```

### Comprobación

1. Apaga la máquina. **Adapter 1**: **NAT**. **Adapter 2**: marca **Enable Network Adapter** y **Attached to: Host-only Adapter**. Arranca la máquina.
2. **En Ubuntu**, `ip -br addr`: ahora hay **dos tarjetas**, `enp0s3` con `10.0.2.15` y `enp0s8` con `192.168.56.101`. Si `enp0s8` sale sin IP, es que Ubuntu Server solo configura al instalarlo las tarjetas que tenía entonces; para esta comprobación basta con pedírsela una vez: `sudo dhcpcd enp0s8`.
3. **Desde Ubuntu**, `ping -c 4 8.8.8.8` responde: sale por la tarjeta NAT, la única con `default via` en `ip route`.
4. **Desde Windows**, `ping 192.168.56.101` responde: llega por la tarjeta Host-only.

## 7. Adaptador puente (*Bridged Adapter*)

- La tarjeta del invitado se conecta **directamente a la red real** del anfitrión, a través de su tarjeta Wi-Fi o Ethernet. Es como enchufar la máquina con un cable al mismo router que el equipo real.
- **El otro extremo** es el **router de la red real**, el del aula o el de casa. Es él quien le da la IP, de la misma red que Windows: si Windows tiene `192.168.1.35`, la máquina recibe, por ejemplo, `192.168.1.50`.
- Para la red, la máquina es **un equipo más**, con su propia MAC y su propia IP: tiene Internet, Windows llega a ella y **también cualquier otro equipo de esa red**.
- En `ipconfig` no aparece ningún adaptador nuevo: VirtualBox usa la tarjeta real.
- **Para qué se usa:** una máquina que hace de servidor (una web, una base de datos) y a la que tienen que llegar otros equipos.
- **Cuidado:** la máquina queda **expuesta a toda la red**, igual que un equipo real. Además, en algunas redes no funciona: con Wi-Fi a veces falla, y en redes con control de acceso, como las de muchos centros, el router puede no darle IP a un equipo que no conoce.

### Comprobación

1. Apaga la máquina (si tiene dos tarjetas, desmarca **Enable Network Adapter** en **Adapter 2**). En **Adapter 1**, **Attached to: Bridged Adapter** (*Adaptador puente*) y, en **Name**, la tarjeta real con la que Windows sale a Internet (la Wi-Fi o la Ethernet). Arranca la máquina.
2. **En Ubuntu**, `ip -br addr` e `ip route`: la IP es de **la misma red que Windows** (`192.168.1.x` en el ejemplo), y la puerta de enlace, `default via 192.168.1.1`, es **la misma que la de Windows** en `ipconfig`: el router real.
3. **Desde Ubuntu**, `ping -c 4 8.8.8.8` responde. **Desde Windows**, `ping` a la IP de Ubuntu responde.

Si `ip -br addr` no muestra ninguna IP en `enp0s3`, el router de esa red no se la ha dado: es una red con control de acceso, de las que no admiten el modo puente.

## 8. Red interna (*Internal Network*)

Una red **solo entre máquinas virtuales**: se conectan entre sí las que tienen en **Name** el mismo nombre de red, por ejemplo `intnet`. No hay Internet, y Windows no está en ella. Tampoco hay quien reparta IP: se ponen a mano en cada máquina. Sirve para practicar redes con varias máquinas sin tocar la red real, así que comprobarla necesita al menos dos máquinas virtuales.

---

## 9. Los modos, de un vistazo

| | Otro extremo | IP de la máquina | Internet | Windows → máquina | Entre máquinas | Otros equipos de la red → máquina |
|---|---|---|---|---|---|---|
| **NAT** | Router de VirtualBox, `10.0.2.2` | `10.0.2.15` | Sí | No | No | No |
| **Host-only** | Adaptador Host-Only de Windows, `192.168.56.1` | `192.168.56.101` | No | Sí | Sí | No |
| **Adaptador puente** | Router de la red real | De la red real, como la de Windows | Sí | Sí | Sí | **Sí** |
| **Red interna** | Las otras máquinas con el mismo nombre de red | La que se ponga a mano | No | No | Sí | No |

**Completa la tabla** con lo que ha salido en tu equipo en las comprobaciones de NAT y Host-only, sin mirar atrás. Después, compárala con la solución:

| Dato | NAT | Host-only |
|---|---|---|
| IP de Windows (tarjeta real) | | |
| IP del adaptador Host-Only de Windows | | |
| IP de Ubuntu | | |
| Puerta de enlace de Ubuntu | | |
| Red de Ubuntu | | |
| ¿Windows llega a Ubuntu? | | |
| ¿Ubuntu tiene Internet? | | |

<details>
<summary>Solución, con las IP del ejemplo</summary>

| Dato | NAT | Host-only |
|---|---|---|
| IP de Windows (tarjeta real) | `192.168.1.35` | `192.168.1.35`: no cambia |
| IP del adaptador Host-Only de Windows | `192.168.56.1`, pero no interviene: no hay nadie al otro extremo | `192.168.56.1` |
| IP de Ubuntu | `10.0.2.15` | `192.168.56.101` |
| Puerta de enlace de Ubuntu | `10.0.2.2`, el router de VirtualBox | Ninguna |
| Red de Ubuntu | `10.0.2.0/24` | `192.168.56.0/24` |
| ¿Windows llega a Ubuntu? | No | Sí |
| ¿Ubuntu tiene Internet? | Sí | No |

</details>

**Para terminar, explica con tus palabras** por qué Ubuntu tiene una IP en NAT y otra distinta en Host-only, si su tarjeta es la misma. (Pista: ¿quién está en el otro extremo en cada modo, y quién le da la IP?)

**Al acabar, vuelve a dejar la máquina como estaba:** apágala, **Adapter 1** en **NAT** y, si se activó, **Adapter 2** desmarcado. Arráncala y comprueba con `ping -c 4 8.8.8.8` que tiene Internet: la necesita para instalar paquetes durante el curso.

---

## En resumen

- `ipconfig` muestra la red **del equipo real**. La red **de la máquina** se mira en **VirtualBox** y con **`ip -br link` / `ip -br addr` en Ubuntu**, y esos dos sí coinciden.
- Cada conexión tiene **un dispositivo de red en cada extremo**. Uno es la tarjeta del invitado; el **modo de red** decide cuál es el otro, y con él la IP de la máquina y con quién se comunica.
- **NAT:** el otro extremo es el router de VirtualBox, que está dentro del programa y Windows no ve. La máquina sale a Internet, pero desde Windows no se llega a ella.
- **Host-only:** el otro extremo es el adaptador *VirtualBox Host-Only*, que es de Windows y sale en `ipconfig`. Se comunican entre ellos, pero no hay Internet.
- **Las dos cosas a la vez:** dos tarjetas, una en NAT y otra en Host-only.
- **Adaptador puente:** el otro extremo es el router de la red real. La máquina es un equipo más de esa red, con Internet, y le llega todo el mundo.
- **Red interna:** una red solo entre máquinas virtuales, sin Internet ni anfitrión.
- Para comprobar un modo: `ip -br addr` e `ip route` en Ubuntu, `ipconfig` en Windows, y `ping` en los dos sentidos.
