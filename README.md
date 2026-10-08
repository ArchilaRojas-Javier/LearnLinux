# Linux 
Conseptos basicos de Linux
## Lista de directorios 
Puedes enlistar todos los archivos y directorios contenidos en en el directorio actual con el comando

``ls``

esto imprimira una lisa simple y orden alfabetico, pero no todos los archivos seran mostrados, en linux existen archivos y directorios escondidos que comienzan por un . los **dotfiles.**

Para tener la lista completa utiliza el argumento "a":

``ls -a``

>Entre los archivos encontraras un . y .. estos hacen referencia al mismo directorio y al directorio padre, para evitarlos utiliza ``ls -A``

### Filtrar o ordenar la lista 
Por defecto se muestra una lista en orden alfabetico pero podemos filtrar la lista por:

- *Tiempo*
- *Tamano*

#### Tiempo
Linux tiene tres diferentes **timestamps** para los archivos:
- atime:(**acces-time**) la ultima vez que fue accedido.
- mtime:(**modified-time**) la ultima vez que su contenido fue modificado.
- ctime:(**change-time**) la ultima vez que cambiaron sus metadatos: permisos, locacion, nombre, etc

Para filtrar por tiempo se agrega entonces el argumento "t"

``ls -t``

esto filtrara usando el **mtime** mostrando desde el mas reciente hasta el mas antiguo.

``ls -tu``

filtrara usando el **atime**

``ls -tc``

filtrara por **ctime**

#### Tamano
``ls -s`` o ``ls --size``

muestra los archivos en orden alfabetico y un numero que reprensenta el tamano en bloques no en bytes.

``ls -S``

muestra la lista por tamano logico de mayor a menor.

#### Formatos 
Se pueden aplicar formatos a las listas 

``ls -m`` o ``ls --format=commas``

Imprime la lista simple pero separada por comas(,).

``ls -l`` o ``ls --format=long``

Imprime la lista de archivos con toda su infomacion: permisos, links, dueno, grupo, tamano, fecha, nombre.

>drwxr-xr-x 1 user 197609       0 Aug 22  2024 'FILE'

``ls -n``

Imprime la misma informacion pero cambia el dueno y grupo por su valos numerico

>drwxr-xr-x 1 197609 197609       0 Aug 22  2024 'FILE'

``ls -l --author``

agrega el creador del archivo 

>drwxr-xr-x 1 user 197609 user       0 Aug 22  2024 'FILE'

``ls -d``

Imprime solo directorios.

Para terminar se pueden combinar argumentos:

``ls -ald``
``ls -al``
``ls -ls``
``ls -lS``











