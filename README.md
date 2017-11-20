# Ejercicio-Packet-Tracer

## **----EJERCICIO A REALIZAR----**

Realizar utilizando Cisco Packet Tracer el siguiente ejercicio:

-   Crear cinco redes:

1.  Crear tres subredes (VLSM), una que soporte 100 host, otra que soporte 30 y
    por último una para 6 host. Sólo esta última podrá salir fuera. Cada una
    tendrá cuatro ordenadores conectados.

2.  8 ordenadores con DHCP.

3.  4 ordenadores con DHCP.

4.  4 ordenadores con IP fija, un punto de acceso con 5 ordenadores con DHCP.

5.  5 ordenadores con IP fija.

-   Todas las redes estarán conectadas mediante routers.

-   Tendremos tres servidores web:

1.  [www.albacete.es](http://www.albacete.es/) : muestra una foto de Albacete.

2.  [www.wagner.de](http://www.wagner.de/) : muestra una foto de Wagner.

3.  [www.dilar.com](http://www.dilar.com/) : muestra una toto de Dílar.

-   Existirá un servidor DNS para resolver los nombres anteriores.

-   Todas las redes deben estar etiquetadas.

-   Subir el fichero a github.com. En github debemos crear un fichero readme.md
    (en formato mark down) donde se explicará todo el ejercicio.
    
    
    
    
    

## **----EXPLICACIÓN DEL EJERCICIO----**

### **PRIMERA RED (COLOR MORADO DE PACKET-TRACER)**

**Crear tres subredes (VLSM), una que soporte 100 host, otra que soporte 30 y
por último una para 6 host. Sólo esta última podrá salir fuera. Cada una tendrá
cuatro ordenadores conectados.**

Para realizar este ejercicio, realizo un cálculo de subnetting sobre la red de
*clase C 192.168.0.0/24* cuyo resultado me dió:

| Nº Hosts | Hosts | Red           | Mascara         | Rango 1 IP    | Rango ult IP  | Broadcast     |
|----------|-------|---------------|-----------------|---------------|---------------|---------------|
| 110      | 126   | 192.168.0.0   | 255.255.255.128 | 192.168.0.1   | 192.168.0.126 | 192.168.0.127 |
| 30       | 30    | 192.168.0.128 | 255.255.255.224 | 192.168.0.129 | 192.168.0.158 | 192.168.0.159 |
| 6        | 6     | 192.168.0.160 | 255.255.255.240 | 192.168.0.161 | 192.168.0.166 | 192.168.0.167 |

Dándome así las 3 subredes necesarias. Conociendo ahora las subredes,
configuramos manualmente las conexiones TCP/IP de cada uno de los 4 ordenadores
que irán en cada subred de tal manera:

| **Subred**       | **Ordenador 1** | **Ordenador 2** | **Ordenador 3** | **Ordenador 4** |
|------------------|-----------------|-----------------|-----------------|-----------------|
| 192.168.0.0/25   | 192.168.0.2     | 192.168.0.3     | 192.168.0.4     | 192.168.0.5     |
| 192.168.0.128/27 | 192.168.0.129   | 192.168.0.130   | 192.168.0.131   | 192.168.0.132   |
| 192.168.0.160/28 | 192.168.0.161   | 192.168.0.162   | 192.168.0.163   | 192.168.0.164   |

Así hemos dividido una red en 3 subredes de manera que no puedan comunicarse
entre ellas. Todos los ordenadores los he conectado al mismo Switch.

La subred 192.168.0.160/28 debe tener acceso al exterior, por lo que he incluido
un router llamado en Packet Tracer Router1 dentro de esta subred con la ip
192.168.0.166/28 para que pueda dar servicio exterior más adelante.

Al tener conexión con un router, les configuro la puerta de enlace a esos 4
ordenadores que deben estar en la misma subred que el router y que tendrán más
adelante salida al exterior añadiendo la ip del router 192.168.0.166 en la
configuración Gateway.

### **SEGUNDA RED (COLOR AZUL DE PACKET-TRACER)**

**8 ordenadores con DHCP.**

Para esta red, voy a poner una de *clase C 192.168.1.0/24*, he instalado un
ordenador servidor con el servicio de DHCP activado en la ip 192.168.1.2
(reservo el 192.168.1.1 para un futuro router) y el rango del DHCP será de
192.168.1.100/24 al 192.168.1.200/24

La configuración del servicio DHCP es la siguiente:

| **Gateway**             | **Servidor DNS** | **DHCP Inicio** | **Máscara**   | **Nº usuarios** |
|-------------------------|------------------|-----------------|---------------|-----------------|
| 192.168.1.1 (reservado) | \-               | 192.168.1.100   | 255.255.255.0 | 100             |

*El servidor de DNS lo dejo en blanco* ya que será más adelante añadido.

De esta manera ya puedo añadir los 8 ordenadores conectándolos al mismo
**SWITCH** que el servidor de DHCP y activando el servicio **DHCP** automático
en cada uno de ellos.

### **TERCERA RED (COLOR VERDE DE PACKET-TRACER)**

**4 ordenadores con DHCP.**

De igual manera que se configuró la red anterior, procedemos a crear una nueva
red, también la haré de clase C 192.168.2.0/24

La configuración del nuevo servidor de **DHCP** es la siguiente:

| **Gateway**             | **Servidor DNS** | **DHCP Inicio** | **Máscara**   | **Nº usuarios** |
|-------------------------|------------------|-----------------|---------------|-----------------|
| 192.168.2.1 (reservado) | \-               | 192.168.2.100   | 255.255.255.0 | 50              |

El servidor de DNS lo dejo igualmente en blanco ya que será más adelante
añadido.

Conecto los 4 ordenadores restantes conectándolos al mismo **SWITCH** que el
servidor y activando el servicio **DHCP** automático en cada uno de los
ordenadores.

### **CUARTA RED (COLOR AMARILLO DE PACKET-TRACER)**

**4 ordenadores con IP fija, un punto de acceso con 5 ordenadores con DHCP.**

Para esta red, he elegido una red de *clase A 10.0.0.0/8* y comenzado con la
instalación del servidor que nos dará servicio **DHCP** en la ip 10.0.0.2/8
reservando como siempre la ip 10.0.0.1/8 para un futuro router. El rango del
DHCP lo he establecido del 10.0.0.50/8 hasta 10.0.2.50/8 (512 ordenadores)

El servicio **DHCP** tiene la siguiente configuración:

| **Gateway**          | **Servidor DNS** | **DHCP Inicio** | **Máscara** | **Nº usuarios** |
|----------------------|------------------|-----------------|-------------|-----------------|
| 10.0.0.1 (reservado) | \-               | 10.0.0.50       | 255.0.0.0   | 512             |

De esta manera ya podemos añadir todos los ordenadores, en total 9, activando en
sólo 5 de ellos el servicio DHCP automático.

Al resto de ordenadores le asignaré la ip manualmente su configuración TCP/IP
siguiendo el siguiente esquema:

|                  | **Ordenador 1** | **Ordenador 2** | **Ordenador 3** | **Ordenador 4** |
|------------------|-----------------|-----------------|-----------------|-----------------|
| **IP**           | 10.0.0.5        | 10.0.0.6        | 10.0.0.7        | 10.0.0.8        |
| **Máscara**      | 255.0.0.0       | 255.0.0.0       | 255.0.0.0       | 255.0.0.0       |
| **Servidor DNS** | \-              | \-              | \-              | \-              |
| **Gateway**      | 10.0.0.1        | 10.0.0.1        | 10.0.0.1        | 10.0.0.1        |

*El servidor DNS igualmente lo dejo en blanco* para más adelante en el futuro
añadirla.

### **QUINTA RED (COLOR ROJO DE PACKET-TRACER)**

**5 ordenadores con IP fija.**

Para esta red he querido seleccionar una de *clase B 172.16.0.0/16* y
manualmente configuramos los 5 ordenadores conectados a su correspondiente
**SWITCH** de la siguiente manera:

|                  | **Ordenador 1**        | **Ordenador 2**        | **Ordenador 3**        | **Ordenador 4**        |
|------------------|------------------------|------------------------|------------------------|------------------------|
| **IP**           | 172.16.0.10            | 172.16.0.11            | 172.16.0.12            | 172.16.0.13            |
| **Máscara**      | 255.255.0.0            | 255.255.0.0            | 255.255.0.0            | 255.255.0.0            |
| **Servidor DNS** | \-                     | \-                     | \-                     | \-                     |
| **Gateway**      | 172.16.0.1 (reservada) | 172.16.0.1 (reservada) | 172.16.0.1 (reservada) | 172.16.0.1 (reservada) |

La ip de **Gateway** la reservo como siempre para un futuro router que iría en
la **10.0.0.1/8**

### **TODAS LAS REDES ESTARÁN CONECTADAS MEDIANTE ROUTERS**

Para realizar este cometido, vamos a añadir nuestros enrutadores que faltan. En
la red número 1 (el de las 3 subredes) ya añadimos un Router llamado Router1, y
ese lo vamos a aprovechar para conectarlo a la red 2 (192.168.1.0/24). La red 4
clase A (10.0.0.0/8) y red 5 clase B (172.16.0.0/16) igualmente las unimos
mediante otro router llamado Router2. Nos falta añadir la red 3 (192.168.2.0/24)
que haremos mediante otro router llamado Router3

Ahora debemos establecer conexiones entre los 3 routers.

Para las configuraciones para nuestros routers aprovechamos las ip’s que dejamos
reservadas siendo:

|         | **Router1**                     | **Router2**              | **Router3**    |
|---------|---------------------------------|--------------------------|----------------|
| **IP:** | 192.168.0.166/28 192.168.1.1/24 | 10.0.0.1/8 172.16.0.1/16 | 192.168.2.1/24 |

Ahora debemos interconectar dichos routers entre sí.

Como ya hemos utilizado los dos puertos **Ethernet RJ45** disponibles en el
Router1 y Router2, apagamos ambos dispositivos y lo ampliamos con una nueva
extensión que podría ser con cable **Ethernet** entrelazado o Serial.

Opto por el de Serial y esos dos nuevos cables los enlazo al Router3 (por lo que
deberé añadir también dos extensiones de cable **Serial** para recibir los
cables **Serial** del Router1 y Router2 respectivamente). La configuración final
por tanto quedaría asi:

|                   | **Router1**                     | **Router2**              | **Router3**                   |
|-------------------|---------------------------------|--------------------------|-------------------------------|
| **IP:**           | 192.168.0.166/28 192.168.1.1/24 | 10.0.0.1/8 172.16.0.1/16 | 192.168.2.1/24                |
| **Cable Serial:** | 192.168.5.1/24                  | 192.168.6.1/24           | 192.168.5.2/24 192.168.6.1/24 |

Por tanto ahora elegimos el método de enrutamiento (versión RIP 2) y realizamos
el enrutamiento siguiente:

|         | **Router1** | **Router2** | **Router3** |
|---------|-------------|-------------|-------------|
| **Red** | 192.168.0.0 |             |             |
| **Red** | 192.168.1.0 |             |             |
| **Red** |             |             | 192.168.2.0 |
| **Red** | 192.168.5.0 |             | 192.168.5.0 |
| **Red** |             | 192.168.6.0 | 192.168.6.0 |
| **Red** |             | 10.0.0.0    |             |
| **Red** |             | 172.16.0.0  |             |

### **TENDREMOS TRES SERVIDORES WEB:**

-   [www.albacete.es](http://www.albacete.es/) : muestra una foto de Albacete.

-   [www.wagner.de](http://www.wagner.de/) : muestra una foto de Wagner.

-   [www.dilar.com](http://www.dilar.com/) : muestra una foto de Dílar.

La inclusión de tres servidores requieren la utilización de una IP’s que esté en
el rango de IP’s de cualquiera de las redes (a excepción de las subredes de
nuestra **RED 1** al cual no facilitamos acceso al Router1)

Por tanto los uniré mediante un nuevo **SWITCH** (también podrían ir
directamente al **SWITCH** ya instalado) a la red diseñada en el ejercicio de la
QUINTA RED.

Ponemos a cada servidor una Ip’s manualmente dentro de esa red 5
(**172.16.0.2/16, 172.16.0.3/16 y 172.16.0.4/16**) y activamos en cada uno de
ellos el servicio de **HTTP** (puerto 80).

Todos los ordenadores de la misma red leerán el contenido inmediatamente,
mientras que el resto de redes tardaran un poco en localizar los servicios si
usamos el navegador web.

### **EXISTIRÁ UN SERVIDOR DNS PARA RESOLVER LOS NOMBRES ANTERIORES.**

Por último nos queda resolver las **DNS** con un nuevo servidor que también lo
conectaré al último **SWITCH** de los servidores web **HTTP**. Instalamos dicho
servidor con una Ip dentro del rango de la red 172.16.0.0 (*que pueda ser
enrutado*) y le ponemos el **172.16.0.254/16** y activamos el servicio de
**DNS**:

En él activamos los siguientes parámetros:

| Nombre                                    | IP         |
|-------------------------------------------|------------|
| [www.albacete.es](http://www.albacete.es) | 172.16.0.2 |
| [www.wagner.de](http://www.wagner.de)     | 172.16.0.3 |
| [www.dilar.com](http://www.dilar.com)     | 172.16.0.4 |

Para que desde cualquier ordenador de toda la red podamos ahora acceder a estos
hosts resolviendo su nombre **DNS**, debemos indicarles la IP del servidor de
**DNS** a los ordenadores con IP fija y a los servidores **DHCP** de cada uno de
ellos para que se las asigne a sus respectivos clientes.

### **TESTEAR TODA LA RED**

Por último ya solo toca enviar **PING’s ó PAQUETES** de una red a otra,
comprobar que de la Subredes sólo puedan tener acceso de salida una de ellas y
comprobar el servicio de **DNS** conjuntamente con la de **HTTP** tecleando en
cada uno de los hosts con acceso las páginas webs alojadas en
[www.albacete.es](http://www.albacete.es), [www.wagner.de](http://www.wagner.de)
y [www.dilar.com](http://www.dilar.com)

**PD. Para acelerar la conectividad de las redes una vez abierto en Packet
Tracer, existe un truco que consiste en darle clicks alternando TIEMPO REAL y
SIMULACIÓN PASO A PASO y las redes entrarán en conexión de forma casi inmediata
sin apenas tiempo de esperas.**
