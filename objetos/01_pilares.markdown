# Pilares de la *POO*
Muchas veces se suele definir la Programación Orientada a Objetos mediante sus características. Por supuesto, esto no debería ser así, sino que todo debe llevar a una idea común de objetos y cómo éstos nos ayudan a resolver problemas de programación.

La *POO* tiene, entre sus características, tres que son principales y por ello se denominan **pilares**. Se corresponden con conceptos que tienen creciente nivel de dificultad, y al ser respetados y aplicados conllevan a un diseño modular y organizado de las clases que nos ayudarán a resolver los problemas de programación.

## Encapsulamiento
El primer principio que veremos será el de **encapsulamiento**, el más sencillo pero fundamental para mantener un código limpio. Hacer un buen trabajo al momento de encapsular una clase nos facilitará de manera sensitiva la modularidad de nuestro código.

Sin más preámbulos, el encapsulamiento es la capacidad que tiene una clase de mantener cierta parte de sí misma aislada del entorno, con el objetivo de que ningún agente externo no autorizado (generalmente otros objetos) afecte su comportamiento.

Es lógico, entonces, que mediante una utilización rigurosa de esta capacidad de los lenguajes de programación orientados a objetos podremos comenzar a allanar el camino hacia la modularidad: cada clase tiene hegemonía sobre una parte del código, por lo que al rastrear efectos colaterales dentro de un gran proyecto no deberíamos alejarnos demasiado del lugar donde específicamente se encuentra nuestro código.

En Java muchos aseguran que simplemente haciendo privados los atributos de las clases se está cumpliendo con el encapsulamiento. No es suficiente, pero es un buen comienzo: *ninguna clase, más allá de la propia, debería conocer las razones que tiene para cambiar un miembro de otra clase*.

El encapsulamiento tiene una contrapartida, y ésta es la decisión bipartita de qué es lo que se encapsula, y qué se deja como **interfaz pública** de una clase. Esto quiere decir: qué miembros deseamos mantener "puertas adentro" y qué miembros revelaremos al "mundo exterior".

En rigor, se define como interfaz pública de una clase al conjunto de responsabilidades que los objetos de esa clase estarán brindando, desde el punto de vista externo a la misma.

### Ocultamiento de la información
El encapsulamiento puede verse desde cierto ángulo como **ocultamiento de la información**, lo que sería incompleto pero un enfoque parcial para comenzar a comprender el concepto.  
Bajo esta luz, el encapsulamiento se refiere a que la representación interna de un objeto estará oculta desde un punto de vista externo a la definición de la clase del mismo. Este ocultamiento ayuda a hacer software más estable y robusto, mediante la prevención de que agentes externos modifiquen algún miembro que afecte el comportamiento del objeto.

### Getters y Setters
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

## Herencia
### Tipos de herencia
#### Herencia de tipos
#### Herencia de comportamiento

## Polimorfismo
### *Sabores* del polimorfismo
#### Asignaciones polimórficas
#### Entidades polimórficas
#### Estructuras de datos polimórficas