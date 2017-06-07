# PATRONES DE DISEÑO JAVASCRIPT

## PATRON MODULE
```
var modulo = (function () {
  var contador = 0;
 
  return {
    incrementar: function () {
      return counter++;
    },
 
    reset: function () {
      console.log( "valor de contador antes del reset: " + counter );
      counter = 0;
    }
  };
})();
 
// Incrementa el contador
modulo.incrementar();
 
// Imprime el valor del contador
modulo.reset();
```

var module = (function(){
    var variablePrivada = 23;
    var metodoPrivado = function suma(a,b) {
        return c = a + b;
    }
    return {
        propiedadPublica: 6,
        metodoPublico: function() {
            metodoPrivado(a,b);
        }
    } 
})();



## Patron Decorador, Decorator Pattern

Tradicionalmente, un decorator ( decorador) es un patrón que nos permite agregar comportamientos o funcionalidades a un objeto de forma dinámica( en tiempo de ejecución). Lo importante aquí es que dichas funcionalidades no son esenciales en el núcleo del objeto en sí, ya que esto nos motivaría a implementarlo en la clase padre en sí.

## ¿Cual es la diferencia entre el decorador y la herencia clásica? 

Por lo general las clases extienden sus funcionalidades a otras mediante la herencia, pero esta característica se realiza de forma estática ( en tiempo de compilación), con el decorator pattern nos garantizamos que esta extensión de funcionalidades se realice de forma dinámica. ¿Pero como se añaden funcionalidades dinámicamente? La idea de este patrón es la de encapsular dentro de un objeto llamado “decorador” las nuevas funcionalidades que se desean añadir al objeto junto con  la llamada al objeto en sí ( al constructor para obtener su instancia) además de poder realizar funciones adicionales antes y después de dicha llamada, hay que destacar también que el objeto que se ha “decorado” es único, es decir si instanciamos otro objeto del mismo tipo que el anterior el decorado no existirá.

 

## Cuándo utilizarlo

Hay varias situaciones en donde se aconseja implementar este patrón sobre una herencia clásica:

 * Cuando desees añadir responsibilidades de forma individual a objetos de forma dinámica.
 * Cuando quieras quitar  responsabilidades más adelante ( undecorate).
 * Cuando el extender subclases crece de forma que su manejo se complica.


 ```
 var Usuario = function(nombre) {
    this.nombre = nombre;
    this.saludo = function() {
        alert("Hola me llamo: " + this.nombre);
    };
}

var Decorador = function(usuario, calle, ciudad) {
    this.usuario = usuario;
    this.nombre = usuario.nombre;
    this.calle = calle;
    this.ciudad = ciudad;
    this.saludo = function() {
        alert("Nombre decorado: " + this.nombre + ", " + this.calle + ", " + this.ciudad);
    };
}

var usuario = new Usuario("Oscar");
usuario.saludo();

var decorador = new Decorador(usuario, "Chichon", "Madrid");
decorador.saludo();

```

# Factory

El patrón Factory se encarga de la creación de objetos (Fabrica de objetos) sin la necesidad de definir la clase exacta del objeto a ser creado. Este patrón se puede separar en 3 tipos de comportamiento según las necesidades:

### Simple Factory

Es la forma más sencilla de implementar este patrón, realmente es un objeto que encapsula la creación de otros objetos. A medida que tu Factory gana en complejidad ( esto es la posibilidad de crear más objetos de diferentes tipos) será necesario que parametrices el objeto para simplificar el mantenimiento. Veamos un ejemplo:

```
// Creamos nuestras clases que crearemos con el Factory
function Perro( params ) {
// setup o valores por default
    this.color = params.color || "Negro";
    this.raza = params.raza || "Labrador";
    this.nombre = params.nombre || "Buddy";
}

function Gato ( params ){
    this.color = params.color || "Blanco";
    this.cazador = params.cazador|| true;
    this.nombre = params.nombre || "Misu";
}

// Creamos el Factory
function AnimalFactory(){}

// y lo extendemos con prototype
AnimalFactory.prototype.createAnimal = function( params ) {
    if (params.tipo == 'perro') {
        return new Perro(params);
    } else if (params.tip o== 'gato') {
        return new Gato(params);
    }
};

Como vemos es muy sencillo, si queremos extender la creación de tipos de objetos simplemente los vamos añadiendo y preguntando por la propiedad params.tipo. Para llamarlo simplemente hacemos lo siguiente:

// creamos la instancia del Factory
var miFactory = new AnimalFactory();

// Si queremos un cachorro
var puppy = miFactory.createAnimal({tipo:"perro",raza:"Chihuahua",color:"Marron"});
console.log(puppy.raza);

//si queremos un lindo gatito
var minino = miFactory.createAnimal({tipo:"gato",nombre:"Chelsea"});
console.log(minino.nombre);

