# Encapsulamiento

El primer principio que veremos será el de **encapsulamiento**, el más sencillo pero fundamental para mantener un código limpio. Hacer un buen trabajo al momento de encapsular una clase nos facilitará de manera sensitiva la modularidad de nuestro código.

Sin más preámbulos, el encapsulamiento es la capacidad que tiene una clase de mantener cierta parte de sí misma aislada del entorno, con el objetivo de que ningún agente externo no autorizado (generalmente otros objetos) afecte su comportamiento.

Es lógico, entonces, que mediante una utilización rigurosa de esta capacidad de los lenguajes de programación orientados a objetos podremos comenzar a allanar el camino hacia la modularidad: cada clase tiene hegemonía sobre una parte del código, y eso hace que al ocurrir defectos de programación no debamos alejarnos demasiado del foco de código para resolverlo (cosa que es moneda corriente cuando hay mucho acoplamiento y baja cohesión modular).

En Java se suele asegurar que simplemente haciendo privados los atributos de las clases se está cumpliendo con el encapsulamiento. No es suficiente, pero es un buen comienzo: *ninguna clase, más allá de la propia, debería conocer las razones que tiene para cambiar un miembro de otra clase*.

El encapsulamiento tiene una contrapartida, y ésta es la de tener que decidir qué es lo que se encapsula y qué se deja como interfaz pública de una clase. Esto quiere decir: qué miembros deseamos mantener "puertas adentro" y qué miembros revelaremos al "mundo exterior".

En rigor, se define como **interfaz pública** de una clase al conjunto de responsabilidades que los objetos de esa clase estarán brindando, desde el punto de vista externo a la misma. Estas responsabilidades deben ser *cohesivas*, pero eso lo veremos más adelante.

## Ocultamiento de la información
El encapsulamiento muchas veces se interpreta como **ocultamiento de la información**, lo que sería incompleto e incorrecto.

Bajo esta luz, el encapsulamiento se refiere a que la representación interna de un objeto estará oculta desde un punto de vista externo a la definición de la clase del mismo. Este ocultamiento ayuda a hacer software más estable y robusto, mediante la prevención de que agentes externos modifiquen algún miembro que afecte el comportamiento del objeto.

> "El diseñador de cada módulo debe seleccionar un subconjunto de las propiedades del módulo como la información oficial acerca del módulo, para hacerla disponible a los autores de módulos cliente".  
> *Bertrand Meyer [MEYER-97]*

Meyer define por contraposición (la interfaz pública) y deja entender que habrá algunas propiedades que no se darán a conocer a los autores de otros módulo.  
Meyer también afirma que el ocultamiento de la información nos permite cumplir con el *principio de continuidad*, que al asumir que todo módulo cambiará a lo largo del tiempo prevee que aquellos cambios se concentren en la parte "escondida" del código, sin afectar la interfaz pública (y como consecuencia, no cambiando el código de los módulos cliente).

Muchas veces este ocultamiento de información no podrá ser físico ya que frecuentemente el código será visible y otros programadores podrán leerlo directamente: debemos lograr el ocultamiento lógico, es decir, *que no se pueda* crear un módulo que dependa de información que está oculta en otro módulo.  
¿Cómo logramos esto? Buenas prácticas de programación, y una regla fundamental: *al escribir un módulo se deberá depender exclusivamente de la interfaz pública de otros módulos y **nunca** de los detalles de implementación*.

## Getters y Setters
Dado que bajo ciertas circunstancias es necesario instruir a un objeto la necesidad de cambiar algún valor interno del mismo, es importante proporcionar un mecanismo para poder hacerlo sin romper el encapsulamiento (en términos rudimentarios, sin hacer públicos algunos -o todos- sus miembros).  
Es por ello que existen dos tipos de métodos muy simples que se denominan **accesores**, y serán los que nos permitan acceder a esos miembros privados *de una manera controlada por el diseñador de la clase*.  
Los getters nos servirán para obtener el valor de un miembro, y los setters para establecerlo. Su raíz en el idioma inglés hace juego con las palabras "get" y "set" (obtener y establecer).  
Típicamente, un getter tiene esta estructura:

    public Integer getEdad() {
        return this.edad;
    }

Un setter, en cambio, responde a la siguiente estructura:

    public void setEdad(Integer edad) {
        this.edad = edad;
    }

Cuando estamos a cargo de la definición de una clase, definimos nosotros mismos el nivel de complejidad que estos métodos encapsulan, y qué tan directamente permitimos que un agente externo acceda a los miembros de la misma.  
> **Nota:** Para utilizar algunas tecnologías Java, es necesario escribir setters y getters de todos los atributos *persistentes* de una clase. Ya llegaremos a eso, pero por el momento es interesante saberlo.

## Tell, don't ask
> El código procedural obtiene información y luego toma decisiones. El código orientado a objetos instruye a los objetos para hacer cosas. 
> Alec Sharp [SHARP-97]

En este sentido, deberíamos pedirle cosas a los objetos en lugar de preguntarle al respecto de su estado, tomar una decisión en función a ello, y luego decirles qué hacer.  
Violaríamos el encapsulamiento al hacerlo de otro modo: si tomásemos decisiones en función del estado de un objeto, estaríamos conociendo *demasiada* información y es muy probable que la decisión que estemos tratando de tomar desde el módulo cliente corresponda al objeto consultado en lugar del módulo que estamos escribendo.

Con esto volvemos a los conceptos de **comandos** y **consultas** que conocemos de capítulos anteriores, y la preferencia de los primeros por sobre los segundos.

Veamos un ejemplo práctico de lo que queremos decir. Podríamos tener el siguiente código (correcto, pero póbremente diseñado):

    public void verificarSobrecalentamiento(Monitor monitor) {
      if (monitor.getTemperatura() > 100) {
        monitor.sonarAlarmas();
      }
    }

En cambio, podríamos reescribir esa pieza teniendo en cuenta los conceptos que acabamos de volcar:

    public class Monitor {
      public void verificarSobrecalentamiento() {
        if (this.temperatura > 100) {
          this.sonarAlarmas();
        }
      }
      //...
    }

Como podemos ver, la decisión de cuánto se considera "sobrecalentamiento" corresponde más al monitor que al cliente. Adicionalmente, éste tiene toda la información y los elementos necesarios para llevar a cabo esta responsabilidad: vigilar el sobrecalentamiento, y sonar las alarmas si corresponde.

## Recursos

### Bibliografía
- [MEYER-97] **Object-oriented software construction** *Bertrand Meyer* - Prentice Hall PTR - 1997
- [SHARP-97] **Smalltalk by example: the developer's guide**
*Alec Sharp* - McGraw Hill - 1997

### Links
- [Tell, don't ask - The Pragmatic Bookshelf](http://pragprog.com/articles/tell-dont-ask)
- [Tell, don't ask - Thoughtbot](http://robots.thoughtbot.com/post/27572137956/tell-dont-ask)
- [Tell, don't ask - c2 wiki](http://c2.com/cgi/wiki?TellDontAsk)