# Linux 
Aprende Comandos basicos de Linux

## Prompt Shell
Comprender el prompt shell es importante es una guia visual para ubicarte dentro del **working tree diretory**

>user@hostName:~$

Cada sesion de shell esta anclada a la poscicion exacta en el **working tree diretory** y a su vez al home directory del usuario y cada comando que se ejecute sin una direccion especefica se ejecutara sobre la poscicion actual(**current directory).  En el ejemplo anterior se puede identificar varios elementos:

- **user:** usuario conectado.
- **@:** separacion entre usuario y host.
- **hostName:** nombre del systema donde corre la sesion(pc, servidor, etc).
- **:** separacion.
- **~** : home directory para user(/home/user).
- **$** : identificador de acceso para usuario standar(# para super administrador o root).

Esta informacion se encuentra en la variable de entorno $PS1 (prompt string 1) y pede ser modificada.

## Working Directory
En linux todo esta reprensentado directorios, el primer directorio del fileSystem es el root representado por /.

<img width="778" height="397" alt="workingdirectory" src="https://github.com/user-attachments/assets/e6ee9469-3b51-4cb3-a836-587c1ba14782" />


Con el comando `pwd` (print working directory) obtendras la ruta absoluta hacia tu posicion actual.

Ahora bien Linux permite acceder a directorios mediante atajos(**symlinks**) que apuntan a otro directorio de esto nace la 
- Ruta Logica(logic)
- Ruta Fisica(Physic)

Si accedes a un directorio a travez de un atajo desde otro directorio al ejecutar `pwd` que por defecto es `pwd -L` te mostrara la ruta logica, esta ruta es sacada de la variable de entorno $PWD ignorando el atajo. Pero si utilizas el comando `pwd -P` linux resolvera el atajo con el kernel (getcwd()) y te devolvera la ruta fisica. 

>En la imagen anterior imagina que dentro de /home/user2/tienes un directorio/atajo que apunta hacia logs, si entras a los logs desde ese punto al ejecutar `pwd` te mostrara /home/user2 pero si en cambio utilizas `pwd -P` te mostrara /var/log

## Crear Directorios
Crea un directorio con el comando `mkdir` (make directory) mas el nombre del directorio.

>`mkdir documentos`

Puedes crear varios a la vez

>`mkdir documentos otrosDocumentos otros`

Puedes crear varios directorios con el mismo nombre 

>`mkdir documento{1..10}`

esto creara 10 directorios llamados documento enumerados(documento1...)

Puedes crear un directorio con un directorio dentro utilizando el argumento -p

>`mkdir -p documento/otrosDocumentos`

## Moverse de directorio
Ya sabes ubicarte en el working directory y crear nuevos directorios para moverte entre ellos utiliza el comando `cd` (change directory) seguido del directorioa donde desplazarte.

>`cd var`

Si no especificas una direccion linux lo resolvera con el PATH home del user guardado en $HOME lo mismo que ejecutar `cd $HOME` o igual que `cd ~` (~ representa home directory).

## Borrar un directorio
Utiliza `rmdir` (remove directory) mas el nombre del directorio.

Para borrar su contenido 

>`rmdir document/*` (* = todo)

Solo se pueden borrar directorios vacios. 

>`rmdir document`

Si un directorio hijo tiene a su vez un directorio no se ejecutara.

Para forzar el borrado se utiliza el comando `rm -rf`, rm se utiliza para borrar archivos pero en linux todo es a su vez un archivo los argumentos r son de recursive y f de force, recursive borra todo en cadena y force lo hace sin preguntar.

## Lista de directorios 
Puedes enlistar todos los archivos y directorios contenidos en en el directorio actual con el comando

``ls``

esto imprimira una lisa simple en orden alfabetico, pero no todos los archivos seran mostrados, en linux existen archivos y directorios escondidos que comienzan por un . los **dotfiles.**

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

### Crear un Archivo
Para crear un archivo se utiliza el copmando `` touch`` mas el nombre que le quieras dar a tu archivo.

>``touch file``

Puedes crear varios a la vez con diferentes nombres 

>``touch file otroFile miFile``

o con el comando 

>``touch file{1..100}``

### Borrar un archivo
Para borrar un archivo utiliza el comando ``rm`` mas el nombre del archivo o archivos:

>``rm file`` o ``rm otroFile miFile``

### Leer un archivo 
Ya sabes ubicarte y dezplazarte en el working directory, crear, borrar, mirar el contenido de un directorio y crear y borrar archivos, ahora aprenderemos a leer un archivo.

Existen varios comandos utiles en diferentes escenarios, el mas basico es ``cat`` este comando imprime en la consola todo el archivo de una vez

>``cat file``

Sin embargo no es muy optimo si el archivo es muy grande, el comando ``more`` imprime un primer segmento del archivo y puedes avanzar pulsando la tecla enter

>``more file``

el comando `less` te permite usar las flechas de navegacion y ademàs buscar coincidencias de palabras dentro del archivo

>``less file `` luego con /buscas una palabra.

el comando `head` te mostrara por defecto las primeras 10 lineas del archivo, tambien puedes especificar el numero de lineas agregando el argumento `-n`

>``head file`` o ``head -n5 file`` (5 es el numero de lineas)

el comando `tail` hace lo mismo pero con las 10 ultimas lineas por defecto 

>``tail file`` o ``tail -n5 file``

Por ultimo se puede leer y ademas editar un archivo con un editor como vim, nano o emacs, vim ofrece un modo solo lectura con el comando `view`. 











