# AngularJS vs ReactJS

## ReactJS no es un framework, es una librería

El primer motivo es que AngularJS se presenta como un framework total. Un framework donde podemos hacer todo lo necesario en una aplicación front compleja. Podemos incluir ciertas extensiones al framework, pero por lo general, el core de AngularJS nos va a permitir realizar un porcentaje altísimo de aplicaciones sin tener que incluir grandes cambios.

ReactJS en cambio se define como una librería. Una librería que tiene como fin un propósito muy definido: ReactJS solo quiere encargarse de gestionar la vista de tu aplicación. Si te acercas a esta librería, te cansarás de que Facebook te diga que si nuestra aplicación está diseñada como un MVC, ReactJS se encargará de dar forma a la V de nuestro patrón.

Por esto está gustando tanto ReactJS. Es una librería ligera que solo se encarga de hacer bien una cosa y nada más. AngularJS ha sufrido muchas críticas en su core. Existen personas que no son partidarias de su sistema de routing por lo poco flexible que es. Otros desarrolladores tienen ciertas dudas en la forma en que trabaja el $scope. Otras en cambio no son partidarias de su filosofía en directivas y el resto, por ejemplo, preferiría usar otro inyector de dependencias diferente al actual.

Menos en el caso del routing, que se encuentra extraído fuera del núcleo, a día de hoy cambiar cualquiera de esas piezas es complicado, ya que tienen una dependencia muy alta de cómo debe funcionar Angular, por lo que cambiar una pieza es harto complejo o nos va a dar más problemas que soluciones el cambiarlo. Como siempre me gusta decir, si decides casarte con AngularJS, será para siempre con sus pros y sus contras.

Con ReactJS esto no pasa. Si nos gusta la forma en que trabaja la librería, simplemente la usaremos para la interacción del usuario y el resto de los módulos software típicos con los que cuenta una aplicación front podrán ser realizadas por las librerías que más nos gusten o por nuestras propias soluciones si ninguna nos convence. Incluso podría llegar un día que ReactJS deje de parecernos la mejor opción y que cambiarla por otra librería nos pueda parecer hasta fácil.

Como vemos es complicado comparar un framework contra una librería, porque sería como comparar una navaja multiusos con un cuchillo. La navaja sabemos que hace muchas cosas que el cuchillo no puede. Lo único que sabemos es que el cuchillo corta muy bien.

## El paradigma de ReactJS no es el de AngularJS

ReactJS nació como una solución para realizar programación declarativa en la capa de interfaz de una aplicación. ReactJS se presenta como una opción muy válida para desarrollar aplicaciones JavaScript por medio del paradigma funcional. Es decir, aplicaciones que solo contengan un único flujo, donde las funciones no contengan estado y si lo contienen, este sea  inmutable, en la medida de lo posible.

Donde la abstracción se consiga por medio de funciones que contengan entradas y salidas sin saber cómo se comportan internamente, simplemente que funcionen como cajas negras que siempre funcionen de la manera esperada, es decir, que dada siempre la misma entrada, siempre devuelvan la misma salida.

Todo esto se traduce a que ReactJS crea interfaces por medio de componentes. Componentes mínima, con funcionalidad mínima que se van componiendo los unos a los otros para formar jerarquías de componentes. Donde los datos fluyen desde las capas más genéricas de componentes hacia los más simples y específicas, formando un árbol donde las entradas son datos y las salidas son html.

Todas estas ideas no son consideradas en AngularJS. AngularJS apostó en su día por ser más tradicional y diseñarse dentro de un patrón estructural MVC que con el tiempo irá dando paso a un MVVM y que a día de hoy tiene la flexibilidad suficiente como para permitir al desarrollador usar el que necesite, denominándose a esto el patrón MVW o MV* (Model-View-Whatever).

Las vistas y los controladores de las aplicaciones AngularJS comparten módelos en los que se cambia el estado y donde no existe nada inmutable. Suelen ser aplicaciones muy parecidas a lo que nos encontrabamos en MVC.NET o Spring de Java pero ahora en la parte cliente. Aplicaciones llenas de clases que son instanciadas por medio del framework según las necesidades.

## Y si ReactJS es una librería que se encarga de la vista ¿Por qué no lo usamos junto con AngularJS?

Al igual que se está poniendo muy de moda el comparar AngularJS con ReactJS. Existen muchos tutoriales de cómo usarlos juntos. Esto es algo que se puede hacer. Podemos hacer que ReactJS se encargue de gestionar la jerarquía de componentes visuales de nuestra aplicación y que AngularJS funcione en el resto de capas.

Particularmente yo no lo recomiendo. Creo que AngularJS cuenta con un motor de vistas por medio de directivas y componentes bastante potente y que se adapta mejor a las necesidades de su framework a como lo hace ReactJS. Creo que ReactJS pierde esencia usándose con AngularJS y creo que migrar aplicaciones a Angular 2 en el futuro se complicaría demasiado.

No soy partidario de crear estos ‘frankensteins’. Me parece más un empecinamiento por usar dentro de nuestra aplicaciones todo aquello nuevo que sale al mercado y seguir las modas, que una necesidad principal para nuestra aplicación. Por lo que no nos dejemos llevar por estas arquitecturas raras.

Si ya tenemos aplicaciones hechas en AngularJS en producción, mejorémoslas para que se adapten mejor al mantenimiento y la reusabilidad que necesitemos actualizando Angular a su versión 1.5 por ejemplo, que nos va a permitir mejorar nuestra aplicación por medio de la  nueva funcionalidad angular.component o con su nuevo router más flexible que el anterior.

Si por el contrario precisamos una aplicación nueva, pero nos da miedo lanzarnos a ReactJS tan pronto. No pasa nada. Sigamos con AngularJS. Aprovechemos todo nuestro conocimiento y experiencia y orquestemos una mejor arquitectura. Quizá una arquitectura orientada a componentes que pueda migrarse en el futuro a Angular 2. No hace falta seguir modas.

Pero si en cambio, sabes de ReactJS, te convence su paradigma y filosofía, no lo dudes y embárcate. Creo que tu workflow y tu ciclo de desarrollo mejorará y que tus aplicaciones serán igual o más competentes.