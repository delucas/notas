# Liskov Substitution Principle - Principio de Sustitución de Liskov

> Las funciones que utilizan punteros o referencias a clases base deben ser capaces de utilizar objetos de clases derivadas sin saberlo.

Barbara Liskov enunció por primera vez este principio en su paper *A behavioral notion of subtyping*, aunque de un modo más formal:

> Requerimiento de Subtipo: Sea *p(x)* una propiedad verificable sobre los objetos *x* de tipo *T*. Entonces *p(y)* debe ser verdadera para objetos *y* del tipo *S*, siendo *S* un subtipo de *T*.

## Teoría de tipos

La **teoría de tipos** define un sistema formal en el cual cada elemento se caracteriza por tener un "tipo", y las operaciones que pueden realizarse entre estos elementos están establecidas por el tipo de los mismos.

El concepto va más allá del ámbito matemático (donde tiene su orígen) y aplica a la programación en forma directa. Tomemos por caso el lenguaje de programación Java. En él, un objeto del tipo `Integer` podrá operarse con otros objetos del mismo tipo, aplicando sumas, restas, etc. Nótese que no nos importará cómo sea la estructura interna del mismo, sino que símplemente debemos contar con que al hacer operaciones éstas se comporten como esperamos.

> Mientras que al objeto que representa el valor 1 se le pueda sumar el objeto que representa el valor 2 y dé como resultado el objeto que representa el valor 3, no deberá interesarnos cuál sea la estructura del mismo sino su capacidad de comportarse **según el tipo de dato** y conforme a las operaciones definidas.

### Subtipos
Un *subtipo* es un tipo de dato que se relaciona con otro tipo de dato (denominado *supertipo*) por cierta relación de sustituibilidad, que implica que las funciones/rutinas/métodos/procedimientos que pueden trabajar sobre los supertipos también lo podrán hacer sobre los subtipos ya que aquellos son sustituíbles por éstos.

Esta definición sienta las bases del Principio de Sustitución de Liskov, y delinea el concepto que generalmente se conoce, en programación orientada a objetos, como polimorfismo de tipos.

Existen principalmente dos esquemas de subtipado:

* **Subtipado nominal,** por el cual los subtipos declaran su relación con los supertipos: es explícito y forzado por la sintaxis del lenguaje. Este modo de definir la relación es característico de los *lenguajes con tipado estático*.
* **Subtipado estructural,** por el cual los subtipos que satisfagan las operaciones de los supertipos se considerarán como pertenecientes a la relación, sin necesidad de declararlo: es implícito y natural. Este modo de definir la relación es característico de los *lenguajes con tipado dinámico*.

De estos dos esquemas podemos encontrar dos tipos de implementación del subtipado:

* **Inclusiva,** por la cual las representaciones del subtipo representan también al tipo (i.e. un `Colibri` es un `Ave`).
* **Coercitiva,** por la cual las representaciones de un subtipo pueden convertirse a las representaciones del supertipo (i.e. un `Double` puede comportarse como un `Integer`).

En la programación orientada a objetos, es característico que el subtipado se implemente mediante el equema inclusivo, ya que es natural a la relación jerárquica entre tipos.

## Diseño por contrato
Un contrato es un acuerdo entre partes en el cual cada una se obliga a ciertas acciones. En el caso del software, se define un contrato al especificar aquellas condiciones que deben cumplirse para que ciertos mensajes que reciba un objeto puedan obtener una contestación válida, o no.

Por ejemplo el caso de una `Calculadora` que posea un método `dividir(dividendo: Integer, divisor: Integer): Double`, puede especificar las siguientes condiciones:

* **Precondición:** que el `divisor` sea distinto de cero
* **Postcondición:** el valor devuelto será el resultado de efectuar la división entre `dividendo` y `divisor`.

Como podemos ver, la *precondición* es la parte del contrato que especifica bajo qué circunstancias el método podrá resolver adecuadamente la operación. La *postcondición*, en cambio, define las circunstancias resultantes de la correcta ejecución de la operación.

Existe otro concepto relativo a los contratos que es el de **invariante de clase**, que establece aquello que no deberá cambiar durante la vida de los objetos que se instancien a partir de la misma. Por ejemplo, la clase `CajaDeAhorros` tiene como invariante que *no podrá poseer un saldo menor a 0.0*

### El contrato en LSP
El Principio de Sustitución de Liskov establece requerimientos estandar en la firma de los métodos de las superclases/subclases, más allá de los nombrados anteriormente. Son éstos los que permitirán evitar profundos problemas de diseño.

* La **contravarianza** de los argumentos dentro del subtipo. Los parámetros de un método de la subclase pueden ser de supertipos del tipo definido en el método de la superclase.
* La **covarianza** de los valores de retorno del subtipo. Los valores de retorno de la subclase pueden ser más específicos que los valores de retorno del mismo método en la superclase.
* La **inexistencia de nuevas excepciones** en los métodos del subtipo (excepto las que son subtipo de las excepciones del supertipo).
* Las **precondiciones** pueden ser más débiles en el subtipo.
* Las **postcondiciones** pueden ser más fuertes en el subtipo.
* Las **invariantes de clase** deben ser honradas y preservadas en el subtipo.
* La **Regla de la Historia**. Dado que los objetos deben ser modificables sólo a través de sus métodos, y que los subtipos pueden introducir métodos que no están presentes en el supertipo, podría introducirse un cambio de estado que no está permitido en el supertipo. La Regla de la Historia lo prohibe, y es el principal aporte de Liskov en su paper.

#### Entendiendo la Regla de la Historia
La Regla de la Historia tiene que ver con las expectativas que los clientes de nuestras clases tienen sobre las mismas. Si se establecen ciertos criterios de funcionamiento para los supertipos, al ser los subtipos sustitutos válidos de los mismos podríamos incurrir en comportamientos inesperados.

Por ejemplo, si existiera un `PuntoMutable` (que puede cambiar) como subtipo de `PuntoInmutable` (que no puede cambiar) estamos incurriendo en una falta a las expectativas de los clientes de nuestras clases: no se espera que cambie un `PuntoMutable`.

## Ejemplo
Supongamos que tenemos las siguientes clases:

    abstract class Figura {
      Double calcularArea();
      Double calcularPerimetro();
    }
    
    class Circulo extends Figura {
      Double radio;
      Circulo(Double radio) { this.radio = radio; }
      Double calcularArea() { return this.radio * this.radio * Math.PI; }
      Double calcularPerimetro() { return 2 * Math.PI * this.radio; }
    }
    
    class Cuadrado extends Figura {
      Double lado;
      Cuadrado(Double lado) { this.lado = lado; }
      Double calcularArea() { return this.lado * this.lado; }
      Double calcularPerimetro() { return 4 * this.lado; }
    }

Como podemos ver en el ejemplo, estamos extendiendo nuestras funcionalidades mediante la inclusión de nuevos subtipos que nos permiten calcular el área y el perímetro de diversas figuras geométricas.

Gracias al polimorfismo de tipos sabemos que cualquier subtipo puede reemplazar al supertipo que declara extender. Sin embargo, *¿estamos seguros de que conformamos el Principio de Sustitución de Liskov?*

En este caso, la respuesta es afirmativa: cumplimos con todas las reglas del contrato establecidas en el apartado anterior: no hay posibilidad de sorpresa para el usuario de nuestras clases, ya que siempre que obtenga una figura puede descansar en que ésta sabrá calcular su área y su perímetro, tal como el contrato que la `Figura` sabe cumplir.

> Es simple cumplir con el Principio de Sustitución de Liskov cuando las clases describen a sus objetos como **inmutables**, ya que se previenen los efectos colaterales no esperados.

En el próximo apartado veremos un caso que merece la pena destacar.

## Violación del LSP: Refused bequest

Empecemos con un ejemplo clásico, que puede encontrarse en casi toda la bibliografía referente al tema. Tomemos en cuenta las siguientes clases:

    class Rectangulo {
      Integer ancho;
      Integer alto;
      void setAncho(Integer ancho) { this.ancho = ancho; }
      void setAlto(Integer alto) { this.alto = alto; }
      void calcularArea() { return this.alto * this.ancho; }
    }
    
    class Cuadrado extends Rectangulo {
      void setAncho(Integer ancho) {
        this.ancho = ancho;
        this.alto = ancho;
      }
      void setAlto(Integer alto) {
        this.ancho = alto;
        this.alto = alto;
      }
    }

Como podemos apreciar, el ejemplo parece ser correcto: todo `Cuadrado` es un `Rectangulo`, aunque su ancho y alto valen lo mismo. El área se calcula del mismo modo, por lo que no debemos sobreescribir ese método. Sin embargo, para establecer tanto el alto como el ancho debemos hacerlo al mismo tiempo, asegurándonos que se mantenga la **invariante de clase** que dice que *un cuadrado tiene todos sus lados iguales*.

Por el momento funcionará correctamente, aunque pronto encontraremos el siguiente problema:

    class PruebaLSP {
      Rectangulo getRectangulo() { return new Cuadrado(); }
      void probarRefusedBequest() {
        Rectangulo r = getRectangulo();
        r.setAlto(10);
        r.setAncho(5);
        assert r.calcularArea() == 50; // error!
      }
    }

Vemos que el resultado de la operación es 25, mientras que esperamos que sea 50. Esto sucede simplemente porque estamos violando las condiciones invariantes del `Rectangulo`, y defraudando (en cierto modo) a aquellos clientes que esperan un `Rectangulo` que puede tener ancho y alto diferentes, y obtienen un `Cuadrado` que aplica invariantes más restrictivas.

Del mismo modo, estamos otorgándole responsabilidades al `Cuadrado` que no son propias del mismo: establecer por separado dos valores que se establecen al unísono.

> **Nota:** Pero... ¿no es cierto que *todo cuadrado es un rectángulo*? Al menos eso nos dijeron en la primaria, y lo mantuvimos hasta este momento. Pues sí: todo cuadrado es un rectángulo, matemáticamente hablando. Sin embargo existe algo llamado la **Ley de la Representación** que enuncia que nuestras clases son representaciones de los objetos en el mundo real, pero *no son los objetos del mundo real*. Por lo tanto podemos convivir con esta dicotomía.

Se denomina **Refused Bequest** a un smell por el cual un subtipo obtiene responsabilidades legadas que no necesita, o que no puede cumplir. De este modo se identifica una efectiva violación al LSP.  
En el caso extremo, el subtipo *se rehusa a cumplir con la interfaz del supertipo*, lanzando excepciones o retornando valores espúreos.

El [siguiente ejemplo](http://www.youtube.com/watch?v=FKg9O9coKGw) es simple y nos ayudará a comprender el concepto:

    interface Ave {
      abstract void volar();
    }
    
    class Gorrion implements Ave {
      void volar() { ... }
    }
    
    class Avestruz implements Ave {
      void volar() { throw new UnsupportedOperationException("¡Un avestruz no puede volar!"); }
    }

Estamos rompiendo el contrato que una línea más arriba nos comprometemos a cumplir: la posibilidad de volar. No conformes con eso, y pudiendo haber dejado el método vacío, lanzamos una excepción anunciando la imposibilidad de cumplir con el pedido.  
Por supuesto, ninguna de las dos aproximaciones es correcta: deberemos solucionar este refused bequest mediante alguno de los métodos que siguen.

### Solución 1 - Push down method / Push down field
Ambas técnicas servirán para solucionar una herencia mal formada, o para adaptar una jerarquía perfectamente formada y permitir la inclusión de un nuevo miembro.

Sigamos con el ejemplo anterior, en el cual tenemos una jerarquía correcta:

    interface Ave {
      abstract void volar();
    }
    
    class Gorrion implements Ave {
      void volar() { ... }
    }

Para poder hospedar al nuevo miembro, `Avestruz`, necesitaremos modelar el concepto de y `AveVoladora`. Para ello, deberemos **empujar hacia abajo** el método `volar():void` dentro de la nueva interfaz y seguir las transiciones en las clases que ya implementaban el concepto de `AveVoladora`:

    interface Ave {
      // removemos el método volar(), empujándolo hacia abajo
    }
    
    interface AveVoladora extends Ave {
      abstract void volar(); // método recibido de Ave
    }
    
    // modificamos la rama de la que pende Gorrion en la jerarquía
    class Gorrion implements AveVoladora {
      void volar() { ... }
    }
    
    class Avestruz implements Ave {
      // al ser Avestruz un Ave, no necesita implementar el método volar(), por lo que evitamos el refused bequest
    }

Nuestro `Gorrion` sigue comportándose como un `Ave`, además de hacerlo como un `AveVoladora`. Así todo programa dependiente de estas clases no dejará de funcionar, y habremos podido hospedar al nuevo miembro.

### Solución 2 - Reemplazar herencia con delegación
Muchas veces es más simple evitar los lazos fuertes que la herencia genera, y preferir una simple delegación. Supongamos otro caso que ilustra mejor el concepto:

    class Vector {
      // ... muchos métodos relativos a Vector
    }
    
    class Pila extends Vector {
      // obtiene los métodos de Vector
    }

Tenemos un potencial caso de refused bequest, dado que la `Pila` no debería permitir la posibilidad de acceder en forma aleatoria a sus miembros: al ser una estructura del tipo *primero entrado, último salido* se maneja como una pila de libros debiendo sacar el último elemento agregado primero.

La tentación de reutilizar la mayoría de los métodos de `Vector` fue muy grande, y caímos en la trampa de generar una herencia ficticia con todas sus potenciales falencias. En este caso, lo mejor sería convertirla en una composición y de ese modo servirnos de los métodos necesarios, exponiendo la interfaz correcta en nuestra clase `Pila`.

    class Vector {
      // ... muchos métodos relativos a Vector
    }
    
    class Pila {
      Vector vector = new Vector();
      boolean estaVacia() { return this.vector.isEmpty(); }
      void push(Object o) { this.vector.add(o); }
      // ...
    }

Y así, mediante la simple composición y delegación de comportamiento estamos reduciendo un fuerte acoplamiento en nuestro árbol de jerarquía para pasar a tener un acoplamiento encapsulado y por ello controlado.

## Conclusión
La conclusión que se encuentra en el artículo de Robert Martin resume las ideas que esta sección trató de sostener. Se reproducirán sus palabras en castellano:

> El Principio Open/Closed está en el corazón de muchas de las afirmaciones hechas para el diseño orientado a objetos. Es cuando se sigue este principio que las aplicaciones son más mantenibles, reusables y robustas. El Principio de Sustitución de Liskov (también conocido como Diseño por Contrato) es una característica importante de todos los programas que cumplen con el Principo Open/Closed. Sólamente cuando los tipos derivados son perfectos sustitutos de sus tipos base es que las funciones que los usan pueden ser reutilizadas con impunidad, y los tipos derivados ser cambiados con impunidad.

En pocas palabras, el LSP refuerza lo que el OCP quiere obtener a largo plazo: reutilización, robustez y mantenibilidad.

## Bibliografía recomendada
* Liskov, Barbara H. A Behavioral Notion of Subtyping. 1994. [PDF](http://www.cs.cmu.edu/~wing/publications/LiskovWing94.pdf).
* Martin, Robert C. The Liskov Substitution Principle. 1996. [PDF](http://www.objectmentor.com/resources/articles/lsp.pdf).

## Links de interés
* "[Interview with Barbara Liskov](http://www.infoq.com/interviews/barbara-liskov)". Blewitt, A. Liskov, B. *infoq.com*, 2 de abril de 2013 (accedido el 9 de abril de 2013)
* "[Principles of OOD](http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod)". Martin, Robert. *butunclebob.com*, 11 de mayo de 2005 (accedido el 12 de marzo de 2013)
* "[Type system](http://en.wikipedia.org/wiki/Type_system)", *Wikipedia, The Free Encyclopedia*. Wikimedia Foundation, 26 de marzo de 2013 (accedido el 27 de marzo de 2013)
* "[Type theory](http://en.wikipedia.org/wiki/Type_theory)", *Wikipedia, The Free Encyclopedia*. Wikimedia Foundation, 19 de marzo de 2013 (accedido el 27 de marzo de 2013)
* "[Subtype](http://en.wikipedia.org/wiki/Subtype)", *Wikipedia, The Free Encyclopedia*. Wikimedia Foundation, 27 de febrero de 2013 (accedido el 27 de marzo de 2013)
* "[SOLID principles – Part 3: Liskov’s Substitution Principle](http://www.ckode.dk/programming/solid-principles-part-3-liskovs-substitution-principle/)". *ckode.dk* (accedido el 25 de marzo de 2013)
* "[Liskov's Substitution Principle](http://www.oodesign.com/liskov-s-substitution-principle.html)". *oodesign.com* (accedido el 24 de marzo de 2013)
* "[Refused bequest](http://sourcemaking.com/refactoring/refused-bequest)". *sourcemaking.com* (accedido el 27 de marzo de 2013)
* "[Push down method](http://sourcemaking.com/refactoring/push-down-method)". *sourcemaking.com* (accedido el 26 de marzo de 2013)
* "[Push down field](http://sourcemaking.com/refactoring/push-down-field)". *sourcemaking.com* (accedido el 26 de marzo de 2013)
* "[Replace inheritance with delegation](http://sourcemaking.com/refactoring/replace-inheritance-with-delegation)". *sourcemaking.com* (accedido el 26 de marzo de 2013)