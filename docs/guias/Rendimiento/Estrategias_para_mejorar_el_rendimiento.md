<style>
h1 {
    color:white;
    background:#7ab6df;
    width:100%;
    padding-left:0.5em;
    padding:auto;
    font-size:3em;
    font-weight:bold;
    letter-spacing:0.01em
 }
h2 {
    color:#7ab6df;
    background:#ffffff;
    font-weight:bold;
    width:100%;
    padding:5px;
    font-size:30px;
    letter-spacing:0.01em;
    border-bottom:1px solid #7ab6df!important;
    margin-top: 40px;
    margin-bottom:40px;
}
h3 {
    color:#7ab6df;
    background:#ffffff;
    width:100%;
    padding:3px;
    font-size:20px;
    font-weight:bold;
    border-bottom:1px solid #7ab6df!important;
    letter-spacing:0.01em;
}
pre {
    background:#e1f0fa!important;
    border: 1px solid #8ac6ef
}
code {
    color:#222;
    font-size:1em;
    font-weight:300;
}

blockquote {
    padding: 1em!important;
    color: #000!important;
    border-left: 0.25em solid #ce7206!important;
    background:#fbebc0;
}
ul {margin:1em}
li{margin:0.5em}
</style>



### Estrategia de carga de la página para obtener un mejor rendimiento 

1. Carga lo esencial primero.
2. Aplaza la carga del contenido no esencial para después. Carga condicional.
3. Usa un renderizado progresivo de imágenes.
    
    * Crear el JPG como progressive.
    * Crear el PNG como interlaced.
    * Mostrar un place holder con el bloque y el color mayoritario de la imagen (esta estrategia la usa google en el buscador de imágenes). 
    * Usa SVG (cuando se pueda).
    * Utiliza Tipografias (cuando se pueda).         
    * Tailored image sizes: Utilizar tamaños de imágenes diferentes según el dispositivo. 

4. Auto-precarga o Cache predictivo de navegador.
5. Usar eventos touch.
    - Esto aplica solo a las aplicaciones móviles. Cuando se toca la pantalla en necesario un tiempo que puede ser entre 300-500 milisegundos 
    para traducir el elevento de tipo touch a un evento de tipo click.

6. Para tareas pesadas usar Webworkers.

### Estrategia para mejorar la apreciación de velocidad

1. Si algo va a tardar mucho tiempo indica la razón.
2. Muestra indicadores de progreso.

### The PRPL Pattern (Progressive Web Apps)

Three cutting-edge new features of the web platform—Web Components, HTTP/2 + Server Push, and Service Worker—all work seamlessly together to provide a totally new and amazingly efficient way to deliver applications to users.

We call this the "PRPL Pattern", and the Polymer App Toolbox and Polymer CLI make it easy to build an application to use this strategy for delivery. The PRPL pattern stands for:
