# Instalación Java Standard Edition - Java Development Kit

Para poder trabajar con el lenguaje de programación Java será necesario instalarlo en nuestro sistema.

> **Nota:** La guía se presenta para usuarios **Windows**, ya que es la plataforma donde más dificultades hemos encontrado. Con el tiempo incorporaremos los otros sistemas operativos.

El proceso de instalación consta de tres etapas: descarga, instalación y configuración del sistema.

## Paso 1: Descarga del software
Deberemos remitirnos a <http://www.oracle.com/technetwork/java/javase/downloads/index.html>, donde se nos presentarán las diferentes versiones de la JDK y JRE que podremos instalar.

> Utilizaremos el **JDK**, es decir, el *Java Development Kit*. El **JRE**, *Java Runtime Environment*, es una versión reducida que sirve para ejecutar programas Java, pero no es adecuado para desarrollo.

Una vez ingresemos al vínculo anteriormente proporcionado, nos encontraremos con una página similar a la siguiente.

![Sitio de descarga de Oracle](/instalacion_jdk_img/step_01.png)

Haciendo el correspondiente scroll, llegaremos a la sección donde se encuentra la versión recomendada a descargarse.

> Trabajaremos con el *JDK Standard Edition 1.6*, es decir, la versión del JDK 6. Elegiremos la revisión más actual al momento de descargarlo (en este caso la 43).

![Descarga del instalador](/instalacion_jdk_img/step_02.png)

Una vez seleccionado, se nos presentará una pantalla en que nos pide aceptar los términos y condiciones. En cuanto lo hagamos, habilitará los links de descarga:

![Selección de la versión adecuada](/instalacion_jdk_img/step_03.png)

Deberemos elegir la versión adecuada para nuestro sistema operativo y arquitectura. En este caso, seleccionamos la arquitectura x86 para Windows.

Por supuesto, guardamos el archivo en una ruta de nuestra preferencia, y comenzará el proceso de descarga del mismo.

![Proceso de descarga](/instalacion_jdk_img/step_04.png)

Esperaremos pacientemente, hasta que termine de descargarse. Podemos ir a prepararnos una chocolatada.

## Paso 2: Instalación del JDK
Ejecutamos el archivo que acabamos de descargar. Nos encontraremos con el típico instalador llamado *"siguiente, siquiente"*

![Primera pantalla del asistente de instalación](/instalacion_jdk_img/step_05.png)

Sólo deberemos tener cuidado en el segundo paso en caso de que deseemos instalar el JDK en otra ubicación. Recordemos esa ruta porque la utilizaremos más adelante.

![Aquí podemos elegir la ruta de instalación](/instalacion_jdk_img/step_06.png)

Esperamos el tiempo necesario y terminará la instalación.

![Esperamos a que termine la instalación](/instalacion_jdk_img/step_07.png)

## Paso 3: Configuración del sistema
Una vez instalado Java ya podremos utilizarlo. Sin embargo, a futuro necesitaremos que existan ciertas variables de entorno. Pasaremos a configurarlas.

Debemos acceder a las *propiedades de la computadora*, y seleccionar las *configuración avanzada del sistema*. Veamos los siguientes dos pasos:

![Propiedades de Mi PC](/instalacion_jdk_img/step_08.png)

![Configuración avanzada del sistema](/instalacion_jdk_img/step_09.png)

Una vez allí encontraremos un botón llamado *Variables de Entorno*.

![Variables de entorno](/instalacion_jdk_img/step_10.png)

Tendremos que agregar dos nuevas variables, con sus correspondientes valores. Las mismas serán:

    JAVA_HOME = C:\Program Files\Java\jdk1.6.0_43
    Path = %Path%;%JAVA_HOME%\bin

![Estableciendo la variable JAVA_HOME](/instalacion_jdk_img/step_11.png)

![Estableciendo la variable Path](/instalacion_jdk_img/step_12.png)

> Es importante respetar la ruta de instalación de Java en la variable `JAVA_HOME`, y colocar correctamente la variable `Path`

Una vez que terminamos con la configuración, para probar que todo ha resultado como esperamos, nos dirigimos a una consola y tipeamos `java -version`. Si obtenemos un cartel similar al siguiente, significa que la instalación se realizó con éxito.

> Para abrir la línea de comando deberemos presionar **Windows + r** y escribir `cmd`.

![Probando la instalación](/instalacion_jdk_img/step_13.png)
