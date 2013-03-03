# Single Responsibility Principle - Principio de Responsabilidad Única

> Una clase debe tener una única razón para cambiar.

Una remembranza de la [Ley de Curly](http://www.youtube.com/watch?v=2k1uOqRb0HU), simple de enunciar y muchas veces dificil de identificar. Este principio enfatiza la importancia de que cada clase tenga un comportamiento cohesivo, y que se apegue al mismo encapsulándolo. Todo comportamiento adicional que no sea cohesivo, debería formar parte de otra clase, y ocasionalmente facilitar la colaboración entre ellas.

>**Cohesión. ** El grado de relación que tienen dos elementos de un módulo entre sí. Una alta cohesión implica una relación cercana, lo que sugiere que esos elementos podrían pertenecer al mismo módulo.

## Cuestión de cambios
Los usuarios reales de nuestros sistemas serán aquellos a los que deberemos proporcionar la solución a sus problemas reales. En tanto la actividad de desarrollo de software tiene que ver con necesidades cambiantes, personas desempeñando sus tareas de nuevas formas y alteraciones en la manera de relacionarse con nuestra solución, estamos sujetos a la posibilidad de que la pieza de software creada en un momento no esté alineada con la necesidad actual.

De acuerdo a Robert Martin, el software tiene dos valores fundamentales. El *valor secundario del software* es su posibilidad de cubrir las necesidades de los usuarios. De esa manera nuestros sistemas servirán a los usuarios actuales. Sin embargo, el *valor primario del software* es su capacidad para adaptarse a los cambios y poder servir a los usuarios futuros, conforme cambien sus necesidades.

Puede tenerse un sistema excelente que sirva a las necesidades de hoy, pero debido a un pobre diseño podría sufrir de *rigidez*, por lo que no podrá cambiar fácilmente para incorporar mejoras o nuevas características.

Cuando nos referimos a *responsabilidades* estamos enumerando indirectamente posibles ejes de cambio. Si nuestras clases encapsulan una única responsabilidad, sólo tienen una razón para cambiar, y este cambio es local (i.e. no afecta a otras clases). Contrariamente, cuantas más responsabilidades engloba nuestra clase, más razones habrá para que cambie.

## Fan-out
En la programación orientada a objetos, tanto el fan-in como el fan-out se refieren a las interacciones entre objetos. *El fan-out de un módulo es la cantidad de mensajes que envía hacia el exterior*.

Esta métrica nos sirve para tener una idea del nivel de acoplamiento de un módulo. Recordemos que cuando nos referimos a módulo estamos hablando de una unidad funcional, ya sea un simple método o una clase (según qué querramos analizar).

## El problema de acoplamiento
Cuanto más mensajes envíe un módulo al exterior, más datos conoce de su entorno. El conocimiento del entorno la hace sensible a cambios en el mismo. Es por ello que si una clase tiene un alto fan-out (o en otras palabras, emite muchos mensajes hacia el exterior del módulo cohesivo en el que se encuentra) hay muchas razones que ocasionalmente podrían incurrir en cambios.

El cambio en sí no es malo: debe introducirse un cambio para poder albergar una nueva funcionalidad, o modificar una existente de modo que esté alineada con las necesidades de nuestros usuarios. El verdadero problema del alto acoplamiento es que puede llevar a modificaciones incidentales en clases relacionadas pero que no tienen que ver directamente con el cambio original.

Adicionalmente, el acoplamiento puede generar que un cambio introducido para satisfacer una necesidad pueda ocasionar que otra necesidad deje de ser satisfecha. Gracias a los cambios locales, consecuencia del uso correcto de este principio, las incidencias de una alteración en el código no impactan más allá del módulo cohesivo que se haya alterado.

## Ejemplo
Supongamos que tenemos el siguiente código:

    public class Calculadora {
      public void sumar(int sumando1, int sumando2){
        int resultado = sumando1 + sumando2;
        System.out.println("El resultado de sumar " + sumando1 + " y " + sumando2 + " es " + resultado);
      }
    }

¿Hay algún problema con esa clase? Tomémonos un segundo para pensarlo y luego sigamos.

Bien, el problema es simple: el método `sumar` de la calculadora está cumpliendo con dos responsabilidades: está efectuando la suma, y a su vez está imprimiendo por pantalla el reporte de la operación realizada. Identificadas dos responsabilidades, serán dos ejes de cambio:
1. si se desea operar de otro modo, cambiando la forma de hacerlo para mejorar el desempeño o aprovechar un cache, por ejemplo.
2. si se desea imprimir otro tipo de reportes, con otro formato u otro idioma.

> **Nota:** Podría haber un tercer eje, de acuerdo a si se desea imprimir en pantalla o en una impresora, por ejemplo, pero dejemos ese caso aparte para simplificar.

La realidad es que nuestra clase `Calculadora` tiene dos razones para cambiar, y eso no es deseable según el SRP. Una mejor aproximación podría ser:

    public class Calculadora {
      public int sumar(int sumando1, int sumando2){
        return sumando1 + sumando2;
      }
    }

    public class ReporteSuma {
      public void reportar(int sumando1, int sumando2, int resultado){
        System.out.println("El resultado de sumar " + sumando1 + " y " + sumando2 + " es " + resultado);
      }
    }

Se podría seguir refinando, pero dejemos el caso en esta instancia.

## Análisis
### Ventajas
* Aumenta la mantenibilidad del código. Sólo debo ejecutar cambios locales conforme se necesite.
* Aumenta la extensibilidad del código. Se puede cambiar y se permite que el eje de cambio se mantenga a lo largo del tiempo.
### Desventajas
* Puede generar una gran cantidad de clases si no se lo considera adecuadamente o si se toma en forma absolutamente estricta (acabando con una clase por método).
* Puede ser complicado, si no se lleva una buena nomenclatura, encontrar aquel punto a cambiar dada la necesidad de alterar el software para cumplir con el nuevo requisito.

## Conclusión
Un eje de cambio será tal siempre que exista la posibilidad real de que nuestro software varíe en ese sentido.

Una falla en la identificación de un eje de cambio recaerá en rigidez, síntoma de que por mal diseño se torna complicado introducir un cambio. La identificación de un eje de cambio innecesario ocasionará complejidad innecesaria, una posibilidad de cambio latente que nunca ocurrirá.

Debemos estar atentos a identificar las responsabilidades de nuestras clases, y facilitar los cambios en ese sentido. El Principio de Responsabilidad Única nos ayudará a hacerlo, pero por sí mismo no alcanzará para obtener diseños correctos y flexibles sino que deberemos agregar las mejores prácticas y el resto de principios SOLID.

## Bibliografía
* [**Principles of OOD**](http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod). Robert Martin. Accedido el 2 de marzo de 2013
* [**SRP**](https://docs.google.com/file/d/0ByOwmqah_nuGNHEtcU5OekdDMkk/edit). Robert Martin. Accedido el 2 de marzo de 2013
* [**The Single Responsibility Principle**](http://do-while-true.blogspot.com.ar/2012/03/single-responsibility-principle-srp.html). Chris Lambrou. Accedido el 2 de marzo de 2013
* [**Curly's Law: Do One Thing**](http://www.codinghorror.com/blog/2007/03/curlys-law-do-one-thing.html). Jeff Attwood. Accedido el 2 de marzo de 2013
* [**Cohesion (computer science)**](http://en.wikipedia.org/wiki/Cohesion_(computer_science)). Wikipedia. Accedido el 2 de marzo de 2013