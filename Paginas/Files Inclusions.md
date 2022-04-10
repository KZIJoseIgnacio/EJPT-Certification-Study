# Files Inclusions

### Path Traversal
También conocida como  cruce de directorios , una vulnerabilidad de seguridad web permite a un atacante leer los recursos del sistema operativo, como los archivos locales en el servidor que ejecuta una aplicación. El atacante aprovecha esta vulnerabilidad manipulando y abusando de la URL de la aplicación web para ubicar y acceder a archivos o directorios almacenados fuera del directorio raíz de la aplicación.

Las vulnerabilidades de cruce de ruta  ocurren cuando la entrada del usuario se pasa a una función como file_get_contents en PHP. Es importante tener en cuenta que la función no es el principal contribuyente a la vulnerabilidad. A menudo, la causa de la vulnerabilidad es una validación o filtrado de entrada deficiente. En PHP, puede usar file_get_contents para leer el contenido de un archivo. 

### Path Traversal Routes
![image](https://user-images.githubusercontent.com/69023634/162599066-473844eb-16f3-425b-b80f-1acd7ea4e542.png)


**/etc/issue**: Contiene un mensaje o identificación del sistema que se imprimirá antes de la solicitud de inicio de sesión.

**/etc/profile**: Controla las variables predeterminadas de todo el sistema, como las variables de exportación, la máscara de creación de archivos (umask), los tipos de terminales, los mensajes de correo para indicar cuándo ha llegado correo nuevo.

**/proc/version**: Especifica la versión del kernel de Linux.

**/etc/passwd**: Tiene todos los usuarios registrados que tienen acceso a un sistema.

**/etc/shadow**: contiene información sobre las contraseñas de los usuarios del sistema.

**/root/.bash_history**: Contiene los comandos de historial para el usuario root.

**/var/log/dmessage**: Contiene mensajes del sistema global, incluidos los mensajes que se registran durante el inicio del sistema.

**/var/mail/root**: Todos los correos electrónicos para el usuario root.

**/root/.ssh/id_rsa**: Claves SSH privadas para un root o cualquier usuario válido conocido en el servidor.

**/var/log/apache2/access.log**: Las solicitudes accedidas para el servidor web Apache.

**C:\boot.ini**: Contiene las opciones de arranque para computadoras con firmware BIOS.

![image](https://user-images.githubusercontent.com/69023634/162599055-9265c7dc-65f2-4eda-9079-f8e9e576dc0b.png)

