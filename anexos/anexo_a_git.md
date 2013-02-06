# Anexo A: Introducción a git
git es un sistema de control de versiones. Se convertirá en nuestro DeLorean personal que nos permitirá viajar por la historia de los proyectos y nos proveerá grandes facilidades para el trabajo en equipo.

Será la herramienta principal con la que administraremos el trabajo, y su incumbencia excede este ámbito: hoy por hoy se ha convertido en el estándar de la industria a nivel global.

## ¿Qué es git?
> git es un sistema de control de versiones distribuído de código abierto, diseñado para la velocidad y eficiencia

### Distribuído
Cada copia de un repositorio git es tan válida como las otras, y puede comportarse como servidor para un equipo de trabajo o simplemente como reservorio del proyecto a modo local.

Esto presenta como ventaja, por ejemplo, la posibilidad de trabajar individualmente desconectado de todo tipo de redes, o en grupo, sin necesidad de tener un servidor centralizado.
*Cualquier nodo aislado es independiente*.

> **Nota:** Otros sistemas de control de versiones necesitan de la presencia de una red y de un servidor centralizado para poder trabajar, ver diferencias en archivos, acceder a la historia del proyecto y generar ramas de desarrollo.

### Código abierto
Si fuera de nuestro interés, podríamos acceder al [repositorio git](http://www.github.com/git/git) donde se encuentra el código de git (sí, git está administrado con git).

El proyecto fue iniciado por [Linus Torvalds](http://www.google.com/search?q=Linus+Torvalds) en 2005 dado su hartazgo por los sistemas de control de versiones de la época, y debido a que su proveedor de preferencia había discontinuado sus servicios.

Hoy en día tiene una legión de programadores alrededor del mundo y cualquiera con una buena experiencia en C y algo de tiempo libre puede mejorar el proyecto.

### Velocidad y eficiencia
Los repositorios de git son inmutables, por lo que (idealmente) nunca se borran datos. Adicionalmente, lo que se resguarda en el repositorio son snapshots de los archivos (y no diferencias a la línea base, como otros sistemas de control de versiones). Y ésto es lo que realmente le brinda mucha velocidad: cada versión guardada de nuestro proyecto es una captura completa (no 100% completa, pero ya veremos) del estado en ese momento.

> **Nota:** la explicación excede los objetivos de estas notas. Sin embargo se pude recurrir a la bibliografía para profundizar en el tema. El libro *Pro git*, de Scott Chacon es excelente.

Para darnos una idea del funcionamiento de git, imaginémonos una [Polaroid](http://polaroidstore.com/products/instant-cameras/14-megapixel-instant-print-digital-camera-z340e-black.htm) tomando fotos de nuestro trabajo, y archivándolas en un álbum bien ordenado cada vez que nosotros ejecutamos un simple comando.

## Manos a la obra: git básico
Para comenzar a trabajar con git necesitamos conocer unos pocos comandos, y una vez adquirida cierta práctica se convertirá en una tarea natural al momento de desarrollar un proyecto.

> **Nota:** se asume que git se encuentra correctamente instalado y configurado, tareas que no son objetivo de este apartado.

### Iniciando un repositorio
La tarea que menos veces haremos es la de crear repositorios, pero es esencial ya que sin ella no hay forma de que git comience a recolectar el estado por el que atravieza el proyecto a cada momento: no sabe que debe empezar a tomar las "fotos".

#### Desde cero
Una de las opciones es comenzar un repositorio vacío. Cuando trabajamos en un proyecto que creamos nosotros, generalmente es la forma de iniciar el repo git.  
Simplemente debemos posicionarnos en el directorio del proyecto y escribir `git init`.

    lucas@falcon:~/notas/demo-git$ pwd
    /home/lucas/notas/demo-git
    lucas@falcon:~/notas/demo-git$ git init
    Initialized empty Git repository in /home/lucas/notas/demo-git/.git/

Cuando hayamos obtenido la confirmación por parte de git de que se ha podido generar el repositorio, estamos listos para comenzar a trabajar.

#### Desde un repositorio ya existente
La otra forma es trayéndonos un repositorio existente, que hayan compartido con nosotros o que hayamos subido a algún servidor desde otra computadora y deseemos descargar en nuestra terminal de trabajo. En regla general, siempre que ya exista el repo, debemos importarlo (la primera vez) para poder trabajar en él.  
Esta vez necesitamos el comando `git clone`, pero deberemos especificarle cuál será la ruta del repositorio desde el cual clonarlo.

    lucas@falcon:~/notas$ git clone git@github.com:tallerweb/notas.git
    Cloning into 'notas'...
    remote: Counting objects: 69, done.
    remote: Compressing objects: 100% (60/60), done.
    remote: Total 69 (delta 21), reused 55 (delta 7)
    Receiving objects: 100% (69/69), 17.29 KiB, done.
    Resolving deltas: 100% (21/21), done.

En el ejemplo anterior, vemos que dentro de nuestro espacio de trabajo escribimos el comando adecuado, indicando la ruta del repo de origen y conseguimos una réplica del mismo en esa ubicación, dentro de un directorio llamado como el repo original.

> **Nota:** no debe crearse el directorio para el repositorio, ya que el comando clone lo hará automáticamente. Se puede especificar otra ruta al final del comando, pero esto es opcional.

### Sondeando el repo
Estamos listos para comenzar a tomar fotos del estado de nuestro proyecto. Sin embargo, para poder hacerlo, necesitamos empezar a trabajar y realizar modificaciones de archivos.  
Podemos dar cuenta de esto si ejecutamos el comando `git status`.

    lucas@falcon:~/notas/demo-git$ git status
    # On branch master
    #
    # Initial commit
    #
    nothing to commit (create/copy files and use "git add" to track)

El mensaje es muy elocuente: "nothing to commit". Dado que no hemos hecho modificaciones en el proyecto no habrá nada a lo que sacar nuevas fotos.

> **Nota:** el comando `git status` será invocado en forma frecuente, ya que nos presenta un reporte del estado actual del directorio de trabajo y de aquello que queremos commitear.

No nos queda más que hacer alguna modificación al repo, para poder comenzar a experimentar con git.

### Sacando fotos
Una vez que comenzamos a trabajar sobre el proyecto, y tenemos un conjunto de cambios que deseamos resguardar, podemos hacer un commit (análogo a "sacar una foto", pero empecemos a tomar el vocabulario). En todo proyecto es buena idea tener un archivo `README.md` que especifique indicaciones generales del mismo, y toda información relevante para futuros usuarios/desarrolladores del mismo. Nosotros ya hemos escrito ese README, por lo que el estado del proyecto será diferente.

    lucas@falcon:~/notas/demo-git$ git status
    # On branch master
    #
    # Initial commit
    #
    # Untracked files:
    #   (use "git add <file>..." to include in what will be committed)
    #
    #	README.md
    nothing added to commit but untracked files present (use "git add" to track)

La clave para comenzar a entender los reportes de estado de git es leer cuidadosamente los mensajes: siempre tienen una ayuda dentro. En este caso, nos avisa que hay archivos no trazados ("untracked"): son aquellos que git aún no conoce, ni ha guardado previamente en ningún commit.

Nuestro primer commit será simple, y utilizaremos la ayuda que nos proveyó el comando `git status`: recurriremos al comando `git add`.

    lucas@falcon:~/notas/demo-git$ git add README.md

Aún no recibiendo respuesta alguna por parte de este comando, podemos intuír que "si nada estalló por los aires, al menos no ha fallado". Veamos el estado de nuestro proyecto ahora mismo:

    lucas@falcon:~/notas/demo-git$ git status
    # On branch master
    #
    # Initial commit
    #
    # Changes to be committed:
    #   (use "git rm --cached <file>..." to unstage)
    #
    #	new file:   README.md
    #

Ahora es diferente: el mismo archivo aparece como "cambios a ser commiteados", es decir, aquello que saldrá en la próxima foto.

> **¡Un momento!** ¿No habíamos sacado ya la foto con el comando `git add`? No. El proceso de tomar fotos lleva dos pasos necesarios. Primero, deben acomodarse las personas que saldrán en la misma y separarse las que no. Luego, puede sacarse la foto.

Muy bien, procedamos a commitear y terminemos con esta primera etapa:

    lucas@falcon:~/notas/demo-git$ git commit -m "Commit inicial"
    [master (root-commit) 4a8a534] Commit inicial
    1 file changed, 3 insertions(+)
    create mode 100644 README.md

Lo que acabamos de ejecutar se compone del comando básico (`git commit`) y un argumento que será el mensaje asociado a ese commit (`-m "Commit inicial"`). Es buena práctica utilizar mensajes descriptivos. En este caso, y al ser el inicio del proyecto, es lo mejor que tenemos.

Repitamos la operación una vez más para obtener algo de práctica con la herramienta. Supongamos que ahora hemos **modificado** el *README.md*, y **agregado** un nuevo archivo llamado *index.html*. Nos encontramos ante uno de los casos más comunes: cada vez que trabajamos en una nueva funcionalidad o mejora, es áltamente probable que agreguemos y modifiquemos. Empecemos con `git status`

    # On branch master
    # Changes not staged for commit:
    #   (use "git add <file>..." to update what will be committed)
    #   (use "git checkout -- <file>..." to discard changes in working directory)
    #
    #	modified:   README.md
    #
    # Untracked files:
    #   (use "git add <file>..." to include in what will be committed)
    #
    #	index.html
    no changes added to commit (use "git add" and/or "git commit -a")

Obtenemos un mensaje más largo que lo habitual, pero muy completo. Básicamente dice que hay cambios en el archivo `README.md`, y que existe uno nuevo que aún no fue registrado en ningún commit anterior llamado `index.html`. Una nueva combinación de `git add` + `git commit` hará su trabajo.

    lucas@falcon:~/notas/demo-git$ git add README.md index.html
    lucas @falcon:~/notas/demo-git$ git commit -m "Se agrega página de inicio"
    [master 40dcdd8] Se agrega página de inicio
    2 files changed, 9 insertions(+)
    create  mode 100644 index.html
    lucas @falcon:~/notas/demo-git$ git status
    # On branch master
    nothing to commit (working directory clean)

Adicionalmente hicimos un `git status` para verificar el estado del proyecto una vez commiteados los archivos.

> **Nota:** No siempre deberemos agregar los archivos de uno en uno. Podemos utilizar el comodín "." para agregar todos los archivos (no recomendado) o el comando `git add -i` para tener un menú interactivo que nos permita elegir qué archivos agregar, actualizar o incluso qué fragmentos de archivo deseamos commitear (áltamente recomendado).

Ya hemos tomado práctica y podemos detenernos a mirar los avances.

### Mirando el álbum
Si deseáramos ver la historia de commits, podríamos recurrir a un comando simple:

    lucas@falcon:~/notas/demo-git$ git log
    commit  40dcdd852ed7904109afe3ee2a5b51781f6b9422
    Author : Lucas Videla <lucas@uno21.com.ar>
    Date :   Fri Feb 1 18:13:21 2013 -0300
     
         Se agrega página de inicio
     
    commit  4a8a534ed145f6f6c187a75af957be9e3479be17
    Author : Lucas Videla <lucas@uno21.com.ar>
    Date :   Thu Jan 31 18:53:20 2013 -0300
     
         Commit inicial

Podemos observar que cada commit tiene una estructura similar: un código alfanumérico (el SHA del commit, su identificador único), quién es el autor, la fecha en que se "tomó esa foto" y el comentario agregado por el autor.

> **Nota:** Ese código alfanumérico extenso tiene un nivel de colisión insignificante. Tal es así que si tomamos sus primeros 7 caracteres podemos prácticamente asegurar a qué commit nos referimos dentro del proyecto.  
> Con ese código indicaremos, en un futuro, un commit en particular.

Una forma alternativa es utilizar el comando `gitk`, que es un inspector gráfico de los commits. Se recomienda su uso cuando se desea ir viendo la evolución del proyecto, y no solamente la información de los commits.

### Volviendo atrás
Muchas veces trabajamos en algo que no rinde sus frutos o que por diversas razones deseamos volver atrás. El comando `git reset` nos ayudará en esta tarea.

Empecemos viendo el estado del proyecto (luego de un cambio que no está especificado en este documento, y utilizando un [comando de log más sintético](http://uberblo.gs/2010/12/git-lol-the-other-git-log)):

    lucas@falcon:~/notas/demo-git$ git lol
    * ac2bb29 (HEAD, master) Un cambio que descartaremos
    * 40dcdd8 Se agrega página de inicio
    * 4a8a534 Commit inicial

En este caso, descartaremos el cambio que así lo indica. Para eso debemos comprender que nuestro repositorio especifica que el último commit realizado es el `ac2bb29` (podemos afirmarlo ya que junto a ese identificador se encuentra la palabra `master`, que no es más que un *puntero al último commit* de esa **rama**).  
Simplemente recurriremos al comando mencionado:

    lucas@falcon:~/notas/demo-git$ git reset --hard 40dcdd8
    HEAD is now at 40dcdd8 Se agrega página de inicio

En este momento HEAD, nuestro *puntero de trabajo actual*, nos dice que nos reposicionó en el commit deseado. Cuando hagamos el próximo commit, éste se ubicará por sobre el indicado, volviendo atrás el cambio descartable que introdujimos al principio del apartado. Por supuesto, de este modo se perderá ese commit para todos fines prácticos.

> **Nota:** la opción `--hard` del comando `git reset` nos indica que quedemos volver atrás el puntero HEAD, descartando los cambios de los archivos definitivamente.  
Si en su lugar hubiésemos empleado la opción `--soft`, descartaría el último commit pero los cambios se encontrarían presentes en el directorio de trabajo por si deseamos modificarlos o emplear una de ellos en el próximo commit.

### Ramas... ramas... ¡ramas!
Una forma más correcta de trabajar en un proyecto de mediana envergadura es mediante ramas de desarrollo. Esto quiere decir que existe un flujo estandarizado para desarrollo, digámosle master por el momento, y cada vez que deseamos agregar una funcionalidad generar una divergencia de ese flujo. Una vez terminado el trabajo, volver a integrarlo al flujo principal.  
Esto presenta muchas ventajas, entre los principales podríamos encontrar:

* La posibilidad de enfocarnos en la rama actual (es decir, en la funcionalidad que estamos desarrollando) sin miedo a ensuciar el flujo principal de desarrollo.
* En caso de necesitar hacer un arreglo sobre el flujo principal, poder cambiar la rama de desarrollo a otra.
* La creación de ramas experimentales, en las cuales se hacen pruebas de concepto totalmente descartables, sabiendo que se puede eliminar la rama una vez se descubra que no es frusctífera.

> **Nota:** Existen [teorías completas](http://martinfowler.com/bliki/FeatureBranch.html) sobre cómo desarrollar con ramas, equipos de trabajo y flujos distribuídos. Por supuesto, exceden los objetivos de este apartado. Sin embargo no debemos descartar que en cada organización se escoja un modo similar pero ligeramente diferente.

Para trabajar con branches, debemos *crearlos*, *commitear en ellos*, *integrarlos* una vez terminado el trabajo y *eliminarlos* cuando el código ha sido asegurado (o desea descartarse).

Hagamos una prueba. Creemos el branch "about", donde escribiremos un *acerca-de* en el proyecto. El comando indicado será `git checkout -b about`, que básicamente significa "creemos una rama aquí mismo, llamada *about*".

    lucas@falcon:~/notas/demo-git$ git checkout -b about
    Switched to a new branch 'about'

Como podemos ver, automáticamente nos ha cambiado al nuevo branch. Por lo tanto, **ya estábamos en uno** (master, como veníamos anticipando). Podemos verificarlo mediante el comando `git branch`:

    lucas@falcon:~/notas/demo-git$ git branch
    * about
      master

> **Nota:** Si quisiéramos volver al branch master (a partir de ahora le diremos así, y no "flujo principal", ya que después de todos son simplemente ramas) sólo necesitaríamos hacer un `git checkout master`, pero lo haremos en su momento.

En este punto es que trabajamos dentro del branch. Saltearemos esta parte, pero resumiendo los hechos, creamos un archivo y lo enlazamos al index:

    lucas@falcon:~/notas/demo-git$ git status
    # On branch about
    # Changes not staged for commit:
    #   (use "git add <file>..." to update what will be committed)
    #   (use "git checkout -- <file>..." to discard changes in working directory)
    #
    #	modified:   index.html
    #
    # Untracked files:
    #   (use "git add <file>..." to include in what will be committed)
    #
    #	about.html
    no changes added to commit (use "git add" and/or "git commit -a")

Nos resta agregar los cambios, commitear, y contemplar cómo queda nuestra pequeña rama de desarrollo:

    lucas@falcon:~/notas/demo-git$ git add index.html about.html
    lucas@falcon:~/notas/demo-git$ git commit -m "Agregamos el about me"
    [about 57c5c7b] Agregamos el about me
     2 files changed, 10 insertions(+)
     create mode 100644 about.html
    lucas@falcon:~/notas/demo-git$ git lol
    * 57c5c7b (HEAD, about) Agregamos el about me
    * 2a799a3 (master) Un cambio deseable
    * 40dcdd8 Se agrega página de inicio
    * 4a8a534 Commit inicial

Como podemos ver, el branch **about** se encuentra por encima de master. Esto es lógico desde el punto de vista de que esta rama ha crecido desde la otra. Si en este punto volviéramos a master, y trabajásemos sobre ella, veríamos la primera divergencia. En lugar de hacer esto, crearemos otra tama (desde master) para un cambio que no deseamos que prospere, así ejemplificamos todos los casos.

Por empezar, volvamos a la rama **master**:

    lucas@falcon:~/notas/demo-git$ git checkout master
    Switched to branch 'master'

Ahora, creamos la nueva rama, digamos **discard**:

    lucas@falcon:~/notas/demo-git$ git checkout -b discard
    Switched to a new branch 'discard'

Trabajando sobre esta rama, podemos obtener un nuevo panorama:

    lucas@falcon:~/notas/demo-git$ vim bepo.html
    lucas@falcon:~/notas/demo-git$ git add .
    lucas@falcon:~/notas/demo-git$ git commit -m "Cambio a descartar"
    [discard 4a2de78] Cambio a descartar
     1 file changed, 3 insertions(+)
     create mode 100644 bepo.html
    
    lucas@falcon:~/notas/demo-git$ git lol
    * 4a2de78 (HEAD, discard) Cambio a descartar
    | * 57c5c7b (about) Agregamos el about me
    |/  
    * 2a799a3 (master) Un cambio deseable
    * 40dcdd8 Se agrega página de inicio
    * 4a8a534 Commit inicial

Se puede ver que ambas ramas nacen desde master, pero divergen en su contenido. Aquella que tiene el indicador "HEAD" es en la que estamos posicionados.

Descartemos esa rama.

    lucas@falcon:~/notas/demo-git$ git checkout about
    Switched to branch 'about'
    lucas@falcon:~/notas/demo-git$ git branch -D discard 
    Deleted branch discard (was 4a2de78).
    lucas@falcon:~/notas/demo-git$ git lol
    * 57c5c7b (HEAD, about) Agregamos el about me
    * 2a799a3 (master) Un cambio deseable
    * 40dcdd8 Se agrega página de inicio
    * 4a8a534 Commit inicial

Como podemos apreciar es necesario salir de la rama a eliminar para luego hacerlo con el comando `git branch -D nombre_rama`. Finalmente, vemos el estado del repo (sin la rama *discard*).

Integremos ahora la rama *about*.

    lucas@falcon:~/notas/demo-git$ git checkout master
    Switched to branch 'master'
    lucas@falcon:~/notas/demo-git$ git merge about 
    Updating 2a799a3..57c5c7b
    Fast-forward
     about.html |    9 +++++++++
     index.html |    1 +
     2 files changed, 10 insertions(+)
     create mode 100644 about.html
    lucas@falcon:~/notas/demo-git$ git lol
    * 57c5c7b (HEAD, master, about) Agregamos el about me
    * 2a799a3 Un cambio deseable
    * 40dcdd8 Se agrega página de inicio
    * 4a8a534 Commit inicial

El procedimiento es similar: debemos salir de la rama, mezclarla desde la rama destino, y finalmente observar que nos quedan ambas en el mismo punto.

Aquí debemos tomar una decisión: ¿tiene sentido conservar la rama? Si el trabajo no ha finalizado (puede necesitarse integrar parcialmente antes de terminar) deberemos conservarla y seguir trabajando en esta rama. Si hemos finalizado, en cambio, no tiene sentido conservar una rama que ha cumplido su objetivo. Para ello:

    lucas@falcon:~/notas/demo-git$ git branch -D about
    Deleted branch about (was 57c5c7b).
    lucas@falcon:~/notas/demo-git$ git lol
    * 57c5c7b (HEAD, master) Agregamos el about me
    * 2a799a3 Un cambio deseable
    * 40dcdd8 Se agrega página de inicio
    * 4a8a534 Commit inicial

Conocíamos el comando, sólamente que ahora hemos resguardado el trabajo mediante el branch master.

> **Nota:** Hemos trabajado con ramas, creándolas, haciéndolas crecer, integrándolas y eliminándolas. Si bien no es necesario utilizarlas, presenta incontables ventajas, como trabajar en dos funcionalidades divergentes, elegir cuál prospera y cuál no, mantener ordenado el código y otras ventajas que iremos descubriendo con el tiempo. El estándar laboral es utilizarlas, por lo que es preferible tomar gimnasia con esta técnica de trabajo.

### Mezclando
Si bien ya estuvimos haciendo una mezcla (al integrar ramas), esta vez veremos dos casos interesantes. El primero involucra una mezcla simple, y el siguiente resolviendo un conflicto.

#### Mezcla sin grumos
Imaginemos el siguiente escenario:

    lucas@falcon:~/notas/demo-git$ git status
    # On branch master
    nothing to commit (working directory clean)
    lucas@falcon:~/notas/demo-git$ git lol
    * db37139 (HEAD, master) Algunas palabras en negrita
    | * a417ce8 (fondoAzul) Se agrega fondo azul al index
    |/  
    * 57c5c7b Agregamos el about me
    * 2a799a3 Un cambio deseable
    * 40dcdd8 Se agrega página de inicio
    * 4a8a534 Commit inicial

Como vemos, hay dos ramas divergentes, pero que no colisionan en sus contenidos (lo veremos luego, pero lo afirmamos a priori). Este es el mejor escenario, ya que simplemente deberemos mezclar los contenidos y no nos ocasionará problemas:

    lucas@falcon:~/notas/demo-git$ git merge fondoAzul 
    Auto-merging index.html
    Merge made by the 'recursive' strategy.
     index.html |    2 +-
     1 file changed, 1 insertion(+), 1 deletion(-)

Ahora mismo, podemos eliminar el branch, luego de haberse realizado la mezcla automática del contenido de los archivos. Es el caso más simple, y el más común para los proyectos pequeños / medianos.

    lucas@falcon:~/notas/demo-git$ git lol
    *   23a4564 Merge branch 'fondoAzul'
    |\  
    | * a417ce8 Se agrega fondo azul al index
    * | db37139 Algunas palabras en negrita
    |/  
    * 57c5c7b Agregamos el about me
    * 2a799a3 Un cambio deseable
    * 40dcdd8 Se agrega página de inicio
    * 4a8a534 Commit inicial

#### Mezcla peligrosa
En este caso, tenemos un escenario como el siguiente:

    lucas@falcon:~/notas/demo-git$ git lol
    * 034d45e (HEAD, master) Otro título
    | * 334de17 (titulo) Cambiamos el título
    |/  
    * 57c5c7b Agregamos el about me
    * 2a799a3 Un cambio deseable
    * 40dcdd8 Se agrega página de inicio
    * 4a8a534 Commit inicial

En este caso, los cambios colisionan. El merge automático nos proporciona el siguiente feedback:

    lucas@falcon:~/notas/demo-git$ git merge titulo 
    Auto-merging index.html
    CONFLICT (content): Merge conflict in index.html
    Automatic merge failed; fix conflicts and then commit the result.

Con el repositorio en este estado, no podemos continuar trabajando. Debe ser prioridad resolver el conflicto para luego poder dedicarnos al desarrollo.

Simplemente recurrimos al siguiente comando:

    lucas@falcon:~/notas/demo-git$ git mergetool
    Merging:
    index.html
    
    Normal merge conflict for 'index.html':
      {local}: modified file
      {remote}: modified file
    Hit return to start merge resolution tool (meld): 

Nos auxiliará alguna herramienta de merging (en este caso, meld, pero bien puede ser alguna alternativa). Básicamente todas apuntan a lo mismo: nos presentan el archivo original, el modificado en una de las ramas y el de la otra (tres vistas en total) y nos permiten elegir con qué contenido quedarnos en cada lugar donde se encuentre conflictuado el archivo.

Una vez resuelto el conflicto con la herramienta propuesta, veremos el estado del repo:

    lucas@falcon:~/notas/demo-git$ git status
    # On branch master
    # Changes to be committed:
    #
    #	modified:   index.html
    #
    # Untracked files:
    #   (use "git add <file>..." to include in what will be committed)
    #
    #	index.html.orig

Podemos ver que agregó ciertos archivos, que podemos eliminar con confianza. Adicionalmente, el que fue mezclado aparece como para ser commiteado. Simplemente lo agregamos y commiteamos, con algún comentario como "Se resuelven conflictos" o algún otro significativo.

> **Nota:** Hay otra estrategia para la mezcla, que es el **rebase**. Por ser ligeramente más complicada e involucrar una estrategia que requiere más cuidado, preferimos dejarla a un lado de este apartado.

Una vez terminada la mezcla, el commit, y el borrado del branch que ya no es de utilidad, nos encontramos con el siguiente escenario:

    lucas@falcon:~/notas/demo-git$ git lol
    *   0d1b4a2 (HEAD, master) Se resuelven conflictos
    |\  
    | * 334de17 Cambiamos el título
    * | 034d45e Otro título
    |/ 
    * 57c5c7b Agregamos el about me
    * 2a799a3 Un cambio deseable
    * 40dcdd8 Se agrega página de inicio
    * 4a8a534 Commit inicial

Con esto hemos concluido nuestro trabajo de mezcla, por lo que podemos continuar con el desarrollo.

### Etiquetando
A veces necesitamos identificar un commit en particular mucho tiempo después de haberlo confeccionado. Sería impráctico tener que recordar su código, aquel SHA que lo identifica unívocamente.  
Es por ello que surge el concepto de etiqueta, o tag (utilizando el léxico de git).

Supongamos que el punto actual de desarrollo deseamos identificarlo porque será la primera puesta en producción (o algún suceso de similar importancia). Podríamos decir que es la versión 1.0, y asignarle una etiqueta conforme a ello:

    lucas@falcon:~/notas/demo-git$ git tag "version-1.0"
    lucas@falcon:~/notas/demo-git$ git lol
    *   0d1b4a2 (HEAD, tag: version-1.0, master) Se resuelven conflictos
    |\  
    | * 334de17 (titulo) Cambiamos el título
    * | 034d45e Otro título
    |/   
    * 57c5c7b Agregamos el about me
    * 2a799a3 Un cambio deseable
    * 40dcdd8 Se agrega página de inicio
    * 4a8a534 Commit inicial

Como podemos ver, el último commit ha sido etiquetado con el nombre indicado. Ahora podremos referirnos a ese emblemático commit mediante el nombre de la etiqueta (para hacer nuevos branches, checkouts, rollbacks y otras operaciones que requieran especificar un commit en particular).

Podemos ver los tags de nuestro proyecto con el simple comando:

    lucas@falcon:~/notas/demo-git$ git tag
    version-1.0

> **Nota:** Puede hacerse otro tipo de tags, el cual es equivalente a un commit (por los datos de autoría que lleva aparejados), pero son conceptos que escapan a los intereses de estas notas. Puede profundizarse sobre ellos en la bibliografía, fundamentalmente en el libro **Pro git**, de *Scott Chacon*.

### Trabajando en equipo
Una de las mayores ventajas que nos presenta el trabajo con un sistema de control de versiones es la posibilidad de cooperar en equipo, y obtener esa sinergia que no se consigue individualmente. Consideremos que la alternativa podría ser enviarse los fragmentos trabajados por correo electrónico, y mezclarlos a mano (completamente arcaico).

A modo de ejemplo utilizaremos [Github](http://www.github.com) como servidor de git, el cual será nuestro repositorio centralizado para permitirnos cooperar.

> **Nota:** Escapa a este apartado la configuración de una cuenta de Github, pero es requisito para trabajar con ella.

#### Compartiendo nuestro trabajo
Si quisiéramos subir nuestro trabajo a Github, deberíamos crear un repositorio en la página y obtener la dirección git del mismo. Una vez hecho esto, procederemos a agregarlo como repositorio externo:

lucas@falcon:~/notas/demo-git$ git remote add origin git@github.com:delucas/demo-git.git

Sin respuesta, podemos suponer que no ha habido errores. Estamos en condiciones de subir nuestro trabajo al repositorio remoto que acabamos de configurar:

    lucas@falcon:~/notas/demo-git$ git push -u origin master
    Counting objects: 30, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (29/29), done.
    Writing objects: 100% (30/30), 2.60 KiB, done.
    Total 30 (delta 16), reused 0 (delta 0)
    To git@github.com:delucas/demo-git.git
     * [new branch]      master -> master
    Branch master set up to track remote branch master from origin.

Para interpretar correctamente el comando ejecutado, podríamos leerlo de la siguiente manera: *"git, empujá en el repo marcado como origin el contenido del branch master"*. Se toma por convención que ambos branches se llaman del mismo modo (tanto remoto como local).
Esto creará un nuevo branch en forma remota, llamado *master* y que nos servirá para subir nuestro trabajo y coordinarlo con el equipo.

#### Actualizando el repo
Una vez que estamos trabajando en equipo, y ya sabiendo compartir un proyecto, necesitamos poder bajar los cambios que nuestros compañeros hagan al mismo.

Para ello, y teniendo en cuenta **tener el stash vacío** (por prudencia, aunque con la práctica no es necesario) y **un estado estable del directorio de trabajo** (esto es, commiteando aquello que desamos conservar y descartando aquello que no), haremos lo siguiente:

    lucas@falcon:~/notas/demo-git$ git pull origin master
    From github.com:delucas/demo-git
     * branch            master     -> FETCH_HEAD
    Updating 23a4564..0d1b4a2
    Fast-forward
     index.html |    2 +-
     1 file changed, 1 insertion(+), 1 deletion(-)

En este caso hemos obtenido el contenido del repositorio remoto sin problemas. En caso de presentarse algún conflicto de merge, deberemos resolverlo tal como vimos en el apartado correspondiente (después de todo, estamos mezclando ramas remotas en lugar de locales, pero ramas al fin).  
Esta vez interpretaremos la línea como *"git, tirá del repo marcado como origin el branch master y colocalo en el branch master local"*. Nuevamente la convención reina sobre los nombres de los repos/ramas.

## Resumen de comandos
* `git init`, para inicializar un repositorio nuevo en el directorio actual.
* `git clone ruta_repo`, para copiar un repositorio existente dentro del directorio actual. Creará un directorio nuevo para el repo.
* `git status`, para ver el estado de nuestro directorio de trabajo, y el stash. Nos permite ver qué se está por commitear, o qué falta agregar a stash.
* `git add nombre_de_archivos`, para agregar uno o más archivos al próximo commit. Se dice que luego del add se han pasado a stash.
* `git commit -m un_comentario`, para realizar efectivamente un commit con todo lo guardado en el área de stash. Dejará el stash limpio.
* `git log`, para tener un listado de los commits, ordenados en forma inversa según la fecha de captura.
* `gitk`, para acceder a un inspector gráfico de la evolución del proyecto.
* `git lol`, un alias para el comando `git log` con muchas opciones y argumentos. Es necesario [configurarlo](http://uberblo.gs/2010/12/git-lol-the-other-git-log).
* `git reset --hard id_commit`, para volver atrás descartando los cambios realizados luego del commit especificado, eliminándolos definitivamente.
* `git reset --soft id_commit`, para volver atrás descartando los cambios realizados luego del commit especificado, dejándolos en el directorio de trabajo.
* `git checkout -b nombre_rama`, para crear una nueva rama desde el punto actual.
* `git checkout nombre_rama`, para pasar de la rama actual hacia otra.
* `git branch`, para ver las ramas actuales.
* `git branch -D nombre_rama`, para eliminar una rama. Es necesario estar posicionado en *otra rama*.
* `git merge nombre_rama`, para mezclar el contenido de la rama especificada dentro de la rama actual.
* `git mergetool`, para mezclar en forma asistida el contenido de archivos conflictuados al hacer un `git merge`. Son aquellos archivos sobre los que no se ha podido hacer una mezcla automática.
* `git tag nombre_tag sha_del_commit`, para etiquetar cierto commit con un identificador de elección propia. Sirve para marcar versiones, entregas o hitos remarcables en el proyecto.
* `git tag -l`, para listar todos los tags del proyecto.
* `git remote add origin direccion_repo_remoto`, para agregar un repositorio remoto al proyecto, llamándolo "origin".
* `git push -u origin master`, para subir el repositorio local en el repositorio remoto. No debe haber conflictos entre ambos para que la operación se resuelva correctamente. De haberlos, deberá resolverse en forma local.
* `git pull origin master`, para bajar una copia del repositorio remoto dentro del branch especificado, en este caso 'master', al repositorio local. Puede haber conflictos de merge, que se resolverán del modo indicado anteriormente.

## Bibliografía
* **Chacon, Scott.** *Pro git.* Berkeley, CA: Apress, 2009
* **Chacon, Scott.** [Pro git](http://github.com/progit/progit/tree/master/es). Libro gratuito y en español.

* **Neo.** [Git immersion](http://gitimmersion.com/). Guía para aprender git paso a paso.
* **Fowler, Martin.** [Feature branch](http://martinfowler.com/bliki/FeatureBranch.html). Cómo desarrollar con ramas.
