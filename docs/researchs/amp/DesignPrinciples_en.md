Estos principios de diseño están destinados a guiar el diseño y desarrollo en curso de AMP. Deben ayudarnos a tomar decisiones internamente consistentes.

Experiencia del usuario> Experiencia del desarrollador> Facilidad de implementación.
En caso de duda, haga lo que sea mejor para la experiencia del usuario final, incluso si esto significa que es más difícil para el creador de la página para construir o para el desarrollador de la biblioteca para implementar.

No diseñar para una hipoteca

No diseñar para un futuro hipotético navegador más rápido.
Hemos elegido construir AMP como una biblioteca en el espíritu del manifiesto web extensible para poder arreglar la web de hoy, no la web de mañana.

AMP debe ser rápido en los navegadores de hoy. Cuando ciertas optimizaciones no son posibles con la plataforma de hoy, los desarrolladores de AMP deben participar en el desarrollo de estándares para que estos se agreguen a la plataforma web.

No rompan la red.
Asegúrese de que si AMP tiene interrupciones o problemas, no perjudica al resto de la web. Eso significa que si el caché de Google AMP, la API de URL o la biblioteca falla, debería ser posible que los sitios web y las aplicaciones de consumo degraden graciosamente. Si algo funciona con una caché de AMP, también debería funcionar sin caché.

Resolver problemas en la capa correcta.
P.ej. No integrar las cosas en el lado del cliente, sólo porque eso es más fácil, cuando la experiencia del usuario sería mejor con una integración del lado del servidor.

Sólo hacer las cosas si se puede hacer rápido.
No introduzca componentes o funciones en AMP que no puedan ejecutarse de forma fiable a 60 fps o dificulten la experiencia de carga instantánea en los dispositivos móviles más comunes de hoy en día.

Priorice las cosas que mejoran la experiencia del usuario, pero comprometa cuando sea necesario.
Algunas cosas se pueden hacer rápidamente y siguen siendo una experiencia de usuario terrible. Los AMP deben ofrecer una experiencia de usuario fantástica y la velocidad es sólo una parte de eso. Sólo un compromiso cuando la falta de apoyo para algo se detiene AMP de ser ampliamente utilizado y desplegado.

No hay listas blancas.
No daremos ningún tratamiento especial a sitios, dominios o orígenes específicos, excepto cuando sea necesario por razones de seguridad o rendimiento.