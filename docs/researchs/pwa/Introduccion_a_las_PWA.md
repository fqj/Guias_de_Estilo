Después de haber defendido la web de los contenidos de calidad gracias a las mejoras de sus algortimos de indexación, algo de lo que nos hemos beneficiado todos menos los piratillas del seo, la siguiente cruzada de google está siendo la velocidad, un tema que en principio suena interesante cuanto menos como punto de fuga para mejorar las páginas y aplicaciones web, algo fundamental en estos tiempos en los que se navega cada vez con mayor frecuencia con dispositivos móviles de conexiones inmundas.

Una de las iniciativas que han lanzado en este sentido son las Accelerated Mobile Pages (AMP), que en esencia consiste en dosificar lo que se va enviando de tal manera que el navegante disponga cuanto antes de contenido relevante. No tengo muy clara mi opinión al respecto, necesitaría profundizar más en el tema, pero, en cualquier caso, es una solución enfocada a las páginas, sobre todo las que van cargadas de publicidad y contenidos superfluos, y se queda corta cuando se trata de aplicaciones web. Para estos casos están manejando otra iniciativa que me parece más interesante: las progresive web apps.

Las webs molan más que las apps
Tal y como explicó Join Alex Russell, uno de los padres de la criatura, en una de las charlas del Chrome Dev Summit de 2015, las aplicaciones para dispositivos móviles son menos cómodas que las webs, pues hay que recorrer un camino demasiado largo para llegar hasta el contenido:

* 1.conocer su existencia,
* 2.abrir una aplicación para descargarse aplicaciones, como el Play Store,
* 3.seleccionarla,
* 4.darle permisos de instalación,
* 5.esperar a que se descargue,
* 6.una vez descargada, aguardar cada vez que se actualice...

En fin, que es bastante más engorroso que acceder a una web desde el navegador, ya sea desde un ordenador o desde un dispositivo móvil, pues basta con introducir una url o un concepto en la barra del navegador o pulsar un enlace o seleccionar un favorito que hayamos guardado.

Además, añado yo, en general, las aplicaciones están cerradas en sí mismas. En cambio desde una web puedo pasar a otra o compartirla en mis redes sociales. Y, sin duda, son más económicas. Cuesta menos desarrollar una sola web responsive y multidispositivo que tantas aplicaciones nativas como sistemas operativos hay en el mercado (cuanto menos, IOS, Android y Windows), incluso aunque estas últimas sean solo webs compiladas con Cordova o cualquier otra herramienta similar. Y por desarrollar debe entenderse también mantener.

En síntesis, las webs son más accesibles, «descubribles» (no sé cómo diantres traducir esto), manejables y económicas que las aplicaciones móviles.

Al lado de esta idea fuerza, podemos incluir otra para completar el cuadro y es que desde hace tiempo existe la tecnología y la demanda para desarrollar aplicaciones web, también como conocidas como single page applications. Gracias a herramientas como angular, backbone, meteor o polymer, ahora es relativamente sencillo preparar una web que formalmente, en apariencia, se comporta como una aplicación de escritorio con pantallas en lugar de páginas.

Alex Russell y Frances Berriman le dieron una vuelta de rosca a estos conceptos y los llevaron más allá con una propuesta que denominaron progressive web apps, en la que sugieren una serie de técnicas para que las webs se asemejen aún más a las aplicaciones, en la medida de las posibilidades de cada navegador, por ejemplo mediante la carga casi instantánea de contenidos gracias a mecanismos de caché o la notificación de mensajes.

Russell mencionaba una serie de principios que debían cumplir este tipos de webs, que Addy Osmany explica en otro artículo fundamental para entrar en faena titulado Getting started with Progressive Web Apps. No los traduzco porque se entienden bien:

* Progressive - Work for every user, regardless of browser choice because they’re built with progressive enhancement as a core tenet.
* Responsive - Fit any form factor, desktop, mobile, tablet, or whatever is next.
* Connectivity independent - Enhanced with service workers to work offline or on low quality networks.
* App-like - Use the app-shell model to provide app-style navigations and interactions.
* Fresh - Always up-to-date thanks to the service worker update process.
* Safe - Served via TLS to prevent snooping and ensure content hasn’t been tampered with.
* Discoverable - Are identifiable as “applications” thanks to W3C manifests and service worker registration scope allowing search engines to find them.
* Re-engageable - Make re-engagement easy through features like push notifications.
* Installable - Allow users to “keep” apps they find most useful on their home screen without the hassle of an app store.
* Linkable - Easily share via URL and not require complex installation.

## Los fundamentos de las progressive web apps
Osmany, además, menciona una serie de fundamentos sobre los que construir las progresive web apps que son muy interesantes:

* Existirá un web app manifest, un fichero json con datos básicos de la aplicación que podrá ser interpretado por los navegadores.
* Se podrá instalar un acceso directo en el escritorio (Home Screen Banner).
* Correrá bajo https.
* Se usarán services workers para cachear todo lo cacheable.
* Se usaran push notifications.
* Seguirán el patron RAIL Performance Model para mejorar la experiencia de usuario.
* Estarán diseñadas siguiendo las directrices de lo que denominan Application Shell Architecture, que en esencia consiste en separar los templates, la carcasa, del contenido, que se obtiene de forma dinámica, y aplicar varias técnicas de optimización.