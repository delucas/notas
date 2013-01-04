# Encapsulamiento

El primer principio que veremos será el de **encapsulamiento**, el más sencillo pero fundamental para mantener un código limpio. Hacer un buen trabajo al momento de encapsular una clase nos facilitará de manera sensitiva la modularidad de nuestro código.

Sin más preámbulos, el encapsulamiento es la capacidad que tiene una clase de mantener cierta parte de sí misma aislada del entorno, con el objetivo de que ningún agente externo no autorizado (generalmente otros objetos) afecte su comportamiento.

Es lógico, entonces, que mediante una utilización rigurosa de esta capacidad de los lenguajes de programación orientados a objetos podremos comenzar a allanar el camino hacia la modularidad: cada clase tiene hegemonía sobre una parte del código, y eso hace que al ocurrir defectos de programación no debamos alejarnos demasiado del foco de código para resolverlo (cosa que es moneda corriente cuando hay mucho acoplamiento y baja cohesión modular).

En Java muchos aseguran que simplemente haciendo privados los atributos de las clases se está cumpliendo con el encapsulamiento. No es suficiente, pero es un buen comienzo: *ninguna clase, más allá de la propia, debería conocer las razones que tiene para cambiar un miembro de otra clase*.

El encapsulamiento tiene una contrapartida, y ésta es la de tener que decidir por un lado qué es lo que se encapsula, y por otro qué se deja como **interfaz pública** de una clase. Esto quiere decir: qué miembros deseamos mantener "puertas adentro" y qué miembros revelaremos al "mundo exterior".

En rigor, se define como interfaz pública de una clase al conjunto de responsabilidades que los objetos de esa clase estarán brindando, desde el punto de vista externo a la misma. Estas responsabilidades deben ser *cohesivas*, pero eso lo veremos más adelante.

## Ocultamiento de la información
El encapsulamiento muchas veces se interpreta como **ocultamiento de la información**, lo que sería incompleto e incorrecto.  
Bajo esta luz, el encapsulamiento se refiere a que la representación interna de un objeto estará oculta desde un punto de vista externo a la definición de la clase del mismo. Este ocultamiento ayuda a hacer software más estable y robusto, mediante la prevención de que agentes externos modifiquen algún miembro que afecte el comportamiento del objeto.  

> "El diseñador de cada módulo debe seleccionar un subconjunto de las propiedades del módulo como la información oficial acerca del módulo, para hacerla disponible a los autores de módulos cliente".  
> *Bertrand Meyer [MEYER-97]*

Como podemos ver, Meyer define por contraposición (la interfaz pública) y deja entender que habrá otras propiedades que no se darán a conocer a otros autores.  
Meyer también afirma que el ocultamiento de la información nos permite cumplir con el *principio de continuidad*, que al asumir que todo módulo cambiará a lo largo del tiempo prevee que aquellos cambios se concentren en la parte "escondida" del código, sin afectar la interfaz pública (y como consecuencia, no cambiando el código de los módulos cliente).

Muchas veces este ocultamiento de información no podrá ser físico ya que frecuentemente el código será visible y otros programadores podrán leerlo directamente: no hablamos de ocultamiento físico de la información. En cambio, lo que debemos lograr es el ocultamiento lógico, es decir, *que no se pueda* crear un módulo descansando en información que está oculta en otro módulo.  
¿Cómo logramos esto? Buenas prácticas de programación, y una regla fundamental: *al escribir un módulo se deberá depender exclusivamente de las interfaces públicas de otros módulos y **nunca** de los detalles de implementación*.

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