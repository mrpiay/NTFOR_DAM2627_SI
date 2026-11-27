# SI · Mini servidor web en Ubuntu, visto desde Windows

## Qué se hace

En la máquina virtual con Ubuntu se sirve una página web muy sencilla, y se abre desde el navegador de Windows, el equipo **anfitrión**. Para eso, la máquina virtual lleva **dos adaptadores de red**:

- el 1 en **NAT**, para que Ubuntu salga a Internet;
- el 2 en **solo-anfitrión** (*host-only*), para que Windows pueda llegar a Ubuntu. Con NAT solo, no puede.

Sirve la máquina con Ubuntu Server de la semana del 9 al 13. No hay que instalar nada: Python 3 ya viene con Ubuntu.

---

## Paso 1 · Los adaptadores: NAT y solo-anfitrión

1. Apaga la máquina virtual de Ubuntu.
2. En VirtualBox, abre **Configuración → Red** de esa máquina.
3. El **Adaptador 1** se queda como está, en **NAT**: es el que da a Ubuntu salida a Internet.
4. En la pestaña **Adaptador 2**, marca **Habilitar adaptador de red** y, en **Conectado a**, elige **Adaptador solo-anfitrión**. En **Nombre** aparece la red solo-anfitrión de VirtualBox (*VirtualBox Host-Only Ethernet Adapter*). Si el campo está vacío, créala en **Archivo → Herramientas → Administrador de red**, pestaña **Redes solo-anfitrión**, botón **Crear**, y vuelve a elegirla.
5. Acepta y arranca la máquina.

**Por qué hace falta.** Con NAT, la máquina virtual sale a Internet a través de Windows, pero queda «escondida» detrás de él: tiene una IP privada (`10.0.2.15`) a la que Windows no puede llegar. La red solo-anfitrión es una red interna entre Windows y las máquinas virtuales, sin salida a Internet, en la que cada una tiene su propia IP y se ven entre sí.

| Modo | Ubuntu sale a Internet | Windows llega a Ubuntu |
|---|---|---|
| NAT | Sí | No |
| Solo-anfitrión | No | Sí |
| Los dos adaptadores a la vez | Sí (por el 1) | Sí (por el 2) |

---

## Paso 2 · La dirección IP de Ubuntu

En Ubuntu, ejecuta:

```bash
ip -br addr
```

`ip addr` muestra las direcciones de cada interfaz de red; con `-br` (*brief*, breve), una línea por interfaz. La salida se parece a esta:

```
lo               UNKNOWN        127.0.0.1/8 ::1/128
enp0s3           UP             10.0.2.15/24 fe80::a00:27ff:fe4e:66a1/64
enp0s8           UP             192.168.56.101/24 fe80::a00:27ff:fe12:3456/64
```

| Interfaz | Qué es |
|---|---|
| `lo` | La interfaz de bucle (*loopback*): la propia máquina hablando consigo misma |
| `enp0s3` | El adaptador 1, en NAT: `10.0.2.15` |
| `enp0s8` | El adaptador 2, solo-anfitrión: **esta es la IP a la que se conecta Windows** |

La IP es lo que va antes de la barra: `192.168.56.101`. El `/24` es la máscara (los 24 primeros bits son la red) y no se escribe al conectarse. En cada equipo la IP puede acabar en otro número: usa la que salga en el tuyo.

Si `enp0s8` sale en `DOWN` o sin dirección IPv4, es porque Ubuntu Server solo configuró al instalarse el adaptador que había entonces. Se le indica que pida IP también por `enp0s8` con un archivo de **netplan**, la configuración de red de Ubuntu:

```bash
sudo tee /etc/netplan/60-hostonly.yaml <<EOF
network:
  version: 2
  ethernets:
    enp0s8:
      dhcp4: true
EOF
sudo chmod 600 /etc/netplan/60-hostonly.yaml
sudo netplan apply
```

y se vuelve a mirar con `ip -br addr`. El archivo se queda, y la IP vuelve a asignarse en cada arranque.

**Comprueba que** Windows llega a Ubuntu: en una terminal de Windows, `ping 192.168.56.101` (con tu IP) recibe respuesta.

---

## Paso 3 · La página y el servidor

En Ubuntu:

```bash
mkdir ~/web
cd ~/web
echo "<h1>Hola desde $(hostname)</h1><p>Servido desde la máquina virtual Ubuntu</p>" > index.html
python3 -m http.server 8000
```

| Orden | Qué hace |
|---|---|
| `mkdir ~/web` y `cd ~/web` | Crea la carpeta `web` en la carpeta personal y entra en ella |
| `echo "…" > index.html` | Escribe la página en el archivo `index.html`. `$(hostname)` se sustituye por el nombre de la máquina, para que se vea que la página viene de Ubuntu |
| `python3 -m http.server 8000` | Arranca un servidor web que sirve los archivos de la carpeta actual en el puerto 8000. Cuando se pide la carpeta, entrega `index.html` |

El servidor queda en marcha mientras la terminal siga abierta. Se para con **Ctrl+C**.

---

## Paso 4 · Abrirla desde Windows

En el navegador de Windows, abre:

```
http://192.168.56.101:8000
```

(con la IP de tu máquina). Sale la página «Hola desde …» con el nombre de tu Ubuntu.

**Comprueba que** en la terminal de Ubuntu aparece una línea por cada petición, con la IP de Windows en la red solo-anfitrión (`192.168.56.1`) y el código `200` (todo bien):

```
192.168.56.1 - - [27/Nov/2026 10:15:02] "GET / HTTP/1.1" 200 -
```

---

## Por qué el puerto 8000

La **IP** indica a qué máquina se llega; el **puerto**, a qué programa de esa máquina. En la misma Ubuntu podría haber un servidor web en el 80, SSH en el 22 y esta prueba en el 8000, a la vez.

- El 8000 es el que se pone al final de la orden `python3 -m http.server 8000`, y es también el que usa si no se pone ninguno.
- El puerto estándar de HTTP es el **80**: por eso el navegador no lo muestra, y `http://192.168.56.101` es lo mismo que `http://192.168.56.101:80`.
- En Linux, los puertos por debajo de 1024 están reservados: solo `root` puede abrir un servidor en ellos. Con un usuario normal, `python3 -m http.server 80` falla con `Permission denied`; con `sudo python3 -m http.server 80` funciona, y basta con abrir `http://192.168.56.101`.
- Para pruebas y desarrollo se usan puertos altos, como el 8000 o el 8080, que no necesitan permisos especiales.

---

## Si no carga

| Qué pasa | Qué mirar |
|---|---|
| `ping` no responde | Que el adaptador 2 esté en **solo-anfitrión** y que la IP sea la de `enp0s8`, no la `10.0.2.15` |
| `ping` responde, pero la página no carga | Que el servidor siga en marcha en Ubuntu y que la dirección lleve `:8000` al final |
| Sigue sin cargar | El cortafuegos de Ubuntu: `sudo ufw status`. Si sale `active`, abre el puerto con `sudo ufw allow 8000` |
