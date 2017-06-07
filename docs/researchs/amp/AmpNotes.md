http://searchengineland.com/need-speed-7-observations-impact-page-speed-future-local-mobile-search-243128


The RAIL Performance Model (Respond, Animate, Idle, Load) by Paul Lewis and Paul Irish

Respond : we want to respond within 100ms to any user action
Animate : 8 ms per frame
Idle work : 50ms chunks
Load : 1000 ms to interactive

Ilya Girgorik:  "High Performance Browser Networking"

How AMP achieves its speed :

amp follow some rules:

Tricks up AMP's sleeve:

    - validation
    - AMP-blessed script exclusively
    - Static layout
    - Async loading of "extension" content
    - Batched DOM read/write
    - Single source analitycs
    - Smart pre-rending

99% of AMP pages load are faster than 8 seconds
NON AMP control pages loads in 22 seconds on average

Under 1 second median load time measured across all AMP pages loaded from google seaarch

From fast to instant:

pre-rendering

There's apparently 640.000 web pages already implemented AMP

the font is critical in the path of rendering a web pages

- static responsive layout
- Dom mutation batching
- FASTDOM
- instant loading

Full list of AMP optimizations: j.mp/amp-speed
Docs: ampproject.org/docs/
GitHub: github.com/ampproject/amphtml

1950 pull request from 160 contributors

Bookkeeping:
ammpbyexample.com
developers.google.com/amp/cache/

Phones have limted CPU and RAM

Is a open-source project and they are shippiong new releases every week

Web App Manifest

Tool usadas para wapo/wap:  
SW-Precache
Buid-time cache generation for app shell

SW-Toolbox
Client-side strategies for content caching


En lo relativo al posicionamiento SEO, la tendencia actual es que Google está comenzando a posicionar en los primeros resultados de las búsquedas orgánicas desde dispositivos móviles contenidos implementados bajo la tecnología AMP.

Google, que el pasado 21 de abril realizó un cambio en su algoritmo por el cuál penalizaría a aquellos sitios que no tuviesen una correcta usabilidad móvil, no ha dejado de investigar hasta lanzar recientemente un proyecto que seguramente favorecerá tu posicionamiento SEO. Los principales objetivos de este proyecto consisten en agilizar y reducir notablemente los tiempos de carga en usuarios con conexiones lentas y facilitar la lectura del contenido.

Qué es AMP ( Accelerated Mobile Pages ) ?
Accelerated Mobile Pages o AMP Project, nombre del proyecto lanzado por el famoso buscador y cada vez más conocido por la comunidad de desarrolladores, es una iniciativa de código abierto que ayuda a estos, a crear sitios web con un tiempo de carga casi instantáneo.

Medios que ya han implementado AMP Project
Muchos han sido los medios que se han animado a participar en este proyecto como por ejemplo:

The Washington Post
The Wall Street Journal
The New York Times
The Guardian
Time
El País,
BBC
Mashable
BuzzFeed
Estos medios, se han visto alertados por el volumen tan grande de usuarios que tienen dificultades para navegar por sus sitios webs, debido al gran peso de recursos que contiene la página y la lentitud de las conexiones que en ocasiones tienen los usuarios.


AMP Caché
Con el objetivo de mejorar todo el desarrollo antes mencionado, Google pone a disposición de los desarrolladores la integración de AMP Caché. Este consiste en un sistema de distribución de contenido y archivos basada en proxy para proporcionar todos los documentos de AMP válidos. Esta caché almacena a modo de captura los diferentes HTML del sitio web de tal modo que la entrega sea aún más ágil. De este modo, todos los archivos se cargan desde el mismo origen que además usa http 2.0 por lo que la entrega de los mismos tendrá la máxima eficiencia.

Otra de las ventajas de su implementación, es la inclusión de un sistema de validación que garantiza el correcto funcionamiento de la página tras realizar diversas comprobaciones en el marcado de la página.

Por último otra de las grandes ventajas de AMP es la validación de errores integrada. Esta permite a los desarrolladores comprobar errores de etiquetado compatible con AMP HTML que pueden afectar al correcto funcionamiento de tu página web.

Tras el lanzamiento de AMP, nace AMP Lite y RAISR.
Las nuevas armas de Google para que navegues a máxima velocidad aún teniendo una conexión limitada.

Con el objetivo de ofrecer la mejor experiencia a los usuarios mientras navegan por internet con una conexión lenta, Google ha lanzado una versión más ligera del proyecto AMP (Accelerated Mobile Pages). Esta nueva versión llamada AMP Lite mejora en un 45% el consumo de los datos de su predecesor. Para ello, se comprime gran parte de la información gráfica. En este proceso, Google comprime las imágenes en un formato llamado WebP sólo con aquellos navegadores con los cuáles es compatible. Estas imágenes hacen uso de otra gran novedad lanzada por el famoso buscador, el algoritmo RAISR. Este algoritmo es capaz de reducir el peso de una imagen en un 75% aunque con una ligera perdida de la calidad, en ocasiones casi inapreciable. Con estos dos avances, Google se pone a la cabeza en la experiencia de usuario en dispositivos móviles.

Hoy hablaré sobre las páginas AMP de Google, una iniciativa conocida como “AMP Project” cuyo objetivo final es que las páginas web carguen más rápido cuando un usuario acceden a un contenido a partir de las SERPs (Search Engine Results Pages) (resultados de búsqueda). A pesar de que el propulsor ha sido el gran Google, ha buscado aliados entre los medios de comunicación a nivel internacional, los cuales han querido manifestar su apoyo

 y utilizan hasta 10 veces menos datos. En los resultados de búsqueda (SERPs) dichas páginas figuran con un rayo dentro un círculo con las siglas AMP. Estas páginas se caracterizan por poseer HTML reestrictivo, con nada de llamada a servidores externos y que se sirven las páginas desde la cache de Google, siendo esta la razón de su carga tan rápida.


# DESCRIPCION GENERAL DE ACCELERATED MOBILES 

## ¿Qué es el proyecto Accelerated Mobile Pages?
El proyecto Accelerated Mobile Pages (AMP) es una iniciativa de software libre que surge de los debates entre editores y empresas tecnológicas sobre la necesidad de mejorar el ecosistema de contenido móvil en su conjunto para todos: editores, plataformas de consumidores, creadores y usuarios.

Hoy en día, se espera que el contenido de las páginas web se cargue muy rápido y que la navegación sea sencilla. En realidad, sin embargo, el contenido puede tardar varios segundos en cargarse o puede no llegar a cargarse completamente porque los usuarios abandonan las páginas lentas. Las páginas Accelerated Mobile Pages son páginas web diseñadas para cargarse casi instantáneamente, en un paso más hacia una Web móvil mejor para todo el mundo.

## ¿Cuáles son las ventajas de Accelerated Mobile Pages?
Nos importa la velocidad; la inmediatez es el objetivo. Las investigaciones han demostrado que los porcentajes de rebote son más altos en páginas web que se cargan más lentamente. El uso del formato AMP fomentará que los usuarios consuman más contenido e interaccionen con él. Pero no solo se trata de velocidad y rendimiento. También queremos promover una mayor distribución con la finalidad de que los editores puedan aprovechar el potencial de la Web abierta para que su contenido se muestre rápidamente en todas partes, tanto en plataformas como en aplicaciones, y esto genere más ingresos a partir de anuncios y suscripciones.

## ¿Cómo funciona Accelerated Mobile Pages?
Las páginas Accelerated Mobile Pages funcionan como cualquier otra página HTML, pero solo admiten un conjunto limitado de funcionalidades técnicas que se define en las especificaciones de AMP de software libre y que se rige por estas mismas especificaciones. Igual que todas las páginas web, Accelerated Mobile Pages se cargará en todos los navegadores modernos y en todas las vistas web de aplicaciones.

Los archivos de AMP se benefician de diferentes enfoques técnicos y arquitectónicos que priorizan la velocidad para proporcionar una experiencia más rápida para los usuarios. Los desarrolladores de AMP pueden utilizar una biblioteca rica y cada vez más completa de componentes web que ofrecen la posibilidad de insertar objetos rich media, como vídeo y publicaciones en redes sociales, mostrar publicidad o recopilar análisis. El objetivo no es homogeneizar la forma en que se ve y se percibe el contenido, sino crear un núcleo técnico más común entre las páginas que acelere el tiempo de carga.

Además, los archivos de AMP pueden almacenarse en caché en la nube, de modo que se reduce el tiempo necesario para que el contenido llegue a los dispositivos móviles de los usuarios. Al utilizar el formato AMP, los creadores de contenidos ponen los archivos de AMP a disposición de terceros para que los almacenen en caché. En estas circunstancias, los editores siguen controlando su contenido, pero las plataformas pueden almacenar el contenido fácilmente en caché o reproducirlo para que la velocidad de publicación sea óptima para los usuarios. Google ofrece una caché que puede utilizar todo el mundo sin coste alguno, se trata de Google AMP Cache donde almacenamos todas las páginas AMP. Otras empresas también pueden crear su propia caché de AMP.

En resumen, el objetivo de este proyecto es combinar una funcionalidad técnica limitada con un sistema de distribución creado en torno al almacenamiento en la memoria caché para ofrecer páginas con un mejor rendimiento y más audiencia para los editores.

## ¿Por qué se utiliza software libre en el proyecto Accelerated Mobile Pages?
Las empresas que participan en el proyecto quieren que la Web móvil funcione mejor para todo el mundo, no solo para una plataforma, un conjunto de tecnologías o un conjunto de editores. Al crear el proyecto con software libre, los usuarios pueden compartir y aportar ideas y código para conseguir una Web móvil más rápida. Acabamos de iniciar este recorrido, en el que esperamos que se unan otros editores y empresas tecnológicas.

## ¿Quién puede usar Accelerated Mobile Pages?
El proyecto está abierto a todas las partes del ecosistema: editores, plataformas de consumidores y creadores. Para hacerte una idea de quiénes son algunas de las empresas y de los sitios web que utilizan AMP, ve a la página Quién.

## ¿Cuáles son las consecuencias de utilizar Accelerated Mobile Pages?
Al utilizar el formato AMP, los creadores de contenidos ponen los archivos de AMP a disposición de terceros para que los rastreen, los indexen y los muestren (de conformidad con el protocolo de exclusión de robots) y los almacenen en caché.

## ¿Qué tipo de contenido funciona mejor con Accelerated Mobile Pages?
El objetivo es que todo el contenido publicado, desde noticias hasta vídeos y desde blogs hasta fotos y GIFs, funcionen con Accelerated Mobile Pages.

Como editor, ¿me llevará más trabajo hacer que mi contenido funcione con Accelerated Mobile Pages?
De entrada, no mucho. Como "AMP HTML" está formado en su totalidad por tecnologías web existentes, el proceso de desarrollo reproduce el que los editores están utilizando en la actualidad. Los editores pueden familiarizarse con AMP HTML en GitHub. Creemos que los que ya utilicen el proceso actual no encontrarán difícil este aprendizaje.

## ¿Cómo puede un editor generar contenido en AMP HTML?
Los editores y los proveedores de sistemas de gestión de contenido (CMS) pueden desarrollar una integración para generar contenido de AMP con su CMS. Automattic ya ha publicado un complemento de AMP para WordPress, y esperamos que todos los sistemas de gestión de contenido ofrezcan compatibilidad con las páginas AMP HTML.

Participación de plataformas y empresas tecnológicas
## ¿Cómo puede una plataforma de consumidores participar en Accelerated Mobile Pages?
El proyecto está abierto a todo el mundo, y los miembros actuales están encantados de colaborar en esta iniciativa con plataformas de usuarios. Google ha abierto su caché para que todo el mundo pueda utilizarla de forma gratuita, incluidas las plataformas de consumidores que quieran mostrar contenido de AMP en su entorno. Ponte en contacto con nosotros a través de GitHub y responderemos a tus preguntas lo antes posible.

## ¿Cómo se gestionan los análisis en el formato AMP?
Un objetivo de diseño fundamental del proyecto es garantizar que los editores puedan obtener datos de análisis útiles. Aunque la compatibilidad con análisis en la versión de demostración es muy limitada, esperamos que la especificación sea compatible con diferente información de análisis y que se integre con sistemas de terceros sin comprometer la velocidad ni el tamaño del archivo de AMP. Hay varios proveedores de análisis que ya participan en el proyecto.


