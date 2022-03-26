# Footprinting & Scanning
Esta es la parte de infraestructura de la recopilación de información.

### Mapping a network
Mapear una red ayuda al pentester a tener una idea de cómo está estructurada la red.

### Ping sweep
El barrido de ping ayuda a encontrar todos los hosts en vivo en un rango de red.
```
fping -a -g 192.168.1.0/24 2>/dev/null
nmap -sn 192.168.1.0/24
```

### OS fingerprinting
La toma de huellas dactilares del sistema operativo es el proceso de determinar el sistema operativo utilizado por un host en una red.
```
# OS Detection, no ping
nmap -Pn -O <target(s)>
```

### Port Scanning
El escaneo de puertos permite el descubrimiento de demonios y servicios en ejecución de cada nodo en la red.
```
# TCP SYN scan or stealth scan
nmap -Ss <target>

# Scripts and version detection
nmap -sC -sV <target>

# All ports, scripts, version
nmap -sC -sV -p- <target>

# UDP and Version check
nmap -sU -sV <target>

# Most used scan
# OS, version, scripts, traceroute, and all ports
nmap -A -p- <target>
```
