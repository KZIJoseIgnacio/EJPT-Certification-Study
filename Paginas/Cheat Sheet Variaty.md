# Pentester Cheat Sheet Variaty

### Services Transfer
**SCP**
```
$ scp file user@host:/path/to/file                        # Copiando un archivo al sistema remoto usando el comando scp
$ scp user@host:/path/to/file /local/path/to/file         # copiando un archivo desde el sistema remoto usando el comando scp
$ scp file1 file2 user@host:/path/to/directory            # copiando varios archivos usando el comando scp
$ scp -r /path/to/directory user@host:/path/to/directory  # Copiar un directorio completo con el comando scp
```

