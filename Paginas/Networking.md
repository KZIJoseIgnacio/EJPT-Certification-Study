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
