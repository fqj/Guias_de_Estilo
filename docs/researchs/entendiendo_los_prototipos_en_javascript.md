# Entendiendo los prototipos en JavaScript

El objeto prototype de JavaScript genera confusión allá por donde pasa. Veteranos profesionales de JavaScript e incluso autores frecuentemente exhiben un entendimiento limitado de este concepto. Creo que gran parte del problema radica en la primera toma de contacto, casi siempre de la mano de new, constructor y la tan desorientadora propiedad prototype de las funciones. En realidad, el prototipado es un concepto notablemente sencillo. Para entenderlo mejor solo es necesario olvidarse de lo que hayamos aprendido sobre prototipos de constructores y empezar de nuevo desde los principios.

## Qué es un prototipo?

Un prototipo es un objeto del cual otros objetos heredan propiedades

## Cualquier objeto puede ser un prototipo?

Sí

## Qué objetos tienen prototipo?

Todo objeto tiene un prototipo por defecto. Como los prototipos son objetos, todos ellos tienen un prototipo también. Solo hay una excepción: el prototipo del objeto por defecto, al final de la cadena de prototipos. Hablaremos más de cadenas de prototipos más adelante.

## Ok, recapitulemos… qué decías que era un objeto?

Un objeto en JavaScript es una colección cualquiera de pares clave-valor. Si no es un valor primitivo (undefined, null, boolean, number o string) es un objeto.

Dices que todo objeto tiene un prototipo. Pero cuando escribo ({}).prototype obtengo undefined. Estás chalado?

Olvida todo lo que hayas aprendido sobre la propiedad prototype – es probablemente la mayor fuente de confusión sobre prototipos. El verdadero prototipo de un objeto es almacenado por la propiedad interna [[Prototype]]. ECMA 5 introduce el método accesor estándar Object.getPrototypeOf(object) que, a día de hoy, es implementado por Firefox, Safari, Chrome y IE9. Además, todos los navegadores excepto IE soportan el accesor no estándar __proto__. Con la salvedad de que sí que podemos pedir la propiedad prototype del constructor de un objeto.

var a = {}; 
 
// Falla en Opera o IE <= 8
Object.getPrototypeOf(a); // [object Object]
 
// Falla en IE
a.__proto__; // [object Object]
 
// En todos los navegadores
// (pero solo si el prototipo del constructor no ha sido reemplazado por uno que falle con Object.create)
a.constructor.prototype; // [object Object]
Vale, bien, pero false es un primitivo, así que por qué false.__proto__ devuelve un valor?

Cuando se le pide su prototipo a un primitivo se fuerza su forma en objeto.

// Functiona en IE <= 8 también, debido a doble negación
false.__proto__ === Boolean(false).__proto__; // true
Quiero usar prototipos para herencia. Qué tengo que hacer?

Rara vez tiene sentido fijar un prototipo para una sola y solo una instancia, ya que sería igualmente ineficiente añadirle propiedades a la instancia directamente. Supongo que si hemos creado un objeto con el que nos gustaría disfrutar de la funcionalidad de otro objeto pre-establecido, como Array, podríamos hacer algo así (en un navegador que soporte __proto__):

// Falla en IE <= 8
var a = {};
a.__proto__ = Array.prototype;
a.length; // 0
Pero el verdadero poder del prototipo sale a relucir cuando varias instancias comparten un prototipo común. Las propiedades del objeto prototipo se definen una vez pero son heredadas por todas las instancias que lo referencien. Las implicaciones en el rendimiento son tan obvias como significativas.

Así que aquí es donde entran en juego los constructores?

Sí. Los constructores proveen de un mecanismo convenientemente cross-browser de asignar un prototipo común al crear una instancia.

Antes de que des un ejemplo necesito saber de qué va todo eso de la propiedad constructor.prototype

Vale. En primer lugar, JavaScript no hace ninguna distinción entre constructores y otras funciones, así que cada función obtiene su propiedad prototype. Al mismo tiempo, cualquier cosa que no es una función, no tiene esa propiedad.

// una función que nunca se usará como constructor tiene una propiedad prototype de todos modos
Math.max.prototype; // [object Object]
 
// una función que se usará como constuctor tiene propiedad prototype
var A = function(name) {
  this.name = name;
}
A.prototype; // [object Object]
 
// Como Math no es una función, no tiene propiedad prototype
Math.prototype; // null
Así que tenemos una nueva definición: La propiedad prototype de una función es el objeto que será asignado como prototipo de todas las instancias creadas cuando ésta sea usada como un constructor. Es importante entender que la propiedad prototype de una función no tiene nada que ver con su verdadero prototipo.

// Falla en IE
var A = function(name) {
  this.name = name;
}
 
A.prototype == A.__proto__; // false
A.__proto__ == Function.prototype; // true - El prototipo de A es la propiedad prototype de su constructor
Un ejemplo, por favor?

Seguramente lo hayas visto cientos de veces, pero aquí está de nuevo, ahora quizá con algo más de perspectiva.

// Constructor. _this_ se devuelve como un nuevo objeto y su propiedad [[prototype]] interna será la propiedad prototype del constructor por defecto
var Circle = function(radius) {
  this.radius = radius;
  // La siguiente línea es implícit y la añado solo para ilustrar el caso
  // this.__proto__ = Circle.prototype;
}
 
// Aumentamos el prototipo por defecto de Circle aumentando, por lo tanto, el prototipo de cada instancia que generemos
Circle.prototype.area = function() {
  return Math.PI * this.radius * this.radius;
}
 
// Creamos dos instancias de un círculo y hacemos uso de su prototipo común
var a = new Circle(3), b = new Circle(4);
a.area().toFixed(2); // 28.27
b.area().toFixed(2); // 50.27
Esto está genial. Y si cambio el prototipo del constructor, incluso las instancias ya existentes tendrán acceso a la última versión, no?

Bueno… no en realidad. Si modifico la propiedad prototype existente se cumple, porque a.__proto__ es una referencia al objeto definido por A.prototype en el momento en el que se creo.

var A = function(name) {
  this.name = name;
}
 
var a = new A('alpha');
a.name; // 'alpha'
 
A.prototype.x = 23;
 
a.x; // 23
Pero si reemplazo la propiedad prototype con un nuevo objeto, a.__proto__ todavía referencia al objeto original.

var A = function(name) {
  this.name = name;
}
 
var a = new A('alpha');
a.name; // 'alpha'
 
A.prototype = {x: 23}
 
a.x; // null
Qué pinta tiene un prototipo por defecto?

Un objeto con una propiedad – el constructor.

var A = function() {};
A.prototype.constructor == A; // true
 
var a = new A();
a.constructor == A; // true (la propiedad constructor de a, heredada de su prototipo)
Qué tiene que ver instanceof con prototype?

La expresión a instanceof A devolverá true si el prototipo de a cae dentro de la misma cadena de prototipos que la propiedad prototype de A. Esto significa que podemos engañar a instanceof para que falle.

var A = function() {}
 
var a = new A();
 
a.__proto__ == A.prototype; // true - así que instanceof A devolverá true
a instanceof A; // true;
 
// liarla parda con el prototipo de a
a.__proto__ = Function.prototype;
 
// El prototipo de a ya no está cae dentro de la cadena de prototipos de la propiedad prototype de A
a instanceof A; // false
Y qué más puedo hacer con prototipos?

Recuerdas que he dicho que cada constructor tiene una propiedad prototype que usa para asignarle un prototipo a todas las instancias que genera? Bueno, esto aplica también a constructores nativos como Function y String. Extendiendo (no reemplazando!) esta propiedad podemos mejorar el prototipo de cada instancia del tipo de corresponda.

He usado esta técnica en muchos artículos previos para demostrar el aumento de funciones. Por ejemplo, la utilidad de trazado que introduje en un artículo anterior necesitaba que todas las instancias de String implementaran times, que devuelve una cadena replicada un número determinado de veces.

String.prototype.times = function(count) {
  return count < 1 ? '' : new Array(count + 1).join(this);
}
 
“hello!”.times(3); // “hello!hello!hello!”
“please...”.times(6); //"please...please...please...please...please...please..."
Dime más sobre cómo funciona la herencia con prototipos. Qué es una cadena de prototipos?

Como cada objeto y cada prototipo (menos uno) tiene un prototipo, podemos pensar en una sucesión de objetos enlazados unos con otros formando una cadena de prototipos. El final de la cadena siempre será el prototipo del objeto por defecto.

a.__proto__ = b;
b.__proto__ = c;
c.__proto__ = {}; // objeto por defecto
{}.__proto__.__proto__; // null
Los mecanismos de herencia prototípica son internos e implícitos. Cuando al objeto a se le pide que evalúe la propiedad foo, JavaScript recorre la cadena de prototipos (empezando por el propio objeto a), comprobando en cada eslabón de la cadena la presencia de la propiedad foo. En cuanto se encuentra foo se devuelve y si no, se devuelve undefined.

Qué hay de la asignación de valores?

La herencia prototípica no entra en juego cuando se asignan valores. a.foo = 'bar' siempre será asignado a a. Para asignar una propiedad a un prototipo necesitas tratar con el prototipo directamente.

Y esto es todo. Creo que dispongo de una opinión bastante bien formada sobre el cocepto de prototipado, pero mi opinión no es para nada la verdad absoluta. No dudes en avisarme de cualquier fallo o desacuerdo, por favor.

Dónde puedo encontrar más información sobre prototipos?

Te recomiendo este excelente artículo por Dmitry A. Soshnikov.