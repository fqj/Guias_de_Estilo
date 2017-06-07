# Flujo de trabajo con git-flow

## Metodología
La forma en la que vamos a trabajar se basa en la metodología `git-flow, modelo propuesto originalmente por Vincent Driessen: ["A successfull Git branching model"](http://nvie.com/git-model)


En resumen el modelo basa en la existencia permamente de dos ramas:

- *`master`*: rama donde van a residir las versiones estables del producto, serán las que se liberen a producción. En principio cada commit de esta rama deberá llevar su tag correspondiente de número de versión. **SOBRE ESTA RAMA NO SE DEBE HACER UN COMMIT DIRECTO NUNCA**, solo debe recibir merges desde ramas inferiores.

- *`develop`*: rama de desarrollo, aquí residirá todo el código que se va generando mergeado desde las ramas features, **al igual que master sobre esta rama no se debe hacer un commit directo nunca**.

Además de estas dos ramas, también tendremos ramas temporales:

- *`feature/nombre_rama_feature`*: Son ramas que deberán contener el bloque de una funcionalidad específica. Se deben crear a partir de la rama *develop* y morir al integrarse de vuelta en la misma.

- *`hotfix/nombre_rama_hotfix`*: Se crean a partir de la rama master. Son ramas inmediatas que se crean para solucionar bugs críticos en el código ya liberado. 
  Al terminar se integran de vuelta a *master* directamente y se hacen descender los cambios también hacia *develop* para incorporar
  el nuevo código al desarrollo en proceso. *La única excepción de esta regla es que cuando exista rama release los cambios deben mergearse hacia release y no hacia develop*. Una vez completado el ciclo la rama muere o queda
  congelada, por lo que si en el futuro es necesario integrar otro grupo de fixes será necesario crear otra rama hotfix.

- *`release/nombre_rama_release`*: Cuando se quiere liberar una nueva versión del producto, se crea una rama release candidate directamente desde *develop*. 
  Una vez creada esta rama sobre ella no se incorpora ninguna funcionalidad nueva siendo cada commit orientado expresamente a la 
  solución de errores para su estabilización y lanzamiento a *master*. Una vez estabilizada y pasados los tests correspondientes se mergean los cambios hacia 
  *master* y se taggea con una nueva versión. Luego se mergean de vuelta a *develop* para integrar los fixes creados y se congela o muere la rama release.

## Herramienta automatizada

En esencia git-flow es una metodología que plantea una estructura de ramas y unos procedimientos determinados
con lo cual puede implementarse usando cualquier cliente git, incluso desde la línea de comandos. No obstante 
existe una herramienta que nos facilita su uso y con unas sentencias específicas automatiza los todos los procedimientos
descritos anteriormente: [https://github.com/nvie/gitflow](https://github.com/nvie/gitflow)

#### Instrucciones de instalación: 

[https://github.com/nvie/gitflow/wiki/Installation](https://github.com/nvie/gitflow/wiki/Installation)


#### Ejemplos de uso

Algunos comandos para la creación y finalización de features y hotfixes:

##### Features:
```
// Al iniciar una funcionalidad. Nos crea la rama y nos posiciona en ella.

$ git flow feature start nombre_de_feature
```
 
 
```
// Ya hemos hecho todos los commits en la feature y hemos terminado el desarrollo. Con este 
comando nos fusiona la rama con develop, borra la rama y cambiamos a develop.

$ git flow feature finish nombre_de_feature
```
    
```
// volver a la rama de una feature para seguir desarrollando en ella.

git flow feature checkout nombre_de_feature
```


##### HotFix:

```
// Se crea la rama a partir de master para comenzar a desarrollar el hotfix.

git flow hotfix start nombre_hotfix
```


```
// Se ha terminado de solucionar el error. Esto fusiona los cambios tanto a develop como a master.

git flow hotfix finish nombre_hotfix
``` 

[(fuente y documentación original)]([https://github.com/nvie/gitflow](https://github.com/nvie/gitflow))