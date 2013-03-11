# Principios SOLID

## Los principios
1. [Single Responsibility Principle](01_srp.md)
2. [Open/Closed Principle](02_ocp.md)
3. [Liskov Substitution Principle](03_lsp.md)
4. [Interface Segregation Principle](04_isp.md)
5. [Dependency Inversion Principle](05_dip.md)

## Introducción
> El único documento que es lo suficientemente específico como para producir software funcionando, es el código fuente.
> *Robert Martin*

Estamos acostumbrados a pensar que los diagramas, esquemas y bocetos de pantallas son la documentación de nuestro software. Sin embargo, el único documento que se corresponde exactamente con el producto que deseamos desarrollar es el código fuente.

Dado que vamos a estar retocando y modificando el propio diseño de nuestro software, necesitamos que esté probado y que fundamentalmente sea claro de leer: debemos **mantener el código limpio**. Para ello habrá que aprender a identificar algunos signos que nos indican un diseño poco claro.

## Software Smells
Se define como *code smell* a cualquier síntoma del código o de la ejecución de un programa que pudiera darnos indicios de la existencia de un problema más profundo que el simple hecho observado.

Por ejemplo, la necesidad de repetir líneas de código nos puede dar pistas de que nuestras clases están mal estructuradas. O externamente, la lentitud con la que se ejecuta una operación puede indicarnos que estamos procesando los datos de forma incorrecta. Si los tests son muy difíciles de escribir, o tardan mucho en ejecutarse, seguramente estamos atando nuestro software a demasiadas dependencias.

Los llamados *code smells* no son bugs, ya que no impiden el funcionamiento del software. Sin embargo, revelan una veta por la cual podrían filtrarse errores en un futuro o que dificultarán el trabajo más adelante. La habilidad para descubrir estos malos olores en nuestro código se desarrolla con el tiempo: es una sensibilidad que requiere de cierta experiencia y de haber *visto y escrito mucho código*.

Existen dos aproximaciones a los *code smells*, según el enfoque que deseemos adoptar. Podemos evitarlos a toda costa (es decir, al encontrarnos con uno, removerlo mejorando el diseño), o analizarlos individualmente y ver si cada uno en particular afecta realmente a nuestro software (es decir, no removerlo a menos que sea necesario). El primer enfoque es más purista, y el segundo es más pragmático. Sea cual fuera el que tomemos, deberemos estar dispuestos a defender nuestra elección con argumentos sólidos.

Existen taxonomías y muchos nombres para cada uno de los *smells*. A continuación se enumeran algunos, sólo para ilustrar el concepto (se citan en inglés para facilitar su búsqueda e investigación):

* **Duplicated code:** varias líneas de código que se repiten a lo largo de diversos métodos en nuestro software.
* **Feature envy:** enviar varios mensajes al mismo objeto desde un mismo método.
* **Compare to null:** comparar variables contra null es un *smell* de que no estamos manejando objetos sino la posibilidad de la ausencia de los mismos.
* **instanceof in conditionals:** al preguntar de qué tipo es un objeto dentro de una condición, estamos desperdiciando el polimorfismo.
* **God class:** una clase que tiene demasiado código, por la que pasa gran parte de la lógica de nuestro software.
* **Too many parameters:** la utilización de excesivos parámetros en un mensaje puede indicar la necesidad de crear una nueva clase que agrupe algunos de ellos.

## El verdadero problema con el código
Por supuesto nadie diseña su software malintencionadamente en un principio: el código se hace de la mejor manera que uno puede manejar en cada momento. Sin embargo el problema del código es que éste va cambiando a lo largo del tiempo, y el agregado indiscriminado de cambios sin cuidar el aspecto y claridad de nuestro código es lo que genera que comiencen a surgir pequeños problemas que eventualmente degenerarán en grandes dificultades. En palabras de Robert Martin, *el código se pudre*.

## S.O.L.I.D.
Se conocen como principios SOLID a los cinco primeros principios de diseño orientado a objetos identificados por Robert Martin en el año 2009. El término surgió gracias a Michael Feathers, quien tomó las iniciales de cada principio y las reordenó para obtener un mnemónico representativo.

Estos principios, llamados *principios de manejo de dependencias*, ayudan a que el software obtenido mediante su seguimiento sea mantenible y que el código sea limpio y no se "pudra", evitando los *code smells* y llevándonos a obtener clases simples, cohesivas y con un bajo nivel de acoplamiento. En palabras de Robert Martin, "componentes específicos de bajo nivel que descansen en políticas generales de alto nivel".

## Conclusión
El código es la especificación completa del software funcionando que entregaremos. A medida que los usuarios vayan descubriendo nuevas necesidades, o viendo que lo que creían que necesitaban no era exactamente de ese modo, o explotando nuevas capacidades que surgen del propio sistema, tendremos que introducir cambios. Es por eso que el desarrollo de software será incremental y adaptativo.

Si se descuida el código fuente comenzaremos a tener trabas en nuestro camino que nos llevarán a que la introducción de cambios se vuelva más costosa, lenta y que comiencen a evidenciarse errores aparentemente no relacionados con la característica introducida. La sensación externa es que los desarrolladores *han perdido el control sobre el código fuente*. Y en la mayoría de los casos es eso lo que sucede.

Mediante buenas prácticas, y una política de mejoras sobre el código para llevarlo a un estado de limpieza y mantenibilidad, se puede evitar este proceso que hemos nombrado como *pudrimiento*. Los principios SOLID son un buen modo de comenzar a introducir mejoras y de guiarnos a lo largo del desarrollo. A lo largo de estos capítulos los iremos estudiando individualmente en detalle.

## Bibliografía
* [What is Software Design?](http://user.it.uu.se/~carle/softcraft/notes/Reeve_SourceCodeIsTheDesign.pdf). *Jack W. Reeves*. 1992. C++ journal.
* [**Principles of OOD**](http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod). Robert Martin. Accedido el 10 de marzo de 2013.
* [Code Smell](http://c2.com/cgi/wiki?CodeSmell).
* [Code Deodorant](http://c2.com/cgi/wiki?CodeDeodorant).
* [Bad Smells in Software - a Taxonomy and an Empirical Study](http://www.soberit.hut.fi/mmantyla/mmantyla_thesis_final_print2.pdf). *Myka Mäntylä*, 2003. Helsinki University of Technology.
* [A Taxonomy for "Bad Code Smells"](http://www.soberit.hut.fi/mmantyla/badcodesmellstaxonomy.htm). *Myka Mäntylä*, 2006. Helsinki University of Technology.
* [SOLID (object-oriented design)](http://en.wikipedia.org/wiki/SOLID_%28object-oriented_design%29). *Wikipedia*. Accedido el 10 de marzo de 2013.
SOLID wikipedia