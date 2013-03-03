# Herencia
Bertrand Meyer, en su libro *Touch of class* brinda un ejemplo muy claro y simple: analiza cómo la botánica debió clasificar, gracias a Linneo, las especies vivientes. Esto muestra como "objetos" de la naturaleza obtienen una taxonomía artificial con el objetivo de poder estudiarlos.  
Por otro lado, los objetos de la matemática (números, funciones, series) son creaciones humanas. Con la venida de Cantor, y sus teorías de conjuntos y grupos se organizaron estos objetos artificiales.
Como programadores nosotros también lidiamos con entidades artificiales, objetos salidos de nuestra imaginación. Para evitar el desorden que fácilmente podemos ocasionar, tenemos a la mano la posibilidad de utilizar una taxonomía.

Es así como organizamos nuestras clases de acuerdo a relaciones jerárquicas, denominadas **herencia**. Así como un perro *es un* mamífero y un mamífero *es un* vertebrado, nuestro objeto Estudiante *es una* persona.

> La herencia nos habilitará a razonar sobre una relación "es un" y utilizar las taxonomías resultantes para estructurar nuestro software.
> Bertrand Meyer [MEYER-2009]

Puesto en esos términos, la herencia es un mecanismo que nos proveen *algunos* lenguajes orientados a objetos para definir relaciones jerárquicas entre clases, que nos permitan estructurarlas de acuerdo a un sentido de genericidad / especialización.  
Breve ejemplo: **Un Estudiante es una Persona**. Estudiante tiene características especializadas, que una Persona común no tiene. La relación entre Estudiante y Persona será:
* *generalización*, si se lee como "un Estudiante es una Persona"
* *especialización*, si la vemos como "algunas Personas son Estudiantes"

Consecuencia de esta relación de especialización/generalización y de la estructuración de las clases obtendremos la posibilidad de compartir comportamiento, ya sea idéntico, modificado, aumentado o totalmente diferente.


## Tipos de herencia
### Herencia de tipos
### Herencia de comportamiento

## Recursos

### Bibliografía
- [MEYER-09] **Touch of class: learning to program well with objects and contracts**, *Bertrand Meyer* - Springer - 2009
- [SHARP-97] **Smalltalk by example: the developer's guide**
*Alec Sharp* - McGraw Hill - 1997

