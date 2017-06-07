1. Crear una página AMP⚡ HTML
2. Incluir una imagen
3. Modificar la presentación y el diseño
4. Versión preliminar y validación
5. Prepara tu página para la detección y la distribución
6. Últimos pasos antes de la publicación


# Crea una página AMP⚡ HTML
El siguiente marcado es un punto de partida o código estándar aceptable. Cópialo y guárdalo en un archivo con extensión .html.
```html
<!doctype html>
<html amp lang="es">
  <head>
    <meta charset="utf-8">
    <script async src="https://cdn.ampproject.org/v0.js"></script>
    <title>Hola, AMP</title>
    <link rel="canonical" href="http://example.ampproject.org/article-metadata.html" />
    <meta name="viewport" content="width=device-width,minimum-scale=1,initial-scale=1">
    <script type="application/ld+json">
      {
        "@context": "http://schema.org",
        "@type": "NewsArticle",
        "headline": "Open-source framework for publishing content",
        "datePublished": "2015-10-07T12:02:41Z",
        "image": [
          "logo.jpg"
        ]
      }
    </script>
    <style amp-boilerplate>body{-webkit-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-moz-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-ms-animation:-amp-start 8s steps(1,end) 0s 1 normal both;animation:-amp-start 8s steps(1,end) 0s 1 normal both}@-webkit-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-moz-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-ms-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-o-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}</style><noscript><style amp-boilerplate>body{-webkit-animation:none;-moz-animation:none;-ms-animation:none;animation:none}</style></noscript>
  </head>
  <body>
    <h1>Bienvenido a la web móvil</h1>
  </body>
</html>
```
El contenido del cuerpo, hasta ahora, es bastante sencillo. 
Sin embargo, hay mucho más código en la etiqueta <head> de la página que podría no ser evidente de inmediato. 
Analicemos el marcado obligatorio.

### **Marcado obligatorio**
Los documentos AMP HTML DEBEN:

1. Comenzar con el tipo de documento <!doctype html>.
2. Contener la etiqueta <html ⚡> en el nivel superior (también se acepta <html amp>).
3. Contener las etiquetas <head> y <body> (opcionales en HTML).
4. Contener la etiqueta <meta charset="utf-8"> como el primer hijo de su etiqueta <head>.
5. Contener la etiqueta <script async src="https://cdn.ampproject.org/v0.js"></script> como el segundo hijo de su etiqueta <head> (esto incluye y carga la biblioteca AMP JS).
6. Contener una etiqueta <link rel="canonical" href="$SOME_URL" /> en la etiqueta <head> orientada a la versión de HTML común del documento de AMP HTML o a sí misma si no existiera dicha versión de HTML.
7. Contener una etiqueta <meta name="viewport" content="width=device-width,minimum-scale=1"> en la etiqueta <head>. También se recomienda incluir initial-scale=1.
8. Contener lo siguiente en su etiqueta <head>: <style amp-boilerplate>body{-webkit-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-moz-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-ms-animation:-amp-start 8s steps(1,end) 0s 1 normal both;animation:-amp-start 8s steps(1,end) 0s 1 normal both}@-webkit-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-moz-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-ms-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-o-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}</style><noscript><style amp-boilerplate>body{-webkit-animation:none;-moz-animation:none;-ms-animation:none;animation:none}</style></noscript>

### **Meta datos opcionales**
Además de los requisitos básicos, en nuestro ejemplo también se incluye una definición Schema.org en el <head>, que no es un requisito estricto para AMP, pero es un requisito para poder distribuir tu contenido en determinados sitios.
Por ejemplo, en la demostración del carrusel de novedades sobre Búsqueda de Google (pruébalo en tu teléfono).

¡Buenas noticias! Eso es todo lo que necesitamos para crear nuestra primera página AMP, aunque por supuesto aún no hay demasiadas noticias respecto del <body>. En la próxima sección, veremos la manera de agregar componentes básicos, como imágenes, elementos de AMP personalizados, de dar estilo a tu página y de definir un diseño responsivo.


# Incluir una imagen
La mayoría de las etiquetas HTML se pueden usar directamente en AMP HTML, pero algunas, como <img>, se reemplazan por etiquetas AMP HTML personalizadas equivalentes o ligeramente optimizadas, y unas pocas etiquetas problemáticas se inhabilitan directamente.  
Para demostrar el aspecto que tendría el marcado adicional, a continuación se muestra el código requerido para integrar una imagen a la página:
```html
<amp-img src="bienvenido.jpg" alt="Bienvenido" height="400" width="800"></amp-img>
```

# Modificar la presentación y el diseño

## Modificar la presentación
Las AMP son páginas web; el diseño de estas y de sus elementos se realiza a través de propiedades CSS comunes. Da estilo a los elementos con selectores de clase o elemento en una hoja de estilo en línea en el "head" llamada "style amp-custom":

```html
<style amp-custom>
  /* Cualquier estilo personalizado va aquí */
  body {
    background-color: white;
  }
  amp-img {
    background-color: gray;
    border: 1px solid black;
  }
</style>
```
Las páginas AMP pueden tener solo una hoja de estilo integrada y hay ciertos selectores que no puedes usar. (mas informacion en el fichero
[css_restrictions_es.md](css_restrictions_es.md) alojado en este mismo repositorio)

## Controla el diseño
AMP sigue reglas estrictas al distribuir elementos en la página.
En una página HTML normal, CSS se usa casi exclusivamente para distribuir elementos. 
Sin embargo, por motivos de rendimiento, AMP requiere que todos los elementos tengan un tamaño explícito configurado desde el principio.

# Versión preliminar y validación
Se puede acceder a la versión preliminar de la página AMP como lo harías con cualquier otro sitio HTML estático. 
No hay pasos de compilación ni procesamientos previos obligatorios. Tienes una de las siguientes opciones:

* Abrirla directamente en el navegador desde el sistema de archivos (ciertos elementos podrían no funcionar debido a errores en XMLHttpRequests).
* Usar un servidor web local.
A continuación, asegúrate de que tu página AMP sea válida; de lo contrario, no podrá detectarse ni distribuirse mediante plataformas de terceros como la Búsqueda de Google. Para la validación:

1. Abre tu página en el navegador.
2. Agrega “#development=1” a la URL; por ejemplo, http://localhost:8000/released.amp.html#development=1.
3. Abre la consola DevTools de Chrome y busca errores de validación.

# Prepara tu página para la detección y la distribución
En algunos casos, podrías tener una versión AMP y una versión no AMP de la misma página; por ejemplo, un artículo informativo. Considera lo siguiente: Si la Búsqueda de Google encuentra la versión no AMP de esa página, ¿cómo sabe que existe una versión AMP?

## Vinculación de páginas con<link>
Para resolver este problema, agregamos información sobre la página AMP a la página no AMP y viceversa en forma de etiquetas <link> en el <head>.

Agrega lo siguiente a la página no AMP:
```html
<link rel="amphtml" href="https://www.ejemplo.com/url/al/documento/amp.html">
```
Y esto a la página AMP
```html
<link rel="canonical" href="https://www.ejemplo.com/url/al/documento/completo.html">
```

¿Qué sucede si tengo una sola página?
Si solo tienes una página y es AMP, debes agregarle el vínculo canónico. Este luego simplemente apuntará a sí mismo.

<link rel="canonical" href="https://www.ejemplo.com/url/al/documento/amp.html">