# Semana 1 · Cap 5 — Understanding bash shell

## Conceptos clave
- Uso de .bashrc y .bash_profile para añadir alias y variables de forma permanente
- Uso de tuberías (pipes)
- Terminado vimtutor (repasar)

## Comandos nuevos
- man file-hierarchy -> muestra la jerarquía de ficheros de Linux y su explicación de cada directorio (muy útil)

## Lo que me ha costado
- Diferenciar entre .bashrc y .bash_profile (repasar esta parte video 5.8)

# Semana 1 · Cap 6 — Exploring filesystem hierarchy

## Conceptos clave
- /usr contiene /bin y /sbin, bin almacena los ficheros ejecutables por usuarios normales mientras que en sbin se almacenan los ejecutables que requieren privilegios de administrador
- /var almacena ficheros creados dinámicamente, como por ejemplo ficheros de registro: /var/log
- /etc es para ficheros de configuración, son escritos en texto plano y legibles 
- /boot contiene el kernel y el resto de requerimientos para arrancar el sistema
- /dev aquí encontramos los ficheros de interfaz de dispositivo, tales como el disco duro primario, en este caso nvme0n1:

## Comandos nuevos
- which -> busca binarios en $PATH
- locate -> usa una base de datos, construida por updatedb (el paquete no estaba instalado)
- find -> `find / -type f -size +100M` busca ficheros en la raiz (/) con tamaño superior a 100MBytes
- `mkdir -p find/contents; sudo find /etc -exec grep -l loren {} \; -exec cp {} find/contents/ \; 2>/dev/null` primero creará la carpeta find/contents, seguido buscará en el directorio /etc por la palabra "loren" y copiará el resultado a find/contents obviando los errores mediante 2>/dev/null. En este caso escapamos el segundo -exec con la contrabarra (\) para que cierre esa ejecución, y así poder utilizar otro exec en el mismo comando
- `sudo sh -c "find /etc/ -name '*' -type f | xargs grep 127.0.0.1"` en este caso xargs toma la salida estándar del comando find y nos permite ejecutar otro comando sobre esa salida, en este caso grep para filtrar que incluya ese texto en los ficheros a buscar
- ln -> enlaces duros o "hard links". 
- ls -> enlaces simbólicos.

### Examples
- ``[root@rhel-control loren]# cp /etc/hosts ./hosts
[root@rhel-control loren]# ln hosts hard
[root@rhel-control loren]# ls -il hosts hard
25804877 -rw-r--r--. 2 root root 384 Jul 12 16:55 hard
25804877 -rw-r--r--. 2 root root 384 Jul 12 16:55 hosts
[root@rhel-control loren]# echo hello >> hard
[root@rhel-control loren]# ls -il hosts hard
25804877 -rw-r--r--. 2 root root 390 Jul 12 16:55 hard
25804877 -rw-r--r--. 2 root root 390 Jul 12 16:55 hosts``

En este caso copiamos el fichero hosts, creamos el "hard link" hacia hard, y al hacer un echo y aumentar su tamaño, comprobamos que ambos ficheros tienen el mismo inode (25804877) y el mismo tamaño de fichero (390). 

## Lo que me ha costado
- Diferencias entre ln y ls: un "hard link" es un segundo nombre que apunta a un mismo inodo. Los inodos apuntan a un bloque del fichero almacenando información vital del fichero, a excepción del nombre y su contenido. Este, conecta el nombre del fichero con los bloques de datos que se ven en el disco duro. Cada fichero o carpeta tendrá un inodo único.
- Los hard links no pueden ser usados sobre directorios, son como accesos directos para ficheros. Apuntan todos al mismo fichero único desde otra ruta, de esta forma puedes tener el mismo fichero en varios sitios, modificando solo el original.

## Conexión con mi homelab
- "esto es lo que pasa cuando hago X en mis LXC"

