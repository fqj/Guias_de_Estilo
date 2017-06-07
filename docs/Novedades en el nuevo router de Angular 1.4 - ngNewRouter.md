# Novedades en el nuevo router de Angular 1.4 - ngNewRouter

AngularJS trae en su recién lanzada versión 1.4 un nuevo sistema de router en el cliente que nos prepara para cuando decidamos dar el salto a la versión 2.0 y el cambio no sea tan drástico. Aún hay por delante los lanzamientos futuros de 
las versiones 1.5 y 1.6 que introducirán más cambios para hacer la transición a la versión 2.0 más llevadera.

El nuevo sistema de enrutamiento se encuenta en la librería angular-new-router que podemos descargar desde npm, y el módulo dependencia a utilizar es ngNewRouter.

El principal cambio es que ahora Angular nos obliga a pensar en componentes, y hace bien. Esto nos permite modularizar nuestras aplicaciones y hacerlas más mantenibles desde el inicio.

Para ello, ahora no necesitamos utilizar $routeProvider en el config de nuestro módulo principal, si no que la aplicación tendrá un controlador con una configuración de rutas, en la que definiremos que componentes han de mostrarse según el path del navegador.

Antes (versiones 1.3 y anteriores) teníamos algo así:


### app.js
```
angular  
  .module('myApp', ['ngRoute'])
  .config(appConfig);

function appConfig ($routeProvider) {  
  $routeProvider
    .when('/' {
      templateUrl: 'js/components/listado/listado.html',
      controller: 'ListadoController',
      controllerAs: 'listado'
    })
    .when('/item/:itemId', {
      templateUrl: 'js/components/item/item.html',
      controller: 'ItemController',
      controllerAs: 'item'
    });
}
```
Esto serían 2 vistas en la aplicación, en la ruta / tendríamos un listado de items, que controlaría ListadoController y en las rutas /item/:itemId veríamos una vista detalle de cada item, que controlaría ItemController.

Con el nuevo router esto cambiaría a lo siguiente:


### app.js o app.controller.js
```
angular  
  .module('myApp', ['ngNewRouter'])
  .controller('AppController', AppController);

function AppController ($router) {  
  // Si necesitamos implementar algo en el controlador
  // principal, sería aquí
}

AppController.$routeConfig = [  
  { path: '/', component: 'listado' },
  { path: '/item/:itemId', component: 'item' }
];
```
Además de este cambio, hay que tener en cuenta la nomenclatura. Si al componente le llamamos listado, su controlador ha de llamarse ListadoController y sus ficheros a ser posible listado.js y listado.html.

La estructura de ficheros debería ser algo como lo siguiente:
```
- index.html
- js/
    - app.js
    - components/
        - listado/
            - listado.js
            - listado.html
        - item
            - item.js
            - item.html
```
listado.js contendría el ListadoController y listado.html sería la plantilla de ese componente, y lo mismo con item.js e item.html que usaría ItemController.
Por último, lo que también cambia es la directiva que utilizamos para insertar las vistas, antes usábamos ng-view ahora se llama ng-viewport.

```
<!-- index.html -->  
<!DOCTYPE html>  
<html>  
  <head>
    <meta charset="UTF-8">
    <title>Mi Aplicación Angular</title>
  </head>
  <body ng-app="myApp" ng-controller="AppController as app">
    <h1>Mi Aplicación Angular</h1>
    <div ng-viewport></div>

    <script src="vendor/angular.js"></script>
    <script src="vendor/router.es5.js"></script>
    <script src="js/app.js"></script>
    <script src="js/components/listado/listado.js"></script>
    <script src="js/components/item/item.js"></script>
  </body>
</html>  
```
