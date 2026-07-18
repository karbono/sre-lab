# Semana 2 · Cap 6 — Archiving files

## Conceptos clave
- tar se utiliza para extraer, comprimir y listar ficheros.

## Comandos nuevos
- tar -cvf my_archive.tar /home /etc
    - De esta forma haremos que 'my_archive.tar' contenga '/home' y '/etc' en su interior.
- tar -tvf my_archive.tar
    - Lista el contenido del fichero.
- tar -xvf my_archive 
    - Extrae el contenido en el directorio actual, podemos añadir '-C' para cambiar el directorio final.
- Para comprimir, utilizaremos '-z', '-j' o '-J', para los diferentes tipos: gzip, bzip2 o xz respectivamente.

# Semana 2 · Cap 7 — Exploring common text tools

## Conceptos clave
- cut -> filtra la salida.
    - cut -d : -f 1 /etc/passwd 
        - En este caso el '-d' indica que el delimitador son los dos puntos (:), '-f 1' indica el campo que quieres ver, y después la ruta del fichero a filtrar.
- sort -> ordena la salida
    - cut -d : -f 1 /etc/passwd | sort
    - sort -t : -k3n /etc/passwd
        - '-t :' define el delimitador, '-k3' indica la clave a ordenador: en este caso la columna 3 (UID). Por último, la 'n' indica que sea un ordenamiento numérico, ya que 'sort' por defecto ordena de forma alfabética.
- tr -> convierte carácteres de minúsculas a mayúsculas por ej:
    - echo hello | tr [:lower:] [:upper:]
        - Interesante sobre todo en scripts, para poder convertir texto que necesitemos recoger a minúsculas o mayúsculas independientemente de cómo se ha ya insertado.
- grep -> filtra la salida por lo que le indiquemos, por ej:
    - ps aux | grep ssh
        - lo que hará es devolvernos el resultado: ```[loren@rhel-control ~]$ ps aux | grep ssh
root        5871  0.0  0.3   8788  6360 ?        Ss   Jul04   0:00 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
root       64730  0.5  0.5  15340 10404 ?        Ss   09:29   0:00 sshd-session: loren [priv]
loren      64753  0.0  0.4  15568  7828 ?        S    09:29   0:00 sshd-session: loren@pts/0
loren      64785  0.0  0.1   6396  2112 pts/0    S+   09:29   0:00 grep --color=auto ssh```

## Comandos nuevos

