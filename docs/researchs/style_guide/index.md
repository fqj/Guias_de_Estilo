#  __GUÍAS DE ESTILO Y BUENAS PRÁCTICAS__

##  __Guías de estilo__

#### Guia de estilo John Papa __ANGULAR 2__

https://angular.io/docs/ts/latest/guide/style-guide.html

#### Guia de estilo John Papa  __ANGULARJS__

https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md

####  __Google Web Component__

https://github.com/GoogleWebComponents/style-guide

####  __Polymer__

https://polymerelements.github.io/style-guide/#documentation

#### Guia de estilo  __Javascript__

https://github.com/airbnb/javascript

#### Recomendaciones estilos  __CSS__

 __AIRBNB__

https://github.com/airbnb/css

Slide de charla de  __Francisco Quintero__, miembro del equipo de Serenity FrontStack

http://slides.com/frontstack/deck-4#/

##  __CLEAN CODE__
###  PRINCIPIOS  __CLEAN CODE__

#### Principio  __DRY__ (Don't repeat yourself)

No repitas código __NUNCA__, El código duplicado es propenso a generar errores y es difícil de mantener. Si estás repitiendo código, extrae ese código a una función para encapsularlo. Si tenemos que hacer un cambio, este estará localizado en un solo punto, y no desperdigado por todo el código fuente.

#### The Principle of Least Surprise.

Las funciones o clases deben hacer lo que (razonablemente) se espera de ellas. Es decir, una función o una clase debe tener, en función de su nombre, un comportamiento obvio para cualquier programador, sin que este tenga la necesidad de sumergirse en su código.

#### Principio __KISS__ (Keep It Simple Stupid)

El diseño de un programa debe ser sencillo. Cuánto más sencillo sea, mejor. Hay que evitar la complejidad como norma general, pero sobre todo la complejidad innecesaria.

#### Principio __SOLID__
Realmente son 5 principios

- __SRP  (Single Responsibility Principle__: Las clases o módulos deben tener una única responsabilidad
- __Open/Close Principle__: Abierto para su extensión, pero cerrado para su modificación. nos dice que el código está mejor diseñado si se puede modificar su comportamiento sin cambiar su código fuente. Debería bastar con añadir código, en lugar de modificarlo. No deberíamos necesitar modificar una clase a no ser que sea para corregir errores.
- __Liskov__: Principio de sustitución, una clase derivada no debe modificar el comportamiento de la clase base.
- __ISP (Interface segregation principle)__: Una clase que implementa una interfaz no debe depender de métodos que no utiliza. Esto como norma general implica que nuestras interfaces deben ser sencillas y tener pocos métodos. Es preferible tener varias interfaces pequeñas, a tener una interfaz grande. Así no obligamos a los clientes a depender de métodos que no necesitan implementar.

- __DIP (Dependency Inversion Principle)__: Las clases de alto nivel, no deben depender de clases de bajo nivel. Ambos deben depender de abstracciones. Además las abstracciones no deben depender de los detalles, si no que los detalles deben depender de las abstracciones. En definitiva, lo que tenemos que hacer es invertir las dependencias.

#### Principio __SoC (separation of concerns)__
Los asuntos, son los diferentes aspectos de la funcionalidad de nuestra aplicación. Por ejemplo la capa de negocio, la capa de datos etc. Un buen ejemplo de separación es el patrón MVC.

#### Principio __YAGNI, (You ain't gonna need it),__
No debemos implementar algo si no estamos seguros de necesitarlo. Así ahorramos tiempo y esfuerzo.

#### Principio __Boy Scout__
El código siempre puede mejorar. Si podemos, debemos refactorizar el código para dejarlo todavía más limpio y simple que antes.

#### __Ley de Demeter__
Una unidad solo debe tener conocimiento limitado de otras unidades, y solo conocer aquellas que están relacionadas. La una unidad solo debe hablar con amigos y nunca con extraños. Además la unidad solo debe hablar con amigos inmediatos.no hay que hablar con extraños.

#### __F.I.R.S.T.__
Los test forman un papel fundamental en el arte de escribir código limpio. No obstante, no es suficiente con escribirlos de cualquier manera. Deben cumplir una serie de reglas.
- __Fast__: Los test deben correr rápido. Deben tardar poco en ejecutarse. De no ser así, es probable que nos de pereza ejecutarlos y, por tanto, que no lo hagamos con la frecuencia deseada. El no ejecutar los test con relativa frecuencia puede hacer que tardemos más en encontrar los problemas que vayan surgiendo.
- __Independent__: Los test deben ser independientes unos de otros. El resultado de un test no debe condicionar el de los siguientes. Deben poder ejecutarse en el orden que se quiera. De lo contrario, un fallo en el primer test, puede desencadenar un fallo en cascada de los demás, haciendo complejo el diagnóstico del sistema.
- __Repeatable__: Los test deben poder ejecutarse en cualquier entorno (desarrollo, pre-producción, producción…). De no ser así, siempre tendremos una excusa para cuando los test fallen.
- __Self-Validating__: Los test deben devolver una respuesta booleana. Pasan o no pasan. No deben dejar una cadena de caracteres en un fichero de log que tengamos que comprobar nosotros mismos, o dejar dos ficheros de un tamaño determinado que, igualmente tengamos que comprobar. De lo contrario, requerirán una alta evaluación manual que nos hará perder tiempo y precisión.
- __Timely__: Los test deben ser escritos antes que el código de producción. De no ser así, el código de producción será difícil de testear.

#### Resumen clean Code interesante
http://samuelcasanova.com/2016/09/resumen-clean-code/

### Herramientas trabajo
Para angular2, VISUAL STUDIO CODE
https://code.visualstudio.com/

Aunque también se puede usar otro editor añadiendo el plugin para TypeScript
para el resto de frameworks,  con el que el desarrollador se sienta más cómodo, (Visual Studio Code, SublimeText, Atom, WebStorm, etc)

Recomendamos instalar un plugin de __ESLINT__, el que corresponda con cada editor, para que muestre en tiempo real errores de estilo de código


## __Progressive Web Application__

https://github.com/GoogleChrome/lighthouse

Auditing, performance metrics, and best practices for Progressive Web Apps
