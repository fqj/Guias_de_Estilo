# Diferencias entre angular1.5 y Angular2

De la versión 1.5 en adelante, las actualizaciones de angular están encaminadas a equiparar las dos familias y los cambios entre unas y otras cada vez serán mayores. Si una compañía comienza a sacar sus proyectos al ritmo de las versiones nuevas que vayan saliendo, en apenas un lustro corre el riesgo de tener un reguero de tecnologías distintas, lo que en principio no es muy recomendable.

## incompatibles con el SEO
La familia 1.*, al menos las versiones conocidas hasta ahora, son incompatibles con el SEO. Los bots son todavía incapaces de renderizar correctamente el contenido de una single page application que trabaja contra un api-rest, por lo que nos ha obligado a realizar sobreesfuerzos absurdos. En teoría, con la versión 2 todo esto será menos problemático.

TODO: Mirar Angular Universal

## Rendimineto en dispositivos

Angular 1.5 tiene un mal rendimineto en dispositivos poco potentes, como es el caso de los móviles, pero al parecer la 2 es hasta 5 veces más rápida.

## Diferencias entre los servicios http de AngularJS y Angular 2

La diferencia principal es que el $http de AngularJS devuelve Promises mientras que el Http de Angular 2 devuelve Observables

* Los observables se pueden cancelar, a diferencia de las promises
* Las promises solo pueden devolver una respuesta (a menos que combines varias promises con $q.all)

Mientras AngularJS comprobaba a cada ciclo si un objeto había cambiado, Angular2 se suscribe al objeto para ser notificado cuando éste cambie.