# Traduccion Guia de actualización Angular1 a Angular2


https://angular.io/docs/ts/latest/guide/upgrade.html

ACTUALIZANDO Angular1.X

# Actualización paso a paso de una aplicación Angular1 hacia Angular2

Disponer de una aplicación desarrollada con Angular1 no implica que no podamos hacer uso de los beneficios que puede ofrecer Angular2. 
Angular2 posee herramientas para migrar una aplicación Angular1 hacia la plataforma Angular2.

Tendremos aplicaciónes mas sencillas de migrar, y hay procedimientos que podemos usar para facilitar el trabajo. Es posible preparar una aplicación desarrollada con Angular1 para migrar a Angular2, este proceso puede hacerse antes de empezar el proceso de migración. Este proceso de preparado tiene como finalidad tener código mas independiente y desacoplado, mas mantenible y preparado para las herramientas de desarrollo actuales. Esta preparación presentará no solo el beneficio de una actualización mas sencilla, sino que también generará una mejoram de nuestra aplicación Angular1.

La clave para lograr una migración satisfactoria es hacerlo de forma incremental, ejecutando los dos frameworks de forma paralela, migrando componente a componente, uno por vez. Esto nos habilita a migrar aplicaciónes de diferentes tamaños y complejidad, también para aplicaciónes grandes, evitando interrupciones en quienes consumen estas aplicaciónes, dado que este trabajo puede hacerse de forma colaborativa y en un periodo de tiempo. El `módulo upgrade` en Angular2 ha sido diseñado para llevar adelante actualizaciónes incrementales.

1. Preparación
    1. Usando la guía de estilos de Angular
    1. Usando un Module Loader
    1. Migrando a Typescript
    1. Usando Component Directives
1. Actualizando con el Upgrade Adapter
    1. Como funciona el Upgrade Adapter
    1. Inicializando aplicaciónes híbridas Angular1+2
    1. Usando componentes Angular2 en el código de Angular1
    1. Usando Component Directives de Angular1 en el código Angular2
    1. Proyectando contenido Angular1 en componentes Angular2
    1. Transcluding contenido de Angular2 en Component Directives de Angular1
    1. Hacer dependencias de Angular1 injectables en Angular2
    1. Hacer dependencias de Angular2 injectables en Angular1
1. Tutorial de actualización PhoneCat
    1. Migrar a Typescript
    1. Instalar Angular2
    1. Inicilización híbrida 1+2 PhoneCat
    1. Actualizar el servicio Phone
    1. Actualizar componentes
    1. Migrar al router Angular2 e inicilizar
    1. Despidiendo a Angular1
    1. Apéndice: Actualizando tests de PhonceCat

## Preparación
Hay muchas maneras de estructurar una aplicación Angular1. Cuando empezamos a migrar a Angular2 algunas formas de organzación presentarán ventajas para el trabajo a realizar. Estas son algunas técnicas y patrones que podemos aplicar justo antes de iniciar la migración.

### Usando la guía de estilos de Angular

La Guía de Estilos de Angular1 recopila patrones y prácticas para disponer de aplicaciónes mantenibles en Angular1. Contiene información de como escribir y organizar en código Angular, e igual de importante, que no se debe hacer al escribir y organizar la aplicación.

Angular2 es una evolución de Angular1, esta evolución ha sido tomando las mejores partes de Angular1. Angular2 es mucho mas que esto por supuesto, pero debemos tener en cuenta que siguiendo esta guía de estilos en una aplicación Angular1 estaremos en alineación y mejor estado hacia una futura versión de nuestra aplicación usando Angular2.

Hay un grupo especial de reglas que hacen mucho mas sencillo una migración incremental hacia Angular2 usando el módulo upgrade:

La regla 1 define que se debe tener un archivo por componente. Esto nos permite que podemos encontrar facilmente un componente y que sea mas sencillo navegar nuestro código. Y también permite que podamos migrar de Angular1 a Angular2 de uno en uno estos componentes. En este ejemplo cada controlador, cada servicio, componente y/o filtros esta definido en su propio archivo.

La regla de estructura de “Directorio por feature” y Modularidad define el mismo concepto en un nivel mayor de abstracción. Diferentes partes de la aplicación deben tener sus correspondientes directorios y módulos Angular.

Cuando una aplicación tiene esta estructura y organización, es posible realizar una migración de a una feature por vez. Si una aplicación no tiene esta organización, aplicar la guía de estilos de Angular es el mejor punto de partida. Esta es una buena recomendación no solo para aplicaciónes que se desee migrar.

### Usando un Module Loader

Al organizar la aplicación en un archivo por componente, generalmente terminamos con un número de muchos archivos pequeños. Esto es mucho mejor que tener pocos archivos de gran tamaño, pero no es muy eficiente cargar todos estos archivos en un html en los tags script. Especialmente cuando tenemos que mantener el orden en que son cargados. Esta es una importante razón para usar un module loader.

Usando un module loader como SystemJS, Webpack o Browserify nos permite hacer uso del sistem de módulos incluidos en Typescript or ES2015 en nuestras aplicaciónes. Podemos usar import y module.export. En ambos casos, el module loader se encarga de cargar cualquier código necesario y en el orden correspondiente.

Cuando instalamos nuestra aplicación en producción, el module loader se encargara del empaquetado correspondiente.

### Migrando a Typescript

Si parte de nuestro plan de actualización a Angular2 es utilizar Typescript, es recomendable incorporar lo necesario para la compilación antes de empezar la migración. Teniendo de esta manera una cosa menos que aprender y en la cual pensar durante la migración. También nos habilita a usar Typescript en nuestro código Angular1.

Dado que Typescript es un superset de ES2015, que es un superset de ECMAScript 5, “cambiar” a Typescript no requiere mas que instalar el compilador y renombrar los archivos de *.js a *.ts. Podemos hacer algunos pasos adicionales para otener un mayor beneficio:

Para aplicaciónes que usen un module loader Typescript imports y exports (que son en realidad ECMAScript 2015 imports y exports) se pueden ayudar para organizar el código en módulos.
Se pueden agregar los tipos a las funciones y variables de forma gradual para sumar el beneficio del checkeo de errores en el momento de la compilación, autocompletado y documentación.<br>

También se pueden agregar de forma gradual las nuevas funcionalidades de ES2015, como let, const, parametros default para funciones, etc.
Controladores y servicios pueden ser convertidos a clases. De esta manera se el código será mas cercano a la forma de Angular2, siendo mas fácil el proceso de migración.

### Usando Component Directives

En Angular2, los componentes son la unidad básica de la cual se construyen las interfaces de usuario. Las diferentes partes de una UI se definen a traves de componentes, para construir las vistas del sistema.

Esto también es posible en Angular1, usando component directives. Estas son directivas que contienen un controlador, la vista, inputs/outputs bindings; esta estructura es compartida en Angular2. Las aplicaciónes construidas usando component directives son mucho mas fáciles de migrar a Angular2 que otras aplicaciónes que hagan uso de ng-controller u ng-include y/o herencia de scope.

Para que un component directive sea compatible en Angular2 se debe aplicar la siguiente configuracion:

* restrict: 'e'. Los componentes se usan como elementos.
* scope: {} - un scope aislado. En Angular2 los componentes siempre estan aislados de su contexto, y debemos aplicar la misma regla en Angular1.
* bindingToController: {}. Los inputs y outputs de un componente deben ser asociados al controlador y no al $scope.
* controller y controllerAs. Un componente tiene su propio controlador.
* template o templateUrl. Un componente tiene su propia vista.

Los component directives pueden también usar los siguientes atributos:

* transclude: true, si el componente necesita hacer transclude de contenidos de algun origen.
* require, si el componente necesita comunicarse con el controlador de un componente padre.

Un component directive no debe usar los siguientes atributos:

* compile. Esto no estará soportado en Angular2.
* replace: true. En Angular2 nunca se reemplaza el componente por su template. Esto ya esta deprecado en Angular1.
* priority y terminal. Aunque pueden ser usados en Angular1, esto no es posible en Angular2; por lo tanto, no es recomendable hacer uso de estos atributos.

El siguiente código presenta un ejemplo en Angular1 de un component directive que cumple con el formato esperado para Angular2:
```
export function heroDetailDirective() {
  return {
    restrict: 'E',
    scope: {},
    bindToController: {
      hero: '=',
      deleted: '&'
    },
    template: `
      <h2>{{ctrl.hero.name}} details!</h2>
      <div><label>id: </label>{{ctrl.hero.id}}</div>
      <button ng-click="ctrl.onDelete()">Delete</button>
    `,
    controller: function() {
      this.onDelete = () => {
        this.deleted({hero: this.hero});
      };
    },
    controllerAs: 'ctrl'
  };
}
```
Angular1.5 incorporó una API para componentes que facilita la creación de este tipo de directivas. Se presentan los siguientes beneficios del uso de esta API:

* Requiere menos código repetitivo.
* Refuerza el uso de buenas prácticas como controllerAs.
* Tiene valores por defecto para attributos de la directiva como scope y restrict.
* Usando la API de componentes la directiva anterior resultaria en:
```
export const heroDetail = {
  bindings: {
    hero: '<',
    deleted: '&'
  },
  template: `
    <h2>{{$ctrl.hero.name}} details!</h2>
    <div><label>id: </label>{{$ctrl.hero.id}}</div>
    <button ng-click="$ctrl.onDelete()">Delete</button>
  `,
  controller: function() {
    this.onDelete = () => {
      this.deleted(this.hero);
    };
  }
};
```
Angular1.5 incorpora métodos al ciclo de vida del controlador de esta directiva de componentes $onInit(), $onDestroy() y $onChange(). Angular2 comparte esta arquitectura en el ciclo de vida del componente, presentando de esta manera una forma conveniente para su compatibilidad entre versiónes.

## Actualizando con el Upgrade Adapter
El módulo `upgrade` de Angular2 es una herramienta muy útil para realizar la actualización de una aplicación. Con esta herramienta podemos disponer de componentes Angular1 y Angular2 en una misma aplicación y hacerlos funcionar sin problemas. Esto nos permite hacer una actualización por partes dado que se podra tener una coexistencia de los dos frameworks durante el periodo de transición.

### Como funciona el Upgrade Adapter

La herramienta primaria del módulo de actualización se llama `UpgradeAdapter`. Este es un servicio híbrido que puede manejar código de Angular2 y Angular1.

Cuando usamos UpgradeAdapter en realidad estamos ejecutando las dos versiónes de Angular al mismo tiempo. Todo el código de Angular2 se ejecuta en el lado de Angular2 y el código de Angular1 en su correspondiente parte. Ambas versiónes disponen de una versión completa de la versión de Angular donde se esta ejecutando. No hay ningun emulador ejecutandose, con lo que el comportamiento esperando es el normal de una aplicación en cada uno de los frameworks.

Lo que sucede en un nivel general es que los componentes y servicios manejados por cada framework pueden comunicarse con los componentes y servicios del otro framework. Esto sucede en tres áreas principales: inyección de dependencias, el DOM, y la detección de cambios.

### Detección de cambios

La inyección de dependencias es central en Angular1 y Angular2, pero existen diferencias significativas en como funcionan en cada versión.

Angular1	                            Angular2
Los token de ID son siempre strings	 Los tokens pueden ser de diferentes tipos.
 	Generalmente son clases y también pueden ser strings.
Hay un unico inyector. Inclusive hay un arbol de herencia de inyectores,
en aplicaciónes multi-módulos,	con un inyector raiz para cada componente.
todo se incorpora a un solo namespace.	 

A pesar de estas diferencias, podemos tener interoperabilidad de la inyeccion de dependencias. El UpgradeAdapter resuelve las diferencias y se ocupa de que todo trabajoe sin problemas:

* Podemos hacer disponibles servicios escritos en Angular1 para inyección en Angular2 al actualizarlos. La misma instancia singleton de cada servicio es compartida en los dos frameworks. En Angular2 estos servicios estarán siempre en el inyector raiz y disponible para todos los componentes. Siempre tendrán tokens strings, los mismos tokens que tendrian en Angular1.

* También podemos hacer disponibles los servicios en Angular2 para ser inyectados en Angular1 mediante una degradación. Sólo los servicios que estén definidos en el inyector raiz de Angular2 pueden ser degradados. De nuevo, la misma instancia del servicio Singleton es compartida entre los dos frameworks. Se define un token string de forma explícita que puede ser usado en Angular1.


### Componentes y el DOM

En el DOM de una aplicación híbrida encontraremos componentes y directivas tanto de Angular1 como de Angular2. Estos componentes se comunican entre si haciendo uso de los entradas y salidas de los bindings de cada framework respectivamente, por medio del puente provisto por el UpgradeAdapter. También pueden comunicarse por medio de la inyección de dependencia descrita anteriormente.

Hay dos puntos principales para entender que es lo que sucede en el DOM de una aplicación híbrida:

* Cada elemento en el DOM pertenece solamente a uno de los dos frameworks. El otro framework no conoce de él. Si el dueño de un elemento es Angular1, Angular2 lo trata como si no existier, y viceversa.
* La raiz de una aplicación es siempre un template de Angular1.

Por lo tanto una aplicación híbrida comienza como una aplicación Angular1, y es Angular1 es quien procesa el raiz de su template. Ese componente puede entonces ser manejado por Angular2, y puede hacer uso de cualquier número de componentes y directivas de Angular2.

Mas allá de esta característica inicial, podemos hacer uso de cualquier combinación de elementos Angular1 o Angular2 . Siempre vamos a cruzar los límites de cualquier de los dos frameworks en una de las dos siguientes formas:

* Usando un componente del otro framework: Una template de Angular1 usando un componente Angular2, una template Angular2 usando un componente Angular1.
* Por medio de transcluding o proyectando contenido del otro framework. El UpgradeAdapter vincula los conceptos relacionados de la transclusión en Angular1 en la proyección de contenido Angular2 juntos.


En calquier parte que hagamos uso de un componente que pertenezca al otro framework, consideremos que usamos un componente de Angular2 desde Angular1 de la siguiente manera:

```
  <ng2-component></ng2-component>
```
El elemento DOM <ng2-component> seguirá siendo un elemento manejado por Angular1, debido a que esta definido en un template de Angular1. Esto significa que se puede aplicar cualquier otra directiva Angular1 al elemento.

### Detección de cambios

La detección de cambios en Angular1 se trata unicamente de scope.$apply()`` . Después de que ocurre un evento, se ejecuta `scope.$apply()`. Esto puede ser ejecutado de forma automática por el framework, o en algunos casos de forma manual en nuestro código. Este es el proceso que actualiza el bindings de los datos.

En Angular2 las cosas son diferentes. Mientras que la detección de cambio ocurre después de cada evento, ninguno tiene que llamar a scope.$apply() para que suceda. Esto se debe a que todo en Angular2 es ejecutado dentro de algo llamado Angular Zone. Angular siempre conoce cuando el código finaliza, por lo tanto conoce cuando debe ejecutar la detección de cambios. El código no debe llamar a scope.apply() o nada parecido por si mismo.

En el caso de aplicaciónes híbridas, el UpgradeAdapter hace de puente entre las estrategias de Angular1 y Angular2. Esto es lo que sucede:

Todo lo que sucede en la aplicación se ejecuta dentro de Angular2 zone. Esto es válido tanto para un evento originado en un código Angular1 o Angular2. La Angular2 zone dispara  la detección de cambio después de cada evento.
El UpgradeAdapter invocará $rootScope.$apply() de Angular1 después de cada ejecución de Angular zone. Esto también dispara la detección de cambio de Angular1 después de cada evento.

En la práctica, esto significa que no tenemos la necesidad de llamar a $apply() en nuestro código, no importa si es desde Angular1 o Angular2. El UpgradeAdapter realiza este trabajo por nosotros. Sin embargo podemos llamar a $apply() desde nuestro código, haciendo que no sea necesario que eliminemos cualquier llamada que tengamos en nuestro código. Solo debemos tener presente que estas llamadas no tendran ningun efecto en una aplicación híbrida.

Cuando degradamos un componente de Angular2 y lo usamos en Angular1, los inputs del componente seráns inspecccionados usando la detección de cambios de Angular1. Cuando esos inputs cambian, las propiedades que correspondan del componente se setean. También podemos intervenir en los cambios implementando la interfaz OnChanges en el componente, de la misma manera que si no fuera degradado.

De la misma manera, cuando actualizamos un componente Angular1 y lo usamos en Angular2, todos los bindings definidos por la directiva componente en el scope (o bindingToController) serán enlazado a la detección de cambios de Angular2. Serán tratados como inputs normales de Angular2 y seteados al scope (o controlador) cuando cambian.

### Usando el UpgradeAdapter con Angular2 NgModules

Angular1 y Angular2 tienen su concepto propio de módulos para ayudar a organizar la aplicación en bloques cohesivos de funcionalidad.

Los detalles de cada uno difieren en arquitectura e implementación. En Angular1, agregamos assets a angular.module. En Angular2, creamos clases a las que se le aplican el decodador NgModule que describen el metadata de Angular. Las diferencias parten desde ahí.

En una aplicación híbrida se ejecutan las dos versiónes de Angular al mismo tiempo. Esto significa que necesitamos al menos un módulo de cada versión. Usaremos el módulo de Angular2 en el UpgradeAdapter mientras que el módulo de Angular1 para inicilizar. Veamos como.

Mas informacion acerca de Angular2 modules en NgModule guide

## Inicializando aplicaciónes híbridas Angular1+2

El primer paso para actualizar una aplicación usando el UpgradeAdapter es inicializarla como una aplicación híbrida que soporte Angular1 y Angular2.

Una aplicación Angular1 pura puede inicializarse de una de las dos maneras: Usando la directiva ng-app en alguna parte del html, o llamando a angular.bootstrap desde JavaScript. En Angular2, solo la segunda forma es posible. Este es también el caso de una aplicación híbrida. Por lo tanto es un buen paso transformar la aplicación Angular1 para usar JavaScript bootstrap antes de cambiar a que sea una aplicación híbrida.

Supogamos que tenemos una aplicación que utiliza ng-app de la siguiente manera:

```
<!DOCTYPE HTML>
<html>
  <head>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.5.3/angular.js"></script>
    <script src="app/1-ng-app/app.module.js"></script>
  </head>
  <body ng-app="heroApp" ng-strict-di>
    <div id="message" ng-controller="MainCtrl as mainCtrl">
      {{ mainCtrl.message }}
    </div>
  </body>
</html>
```
Podemos borrar las directivas ng-app y ng-strict-di del html, y en su lugar llamar angular.bootstrap desde Javascript, que terminará en algo de este estilo:

````
angular.bootstrap(document.body, ['heroApp', {strictDi: true}]);
```

Ahora podemos introducir Angular2 al proyecto. Inspirado en las instrucciones provistas por QuickStart, se puede copiar selectivamente usando el repositorio QuickStart github.

El paso siguiente es crear el archivo app.module.ts y la clase NgModule:

```
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
@NgModule({
  imports: [ BrowserModule ]
})
export class AppModule {}
```

Este mínimo uso de NgModule importa BrowserModule, el módulo que importa toda app Angular basada en el uso de un browser. Ese método toma los mismos argumentos que angular.bootstrap:
```
import { UpgradeAdapter } from '@angular/upgrade';
/* . . . */
const upgradeAdapter = new UpgradeAdapter(AppModule);
upgradeAdapter.bootstrap(document.body, ['heroApp'], {strictDi: true});

```
Enhorabuena!!, ya estamos ejecutando una aplicación híbrida Angular1+2! El código existente en Angular1 funciona igual que antes y está lista para usar Angular2.

Nótese que, distinto de angular.bootstrap, el upgradeAdapter.bootstrap se ejecuta de forma asíncrona. La aplicación no es ejecutada de forma inmediata. Un tiempo debe pasar después de que la inicialiazion se llamó.
Cuando empecemos a migrar componentes a Angular2, usaremos el UpgradeAdapter para otras táreas adicionales que solo la inicializacion. Es importante usar la misma instancia del adaptador en toda la aplicación, dado que guarda informacion acerca de lo que está ocurriendo en la apliación. Será util tener un módulo para compartir la instancia de UpgradeAdapter en el proyecto:

```
file: upgrade_adapter.ts
import { UpgradeAdapter } from '@angular/upgrade';
export const upgradeAdapter = new UpgradeAdapter(AppModule);
```
Esta instancia compartida puede ser obtenida en un módulo cuando la necesitamos:
```
import { upgradeAdapter } from './upgrade_adapter';
/* . . . */
upgradeAdapter.bootstrap(document.body, ['heroApp'], {strictDi: true});
```

### Usando componentes Angular2 en el código de Angular1

Una vez que estamos ejecutando nuestra aplicación híbrida, podemos empezar el proceso gradual de actualización. Esto puede ser un componente completamente nuevo o un componente que fuera parte de Angular1 anteriormente y que se reescriba en Angular2.

Digamos que tenemos un componente en Angular2 que muestra informacion de un Hero:

```
import { Component } from '@angular/core';
@Component({
  selector: 'hero-detail',
  template: `
    <h2>Windstorm details!</h2>
    <div><label>id: </label>1</div>
  `
})
export class HeroDetailComponent {
}
```

Si queremos usar este componente desde Angular1, necesitamos degradarlo utilizando el upgrade adapter. Lo que obtenemos cuando hacemos esto es una directiva Angular1, que podemos registrar en nuestro módulo Angular1:

```
import { HeroDetailComponent } from './hero-detail.component';
/* . . . */
angular.module('heroApp', [])
  .directive('heroDetail', upgradeAdapter.downgradeNg2Component(HeroDetailComponent));
```
Dado que HeroDetailComponent es un componente Angular2, necesitamos agregarlo en las declarations en AppModule.

```
import { HeroDetailComponent } from './hero-detail.component';
@NgModule({
  imports: [ BrowserModule ],
  declarations: [ HeroDetailComponent ]
})
export class AppModule {}
```
Todos los componentes, directivas y pipes en Angular2 deben ser incluidos en NgModule.
Obtendremos como resultado una directiva Angular1 llamada heroDetail, que podemos usar de la misma forma que cualquier otra directiva en los templates de Angular1.

```
<hero-detail></hero-detail>
```

Nótese que esta directiva en Angular1 es una directiva de elemento (restrict: 'E') llamada heroDetail. Una directiva de elemento en Angular1 se usa con un elemento que sea equivalente a su nombre. El metadata selector del degradado del componente de Angular2 es ignorado.
Muchos componentes no son tan simples como este, por supuesto. Muchos de ellos tienen inputs y outpus que los conectan con el mundo exterior. Un componente hero-detail en Angular2 con inputs y outputs luce de la siguiente manera:

```
import { Component, EventEmitter, Input, Output } from '@angular/core';
import { Hero } from '../hero';
@Component({
  selector: 'hero-detail',
  template: `
    <h2>{{hero.name}} details!</h2>
    <div><label>id: </label>{{hero.id}}</div>
    <button (click)="onDelete()">Delete</button>
  `
})
export class HeroDetailComponent {
  @Input() hero: Hero;
  @Output() deleted = new EventEmitter<Hero>();
  onDelete() {
    this.deleted.emit(this.hero);
  }
}

```
Estos inputs y outputs pueden ser provistos desde un template Angular1, y el UpgradeAdapter realiza el trabajo de hacer los bindings correspondientes:

```
<div ng-controller="MainController as mainCtrl">
  <hero-detail [hero]="mainCtrl.hero"
               (deleted)="mainCtrl.onDelete($event)">
  </hero-detail>
</div>
```

Nótese de que a pensar de que estamos en un template de Angular1, estamos usando la sintaxis de atributos de Angular2 para los bindings de inputs y ouputs. Esto es un requerimiento para los componentes degradados. Las expresiones utilizadas son expresiones de la forma de Angular1.

Se debe usar KEBAB-CASE para los atributos de un componente degradado.

Hay una excepcion especial para usar la regla de la sintaxis de los atributos de un componente Angular2. Es aplicable a los nombres de los inputs y outputs que consisten en multiples palabras. En Angular2 usamos camelCase:

```
[myHero]="hero"
```

pero cuando lo usamos desde un template de Angular1, necesitmos usar kebab-case:

```
[my-hero]="hero"
```

La variables $event puede ser usada en los outputs para acceder al objeto que fue emitido. En este caso será el objeto Hero, dado que eso fue enviado a this.deleted.emit().

Dado que esto es un template de Angular1, podemos seguir usando directivas Angular1 en el elemento, mismo si tiene atributos bideados en él. Podemos por ejemplo hacer copias del elemento usando ng-repeat:

```
<div ng-controller="MainController as mainCtrl">
  <hero-detail [hero]="hero"
               (deleted)="mainCtrl.onDelete($event)"
               ng-repeat="hero in mainCtrl.heroes">
  </hero-detail>
</div>
```

### Usando Component Directives de Angular1 en el código Angular2


Entonces, podemos crear un componente en Angular2 y usarlo desde Angular1. Esto es muy útil cuando comenzamos nuestra migración para componentes de bajo nivel y luego vamos migrando el resto. Pero en algunos casos es conveniente hacer las cosas de forma inversa: comenzar por componentes de alto nivel y luego ir hacia abajo. Esto también puede hacerse usando el UpgradeAdapter. Podemos actualizar directivas de Angular1 y usarlas en Angular2.

No todo tipo de directivas Angular1 pueden ser actualizadas. El tipo de directiva actualizable es la de tipo componente, con las caracteristicas descriptas anteriormente. La mejor forma de asegurar compatibilidad es utilidad la API de componentes de Angular1.5.

Un ejemplo simple de la actualización de un componente es uno con unicamente un controlador y una template:

```
export const heroDetail = {
  template: `
    <h2>Windstorm details!</h2>
    <div><label>id: </label>1</div>
  `,
  controller: function() {
  }
};
```

Podemos actualizar este componente a Angular2 usando el método upgradeNg1Component de UpgradeAdapter. Este método necesita el nombre del componente Angular1 y devuelve una clase componente en Angular2. Debemos inlcuir esta clase en NgModule como cualquier otro componente Angular2:

```
const HeroDetail = upgradeAdapter.upgradeNg1Component('heroDetail');
@NgModule({
  imports: [ BrowserModule ],
  declarations: [ ContainerComponent, HeroDetail ]
})
export class AppModule {}
```

Un componente actualizado siempre tiene un elemento selector, que es basado en el nombre original de la directiva componente en Angular1.

* Definición de Binding	Sintaxis del template:

```
Binding de Atributo	myAttribute:	
 	‘@myAttribute’	 
Binding de Expresion	myOutput:	<my-component (myOutput)=”action()”>
 	‘&myOutput’	 
Binding de una via	myValue:	<my-component [myValue]=”anExpression”>
 	‘<myValue’	 
Binding de dos vias	myValue:	Binding de dos vias: <my-component [(myValue)]=”anExpression”>
 	‘=myValue’	En la mayoria de los casos binding de una via es suficiente,
 	[myValue]=”anExpression”>.	 
```

Como ejemplo, supongamos que tenemos una directiva-componente en Angular1 que sea el detalle de un Hero:

```
export const heroDetail = {
  bindings: {
    hero: '<',
    deleted: '&'
  },
  template: `
    <h2>{{$ctrl.hero.name}} details!</h2>
    <div><label>id: </label>{{$ctrl.hero.id}}</div>
    <button ng-click="$ctrl.onDelete()">Delete</button>
  `,
  controller: function() {
    this.onDelete = () => {
      this.deleted(this.hero);
    };
  }
};
```

Podemos actualizar este componente a Angular2, y proveer el input y el output usando la sintaxis de template de Angular2:

```
import { Component } from '@angular/core';
import { Hero } from '../hero';
@Component({
  selector: 'my-container',
  template: `
    <h1>Tour of Heroes</h1>
    <hero-detail [hero]="hero"
                 (deleted)="heroDeleted($event)">
    </hero-detail>
  `
})
export class ContainerComponent {
  hero = new Hero(1, 'Windstorm');
  heroDeleted(hero: Hero) {
    hero.name = 'Ex-' + hero.name;
  }
}
```

### Proyectando contenido Angular1 en componentes Angular2

Cuando usamos un componente degradado de Angular2 desde una template Angular1 , puede presentarse la necesidad de hacer transclude en él. Esto también es posible. Debido a que no existe nada con el concepto de transclude en Angular2 , tenemos un concepto similar llamado proyección de contenido. El UpgradeAdapter permite que las dos funcionalidades puedan interoperar entre si.

Un componente de Angular2 que soporta proyeccion de contenido utiliza el tag <ng-content>. Ejemplo:
```
import { Component, Input } from '@angular/core';
import { Hero } from '../hero';
@Component({
  selector: 'hero-detail',
  template: `
    <h2>{{hero.name}}</h2>
    <div>
      <ng-content></ng-content>
    </div>
  `
})
export class HeroDetailComponent {
  @Input() hero: Hero;
}
```

Cuando usamos este componente desde Angular1, podemos proveer de contendidos hacia él. De la misma manera que puede usarse el transclude en Angular1, se incluye el contenido en el tag de Angular2.
```
<div ng-controller="MainController as mainCtrl">
  <hero-detail [hero]="mainCtrl.hero">
    <!-- Everything here will get projected -->
    <p></p>
  </hero-detail>
</div>
```
Cuando el contenido de Angular1 es proyectado dentro de un componente de Angular2, todavia se encuentra en “tierra de Angular1” y es manejado por Angular1.

### Transcluding contenido de Angular2 en Component Directives de Angular1

De la misma forma que podemos proyectar contenido de Angular1 dentro de componentes de Angular2, podemos hacer transclude de contenido de Angular2 dentro de Angular1, siempre que estemos haciendo uso de versiónes actualizadas de estos.

Cuando una directiva de componente soporta transcluding, puede utilizar el tag de directive ng-transclude para marcar el punto de transcluding.

```
export const heroDetailComponent = {
  bindings: {
    hero: '='
  },
  template: `
    <h2>{{$ctrl.hero.name}}</h2>
    <div>
      <ng-transclude></ng-transclude>
    </div>
  `
};
```

Esta directiva necesita tener transclude: true habilitado. Está habilitado por default en la API de directiva componente en Angular1.5.
Al actualizar este componente y usándolo desde Angular2, podemos popular el tag del componente con contenidos que sera usado con transluding:

```
import { Component } from '@angular/core';
import { Hero } from '../hero';
@Component({
  selector: 'my-container',
  template: `
    <hero-detail [hero]="hero">
      <!-- Everything here will get transcluded -->
      <p>{{hero.description}}</p>
    </hero-detail>
  `
})
export class ContainerComponent {
  hero = new Hero(1, 'Windstorm', 'Specific powers of controlling winds');
}
```

### Hacer dependencias de Angular1 inyectables en Angular2

Cuando ejecutamos una aplicación híbrida, se presentan casos donde debemos poder hacer uso de las dependencias de Angular1 inyectable en el código de Angular2. Eso puede ser porque tenemos parte de nuestra logica en servicios de Angular1, o necesitamos algun servicio que solo existe en Angular1 como $location o $timeout.

En estas situaciones, es posible actualizar un provider de Angular1 a Angular2. Esto habilita inyectarlos en alguna parte de Angular2. Por ejemplo, podemos tener un servicio HeroesService en Angular1:

```
import { Hero } from '../hero';
export class HeroesService {
  get() {
    return [
      new Hero(1, 'Windstorm'),
      new Hero(2, 'Spiderman')
    ];
  }
}
```

Podemos actualizar el servicio usando upgradeNg1Provider de UpgradeAdapter dando el nombre del servicio. Esto agrega el servicio en el raiz del injector de Angular2.

```
angular.module('heroApp', [])
  .service('heroes', HeroesService)
  .directive('heroDetail',
    upgradeAdapter.downgradeNg2Component(HeroDetailComponent));
upgradeAdapter.upgradeNg1Provider('heroes');
```

Con esta adaptación podemos inyectarlo en Angular2 usando el token string que equivale al nombre original en Angular1:

```
import { Component, Inject } from '@angular/core';
import { HeroesService } from './heroes.service';
import { Hero } from '../hero';
@Component({
  selector: 'hero-detail',
  template: `
    <h2>{{hero.id}}: {{hero.name}}</h2>
  `
})
export class HeroDetailComponent {
  hero: Hero;
  constructor(@Inject('heroes') heroes: HeroesService) {
    this.hero = heroes.get()[0];
  }
}
```

En este caso hemos actualizado una clase servicio, que tiene el beneficio de user la anotación TypeScript cuando lo inyectamos. Mientras que esto no afecta a como es manejada la inyección, habilita también el beneficio del chequeo estatico de tipos. A pesar de que no es requerido, todo servicio, factoría o proveedor en Angular1 puede ser actualizado.

### Hacer dependencias de Angular2 injectables en Angular1

De forma adicional a la actualización de las dependencias de Angular1, podemos degradar una dependencia Angular2, para poder usarla en Angular1. Esto es ítil cuando empezamos a migrar servicios a Angular2 o a crear nuevos servicios en Angular2 mientras que seguimos teniendo componentes escritos en Angular1.

Por ejemplo, tenemos un servicio en Angular2 llamado Heroes:

```
import { Injectable } from '@angular/core';
import { Hero } from '../hero';
@Injectable()
export class Heroes {
  get() {
    return [
      new Hero(1, 'Windstorm'),
      new Hero(2, 'Spiderman')
    ];
  }
}
```

Nuevamente, como otros componentes en Angular2, registramos este proveedor en NgModule en la lista de proveedores.

```
import { Heroes } from './heroes';
@NgModule({
  imports: [ BrowserModule ],
  providers: [ Heroes ]
})
export class AppModule {}
```

Ahora podemos enmascarar Heroes de Angular2 en una funciónon de factoría en Angular1 usando upgradeAdapter.downgradeNg2Provider() y conectar la factoría en un módulo de Angular1. El nombre de la dependencia en Angular1 depende de uno:

```
angular.module('heroApp', [])
  .factory('heroes', upgradeAdapter.downgradeNg2Provider(Heroes))
  .component('heroDetail', heroDetailComponent);
```

después de esto, el servico es inyectable en cualquier parte de nuestro código de Angular1:

```
export const heroDetailComponent = {
  template: `
    <h2>{{$ctrl.hero.id}}: {{$ctrl.hero.name}}</h2>
  `,
  controller: ['heroes', function(heroes: Heroes) {
    this.hero = heroes.get()[0];
  }]
};
```

## Tutorial de actualización PhoneCat

En esta sección veremos un ejemplo completo de la actualización de una aplicación usando el módulo upgrade. La aplicación con la que vamos a trabajar es Angular PhoneCat del tutorial original de Angular1, donde muchos usuarios iniciaron sus aventuras en angular. Vamos a ver como migramos esta aplicación a Angular2.

Durante el proceso iremos aprendiendo como aplicar los pasos mas importantes de la guía de preparación en práctica: Alinearemos la aplicación con Angular2 y comenzaremos a usar TypeScript.

Para seguir este tutorial, se debe clonar el repositorio de angular-phonecat y aplicar los pasos a medida que se avanza.

Esta es la estructura inicial:

```
angular-phonecat
-- bower.json
-- karma.conf.js
-- package.json
-- app
-- -- core
-- -- heckmark
-- -- -- checkmark.filter.js
-- -- -- checkmark.filter.spec.js
-- -- phone
-- -- -- phone.module.js
-- -- -- phone.service.js
-- -- -- phone.service.spec.js
-- -- core.module.js
-- -- phone-detail
-- -- -- phone-detail.component.js
-- -- -- phone-detail.component.spec.js
-- -- -- phone-detail.module.js
-- -- -- phone-detail.template.html
-- -- phone-list
-- -- -- phone-list.component.js
-- -- -- phone-list.component.spec.js
-- -- -- phone-list.module.js
-- -- -- phone-list.template.html
-- -- img
-- -- -- ...
-- -- phones
-- -- -- ...
-- -- app.animations.js
-- -- app.config.js
-- -- app.css
-- -- app.module.js
-- -- index.html
-- e2e-tests
-- -- protractor-conf.js
-- -- scenarios.js 
```

Este es un buen punto de inicio. El código usa la API de componentes de Angular1.5 y la organización sigue la guía de estilos de Angular1, el cual es un paso importante de la preparación antes de una migración satisfactoria.

Cada componente, servicio y filtro está definido en su propio archivo, como describe la regla 1.
Los módulos core, phone-detail y phone-list están cada uno en su propia carpeta. Esos subdirectorios contienen el código JavaScript y los templates html que pertenecen a cada feature. Esto va en línea con las reglas de Folders-by-Feature Structure y Modularity.
Los tests unitarios están completos para cada feature y son sencillos de ubicar como describe la organizacion de los tests.

### Migrar a Typescript

Dado que vamos a usar TypeScript para desrrollar la aplicación en Angular2, el primer paso es intalar el compilador antes de actualizar.

Iremos migrando los paquetes definidos con Bower en favor de NPM. Instalaremos las nuevas dependencias usando NPM, brindando la posibilidad al final de borrar Bower.

Comencemos instalando TypeScript en el proyecto:

```
npm i typescript --save-dev
```

Agreguemos un script de ejecución para el compilador de TypeScript tsc a package.json:
```
{
  "scripts": {
    "tsc": "tsc",
    "tsc:w": "tsc -w"
  }
}
```
Ahora podemos instalar la definición de tipos de las librerias existentes que no estan incluidas en los tipos preempaquetados: Angular1 y Jasmine Unit tests framework.

```
npm install @types/jasmine
            @types/angular
            @types/angular-animate
            @types/angular-cookies
            @types/angular-mocks 
            @types/angular-resource 
            @types/angular-route 
            @types/angular-sanitize --save-dev
```

También debemos configurar TypeScript para que tenga conocimiento de nuestro proyecto. Agregaremos un archivo tsconfig.json en el directorio del proyecto, de la misma manera que lo hicimos en Quickstart. Esto instruye al compilador de TypeScript como interpretar nuestro código fuente.

```
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "moduleResolution": "node",
    "sourceMap": true,
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "removeComments": false,
    "noImplicitAny": false,
    "suppressImplicitAnyIndexErrors": true
  }
}
```

Le indicamos al compilador de TypeScript compilar los archivos a ES5 agrupados en módulos CommonJS.

Podemos ahora inicializar el compilador de TypeScript desde la línea de comandos. Pondremos a observar los archivos .ts y compilarlos a JavaScript on the fly. Esos archivos compilados .js son cargados enr el navegador por SystemJS. Este es un procesos que queremos que se ejecute en segundo plano de forma automática.

```
npm run tsc:w
```

El siguiente paso que se realiza será convertir nuestros archivos JavaScript en TypeScript. Dado que TypeScript es un superset de ECMAScript 2015, que es un superset de ECMAScript 5, simplemente puedes renombrar nuestros archivos de .js a .ts y todo funcionará de forma habitual. Cada vez que el compilador de TypeScript se ejecute generará los archivos .js correspondientes que son los que son ejecutados. Si iniciamos el servidor http con `npm start`, deberiamos ver la aplicación funcionando en el navegador.

Ahora que tenemos TypeScript funcionando, podemos empezar a beneficionarnos de sus funcionalidades.

TypeScript es un superset de ES2015. Cualquier aplicación que se escribió previamente en ES5 - como fue el caso de PhoneCat - puede empezar a incorporar los beneficios de ES2015. Este incluye funcionalidades como let y const, arrow functions, parametros default, y asignaciones destructivas.

Otra cosa que podemos hacer es type safety a nuestro código. Esto ha sido parcialmente agregado de forma automática cuando agregamos los tipos para Angular1. TypeScript chequea de forma automática que estemos llamando a la API de forma correcta cuando hacemos cosas como registrar componentes en los módulos de Angular.

Pero también podemos agregar type annotations para agregar un mayor beneficio a nuestro sistema usando TypeScript. Por ejemplo podemos anotar el filtros checkmark para verificar de forma explicita los argumentos booleanos. Esto presenta de forma mas clara la finalidad de filter.
```
angular.
  module('core').
  filter('checkmark', function() {
    return function(input: boolean) {
      return input ? '\u2713' : '\u2718';
    };
  });
```

En el servicio Phone podemos usar la anotacion explícita en la dependencia $resource con angular.resource.IResourceService - Un tipo definido en Angular1 typings.
```
angular.
  module('core.phone').
  factory('Phone', ['$resource',
    function($resource: angular.resource.IResourceService) {
      return $resource('phones/:phoneId.json', {}, {
        query: {
          method: 'GET',
          params: {phoneId: 'phones'},
          isArray: true
        }
      });
    }
  ]);
```

Podemos aplicar el mismo trabajo en el archivo de configuración de las rutas app.config.ts donde usamos los servicios location y route. Agregando las anotaciones correspondientes en TypeScript podremos verificar si llamamos a las API con los correspondientes argumentos.
```
angular.
  module('phonecatApp').
  config(['$locationProvider', '$routeProvider',
    function config($locationProvider: angular.ILocationProvider,
                    $routeProvider: angular.route.IRouteProvider) {
      $locationProvider.hashPrefix('!');
      $routeProvider.
        when('/phones', {
          template: '<phone-list></phone-list>'
        }).
        when('/phones/:phoneId', {
          template: '<phone-detail></phone-detail>'
        }).
        otherwise('/phones');
    }
  ]);
```

Angular1 type definitions que se utiliza no son oficialmente mantenidas por el equipo de Angular, pero son muy completas. Es factible crear una aplicación Angular1 con soporte completo de tipos anotados haciendo uso de esta librearia.
Si este es uno de nuestros objetivos, es una buena idea activar `noImplicityAny` como una opcion de configuracion en tsconfig.ts. Esto indicará que TypeScript muestre una advertencia para cualquier parte de nuestra aplicación que no tenga las anotaciones de tipos incorporados. Esto nos puede dar una guia acerca de la evolucion del soporte de tipos anotados en nuestro proyecto.
Otra funcionalidad de TypeScript que podemos usar son las clases. Eso es el motivo por el cual estan las clases en ES2015/TypeScript, esto significa que podemos conectar nuestras clases como controladores de componentes y Angular1 podrá usarlo.
```
class PhoneListController {
  phones: any[];
  orderProp: string;
  query: string;
  static $inject = ['Phone'];
  constructor(Phone: any) {
    this.phones = Phone.query();
    this.orderProp = 'age';
  }
}
angular.
  module('phoneList').
  component('phoneList', {
    templateUrl: 'phone-list/phone-list.template.html',
    controller: PhoneListController
  });
```

Lo que antes se hacia en el controlador, ahora es una tárea que se usa en el constructor de la clase. Las anotaciones de la inyección de dependencias están asociadas a la clase que usa una propiedad estática `$inject`. En tiempo de ejecución esto se transforma en la propiedad `PhoneListController.$inject`.

La clase declara de forma adicional tres miembros: el array de teléfonos, el nombre de key actual, y el parámetro de búsqueda. Estas son todas las cosas que teniamos asociadas al controlador anteriormente pero no habiamos declarado de forma explícita. El último de estos no es utilizado en el código TypeScript dado que solo es referenciado en el template, pero por un motivo de claridad es bueno definir todos los miembros que nuestro controlador tendrá.

En el controlador de detalle tendremos dos miembros: Uno para el teléfono que el usuario está viendo y otro para la url que se está mostrando:

```
class PhoneDetailController {
  phone: any;
  mainImageUrl: string;
  static $inject = ['$routeParams', 'Phone'];
  constructor($routeParams: angular.route.IRouteParamsService, Phone: any) {
    let phoneId = $routeParams['phoneId'];
    this.phone = Phone.get({phoneId}, (phone: any) => {
      this.setImage(phone.images[0]);
    });
  }
  setImage(imageUrl: string) {
    this.mainImageUrl = imageUrl;
  }
}
angular.
  module('phoneDetail').
  component('phoneDetail', {
    templateUrl: 'phone-detail/phone-detail.template.html',
    controller: PhoneDetailController
  });
```
La tárea que antes se hacía en la función controlador, ahora se hace en el constructor de la función. Las anotaciones de dependencia de inyección son asociadas a la clase usando la propiedad estática $inject. En tiempo de ejecución esto se convierte en una propiedad PhoneListController.$inject.

La clase declara tres miembros adicionales: un array de teléfonos, el nombre de la clave de ordenamiento, y el parametro de búsqueda. El último de estos tres no es usado en el código TypeScript y solo es referenciado en el template, pero con el objetivo de la mayor claridad definimos todos los miembros que nuestro controlador tendrá.

En el controlador de detalle de Phone tendremos dos miembros: uno para el Phone que esta siendo utilizado por el usuario y otro para la URL de la image utilizada:

```
class PhoneDetailController {
  phone: any;
  mainImageUrl: string;
  static $inject = ['$routeParams', 'Phone'];
  constructor($routeParams: angular.route.IRouteParamsService, Phone: any) {
    let phoneId = $routeParams['phoneId'];
    this.phone = Phone.get({phoneId}, (phone: any) => {
      this.setImage(phone.images[0]);
    });
  }
  setImage(imageUrl: string) {
    this.mainImageUrl = imageUrl;
  }
}
angular.
  module('phoneDetail').
  component('phoneDetail', {
    templateUrl: 'phone-detail/phone-detail.template.html',
    controller: PhoneDetailController
  });
```

Esto hace que el código de nuestro controlador luzca mucho mas parecido a un controlador de Angular2. Ahora tenemos todo listo para introducir Angular2 en el proyecto.

Cualquier servicio que tengamos en Angular1 en el proyecto, será un buen candidato para convertirlo en una clase, dado que los controladores son también funciones constructoras. Pero solo tenemos la factoría Phone en el proyecto, y es especial dado que es una factoria ngResource. Por lo tanto no haremos nada en el moento de la preparación. Lo convertiremos directamente en un servicio Angular2.

### Instalar Angular2

Habiendo terminado el trabajo de preparapcion, empecemos el trabajo de actualización de PhoneCat. Haremos esto de forma incremental con la ayuda del module upgrade que viene con Angular2. Al momento en que terminemos, podremos borrar Angular1 completamente, pero la clave es hacerlo pieza a pieza sin romper la aplicación.

El proyecto también tiene algunas animaciones, que todavia no han sido actualizadas en esta versión de la guía. Esto cambiará en una versión futura.
Vamos a instalar Angular2 en el proyecto, junto con SystemJS module loader. Se puede revisar en la guía QuickStart para obtener las siguientes configuraciones de ahi:

Agregar Angular2 y cualquier otra nueva dependencia en package.json.
El archivo de configuracion de SystemJS systemjs.config.js al raiz del proyecto.
Una vez que se dipone del paso anterior, ejecute:

```
  npm install
```

En brebe podremos cargar las dependencias de Angular2 en la aplicación via index.html, pero antes debemos hacer algunos ajustes en los paths. Eso es debido a que tendremos que leer algunos archivos desde node_modules y el raiz del proyecto, dado que antes todo era cargado desde el directorio /app.

Movemos el archivo app/index.html a la raiz del proyecto. Ahora cambiamos el raiz del proyecto de desarrollo en package.json a que apunte a la raiz del proyecto también en lugar de app:

```
{
  "scripts": {
    "start": "http-server -a localhost -p 8000 -c-1 ./"
  }
}
```

Ahora podemos servir todo desde el raiz del proyecto hacia el navegador. Pero no queremos tener que cambiar todas las imagenes y los paths de datos en el código de la aplicación para que sea adecuado a la configuración de development. Por esta razón, agregaremos el tag <base> al index.html que generarán que las urls relativas resulvean hacia el directorio /app:

```
<base href="/app/">
```

Ahora podemos cargar Angular2 mediante SystemJS. Agregaremos los polyfills de Angular2 y el config de SystemJS al final de la sección <head> y luego usaremos System.import para cargar la aplicación actual:

```
<script src="/node_modules/core-js/client/shim.min.js"></script>
<script src="/node_modules/zone.js/dist/zone.js"></script>
<script src="/node_modules/reflect-metadata/Reflect.js"></script>
<script src="/node_modules/systemjs/dist/system.src.js"></script>
<script src="/systemjs.config.js"></script>
<script>
  System.import('/app');
</script>
```

En el archivo systemjs.config.js que obtuvimos de la guia Quickstart también haremos algunos ajustes dada la estructura de nuestro proyecto. Queremos apuntar el navegador al raiz del proyecto cuando cargamos cosas por medio de SystemJS, en lugar de usar la URL <base>:

```
System.config({
  paths: {
    // paths serve as alias
    'npm:': '/node_modules/'
  },
  map: {
    app: '/app',
    /* . . . */
  },
```


### Creado el AppModule

Ahora tenemos que crear la clase raiz llamada AppModule que contiene el NgModule. Ya existe un archivo llamado app.module.ts que contiene el módulo de Angular1. Lo renombramos a app.module.ng1.ts y actualizamos el correspondiente nombre en el archivo index.html. Este archvivo quedaría con el siguiente contenido:

```
file: app.module.ng1.ts

'use strict';
// Define the `phonecatApp` Angular1 module
angular.module('phonecatApp', [
  'ngAnimate',
  'ngRoute',
  'core',
  'phoneDetail',
  'phoneList',
]);
```
Ahora creamos un archivo nuevo app.module.ts con lo minimo necesario para la clase NgModule:

```
file: app.module.ts

import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
@NgModule({
  imports: [
    BrowserModule,
  ],
})
export class AppModule {}
```

### Inicilizacion híbrida 1+2 PhoneCat

Lo próximo que haremos es inicializar la aplicación como una aplicación híbrida que soporte ambos, Angular1 y componentes Angular2. Una vez que hicimos esto, podemos empezar a convertir piezas individuales a Angular2.

Para inicialiazr una aplicación híbrida, primero debemos inicializar el UpgradeAdapter, que proporciona el pegamento que conecta ambos frameworks. Vamos a importar la clase UpgradeAdapter en un archivo nuevo app/main.ts. El archivo se ha configurado como el punto de entrada de la aplicación en systemjs.config.js, por lo tanto ya ha sido cargado en el navegador.

```
file: app/main.ts

import { UpgradeAdapter } from '@angular/upgrade';
declare var angular: any;
import { AppModule } from './app.module';
```

#### ¿Por qué declarar angular como any?

Una referencia fija de angular hacia Angular1 seria excelente. Pero no podemos importar la libreria UMD typings, @types/angular, sin importar Angular1 mismo por medio import * as angular from 'angular'.
Angular1 es cargado en el tag de script en index.html y migrar a ES6 no lleva un esfuerzo considerable. Por lo tanto declarmos angular sin tipo especifico y con tipo any para evitar errores.
Podemos crear un adaptador instalando la clase:
```
let upgradeAdapter = new UpgradeAdapter(AppModule);
```
Nuestra aplicación es inicializada usando el tag ng-app de Angular1 actualmente attachado a <html> que se encuentra en la página host. Esto no functiona en Angular2. Debemos cambiar a inicializar la aplicación por medio de inicializarla por javascript. Por lo tanto, tenemos que borrar el tag ng-app de index.html, y agregamos lo siguiente a main.ts:

```
upgradeAdapter.bootstrap(document.documentElement, ['phonecatApp']);
```

En el adaptador usamos el elemento raiz de la aplicación (que es el mismo elemento que usabamos en ng-app anteriormente) y los módulos de Angular1 que queremos cargar. Dado que estamos inicializando la aplicación por medio del UpgradeAdapter, estamos ahora ejecutando una aplicación híbrida Angular1+2.

Esto significa que estamos ejecutando ambos, Angular1 y 2, al mismo tiempo. Todavia no estamos ejecutando ningun componente Angular2, ese es el siguiente paso.

### Actualizar el servicio Phone

La primer pieza que vamos a migrar a Angular2 es el servicio Phone, que reside en app/code/phone/phone.service.ts y hace posible para un componente cargar informacion de un phone desde el servidor. Ahora es implementado con ngResource y lo utilizamos para dos finalidades:

* Para cargar la lista de todos los phones en el componente phone list
* Para cargar el detalle de un phone en el componente phone detail

Podemos reeplazar esta implementación con una clase Angular2, manteniendo nuestro controlador en el lado de Angular1.

En la nueva versión, importamos el moduleo HTTP de Angular2 y llamamos al servicio Http en lugar de ngResource.

Editamos el archivo app.module.ts, agregamos e importamos HttpModule al array de imports de AppModule:

file: app.module.ts

import { HttpModule } from '@angular/http';
@NgModule({
  imports: [
    BrowserModule,
    HttpModule,
  ],
})
export class AppModule {}

Ahora estamos listos para actualizar el servicio Phone perse. Reemplazamos el servicio en phone.service.ts basado en ngResource por una clase en TypeScript decorada con @Injectable:

```
file: app/core/phone/phone.service.ts(skeleton)

@Injectable()
export class Phone {
/* . . . */
}
```

El decorador @Injectable attachara metadata a la clase, informando a Angular2 saber de sus dependencias. Como se describe en Dependency Injection Guide, usamos este decorador cuando tenemos una clase que no tiene ningun otro decorador pero que al mismo tiempo sigue necesitando que se injecten sus dependencias.

En su constructor la clase espera recibir el servicio Http. Se le inyecta a la clase y lo almacena como una clase privada. El servicio es usado en sus dos métodos, uno carga la lista de todos los phones y el otro el detalle de una phone en particular:

```
@Injectable()
export class Phone {
  constructor(private http: Http) { }
  query(): Observable<PhoneData[]> {
    return this.http.get(`phones/phones.json`)
      .map((res: Response) => res.json());
  }
  get(id: string): Observable<PhoneData> {
    return this.http.get(`phones/${id}.json`)
      .map((res: Response) => res.json());
  }
}
```

Los métodos devuelves Observables de tipo PhoneData y PhoneData[]. Este es un tipo que todavia no tenemos, por lo tanto agreguemos una interfaz:

```
file: app/core/phone/phone.service.ts(interface)

export interface PhoneData {
  name: string;
  snippet: string;
  images: string[];
}
```

A continuación se puede ver el código del servicio en su versión Angular2:

```
file: app/core/phone/phone.service.ts

import { Injectable } from '@angular/core';
import { Http, Response } from '@angular/http';
import { Observable } from 'rxjs/Rx';
import 'rxjs/add/operator/map';
export interface PhoneData {
  name: string;
  snippet: string;
  images: string[];
}
@Injectable()
export class Phone {
  constructor(private http: Http) { }
  query(): Observable<PhoneData[]> {
    return this.http.get(`phones/phones.json`)
      .map((res: Response) => res.json());
  }
  get(id: string): Observable<PhoneData> {
    return this.http.get(`phones/${id}.json`)
      .map((res: Response) => res.json());
  }
}
```

Nótese que estamos importantando el operador map desde RxJS Observable directamente. Tenemos que hacer esto para cada operador que queramos usar en Angular2 dado que no los importa de forma automática o por defecto.

El nuevo servicio Phone tiene las mismas funcionalidades que el original, basado-en-ngResource. Dado que es un servicio Angular2, lo tenemos que registrar con los proveedores en NgModule:

```
file: app.module.ts

import { Phone } from './core/phone/phone.service';
@NgModule({
  imports: [
    BrowserModule,
    HttpModule,
  ],
  providers: [ Phone ]
})
export class AppModule {}
```

UpgradeAdapter tiene un método downgradeNg2Provider para conectar servicios en Angular2 y hacerlos disponibles en Angular1. Se debe usar para conectar el servicio Phone:

file: app/main.ts(expert)

import { Phone } from './core/phone/phone.service';

/* . . . */

angular.module('core.phone')
  .factory('phone', upgradeAdapter.downgradeNg2Provider(Phone));

Ahora que estamos cargando phone.service.ts por medio de un import que lo resuelve SystemJS, tenemos que **eliminar el tag.
En este punto podemos hacer un intercambio entre nuestros dos componentes y usar el nuevo servio en lugar del anterior. Lo inyectamos como haciamos con la factory phone usando $inject, pero en realidad es una instancia de la clase Phone, por lo tanto, podemos anotar su tipo de datos:

file: app/phone-list/phone-list.component.ts

import { Phone, PhoneData } from '../core/phone/phone.service';
declare var angular: any;
class PhoneListController {
  phones: PhoneData[];
  orderProp: string;
  static $inject = ['phone'];
  constructor(phone: Phone) {
    phone.query().subscribe(phones => {
      this.phones = phones;
    });
    this.orderProp = 'age';
  }
}
angular.
  module('phoneList').
  component('phoneList', {
    templateUrl: 'app/phone-list/phone-list.template.html',
    controller: PhoneListController
  });
file: app/phone-detail/phone-detail.component.ts

import { Phone, PhoneData } from '../core/phone/phone.service';
declare var angular: any;
class PhoneDetailController {
  phone: PhoneData;
  mainImageUrl: string;
  static $inject = ['$routeParams', 'phone'];
  constructor($routeParams: angular.route.IRouteParamsService, phone: Phone) {
    let phoneId = $routeParams['phoneId'];
    phone.get(phoneId).subscribe(data => {
      this.phone = data;
      this.setImage(data.images[0]);
    });
  }
  setImage(imageUrl: string) {
    this.mainImageUrl = imageUrl;
  }
}
angular.
  module('phoneDetail').
  component('phoneDetail', {
    templateUrl: 'phone-detail/phone-detail.template.html',
    controller: PhoneDetailController
  });
Ya tenemos dos componentes Angular1 usando un servicio de Angular2. Los componentes no necesitas saber acerca de la versión del servicio, sin importar que el servicio ahora devuelve un Obserable y no uns Promesa, cambio que es un gran avance. En cualquier caso, este paso nos ha permitido migrar un servicio sin importar que versión del framework lo consume.

Podemos usar el método toPromise de un Observable para convertir Observables en Promises en el servicio. Esto puede reducir la necesidad de cambios en controladores en muchos casos.

### Actualizar componentes
Siguiente paso, podemos actualizar nuestros componentes de Angular1 a componentes en Angular2. Lo haremos de a uno por vez, mientras que mantenemos la aplicación en modo híbrido. Mientras realizamos estas conversiónes, también podmeos definir nuestros primeros Angular2 pipes.

Veamos el component phone list primero. Por el momento contiene una clase en TypeScript que define un controlador y la definición de un objecto. Podemos transformar esto en un componente renombrando la clase del controlador y convirtiendo el componente de Angular1 en un objeto de Angular2 que utilice el decorador @Component. También podemos borrar la propiedad estática $inject de la clase:

```
file: app/phone-list/phone-list.component.ts

import { Component } from '@angular/core';
import { Phone, PhoneData } from '../core/phone/phone.service';
@Component({
  moduleId: module.id,
  selector: 'phone-list',
  templateUrl: 'phone-list.template.html'
})
export class PhoneListComponent {
  phones: PhoneData[];
  query: string;
  orderProp: string;
  constructor(phone: Phone) {
    phone.query().subscribe(phones => {
      this.phones = phones;
    });
    this.orderProp = 'age';
  }
}
```
El atributo selector es un selector CSS que define donde va a ir el componente en la página. En Angular1 se realiza una equivalencia con el nombre del componente, pero en Angular2 tenemos estos selectores explicitos. Esto equivaldrá con elementos con el nombre phone-list, igual que la versión Angular1 lo hacia.

También tenemos que convertir el template de este componente en la sintaxis valida de Angular2. Los controles de search de Angular1 $ctrl se expresan en Angular2 de dos vias con [(ngModel)]:
```
<p>
  Search:
  <input [(ngModel)]="query" />
</p>

<p>
  Sort by:
  <select [(ngModel)]="orderProp">
    <option value="name">Alphabetical</option>
    <option value="age">Newest</option>
  </select>
</p>
```
Reemplazamos en la lista el ng-repeat por *ngFor como describe la página de sintaxis de templates. Reemplazamos en la imagen el tag ng-src por el atributo nativo src.
```
file: app/phone-list/phone-list.template.html(phones)

<ul class="phones">
  <li *ngFor="let phone of getPhones()"
      class="thumbnail phone-list-item">
    <a href="/#!/phones/{{phone.id}}{% endra w%}" class="thumb">
      <img [src]="phone.imageUrl" [alt]="phone.name" />
    </a>
    <a href="/#!/phones/{% raw %}{{phone.id}}" class="name">{{phone.name}}</a>
    <p>{{phone.snippet}}</p>
  </li>
</ul>
```
No existe filter o orderBy en Angular2

En Angular1 tenemos filter o orderBy predefinidos, pero estos no existen en Angular2, por lo tanto tenemos que hacer el filtrado y ordenamiento nosotros.

Reemplazamos filter y orderBy por medio de bindings a getPhones() a un método del controlador, que implementa el filtrado y el la logica del ordenamiento dentro del componente mismo.
```
file: app/phone-list/phone-list.component.ts

getPhones(): PhoneData[] {
  return this.sortPhones(this.filterPhones(this.phones));
}
private filterPhones(phones: PhoneData[]) {
  if (phones && this.query) {
    return phones.filter(phone => {
      let name = phone.name.toLowerCase();
      let snippet = phone.snippet.toLowerCase();
      return name.indexOf(this.query) >= 0 || snippet.indexOf(this.query) >= 0;
    });
  }
  return phones;
}
private sortPhones(phones: PhoneData[]) {
  if (phones && this.orderProp) {
    return phones
      .slice(0) // Make a copy
      .sort((a, b) => {
        if (a[this.orderProp] < b[this.orderProp]) {
          return -1;
        } else if ([b[this.orderProp] < a[this.orderProp]]) {
          return 1;
        } else {
          return 0;
        }
      });
  }
  return phones;
}
```

El nuevo PhoneListComponent usa la directiva ngModel de Angular2, que es provista por FormsModule. Agregamos FormsModule a los imports de NgModule y declaramos el nuevo PhoneListComponent:
```
file: app.module.ts

import { FormsModule } from '@angular/forms';
import { PhoneListComponent } from './phone-list/phone-list.component';
@NgModule({
  imports: [
    BrowserModule,
    HttpModule,
    FormsModule,
  ],
  declarations: [
    PhoneListComponent,
  ],
  providers: [ Phone ]
})
export class AppModule {}
```

En el archivo main.ts conectaremos el componente en el módulo Angular1.

En lugar de registrar un componente, registramos una directiva phoneList, una versión degradada del componente en Angular2. El UpgradeAdapter crea un puente entre los dos:
```
file: app/main.ts (excerpt)

import { PhoneListComponent } from './phone-list/phone-list.component';

/* . . . */

angular.module('phoneList')
  .directive(
    'phoneList',
    upgradeAdapter.downgradeNg2Component(PhoneListComponent) as angular.IDirectiveFactory
  );
```
El as angular.IDirectiveFactory indica al compilador de TypeScript que el valor devuelto del método de degradacion es una fabrica de la dorectiva.

Debemos devolver del tag
Asi es como queda phone-detail.component.ts:

```
file: app/phone-detail/phone-detail.component.ts

import { Component, Inject } from '@angular/core';
import { Phone, PhoneData } from '../core/phone/phone.service';
@Component({
  moduleId: module.id,
  selector: 'phone-detail',
  templateUrl: 'phone-detail.template.html',
})
export class PhoneDetailComponent {
  phone: PhoneData;
  mainImageUrl: string;
  constructor(@Inject('$routeParams')
                $routeParams: angular.route.IRouteParamsService,
              phone: Phone) {
    phone.get($routeParams['phoneId']).subscribe(phone => {
      this.phone = phone;
      this.setImage(phone.images[0]);
    });
  }
  setImage(imageUrl: string) {
    this.mainImageUrl = imageUrl;
  }
}
```
Esto es similar al componente phone list. Lo nuevo es el decorador @Inject que identifica la dependencia $routeParams.

El injector de Angular1 tiene una dependencia llamada $routeParams que fue injectado en PhoneDetails cuando todavia estaba en el ambito del controlador de Angular1. Ahora intentamos injectarlo en el nuevo PhoneDetailsComponent.

Desafortunadamente, las dependencias en Angular1 no esta disponibles de forma automática en los componentes de Angular2. Debemos usar el UpgradeAdapter para hacer $routeParams un provedor en Angular2. Hacemos esto en main.ts:

file: app/main.ts ($routeParams)

upgradeAdapter.upgradeNg1Provider('$routeParams');
No se debe registrar un proveedor Angular1 en NgModule
Convertimos el componente de phone detail en sintaxis de Angular2:

file: app/phone-detail/phone-detail.template.html

<div *ngIf="phone">
  <div class="phone-images">
    <img [src]="img" class="phone"
        [ngClass]="{selected: img === mainImageUrl}"
        *ngFor="let img of phone.images" />
  </div>
  <h1>{{phone.name}}</h1>
  <p>{{phone.description}}</p>
  <ul class="phone-thumbs">
    <li *ngFor="let img of phone.images">
      <img [src]="img" (click)="setImage(img)" />
    </li>
  </ul>
  <ul class="specs">
    <li>
      <span>Availability and Networks</span>
      <dl>
        <dt>Availability</dt>
        <dd *ngFor="let availability of phone.availability">{{availability}}</dd>
      </dl>
    </li>
    <li>
      <span>Battery</span>
      <dl>
        <dt>Type</dt>
        <dd>{{phone.battery?.type}}</dd>
        <dt>Talk Time</dt>
        <dd>{{phone.battery?.talkTime}}</dd>
        <dt>Standby time (max)</dt>
        <dd>{{phone.battery?.standbyTime}}</dd>
      </dl>
    </li>
    <li>
      <span>Storage and Memory</span>
      <dl>
        <dt>RAM</dt>
        <dd>{{phone.storage?.ram}}</dd>
        <dt>Internal Storage</dt>
        <dd>{{phone.storage?.flash}}</dd>
      </dl>
    </li>
    <li>
      <span>Connectivity</span>
      <dl>
        <dt>Network Support</dt>
        <dd>{{phone.connectivity?.cell}}</dd>
        <dt>WiFi</dt>
        <dd>{{phone.connectivity?.wifi}}</dd>
        <dt>Bluetooth</dt>
        <dd>{{phone.connectivity?.bluetooth}}</dd>
        <dt>Infrared</dt>
        <dd>{{phone.connectivity?.infrared | checkmark}}</dd>
        <dt>GPS</dt>
        <dd>{{phone.connectivity?.gps | checkmark}}</dd>
      </dl>
    </li>
    <li>
      <span>Android</span>
      <dl>
        <dt>OS versión</dt>
        <dd>{{phone.android?.os}}</dd>
        <dt>UI</dt>
        <dd>{{phone.android?.ui}}</dd>
      </dl>
    </li>
    <li>
      <span>Size and Weight</span>
      <dl>
        <dt>Dimensions</dt>
        <dd *ngFor="let dim of phone.sizeAndWeight?.dimensions"></dd>
        <dt>Weight</dt>
        <dd>{{phone.sizeAndWeight?.weight}}</dd>
      </dl>
    </li>
    <li>
      <span>Display</span>
      <dl>
        <dt>Screen size</dt>
        <dd>{{phone.display?.screenSize}}</dd>
        <dt>Screen resolution</dt>
        <dd>{{phone.display?.screenResolution}}</dd>
        <dt>Touch screen</dt>
        <dd>{{phone.display?.touchScreen | checkmark}}</dd>
      </dl>
    </li>
    <li>
      <span>Hardware</span>
      <dl>
        <dt>CPU</dt>
        <dd>{{phone.hardware?.cpu}}</dd>
        <dt>USB</dt>
        <dd>{{phone.hardware?.usb}}</dd>
        <dt>Audio / headphone jack</dt>
        <dd>{{phone.hardware?.audioJack}}</dd>
        <dt>FM Radio</dt>
        <dd>{{phone.hardware?.fmRadio | checkmark}}</dd>
        <dt>Accelerometer</dt>
        <dd>{{phone.hardware?.accelerometer | checkmark}}</dd>
      </dl>
    </li>
    <li>
      <span>Camera</span>
      <dl>
        <dt>Primary</dt>
        <dd>{{phone.camera?.primary}}</dd>
        <dt>Features</dt>
        <dd>{{phone.camera?.features?.join(', ')}}</dd>
      </dl>
    </li>
    <li>
      <span>Additional Features</span>
      <dd>{{phone.additionalFeatures}}</dd>
    </li>
  </ul>
</div>
Hay varios cambios importantes aca:

Se eliminó el prefijo $ctrl de todas las expresiones.
De la misma manera que se hizo en phone list, reemplazamos ng-src con la propiedad estandar src.
Se utiliza la sintaxis de binding alrrededor de ng-class. Angular2 tiene una sintaxis bastante similar ngClass a la que tiene Angular1, su valor no se evalua automáticamente como una expresión. En Angular2 siempre se especifica en el template cuando el valor de un atributo es una expresión de un atributo, en oposición de una cadena literal.
Reemplazamos ng-repeat por *ngFor.
Reemplazamos ng-click con un binding de eventos de click.
Se agrupa toda la vista en un ngIf que controla que se muestre el contenido de la vista sólo cuando se tiene un phone presente. Esto se necesita para si se carga el componente por primera vez, no tenemos definido un phone todavia y las expresiones hacen referencia a un valor que todavía no existe. A diferencias de Angular1, en Angular2 cuando una expresión falla genera un error cuando hace referencia a propiedades de objetos no definidos. Debemos ser explícitos cuando estas excepciones pueden presentarse.
Agregamos PhoneDetailComponent a las declaraciones NgModule y a entryComponents:
```
file: app.module.ts

import { PhoneDetailComponent } from './phone-detail/phone-detail.component';
@NgModule({
  imports: [
    BrowserModule,
    UpgradeModule,
    HttpModule,
    FormsModule,
  ],
  declarations: [
    PhoneListComponent,
    PhoneDetailComponent,
  ],
  entryComponents: [
    PhoneListComponent,
    PhoneDetailComponent
  ],
  providers: [
    Phone,
    {
      provide: '$routeParams',
      useFactory: routeParamsFactory,
      deps: ['$injector']
    }
  ]
})
export class AppModule {
  ngDoBootstrap() {}
}
```
Debemos también quitar la línea de phone detail de las entradas de

Agregar CHECKMARKPIPE

La directiva Angular1 tienen un filtro checkmark. Vamos a convertilo en un pipe de Angular2.

No hay una actualización posible para convertir filtros en pipes. Es facil de convertir un filtro en su clase pipe equivalente. La implementacion es la misma que antes, reempaquetarla en el método transform. Renombramos el archivo a checkmark.pipe.ts para aplicar las convenciones de Angular2:

file: app/core/checkmark/checkmark.pipe.ts

import { Pipe, PipeTransform } from '@angular/core';

@Pipe({name: 'checkmark'})
export class CheckmarkPipe implements PipeTransform {
  transform(input: boolean) {
    return input ? '\u2713' : '\u2718';
  }
}
Debemos importar y declarar el nuevo pipe creado y quitar el tag
file: app.module.ts

import { CheckmarkPipe } from './core/checkmark/checkmark.pipe';
@NgModule({
  imports: [
    BrowserModule,
    UpgradeModule,
    HttpModule,
    FormsModule,
  ],
  declarations: [
    PhoneListComponent,
    PhoneDetailComponent,
    CheckmarkPipe
  ],
  entryComponents: [
    PhoneListComponent,
    PhoneDetailComponent
  ],
  providers: [
    Phone,
    {
      provide: '$routeParams',
      useFactory: routeParamsFactory,
      deps: ['$injector']
    }
  ]
})
export class AppModule {
  ngDoBootstrap() {}
}
Migrando al router Angular2 e inicializar

En este punto ya hemos reemplazado todos los componentes de Angular1 con sus equivalentes de Angular2.

La aplicación todavia es inicializada como una aplicación híbrida. Ya no se necesita este tipo de inicializacion. Es momento de quitar los ultimos rastros de Angular1 en dos pasos finales:

Cambiar al ruter de Angular2
Inicializar como una aplicación Angular2 pura.
Cambiar al router de Angular2

Angular2 tiene un router totalmente nuevo.

Como todo router, necesita un lugar en el UI para desplegar las vistas de las rutas. En Angular2 este trabajo es realizado por <router-outlet> y pertenece a un componente raiz en el arbol de compomnentes de una aplicación.

Todavia no tenemos este tipo de componente, dado que nuestra aplicación todavia es manejada por Angular1. Debemos crear el archivo app.component.ts con la clase AppComponent:

file: app/app.component.ts

import { Component } from '@angular/core';

@Component({
  selector: 'phonecat-app',
  template: '<router-outlet></router-outlet>'
})
export class AppComponent {
}
Tiene una vista muy simple que solo contiene <router-outlet>. Este componente renderea el contenido de la ruta actual y nada mas.

El selector le inidica a Angular2 el poner este componente raiz dentro del elemento <phonecat-app> en la página ppal de la apliacion cuando se inicializa.

Debemos agregar el elemento <phonecat-app> al index.html. Este reemplaza la directiva de Angular1 ng-view:

file: index.html (body)

  <body>
    <phonecat-app></phonecat-app>
  </body>
</html>
Creando el routing module

Un router necesita una configuracion sin importar si es Angular1 o 2 o cualquier otro.

Los detales de la configuracion del router de Angular2 se puede encontrar en la documentacion del router que recomiendan crear un módulo NgModule dedicado a la configuracion del router (llamado un Routing Module):

file: app/app.routing.module.ts

import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import { APP_BASE_HREF, HashLocationStrategy, LocationStrategy } from '@angular/common';
import { PhoneDetailComponent } from './phone-detail/phone-detail.component';
import { PhoneListComponent }   from './phone-list/phone-list.component';
const routes: Routes = [
  { path: '', redirectTo: 'phones', pathMatch: 'full' },
  { path: 'phones',          component: PhoneListComponent },
  { path: 'phones/:phoneId', component: PhoneDetailComponent }
];
@NgModule({
  imports: [ RouterModule.forRoot(routes) ],
  exports: [ RouterModule ],
  providers: [
    { provide: APP_BASE_HREF, useValue: '!' },
    { provide: LocationStrategy, useClass: HashLocationStrategy },
  ]
})
export class AppRoutingModule {}
Este module define el objeto routes con las dos rutas a los dos componentes phone y una ruta default ‘/’. Envia routes al medodo RouterModule.forRoot que realiza el resto.

Se habilitan las rutas con URLs de formato “hash” al estilo #!/phones en lugar de la estrategia “push state”.

Actualizamos AppModule para importar AppRoutingModule y declarar el raiz AppComponent:

file: app/app.module.ts

import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';
import { AppRoutingModule } from './app-routing.module';
import { AppComponent }     from './app.component';
import { CheckmarkPipe }    from './core/checkmark/checkmark.pipe';
import { Phone }            from './core/phone/phone.service';
import { PhoneDetailComponent } from './phone-detail/phone-detail.component';
import { PhoneListComponent }   from './phone-list/phone-list.component';
@NgModule({
  imports: [
    BrowserModule,
    FormsModule,
    HttpModule,
    AppRoutingModule
  ],
  declarations: [
    AppComponent,
    PhoneListComponent,
    CheckmarkPipe,
    PhoneDetailComponent
  ],
  providers: [
    Phone,
  ],
  bootstrap: [ AppComponent ]
})
export class AppModule {}
El router de Angular2 envia parametros diferente. Actualizamos el constructor del componente PhoneDetail para esperar y recibir un objeto ActivatedRoute. Extraemos el phoneId de ActivatedRoute.snapshot.params y obtenemos los datos del telefono como antes:

file: app/phone-detail/phone-detail.component.ts

import { Component }      from '@angular/core';
import { ActivatedRoute } from '@angular/router';
import { Phone, PhoneData } from '../core/phone/phone.service';
@Component({
  moduleId: module.id,
  selector: 'phone-detail',
  templateUrl: 'phone-detail.template.html'
})
export class PhoneDetailComponent {
  phone: PhoneData;
  mainImageUrl: string;
  constructor(activatedRoute: ActivatedRoute, phone: Phone) {
    phone.get(activatedRoute.snapshot.params['phoneId'])
      .subscribe((p: PhoneData) => {
        this.phone = p;
        this.setImage(p.images[0]);
      });
  }
  setImage(imageUrl: string) {
    this.mainImageUrl = imageUrl;
  }
}
Generar links para cada telefono

Ya no tenemos que setear manualmente los links al detalle de un telefono desde la lista de estos. Podemos generar los links a cada id de los telefonos a la directiva routerLink y dejando a la directiva construir la URL apropiada a PhoneDetailComponent:

file: app/phone-list/phone-list.template.html (list with links)

<ul class="phones">
  <li *ngFor="let phone of getPhones()"
      class="thumbnail phone-list-item">
    <a [routerLink]="['/phones', phone.id]" class="thumb">
      <img [src]="phone.imageUrl" [alt]="phone.name" />
    </a>
    <a [routerLink]="['/phones', phone.id]" class="name">{{phone.name}}</a>
    <p>{{phone.snippet}}</p>
  </li>
</ul>
Inicializando la aplicación como Angular2

Se puede notar una entrada de metadata adicional en bootstrap agregada al AppModule

file: app/app.module.ts (booststrap)
bootstrap: [ AppComponent ]
Esto indica a Angular2 que debe inicilizar la app con AppComponent como raiz e insertar su vista en el host de la página.

Ahora cambiamos el método de inicializacionde UpgradeAdapter hacia la forma de Angular2.

Ahora podemos borrar upgrade.bootstrap de nuestra inicialización de la aplicación, y eliminamos el ngDoBootstrap() reemplazado por app.module.ts

```
file: main.ts

import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { AppModule } from './app.module';
platformBrowserDynamic().bootstrapModule(AppModule);
file: app.module.ts

import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';
import { AppRoutingModule } from './app-routing.module';
import { AppComponent }     from './app.component';
import { CheckmarkPipe }    from './core/checkmark/checkmark.pipe';
import { Phone }            from './core/phone/phone.service';
import { PhoneDetailComponent } from './phone-detail/phone-detail.component';
import { PhoneListComponent }   from './phone-list/phone-list.component';
@NgModule({
  imports: [
    BrowserModule,
    FormsModule,
    HttpModule,
    AppRoutingModule
  ],
  declarations: [
    AppComponent,
    PhoneListComponent,
    CheckmarkPipe,
    PhoneDetailComponent
  ],
  providers: [
    Phone,
  ],
  bootstrap: [ AppComponent ]
})
export class AppModule {}
```

Ahora estamos ejecutando una aplicación Angular2 pura.

### Despidiendo a Angular1

Ya es momento de borrar todo rastro de Angular1 en nuestra aplicación. Solo nos queda por quitar cualquier código que haga referencia.

Tenemos que quitar todas las referencias a UpgradeMaodule en app.module.ts, como también cualquier service de Angular1 del tipo (Factory provider)[https://angular.io/docs/ts/latest/guide/upgrade.html#making-angular-1-dependencies-injectable-to-angular-2]. También debemos borrar cualquier ocurrencia de `downgradeComponent()` que encontremos, y también cualquier directiva que esté declarada en Angular1.

Debemos borrar los siguiente archivos. Estos son módulos de configuracion que no son necesarios en Angular2:

app/app.module.ng1.ts
app/app.config.ts
app/core/core.module.ts
app/core/phone/phone.module.ts
app/phone-detail/phone-detail.module.ts
app/phone-list/phone-list.module.ts
Se pueden desinstalar los typings de Angular1. Solo es necesario mantener los referentes a Jasmine y Angular2 polyfills.

npm uninstall @types/angular @types/angular-animate @types/angular-cookies @types/angular-mocks @types/angular-resource @types/angular-route @types/angular-sanitize –save-dev
Finalmente, en index.html, eliminamos cualquier referencia a scripts de Angular1, al upgrade module de Angular2, y jQuery. Cuando terminamos debe quedar de la siguiente manera:

file: index.html

<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <base href="/app/">
    <title>Google Phone Gallery</title>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css" />
    <link rel="stylesheet" href="app.css" />
    <script src="/node_modules/core-js/client/shim.min.js"></script>
    <script src="/node_modules/zone.js/dist/zone.js"></script>
    <script src="/node_modules/reflect-metadata/Reflect.js"></script>
    <script src="/node_modules/systemjs/dist/system.src.js"></script>
    <script src="/systemjs.config.js"></script>
    <script>
      System.import('/app');
    </script>
  </head>
  <body>
    <phonecat-app></phonecat-app>
  </body>
</html>
Esta es la ultima vez que veremos Angular1, ya podemos decirle adios.

Apendice: Angualizando tests de PhoneCat

Los tests deben ser actualizados en este proceso también, y también pueden ser usados para asegurar este proceso de migracion. Los tests E2E son especialmente utiles duranete este proceso.

E2E tests

El proyecto PhoneCat tiene ambos, E2E Protractor y algunos tests de unidad. De ambos, los tests E2E pueden ser tratados mucho mas facil: por definición, los tests E2E acceden a nuestra aplicación por fuera interactuando con los elementos que la aplicación pone en la pantalla. Los tests E2E no tienen un alto concimiento de la estructura interna de los componentes de la aplicación. A pesar de todas las modificaciones efectuadas, nuestros tests E2E deberian funcionar con solo unas pequeñas modificaciones. Esto se debe a que no hemos cambiado la aplicación desde el punto de vista del usuario.

Durante la conversión TypeScript, no hay nada que debamos hacer para que los tests E2E sigan funcionando. Debemos hacer cambios cuando cambiamos la inicializacion a la forma híbrida.

El cambio debe ser realizado en el archivo protractor-conf.js para que sincronice con una aplicación híbrida:

ng12Hybrid: true
Los siguientes cambios se deben realizar cuando empezamos a actualizar componentes y sus vistas en Angular2. Esto se debe a que los tests E2E tienen matchers que son especificos de Angular1. Para PhoneCat tenemos que hacer los siguientes cambios para que las cosas funcionen con Angular2:

código Anterior	Nuevo código	Notas
by.repeater(‘phone in	by.css(‘.phones .name’)	El repetidor recide en
$ctrl.phones’).column(‘phone.name’)	 	Angular1 ng-repeat
by.repeater(‘phone in $ctrl.phones’)	by.css(‘.phones li’)	El repetidor recide en
 	 	Angular1 ng-model
by.model(‘$ctrl.query’)	by.css(‘select’)	El repetidor recide en
 	 	Angular1 ng-model
by.model(‘$ctrl.orderProp’)	by.css(‘h1’)	El matcher del binding
 	 	se aplica en el binding de datos
Cuando el método de inicializacion se cambia de UpgradeModule a una aplicación de Angualr 2, Angular1 deja de existir por completo. En este momento debemos decir a Protractor que no debe seguir buscando una aplicación Angular1 y que debe buscar una aplicación Angular2.

Reemplazamos el ng12Hybrid que agregamos anteriormente en el archivo protractor-conf.js:

useAllAngular2AppRoots: true,
En los tests de PhoneCat hay llamadas a la API de Protractor que hacen uso del servicio $location indirectamente. Y dado que este servicio no existe después de la actualización, debemos reemplazar estas llamadas con unas que usen llamadas genericas a URLs de la API de WebDriver. La primera de estas es la redicreccion spec:

file: e2e-tests/scenarios.ts

it('should redirect `index.html` to `index.html#!/phones', function() {
  browser.get('index.html');
  browser.waitForAngular();
  browser.getCurrentUrl().then(function(url: string) {
    expect(url.endsWith('/phones')).toBe(true);
  });
});
Y la segunda es los links de phone spec:

file: e2e-tests/scenarios.ts

it('should render phone specific links', function() {
  let query = element(by.css('input'));
  query.sendKeys('nexus');
  element.all(by.css('.phones li a')).first().click();
  browser.getCurrentUrl().then(function(url: string) {
    expect(url.endsWith('/phones/nexus-s')).toBe(true);
  });
});
Tests de unidad

Para los tests de unidad se necesita mayor trabajo para la migracion. En realidad se necesita actualizar en paralelo con el código de produccion.

Durante la conversión a TypeScript no hay que realizar ningun cambio. Pero puede ser de utilidad convertir el código a TypeScript, los mismos beneficios que se aplican en el código de produccion se aplicaran a los tests.

Por ejemplo, en la spec del componente phone detail podemos usar las capacidades ES2015 como arrow functions y variables de scope, pero también la definición de tipos de algunos de los servicios que consumimos:

file: app/phone-detail/phone-detail.component.spec.ts

describe('phoneDetail', () => {
  // Load the module that contains the `phoneDetail` component before each test
  beforeEach(angular.mock.module('phoneDetail'));
  // Test the controller
  describe('PhoneDetailController', () => {
    let $httpBackend: angular.IHttpBackendService;
    let ctrl: any;
    let xyzPhoneData = {
      name: 'phone xyz',
      images: ['image/url1.png', 'image/url2.png']
    };
    beforeEach(inject(($componentController: any,
                       _$httpBackend_: angular.IHttpBackendService,
                       $routeParams: angular.route.IRouteParamsService) => {
      $httpBackend = _$httpBackend_;
      $httpBackend.expectGET('phones/xyz.json').respond(xyzPhoneData);
      $routeParams['phoneId'] = 'xyz';
      ctrl = $componentController('phoneDetail');
    }));
    it('should fetch the phone details', () => {
      jasmine.addCustomEqualityTester(angular.equals);
      expect(ctrl.phone).toEqual({});
      $httpBackend.flush();
      expect(ctrl.phone).toEqual(xyzPhoneData);
    });
  });
});
Una vez que iniciamos el proceso de actualización e introducimos SystemJS, necesitamos hacer algunos cambios para Karma. Necesitamos que SystemJS cargue el código Angular2 que puede realizarse con el siguiente código:

file: karma-test-shim.js

// /*global jasmine, __karma__, window*/
Error.stackTraceLimit = 0; // "No stacktrace"" is usually best for app testing.
// Uncomment to get full stacktrace output. Sometimes helpful, usually not.
// Error.stackTraceLimit = Infinity; //
jasmine.DEFAULT_TIMEOUT_INTERVAL = 1000;
var builtPath = '/base/app/';
__karma__.loaded = function () { };
function isJsFile(path) {
  return path.slice(-3) == '.js';
}
function isSpecFile(path) {
  return /\.spec\.(.*\.)?js$/.test(path);
}
function isBuiltFile(path) {
  return isJsFile(path) && (path.substr(0, builtPath.length) == builtPath);
}
var allSpecFiles = Object.keys(window.__karma__.files)
  .filter(isSpecFile)
  .filter(isBuiltFile);
System.config({
  baseURL: '/base',
  // Extend usual application package list with test folder
  packages: { 'testing': { main: 'index.js', defaultExtension: 'js' } },
  // Assume npm: is set in `paths` in systemjs.config
  // Map the angular testing umd bundles
  map: {
    '@angular/core/testing': 'npm:@angular/core/bundles/core-testing.umd.js',
    '@angular/common/testing': 'npm:@angular/common/bundles/common-testing.umd.js',
    '@angular/compiler/testing': 'npm:@angular/compiler/bundles/compiler-testing.umd.js',
    '@angular/platform-browser/testing': 'npm:@angular/platform-browser/bundles/platform-browser-testing.umd.js',
    '@angular/platform-browser-dynamic/testing': 'npm:@angular/platform-browser-dynamic/bundles/platform-browser-dynamic-testing.umd.js',
    '@angular/http/testing': 'npm:@angular/http/bundles/http-testing.umd.js',
    '@angular/router/testing': 'npm:@angular/router/bundles/router-testing.umd.js',
    '@angular/forms/testing': 'npm:@angular/forms/bundles/forms-testing.umd.js',
  },
});
System.import('systemjs.config.js')
  .then(importSystemJsExtras)
  .then(initTestBed)
  .then(initTesting);
/** Optional SystemJS configuration extras. Keep going w/o it */
function importSystemJsExtras(){
  return System.import('systemjs.config.extras.js')
  .catch(function(reason) {
    console.log(
      'Warning: System.import could not load the optional "systemjs.config.extras.js". Did you omit it by accident? Continuing without it.'
    );
    console.log(reason);
  });
}
function initTestBed(){
  return Promise.all([
    System.import('@angular/core/testing'),
    System.import('@angular/platform-browser-dynamic/testing')
  ])
  .then(function (providers) {
    var coreTesting    = providers[0];
    var browserTesting = providers[1];
    coreTesting.TestBed.initTestEnvironment(
      browserTesting.BrowserDynamicTestingModule,
      browserTesting.platformBrowserDynamicTesting());
  })
}
// Import all spec files and start karma
function initTesting () {
  return Promise.all(
    allSpecFiles.map(function (moduleName) {
      return System.import(moduleName);
    })
  )
  .then(__karma__.start, __karma__.error);
}
Este código primero carga la configuracion de SystemJS, luego las librerias de soporte de test de Angular2, y luego los archivos specs de la aplicación.

En la configuracion de Karma debe cambiarse a que utilice el directorio raiz como el directorio base, en lugar de app:

file: karma.conf.js
basePath: './',
Una vez que hacemos esto podemos cargar SystemJS y otras dependencias, y se cambia la configuracion para cargar los archivos de la aplicación para que no sean incluidos en la página por medio de Karma. Dejaremos que shim y SystemJS los carguen.

file: karma.conf.js

// System.js for module loading
'node_modules/systemjs/dist/system.src.js',
// Polyfills
'node_modules/core-js/client/shim.js',
'node_modules/reflect-metadata/Reflect.js',
// zone.js
'node_modules/zone.js/dist/zone.js',
'node_modules/zone.js/dist/long-stack-trace-zone.js',
'node_modules/zone.js/dist/proxy.js',
'node_modules/zone.js/dist/sync-test.js',
'node_modules/zone.js/dist/jasmine-patch.js',
'node_modules/zone.js/dist/async-test.js',
'node_modules/zone.js/dist/fake-async-test.js',
// RxJs.
{ pattern: 'node_modules/rxjs/**/*.js', included: false, watched: false },
{ pattern: 'node_modules/rxjs/**/*.js.map', included: false, watched: false },
// Angular2 itself and the testing library
{pattern: 'node_modules/@angular/**/*.js', included: false, watched: false},
{pattern: 'node_modules/@angular/**/*.js.map', included: false, watched: false},
{pattern: 'systemjs.config.js', included: false, watched: false},
'karma-test-shim.js',
{pattern: 'app/**/*.module.js', included: false, watched: true},
{pattern: 'app/*!(.module|.spec).js', included: false, watched: true},
{pattern: 'app/!(bower_components)/**/*!(.module|.spec).js', included: false, watched: true},
{pattern: 'app/**/*.spec.js', included: false, watched: true},
{pattern: '**/*.html', included: false, watched: true},
Dado que los templates HTML de los componentes de Angular2 también seran cargados, necesitamos ayudar a Karma para que los pueda enrutar de forma correcta:

file: karma.conf.js

// proxied base paths for loading assets
proxies: {
  // required for component assets fetched by Angular's compiler
  "/phone-detail": '/base/app/phone-detail',
  "/phone-list": '/base/app/phone-list'
},
Los archivos de test deben ser migrados a Angular2 al mismo que el componente original es migrado. El spec de pipe de checkmark es el mas sencillo de migrar ya que no tiene dependencias:

file: app/core/checkmark/checkmark.pipe.spec.ts

import { CheckmarkPipe } from './checkmark.pipe';
describe('CheckmarkPipe', function() {
  it('should convert boolean values to unicode checkmark or cross', function () {
    const checkmarkPipe = new CheckmarkPipe();
    expect(checkmarkPipe.transform(true)).toBe('\u2713');
    expect(checkmarkPipe.transform(false)).toBe('\u2718');
  });
});
Los tests de unidad del servicio phone es un poco mas complicado. Necesitamos hacer un cambio desde Angular1 $httpBackend hacia Angular2 Http Backend.

file: app/core/phone/phone.service.spec.ts

import { inject, TestBed } from '@angular/core/testing';
import {
  Http,
  BaseRequestOptions,
  ResponseOptions,
  Response
} from '@angular/http';
import { MockBackend, MockConnection } from '@angular/http/testing';
import { Phone, PhoneData } from './phone.service';
describe('Phone', function() {
  let phone: Phone;
  let phonesData: PhoneData[] = [
    {name: 'Phone X', snippet: '', images: []},
    {name: 'Phone Y', snippet: '', images: []},
    {name: 'Phone Z', snippet: '', images: []}
  ];
  let mockBackend: MockBackend;
  beforeEach(() => {
    TestBed.configureTestingModule({
      providers: [
        Phone,
        MockBackend,
        BaseRequestOptions,
        { provide: Http,
          useFactory: (backend: MockBackend, options: BaseRequestOptions) => new Http(backend, options),
          deps: [MockBackend, BaseRequestOptions]
        }
      ]
    });
  });
  beforeEach(inject([MockBackend, Phone], (_mockBackend_: MockBackend, _phone_: Phone) => {
    mockBackend = _mockBackend_;
    phone = _phone_;
  }));
  it('should fetch the phones data from `/phones/phones.json`', (done: () => void) => {
    mockBackend.connections.subscribe((conn: MockConnection) => {
      conn.mockRespond(new Response(new ResponseOptions({body: JSON.stringify(phonesData)})));
    });
    phone.query().subscribe(result => {
      expect(result).toEqual(phonesData);
      done();
    });
  });
});
Para la spec del componente podemos mockear el servicio mismo Phone, y proveer datos de telefonos. Usamos la API de componentes de test de unidad de Angular.

file: app/phone-detail/phone-detal.component.spec.ts

import { ActivatedRoute } from '@angular/router';
import { Observable } from 'rxjs/Rx';
import { async, TestBed } from '@angular/core/testing';
import { PhoneDetailComponent } from './phone-detail.component';
import { Phone, PhoneData } from '../core/phone/phone.service';
import { CheckmarkPipe } from '../core/checkmark/checkmark.pipe';
function xyzPhoneData(): PhoneData {
  return {
    name: 'phone xyz',
    snippet: '',
    images: ['image/url1.png', 'image/url2.png']
  };
}
class MockPhone {
  get(id: string): Observable<PhoneData> {
    return Observable.of(xyzPhoneData());
  }
}
class ActivatedRouteMock {
  constructor(public snapshot: any) {}
}
describe('PhoneDetailComponent', () => {
  beforeEach(async(() => {
    TestBed.configureTestingModule({
      declarations: [ CheckmarkPipe, PhoneDetailComponent ],
      providers: [
        { provide: Phone, useClass: MockPhone },
        { provide: ActivatedRoute, useValue: new ActivatedRouteMock({ params: { 'phoneId': 1 } }) }
      ]
    })
    .compileComponents();
  }));
  it('should fetch phone detail', () => {
    const fixture = TestBed.createComponent(PhoneDetailComponent);
    fixture.detectChanges();
    let compiled = fixture.debugElement.nativeElement;
    expect(compiled.querySelector('h1').textContent).toContain(xyzPhoneData().name);
  });
});
file: app/phone-list/phone-list.compomnent.spec.ts

import { NO_ERRORS_SCHEMA } from '@angular/core';
import { ActivatedRoute } from '@angular/router';
import { Observable } from 'rxjs/Rx';
import { async, ComponentFixture, TestBed } from '@angular/core/testing';
import { SpyLocation } from '@angular/common/testing';
import { PhoneListComponent } from './phone-list.component';
import { Phone, PhoneData } from '../core/phone/phone.service';
class ActivatedRouteMock {
  constructor(public snapshot: any) {}
}
class MockPhone {
  query(): Observable<PhoneData[]> {
    return Observable.of([
      {name: 'Nexus S', snippet: '', images: []},
      {name: 'Motorola DROID', snippet: '', images: []}
    ]);
  }
}
let fixture: ComponentFixture<PhoneListComponent>;
describe('PhoneList', () => {
  beforeEach(async(() => {
    TestBed.configureTestingModule({
      declarations: [ PhoneListComponent ],
      providers: [
        { provide: ActivatedRoute, useValue: new ActivatedRouteMock({ params: { 'phoneId': 1 } }) },
        { provide: Location, useClass: SpyLocation },
        { provide: Phone, useClass: MockPhone },
      ],
      schemas: [ NO_ERRORS_SCHEMA ]
    })
    .compileComponents();
  }));
  beforeEach(() => {
    fixture = TestBed.createComponent(PhoneListComponent);
  });
  it('should create "phones" model with 2 phones fetched from xhr', () => {
    fixture.detectChanges();
    let compiled = fixture.debugElement.nativeElement;
    expect(compiled.querySelectorAll('.phone-list-item').length).toBe(2);
    expect(
      compiled.querySelector('.phone-list-item:nth-child(1)').textContent
    ).toContain('Motorola DROID');
    expect(
      compiled.querySelector('.phone-list-item:nth-child(2)').textContent
    ).toContain('Nexus S');
  });
  xit('should set the default value of orderProp model', () => {
    fixture.detectChanges();
    let compiled = fixture.debugElement.nativeElement;
    expect(
      compiled.querySelector('select option:last-child').selected
    ).toBe(true);
  });
});
Finalmente, necesitamos revisar los tests de componentes cuando cambiamos al router de Angular2. Para el componente de detalle tenemos que proveer un mock para el objeto de Angular2 ActivatedRoute en lugar de usar $routeParams de Angular1:

file: app/phone-detail/phone-detail.component.spec.ts

import { ActivatedRoute } from '@angular/router';
/* . . . */
class ActivatedRouteMock {
  constructor(public snapshot: any) {}
}
/* . . . */
  beforeEach(async(() => {
    TestBed.configureTestingModule({
      declarations: [ CheckmarkPipe, PhoneDetailComponent ],
      providers: [
        { provide: Phone, useClass: MockPhone },
        { provide: ActivatedRoute, useValue: new ActivatedRouteMock({ params: { 'phoneId': 1 } }) }
      ]
    })
    .compileComponents();
  }));
Y para el componente de lista necesitamos configurar algunas cosas para el router en si mismo para que la directiva del link funcione.

file: app/phone-list/phone-list.component.spec.ts

import { NO_ERRORS_SCHEMA } from '@angular/core';
import { ActivatedRoute } from '@angular/router';
import { Observable } from 'rxjs/Rx';
import { async, ComponentFixture, TestBed } from '@angular/core/testing';
import { SpyLocation } from '@angular/common/testing';
import { PhoneListComponent } from './phone-list.component';
import { Phone, PhoneData } from '../core/phone/phone.service';
/* . . . */
  beforeEach(async(() => {
    TestBed.configureTestingModule({
      declarations: [ PhoneListComponent ],
      providers: [
        { provide: ActivatedRoute, useValue: new ActivatedRouteMock({ params: { 'phoneId': 1 } }) },
        { provide: Location, useClass: SpyLocation },
        { provide: Phone, useClass: MockPhone },
      ],
      schemas: [ NO_ERRORS_SCHEMA ]
    })
    .compileComponents();
  }));
  beforeEach(() => {
    fixture = TestBed.createComponent(PhoneListComponent);
  });