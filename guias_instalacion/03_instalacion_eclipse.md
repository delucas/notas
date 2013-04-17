# Instalación Eclipse

Para poder administrar nuestros proyectos de una forma automatizada y obtener todas las ventajas de utilizar un IDE, necesitaremos instalar uno.

El que usaremos será Eclipse, aunque hay muchas alternativas (las cuales representan una porción menor del mercado). La compatibilidad e instalación de las mismas queda bajo exclusiva responsabilidad del lector.

> **Nota:** La guía se presenta para usuarios **Windows**, ya que es la plataforma donde más dificultades hemos encontrado. Con el tiempo incorporaremos los otros sistemas operativos.

El proceso de instalación consta de tres etapas: descarga, instalación del IDE y configuración del JDK dentro de Eclipse.

## Paso 1: Descarga del software
Deberemos remitirnos a <http://eclipse.org/downloads/>, donde se nos presentarán las diferentes versiones de Eclipse que podremos instalar.

> Utilizaremos la versión **Eclipse IDE for Java EE Developers**, ya que tiene todas las herramientas que necesitamos para desarrollar proyectos de mediana y gran escala.

Una vez ingresemos al vínculo anteriormente proporcionado, nos encontraremos con una página similar a la siguiente.

![Sitio de descarga de eclipse.org](/instalacion_eclipse_img/step_01.png)

> Trabajaremos con el Eclipse Juno (que al momento de escribir esta guía es la última versión). Por supuesto, deberemos elegir el de la arquitectura que nuestra computadora soporte.

Una vez seleccionado, se nos presentará una pantalla en que nos pide seleccionar un mirror desde el cual iniciar la descarga. Simplemente seleccionamos el más cercano a nuestra ubicación.

Guardamos el archivo en una ruta de nuestra preferencia, y comenzará el proceso de descarga.

![Proceso de descarga](/instalacion_eclipse_img/step_02.png)

Esperaremos pacientemente, hasta que termine de descargarse. Podemos ir a prepararnos un capuchino.

## Paso 2: Instalación del IDE
Eclipse no se instala, sino que se descomprime. Por lo tanto lo extraemos en nuestra ubicación de preferencia.

> Recomendamos instalarlo en una ruta sin espacios, fácilmente accesible. Por ejemplo `c:\eclipse`

Esperamos el tiempo necesario y terminará la descompresión.

## Paso 3: Configuración del JDK
Una vez hemos descomprimido Eclipse, podremos utilizarlo. Sin embargo preferimos asegurarnos de que ciertas variables estén definidas.

> Al abrir Eclipse, nos presenta un cuadro de diálogo preguntándonos qué *workspace* deseamos tener. El workspace será el directorio donde se encontrarán nuestros proyectos. Recomendamos, por supuesto, tenerlo al alcance de la mano, y saber exactamente su ubicación. Un buen ejemplo podría ser `c:\java\workspace`

![Selección del workspace](/instalacion_eclipse_img/step_03.png)

La pantalla de bienvenida es muy simpática, pero podemos cerrarla sin dudas ya que no nos aportará mayor información.

![Pantalla de bienvenida](/instalacion_eclipse_img/step_04.png)

Una vez abierto Eclipse, debemos acceder al menú *Window*, *Preferences* y en la caja de texto de la parte superior izquierda, escribir `jre`. Nos abrirá varias opciones en el árbol inferior, de las cuales debemos seleccionar *Installed JREs*. Simplemente habrá que chequear que esté configurada la de la instalación que hemos hecho anteriormente, y marcada como predeterminada:

![Installed JREs](/instalacion_eclipse_img/step_05.png)

> En caso de no tener configurada esa variable, deberemos agregar una nueva y marcarla como predeterminada. La ruta de la misma debe ser la de la instalación que hemos efectuado.

Y eso es todo. Eclipse está listo para recibir nuestro primer proyecto.
