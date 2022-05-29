# Pivoting
Pivotar es el método exclusivo de usar una instancia también conocida como "punto de apoyo" para poder "moverse" de un lugar a otro dentro de la red comprometida. Utiliza el primer punto de apoyo del sistema comprometido para permitirnos comprometer otros dispositivos y servidores que de otro modo serían inaccesibles directamente.

![image](https://user-images.githubusercontent.com/69023634/170847883-8c25c85a-620f-4366-b28d-674b87f58c3f.png)

Ejemplo: digamos que un atacante tiene la dirección IP 192.168.56.101. Luego, el atacante compromete otra computadora con la dirección 192.168.56.202, pero esta computadora también tiene acceso a otro rango de IP de 10.10.10.0/24. Ahora el atacante puede usar la máquina comprometida para "girar" u obtener acceso a la segunda red a la que inicialmente no tenía acceso.

### Metasploit Pivoting
Hemos comprometido una máquina y ahora tenemos un shell meterpreter en ella. Ejecutar el comando ifconfig revela otra dirección IP fuera de 10.10.1.101. Metasploit tiene un script AutoRoute incorporado que podemos usar para atacar la segunda red a través de la primera máquina comprometida.


```
# Antecedentes de la sesión inicial
background

# Agregar la nueva ruta hacia el nuevo rango de red
run autoroute -s 10.10.1.0/24

# Usando el módulo auxiliar de escaneo tcp ahora podemos escanear el nuevo objetivo encontrado
use auxiliary/scanner/portscan/tcp
set PORTS <list of common ports>
set RHOSTS 10.10.1.101
run
```
