# Open/Closed Principle - Principio Abierto/Cerrado

> Debe poderse cambiar el comportamiento de una clase sin necesidad de modificarla.

Bertrand Meyer enunció este principio en la primera edición de su libro *Object-Oriented Software Construction* de la siguiente manera: *las entidades de software (clases, módulos, funciones, etc) deben estar abiertas para la extensión, pero cerradas para la modificación*.

## ¿Abierto y cerrado?
> Se dice que **un módulo está abierto** si es que aún *permite* su extensión. Esto puede ser mediante el agregado de operaciones, estructuras de datos, campos, etcétera.

> **Un módulo está cerrado** si *está disponible* para el uso por parte de otros módulos. Esto sucederá si se puede otorgar una descripción estable y bien definida de su funcionamiento (podríamos decir que nos referimos a su *interfaz*).

En pocas palabras, *abierto para la extensión y cerrado para la modificación*.

Desde el punto de vista de los desarrolladores, siempre es necesario dejar los módulos abiertos ya que es imposible prever todos los cambios que podrían efectuarse a lo largo del tiempo en el software. Podemos llegar a estimar algunos ejes de extensión, pero necesitaremos la posibilidad de hacerlo de nuevas maneras no previstas.  
También será necesario cierto nivel de cierre, para poder liberar versiones de nuestros módulos y que éstos puedan ser empleados por otros desarrolladores. Si no cerramos un módulo, no podríamos trabajar con esquemas modulares.

Aunque esta premisa de la simultaneidad de apertura y cierre de un módulo tiene lógica en teoría, parece imposible de llevar a cabo en la práctica: podemos dejar el módulo abierto a extensión y no dejar que nadie lo utilice, o cerrarlo y al necesitar un cambio arrastrarlo hacia todos los módulos que dependen del nuestro. De hecho, la correcta aplicación del principio es dificultosa.

## El polimorfismo al rescate
No existiría un principio si no hubiera una forma de llevarlo a la práctica. La programación orientada a objetos nos ayuda brindándonos el polimorfismo.

La implementación involucra la definición de una política de alto nivel y de una serie de implementaciones de bajo nivel que puedan ir incorporándose conforme los requerimientos se extiendan.

La **política de alto nivel** será aquella pública, de la cual dependerán los módulos que requieran del nuestro. Carece de detalles puntuales, pero expone la responsabilidad que se satisfará con **implementaciones de bajo nivel**. Estas implementaciones no se expondrán a los módulos cliente para reducir acoplamientos innecesarios.

Es con estos dos tipos de componentes que **cerramos las políticas de alto nivel para la modificación, pero abrimos su extensión mediante nuevas implementaciones de bajo nivel**. De este modo reducimos la volatilidad de los puntos de acoplamiento, pero mantenemos la variabilidad de las especificaciones.

## Diseño ordinario y diseño revolucionario
Kent Beck explica de un modo muy interesante esta diferenciación, basándose en las categorías establecidas por Thomas Kuhn en *La estructura de las revoluciones científicas*.

Kent separa los tipos de diseño de la siguiente manera:

* **Diseño ordinario**, aquel que se hace día a día, como extraer un método, un objeto, mover la lógica de un lado a otro para mejorar su estructura y llevarla más cerca del sitio al que pertenece. De ese modo, todo encaja, y puede ir refinándose el diseño de un sistema adecuándolo al Principio Open/Closed.
* **Diseño revolucionario**, cuando se aproxima una nueva funcionalidad que no encaja en el diseño actual y requiere de técnicas que no se ajustan al Principio.

Cada vez que nos encontramos con la necesidad de revolucionar nuestro diseño deberemos romper el Principio Open/Closed, ya que habrá que crear nuevas abstracciones, *abrir* las antiguas para que pueda hacerse espacio a lo nuevo, y hacer todas las modificaciones necesarias. Una vez terminado el proceso, podrá volver a *cerrarse* el diseño y pasar a una fase de *diseño ordinario*.

Kent enfatiza por qué es necesario hacer una distinción entre estos dos tipos de diseño:

* Cuando hacemos *diseño ordinario* tenemos definido mentalmente un conjunto con las operaciones que podemos ejecutar. Simples refactorizaciones, extracción de interfaces, extensión de modelos. Son operaciones que no necesitan de gran cuidado ya que pueden llamarse "de rutina".
* En cambio, cuando hacemos *diseño revolucionario* debemos avanzar con cautela: estaremos dispuestos a duplicar código, explorar nuevos diseños y modificar jerarquías que funcionaban sólamente para poder recibir el nuevo factor que aparentemente no encaja en el código tal como está.

En el *diseño ordinario* se tiende a mejorar el código, puliendo iterativamente. En el *diseño revolucionario* se permiten concesiones que no mejoran el código, pero que sientan las bases para refinarlo una vez que se hayan introducido las nuevas características.

No debe entenderse que estos tipos de diseño son excluyentes, o que debemos priorizar uno por sobre el otro: dada la circunstancia adecuada, se deberá proceder con el modo de trabajo necesario para sobrellevarla de la mejor manera. Recordemos que el diseño emerge de la continua incorporación de funcionalidades al software, y debe adaptarse conforme transcurre el tiempo para el proyecto.

En pocas palabras, *diseñamos ordinariamente hasta necesitar una revolución... pero luego volvemos a lo ordinario*.

## Ejemplo
> Veremos un ejemplo extraído de [oodesign.com](http://www.oodesign.com/open-close-principle.html). El crédito es para ellos, aunque nos permitiremos algunas licencias en la transcripción del ejemplo para mejorar el estilo y hacerlo más simple.

Se trata de un editor gráfico que maneja la impresión de diversas figuras en pantalla. 

    class EditorGrafico {
      public void dibujarForma(Forma forma) {
        if (forma.getTipo().equals("rectangulo")) {
          dibujarRectangulo(forma);
        } else if (forma.getTipo().equals("circulo")) {
          dibujarCirculo(forma);
        }
      }
      public void dibujarCirculo(Circulo circulo) {...}
      public void dibujarRectangulo(Rectánculo rectangulo) {...}
    }

Como podemos ver, cada vez que se pueda dibujar un nuevo tipo forma habrá que agregar una bifurcación a la condición del método `dibujarForma(Forma)`, y generar un nuevo método auxiliar para el dibujo propiamente dicho. Todo esto, modificando la clase `EditorGrafico`.

Este código no cumple con el Principio Open/Closed. Sin embargo, si estos dos casos fueran los únicos dentro de los requerimientos no tendríamos argumento para refactorizar en favor del postulado. Como sabemos que el código crecerá hacia nuevas formas, como ser triángulos y todo tipo de polígonos, prepararemos el camino para luego, ya que...

> Your future self will thank you. *(Tu futuro "yo" te lo agradecerá)*.

Afortunadamente ya tenemos las abstracciones armadas: del código se infiere que hay una jerarquía de clases, con raíz en `Forma`, y dos subclases (`Circulo` y `Rectangulo`). Será cuestión de reubicar responsabilidades y delegar alguna llamada, facilitando que el polimorfismo maneje esa decisión que no queremos tomar en el código.

    class EditorGrafico {
      public void dibujarForma(Forma forma) {
        forma.dibujar();
      }
    }

    abstract class Forma {
      public abstract void dibujar();
    }

    class Circulo extends Forma {
      public void dibujar() {...}
    }

    class Rectangulo extends Forma {
      public void dibujar() {...}
    }

Esta refactorización del código nos presenta un escenario mucho más favorable: al introducir una nueva forma entre las existentes, sólamente deberemos extender la clase base `Forma` y brindarle comportamiento al método encargado de dibujarla. Nuestro pequeño sistema está *cerrado para la modificación y abierto para la extensión*.

Por supuesto, abierto para **ese eje de cambio**...

## Consejos de Meyer
En su libro, Meyer nos aclara que este principio no sugiere que comencemos a modificar el código cual fanáticos. Puntualmente:

* Si tenemos el control sobre el software y sus dependencias, y podemos reescribir el módulo que debe cambiar, debe hacerse.
* La aplicación de este principio no es una forma de corregir errores de diseño, ni bugs. Si hay algo mal con un módulo, se debe arreglar (y no dejar el original inalterado y modificar una subclase... a menos que no tengamos control sobre el módulo original, por supuesto).

La idea general de este principio es desarrollar módulos saludables, que puedan mantenerse en el tiempo y admitir los cambios necesarios en las especificaciones.

## Análisis
Muy costoso de aplicar correctamente y con alto riesgo de aplicarlo en los casos indicados, se dice que a menos que tengamos pleno conocimiento del futuro de los requerimientos no podrá aplicarse directamente en la primera iteración. Por lo tanto, deberemos estar preparados para hacer diseño revolucionario de tanto en tanto. Mejor ir tendiendo las redes con tests, para evitar caídas abruptas.

### Ventajas
* El **diseño es muy claro** una vez que se entiende cómo funciona el polimorfismo y la extensión del comportamiento.
* El **código queda limpio**, evitando condiciones innecesarias.
* Se facilita que los módulos cliente del nuestro puedan descansar en **políticas de alto nivel que por lo general no cambian**, dejando los detalles para implementaciones de bajo nivel.

### Desventajas
* **Es costoso** ya que demanda esfuerzo de previsión, diseño e implementación.
* Cuando no disponemos de la suficiente información sobre los requerimientos podemos **implementarlo en casos que no lo requerían** en un principio.
* Es **difícil de identificar y seguir** cuando se carece de suficiente experiencia en la programación orientada a objetos.

## Conclusión
La aplicación del Principio [Open/Closed](http://www.youtube.com/watch?v=OBZsuTQtoPc) es costosa: lleva tiempo de diseño, implementación, y una buena dosis de adivinación. No siempre seremos capaces de identificar los ejes de cambio de nuestro software con suficiente antelación como para planificar un conjunto de clases que respondan correctamente a este principio.

Es por este alto costo que debemos aplicar la premisa conocida como *arreglar cuando duela*. Si se vuelve recurrente cierto eje de cambio o si vemos una potencialidad real al utilizar estas técnicas, valdrá la pena hacerlo. Sin embargo, y siguiendo los consejos de Meyer, la aplicación tiene su justa medida y lugar: si puede evitarse, debe evitarse. Y si el código necesita modificarse, deberá modificarse.

## Bibliografía recomendada
* Bertrand Meyer. 1997. Object-Oriented Software Construction (2nd Ed.). Prentice-Hall, Inc., Upper Saddle River, NJ, USA.
* Martin, Robert C. The Open-Closed Principle. 1996. [PDF](http://www.objectmentor.com/resources/articles/ocp.pdf).
* Larman, Craig. Protected Variation: The Importance of Being Closed. 2001. [PDF](http://martinfowler.com/ieeeSoftware/protectedVariation.pdf)

## Links de interés
* "[Open/closed principle](http://en.wikipedia.org/wiki/Open/closed_principle)", *Wikipedia, The Free Encyclopedia*. Wikimedia Foundation, 5 de marzo de 2013 (accedido el 13 de marzo de 2013)
* "[Principles of OOD](http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod)". Martin, Robert. *butunclebob.com*, 11 de mayo de 2005 (accedido el 12 de marzo de 2013)
* "[The Open/Closed/Open Principle](http://www.threeriversinstitute.org/blog/?p=242)". Beck, Kent.  *threeriversinstitute.org*, 21 de junio de 2009 (accedido el 12 marzo de 2013)
* "[Design is an island](http://www.threeriversinstitute.org/blog/?p=122)". Beck, Kent.  *threeriversinstitute.org*, 11 de abril de 2009 (accedido el 12 marzo de 2013)
* "[The open closed principle](http://lostechies.com/gabrielschenker/2009/02/13/the-open-closed-principle/)". Schenker, Gabriel. *lostechies.com*, 13 de febrero 2009 (accedido el 11 de marzo de 2013)
* "[Open Close Principle](http://www.oodesign.com/open-close-principle.html)". *oodesign.com* (accedido el 13 de marzo de 2013)
* "[The Open/Closed Principle: Concerns about Change in Software Design](http://blog.symprise.net/2009/06/open-closed-principle-concerns-about-change-in-software-design/)". Peixoto de Azevedo, Rafael. *symprise.net*, 23 de junio de 2009 (accedido el 13 de marzo de 2013)
* "[A simple example of the Open/Closed principle](http://joelabrahamsson.com/a-simple-example-of-the-openclosed-principle/)". Abrahamsson, Joel. *joelabrahamsson.com* (accedido el 13 de marzo de 2013)
* "[Revisiting Fowler's Video Store: Adopting Object Oriented Syntax](http://blog.symprise.net/2009/01/revisiting-fowlers-video-store-01-object-oriented-syntax/)". Peixoto de Azevedo, Rafael. *symprise.net*, 14 de enero de 2009 (accedido el 13 de marzo de 2013)