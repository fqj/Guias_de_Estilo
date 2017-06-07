# **Cambios entre AngularJS y Angular2**

## Controladores y Componentes

### En Angular 1:
```
<body ng-controller="PeliculasController as peli">  
  <h3>{{peli.data.titulo}}</h3>
  <h3 ng-bind="peli.data.titulo"></h3>
</body>  
<script type="text/javascript">  
(function (){
  angular
    .module('app')
    .controller('PeliculasController', PeliculasController);
 
  function PeliculasController() {
    var peli = this;
    peli.data= { id: 45, titulo: 'Una historia real' };
  }
})();
</script>  
```

### En Angular 2
```
import { Component } from 'angular2/core';
 
@Component({
  selector: 'pelicula',
  template: '<h2>{{pelicula.titulo}}</h2>'
})
export class PeliculaComponent {  
  public pelicula = { id: 45, titulo: 'Una historia real' };
}
```

## Bootstrapping

### En Angular 1:
```
<html ng-app="app">  
```
### En Angular 2:
```
import { bootstrap } from 'angular2/platform/browser';  
import { AppComponent } from './app.component';

bootstrap(AppComponent);  
```
<br>
<br>
<br>
<br>


## Directivas

### En Angular 1:
```
<ul>  
  <li ng-repeat="peli in peliculas.data">
    {{peli.titulo}}
  </li>
</ul> 
``` 

### En Angular 2:
```
<ul>  
  <li *ngFor="#peli of peliculas">
    {{peli.titulo}}
  </li>
</ul> 
```
## Data Binding

### En Angular 1:
```
<!-- interpolación --> 
<h4>{{peliculas.data.titulo}}</h4>
 
<!-- one way binding --> 
<h4 ng-bind="peliculas.data.titulo"></h4>
 
<!-- two way binding --> 
<input ng-model="peliculas.data.titulo">
 
<!-- eventos --> 
<button 
  ng-click="peliculas.log('click')"
  ng-blur="peliculas.log('blur')">
Aceptar
</button>
```

### En Angular 2:
```
<!-- interpolacion --> 
<h4>{{pelicula.titulo}}</h4>
 
<!-- one way binding --> 
<h4 [innerText]="pelicula.titulo"></h4>
 
<!-- two way binding --> 
<input [(ngModel)]="pelicula.titulo">
 
<!-- eventos --> 
<button 
  (click)="log('click')"
  (blur)="log('blur')">Aceptar</button>
  ```

<br>
<br>
<br>

## Servicios

En Angular 1, había muchas formas de crear servicios, en Angular 2, sólo hay una forma y es definiendo una clase Injectable.
### En Angular 1:
```
angular  
  .module('app')
  .service('PeliculasService', PeliculasService);
 
function PeliculasService() {  
  this.getPeliculas = function () {
    return [
      { id: 1, titulo: 'Peli 1' },
      { id: 2, titulo: 'Peli 2' },
      { id: 3, titulo: 'Peli 3' }
    ];
  };
}
```
### En Angular 2:
```
import { Injectable } from 'angular2/core';
 
@Injectable()
export class PeliculasService {  
  public getPeliculas = () => [
    { id: 1, titulo: 'Peli 1' },
      { id: 2, titulo: 'Peli 2' },
      { id: 3, titulo: 'Peli 3' }
  ];
}
```

## Inyección de dependencias

### En Angular 1:
```
angular  
  .module('app')
  .controller('PeliculasController', PeliculasController);
 
PeliculasController.$inject = ['PeliculasService'];
 
function PeliculasController(PeliculasService) {  
  var peliculas = this;
  peliculas.data = PeliculasService.getPeliculas();
}
```
### En Angular 2:
```
import { PeliculasService } from './peliculas.service';
 
@Component({
  selector: 'peliculas',
  templateUrl: 'app/peliculas.component.html',
  providers: [PeliculasService]
})
export class PeliculasComponent {  
  constructor(private _peliculasService: PeliculasService) {}
  public peliculas = this._peliculasService.getPeliculas();
}
```
