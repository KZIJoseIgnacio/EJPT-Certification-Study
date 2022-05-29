# Networking

### IPv4 Addressing/Subnetting
| slash notation | net mask        | number of hosts |
|----------------|-----------------|-----------------|
| /0             | 0.0.0.0         | 4294967296      |
| /1             | 128.0.0.0       | 2147483648      |
| /2             | 192.0.0.0       | 1073741824      |
| /3             | 224.0.0.0       | 536870912       |
| /4             | 240.0.0.0       | 268435456       |
| /5             | 248.0.0.0       | 134217728       |
| /6             | 252.0.0.0       | 67108864        |
| /7             | 254.0.0.0       | 33554432        |
| /8             | 255.0.0.0       | 16777216        |
| /9             | 255.128.0.0     | 8388608         |
| /10            | 255.192.0.0     | 4194304         |
| /11            | 255.224.0.0     | 2097152         |
| /12            | 255.240.0.0     | 1048576         |
| /13            | 255.248.0.0     | 524288          |
| /14            | 255.252.0.0     | 262144          |
| /15            | 255.254.0.0     | 131072          |
| /16            | 255.255.0.0     | 65536           |
| /17            | 255.255.128.0   | 32768           |
| /18            | 255.255.192.0   | 16384           |
| /19            | 255.255.224.0   | 8192            |
| /20            | 255.255.240.0   | 4096            |
| /21            | 255.255.248.0   | 2048            |
| /22            | 255.255.252.0   | 1024            |
| /23            | 255.255.254.0   | 512             |
| /24            | 255.255.255.0   | 256             |
| /25            | 255.255.255.128 | 128             |
| /26            | 255.255.255.192 | 64              |
| /27            | 255.255.255.224 | 32              |
| /28            | 255.255.255.240 | 16              |
| /29            | 255.255.255.248 | 8               |
| /30            | 255.255.255.252 | 4               |
| /31            | 255.255.255.254 | 2               |
| /32            | 255.255.255.255 | 1               |

### Common ports & Protocols
| Port | Protocol | Hint                   |
|------|----------|------------------------|
| 21   | FTP      |                        |
| 22   | SSH      |                        |
| 23   | TELNET   |                        |
| 25   | SMTP     |                        |
| 53   | DNS      |                        |
| 80   | HTTP     |                        |
| 110  | POP3     |                        |
| 115  | SFTP     |                        |
| 137  | NETBIOS  | find work groups       |
| 138  | NETBIOS  | list shares & machines |
| 139  | NETBIOS  | transit data           |
| 143  | IMAP     |                        |
| 443  | HTTPS    |                        |
| 445  | Samba    | find user and files    | 
| 1433 | MS SQL   |                        |
| 3389 | RDP      |                        |
| 3306 | MYSQL    |                        |

### Routing
Para ver cómo se ve su tabla de enrutamiento actual, use los siguientes comandos:
- ip route <b>en Linux</b>
- route print <b>en Windows</b>
- netstat -r <b>en OSX</b>

**Añadiendo una nueva ruta**
```
ip route add <network_ip>/<cidr> via <gateway_ip>
```

### MAC Address
Para descubrir la dirección MAC de las tarjetas de red instaladas, puede utilizar:
- ipconfig /all <b>en Windows</b>
- ip addr <b>en Linux</b>
- ifconfig <b>en OSX</b>

### ARP Cache
Puede verificar el caché ARP de sus hosts escribiendo:
- arp -a <b>on Windows</b>
- ip neighbour <b>on Linux</b>
- arp <b>on OSX</b>

### Netstat Command
Para verificar los puertos de escucha y las conexiones (TCP) actuales en un host, puede usar:
- netstat -ano <b>on Windows</b>
- netstat -tunp <b>on Linux</b>
- netstat -p tcp -p udp <b>together with</b></br>
  lsof -n -i4TCP -i4UDP <b>on MacOS</b>

### Wireshark

Wireshark es un sniffer de red y analizador de protocolos.
Estos son algunos filtros de captura básicos:

| syntax                   | Description                                                                                  |
|--------------------------|----------------------------------------------------------------------------------------------|
| ip                       | Solo paquetes que utilizan IP como protocolo de capa 3.                                      |
| not ip                   | Lo contrario de la sintaxis anterior.                                                        |
| tcp port 80              | Paquetes donde el puerto TCP de origen o destino es 80.                                      |
| net 192.168.54.0/24      | Paquetes desde y hacia la red especificada.                                                  |
| src port 1234            | El puerto de origen debe ser 1234; el protocolo de transporte no importa.                    |
| src net 192.168.1.0/24   | La dirección IP de origen debe estar en la red especificada.                                 |
| host 192.168.45.65       | Todos los paquetes desde o hacia el host especificado.                                       |
| host www.example.com     | Todos los paquetes desde o hacia el nombre de host especificado.                             |
