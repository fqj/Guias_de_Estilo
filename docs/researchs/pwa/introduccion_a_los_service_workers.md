Las progressive web apps (pwa) son uno de los grandes puntos de fuga del desarrollo web y supongo que no tardarán en formar parte del ecosistema natural de internet tal y como ocurrió en su día con el responsive design o las single page applications. Uno de sus fundamentos es que la aplicación web se cargue de la forma más rápida posible, casi de manera instantánea, e incluso sea totalmente operativa en modo offline, lo cual se consigue mediante los llamados service workers, que será el tema que trataré en esta entrada. Sin embargo, antes tenemos que recordar en qué consiste la esencia de las pwa: la application shell architecture.

El epíteto de «arquitectura» es exagerado, quizás sería más apropiado hablar de patrón o propuesta, pero por lo demás la shell arch.  es muy interesante. Entre otras cosas, aboga por una distinción neta entre la forma y el contenido, entre la carcasa -que es siempre la misma- y lo que contiene, que se suele obtener de forma dinámica, al menos en las spas, que son la quintaesencia de las pwas. Por ejemplo, este web log que está hecho sobre wordpress, tiene una carcasa -las templates de php-, que se nutre del contenido dinámico de una base de datos. Y en este sentido «contenedor» incluye no solo el frame js de turno, sino también las css, el html, las librerías y cualquier otro elemento estático que sirve para dar forma estructural y gráfica al contenido. Y si este este contenedor, si esta carcasa no va a cambiar, argumentan Addy Osmani y demás artífices de la criatura, podemos guardarla -cachearla- en el ordenador del cliente para no tener que cargarla cada vez que se entra en la aplicación. Aquí es donde entran en escena los service workers.

 

## Service Worker
Un service worker para la caché es una especie de proxy de javaScript, que se ejecuta en el navegador del cliente, el cual intercepta las llamadas HTTP realizadas desde el sitio web que se está visitando. Una vez interceptada una llamada, consulta si el contenido solicitado está cacheado en el ordenador cliente, en cuyo caso lo devuelve ahorrándole el viaje al servidor, y si no lo está aún, cuando llega lo guarda para la próxima vez.

interceptor

De esta manera, incluso aunque se carezca de conexión a Internet, se puede navegar por una aplicación web. Es una nueva manera de enforcar el desarrollo que se conoce como off-line first y sin duda está muy bien; sin embargo, es importante saber que aún no está disponible en todos los navegadores. Chrome y Firefox ya han implementado los sw y, al parecer, pronto estarán también disponibles en el explorer edge; pero no está claro para cuándo estarán disponibles en el Safari. En cualquier caso, esto no debería preocuparnos, pues recordemos que las pwa deben ser «progressive», deben ser perfectamente navegables sin estas mejoras. Dicho de otra forma: si un internauta está usando un navegador obsoleto, se perderá las ventajas que aportan los sw, pero eso no le impedirá moverse por la aplicación web. 

## hola mundo en service workers.

Los sw solo funcionan con el protocolo https. Para hacer pruebas podemos trabajar en localhost, vale cualquier cosa que levante un server en local, como un express o un xampp, o las gh-pages de git hub.

### Hola mundo

Lo primero es preparar el scaffolding que nos servirá para desarrollar este tutorial. No es nada complicado, en un directorio guardamos un archivo js que contendrá el core de la aplicación; en otro un archivo css con alguna que otra regla y en el raíz un index.html y otro archivo js donde escribiremos el sw. Algo así:
```
    ./
    js/
    app.js
    css/
    main.css
    index.html
    sw.js
```
La primera pregunta que podríamos hacernos viendo esta estructura es ¿por qué debemos situar el sw en el directorio raíz? Esto es porque así cubre todo el dominio, pues solo contempla las páginas que se encuentran por debajo de su nivel. Por ejemplo, si tuviéramos esta estructura...
```
    ./
    index.html
    foo/
    foo.html
    sw.js
    bar/
    bar.html
```

El sw solo cachearía lo que se solicita desde el directorio foo hacia abajo y lo que hay en bar quedaría fuera.

Una vez preparada la estructura, en el index.html enlazamos el archivo main.js, en el cual registraremos el sw. 
Los service workers tienen un ciclo de vida (lifecycle), Este abarca desde que se ponen en marcha hasta que concluye su tarea. 
Este ciclo pasa por estas fases:

### 1. Si no existe, se «registra», es decir, se instala.
A continuación, si no se ha producido un error durante el registro, se activa.
Luego entra en un estado ocioso, de latencia, hasta que o bien se produce un evento fetch, que veremos luego, o se da por concluida su tarea.
Para registrar el sw usamos el método register(), el cual acepta dos parámetros: el path del sw y un objeto para definir opciones, aunque de momento no sirve para nada relevante y está pensado para futuras necesidades. Así que en nuestro app.js podemos escribir algo así (el objeto es opcional, una manía que tengo yo de meterlo todo en algún lado):

```
const init = {
     initServiceWorker: ()=> {
/* Comprobamos si el navegador soporta service workers */

        if ('serviceWorker' in navigator) {
            console.log('Service Worker is supported');

        /* En ese caso, registramos nuestro sw mediante el método register(), que devuelve una promesa */
            navigator.serviceWorker.register('./sw.js').then(function(registration) {
                console.log('sw registered: ', registration);
            }).catch(function(err) {
                console.log('Service Worker registration failed: ', err);
            });
        }
    }
};
init.initServiceWorker();
```
Con esto ya tendríamos nuestro primer sw registrado, tal y como podemos comprobar si accedemos a chrome://serviceworker-internals/ en el chrome (y es sorprendente, por cierto, ver la cantidad de sws que tienes ya registrados de varios sitios webs, como el de twitter).

### 2. sw-internals

Con todo listo, ya solo nos falta preparar el propio sw.

Durante el desarrollo del sw viene muy bien trabajar con la pestaña Application de la consola del chrome. Ahí marcamos la opción Update on reload, 
para que al refrescar se actualicen los cambios. De lo contrario, hay que ir abriendo pestañas de incógnito, que es una lata.

### 3. tab-application


El api de los service workers incluye varios interfaces, entre los que se encuentra el ServiceWorkerGlobalScope, que en cierta manera equivaldría al objeto window en el mundo de los sw 
(en términos técnicos, es el contexto global donde se está ejecutando el sw). El nombre es un tanto verboso, pero lo bueno es que dentro del sw podemos referirnos a este objeto con la partícula self.

self.registration
El ServiceWorkerGlobalScope tiene varios métodos, propiedades y eventos, pero de momento solo nos interesan tres cosas: 
    1. los eventos principales que se disparan en el ciclo de vida del sw que vimos antes. Estos son:

        __install__: cuando se instala.
        __activate__: cuando se activa tras la instalación.
        __fetch__: cuando se solicita algo que puede interceptar el sw.

Así que de momento, nuestro script sw podría ser parecido a este:
```
    self.addEventListener('install', function(event) {
        console.log('Installed', event);
        // aquí añadiremos cosas
    });
    self.addEventListener('activate', function(event) {
        console.log('Activated', event);
    // aquí no vamos a añadir nada
    });
    self.addEventListener('fetch', function(event) {
        console.log('fetch', event);
    // aquí añadiremos cosas
    });
```
Durante el evento install vamos a guardar los archivos que queremos cachear, los que interceptará el sw la próxima vez que se soliciten, 
que en nuestro caso podrían ser el index.html, app.js y main.css; y para estar seguros de que no se devuelve la promesa hasta que no está concluida esta tarea
vamos a usar el método waitUntil().
Pero antes de seguir hay que aclarar dónde los vamos a guardar.

El almacenamiento en los sw es tema complejo que se puede solucionar de varias formas, pero para este tutorial utilizaremos dos apis relacionadas directamente con el tema: 
    CacheStorage y Cache.
De la primera nos interesa el método open(nombreCache), que abre o crea la caché indicada como parámetro según exista o no para devolverla como una promesa;
 y de la segunda el método add(), en el que indicaremos el path (la uri) del recurso que queremos guardar, en nuestro caso, las css.

En código, todo lo anterior resulta menos enrevesado, así que vamos a refactorizar ya nuestro evento install recogiendo estas ideas:

```
    self.addEventListener('install', function(event) {
        event.waitUntil(  
            caches.open('nombreCache').then(function(cache) {
                return cache.add('/css/main.css');
            });
        );
    });
```

Que hacemos en la funcion anterior?

   Primero, Pausamos al ejecución de la promesa hasta que no esté todo guardado,
   Segundo, Creamos o abrimos la caché 
   Tercero, Guardamos el fichero css

Una vez hecho esto, en el cache storage debería encontrarse ya el archivo css.

# sw-cache

Para guardar varios archivos, en lugar de add hay que usar el método addAll(), al que se le pasa un array con las uris. Por ejemplo:
```
    let resourcesToCache = [ '/', '/css/main.css', '/js/app.js'];

    caches.open('nombreCache').then(function(cache) {
        return cache.addAll(resourcesToCache);
    })
```
Sin embargo, para que funcione este método en las últimas versiones del chrome, al menos en el momento de escribir estas líneas, hay que cumplir determinados requisitos que nos alejarían del tono sencillo de este tutorial si estamos trabajando en localhost, así que en su lugar usamos el método add() mencionado.

Ahora que ya tenemos un recurso guardado podemos recuperarlo cuando se produzca el evento fetch.
Una vez activado, nuestro sw se queda a la espera de que se solicite un recurso, momento en el que se dispara el evento fetch. 
Entonces intercepta la llamada y responde con el método respondWith() en el caso de que haya encontrado el recurso solicitado en la caché con el método match()
 y si no lo encuentra devolvemos el resultado natural de la llamada con el nuevo api fetch, que no debemos confundir con el evento homónimo.

```
    self.addEventListener ('fetch', function(event) {
        event.respondWith (
            caches.match(event.request)
            .then(function(response) {
                if (response) {
                    return response;
                }
                 return fetch(event.request);
            });
        );
    });
```


 