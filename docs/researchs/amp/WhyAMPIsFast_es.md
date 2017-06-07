Por qué AMP es rápido
El proyecto AMP tiene como objetivo traer renderización instantánea al contenido web. Esta es una lista sin clasificar de optimizaciones que se aplican a todos los documentos basados ​​en AMP, que en conjunto les hace cargar rápidamente. Cada página web puede tener estas optimizaciones, pero las páginas de AMP no pueden no tenerlas.
Si bien este artículo trata sobre las optimizaciones en AMP, también podría ser útil como un tipo de lista de tareas para optimizar un sitio web que no sea de AMP. Si nos falta alguna optimización que pudiera ser benifítica para AMP, por favor deje un comentario o envíenos una solicitud de pull.

## Lazy Load
Los recursos son cargados con pereza cuando es probable que sean vistos por el usuario o cuando el documento esté inactivo.
Uso extensivo de Preconnect
La nueva API de preinstalación se utiliza intensamente para garantizar que las solicitudes HTTP sean lo más rápidas posible cuando se realizan. Esto ayuda a que las solicitudes cargadas con pereza sean más rápidas cuando se hacen.
## Prefetching de recursos cargados perezosamente
Los recursos se cargan lo más tarde posible, pero se buscan lo antes posible. De esa manera las cosas se cargan muy rápido, pero la CPU sólo se utiliza cuando los recursos se muestran a los usuarios.
## Solo JavaScript asíncrono
Los archivos AMP sólo son válidos si todos los archivos JavaScript se cargan asincrónicamente.
## Hojas de estilo en línea
Sólo se permiten hojas de estilo en línea en AMP. Esto elimina 1 o muchas veces más solicitudes HTTP de la ruta de renderización crítica en comparación con la mayoría de las páginas web.
## Las solicitudes de cero HTTP bloquean las descargas de fuentes.
Debido a que todos los JS en AMP tiene el atributo asíncrono y sólo hojas de estilo en línea se permiten, ninguna solicitud HTTP bloquear el navegador de la descarga de fuentes.
## Carga instantánea a través de prerendering
AMP está optimizado para que sea relativamente "barato" y fiable para prerender un recurso. Esto significa que se procesa antes de que el usuario indique explícitamente que desea navegar a una página. Con esto, una página ya estará disponible en el momento en que el usuario la selecciona, lo que lleva a una carga instantánea.
Mientras que prerendering se puede aplicar a todo el contenido web, que puede (y lo hace en la práctica) el uso de una gran cantidad de ancho de banda y CPU. AMP está optimizado para reducir ambos factores:
## Prerendering sólo descarga recursos por encima del doble
Cuando los documentos de AMP obtienen prerendered para la carga instantánea, sólo los recursos por encima del pliegue son realmente descargados. Detalles.
## Prerendering no hace cosas que podrían ser caras en términos de CPU
Cuando los documentos de AMP obtienen prerendered para la carga instantánea, los recursos que podrían utilizar una gran cantidad de CPU (como iframes de terceros) no se descargan. Detalles.
## Priorización inteligente de recursos
Cuando AMP descarga recursos, optimiza las descargas para que los recursos que son actualmente más importantes para el usuario se descarguen primero.
Desacoplamiento del diseño del documento de las descargas de recursos
Los recursos externos, como imágenes, anuncios o iframes, deben indicar su tamaño en el HTML. Eso significa que no tienen que ser descargados primero para diseñar el documento.
## Tamaño máximo de la hoja de estilo
La hoja de estilo en línea tiene un tamaño máximo. Aunque este tamaño es lo suficientemente grande para páginas muy sofisticadas, todavía requiere que el autor de la página practique una buena higiene CSS.
Cambio de cambio DOM de estilo FastDOM
Batch todas las operaciones de medición y mutación de DOM para minimizar los recálculos de estilo en los navegadores.
En la práctica, esto significa que en cada "marco de animación" primero hacemos todas las operaciones de lectura de DOM, y luego cuando se hacen, hacer todas las operaciones de escritura. El resultado es una reducción a 1 estilo de recálculo por fotograma.
## Optimizado para recuentos bajos de recálculos de estilo y diseño
Independiente de lo anterior, AMP está optimizado para evitar costosos recálculos de estilo y diseños en el navegador.
## Mitigación de las peores prácticas de JS de terceros, como document.write
En particular, si JS de terceros usa la API "document.write" de super-malo para el rendimiento, no bloquea la representación de la página principal.
El coste de tiempo de ejecución de la instrumentación de análisis es independiente del número de proveedores de análisis utilizados
La forma analítica que se están implementando en AMP, las páginas que tienen más de un proveedor de análisis no se hinchan con JavaScript adicional y no utilizan una CPU adicional significativa.
## Las extensiones no bloquean el diseño de página
AMP admite extensiones para cosas como cuadros de luz, insertos de instagram, tweets, etc. Si bien estos requieren solicitudes HTTP adicionales, esas solicitudes no bloquean el diseño y la representación de la página.
## Entrega de CDN disponible para todos los documentos de AMP
AMP ofrece un CDN basado en proxy para entregar todos los documentos válidos de AMP, ofreciendo un rendimiento rápido y confiable en todo el contenido de AMP.
Todos los recursos y el documento se cargan desde el mismo origen a través del mismo túnel HTTP 2.0
Cuando se utiliza el CDN AMP basado en proxy, el documento, todos los archivos JS y todas las imágenes se cargan desde el mismo origen que utiliza HTTP 2.0 para obtener la máxima eficiencia.
## Animaciones aceleradas por GPU
Las reglas de CSS relacionadas con la animación en AMP aseguran que las animaciones pueden ser aceleradas por GPU en dispositivos modernos, por lo que son suaves y con mantequilla.