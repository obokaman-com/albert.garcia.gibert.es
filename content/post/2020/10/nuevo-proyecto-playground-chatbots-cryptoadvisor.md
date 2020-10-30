+++
date = 2020-10-28T19:27:36Z
image = "/images/2020/10/cryptoadvisor-screenshot-dark.png"
slug = "nuevo-proyecto-playground-chatbots-cryptoadvisor"
tags = ["proyectos", "criptomonedas"]
title = "CryptoAdvisor.Club: El asistente virtual para invertir en criptomonedas"

+++
Esta semana _Albert Lombarte_ y yo ponemos en marcha [**CryptoAdvisor.Club**](https://cryptoadvisor.club/es), un asistente virtual en forma de bot 🤖 de Telegram que puede ayudarnos a sacar mayor partido a nuestra cartera de criptomonedas. Se trata de un _side project_ en el que hemos trabajado los últimos dos meses, con la intención de **aprender todo lo necesario para montar un chatbot**: UX para interfaces conversacionales, librerías y herramientas disponibles, sistemas de analítica para bots, buenas prácticas para el diseño de la infraestructura técnica necesaria, particularidades de las diferentes plataformas de chat disponibles (_Telegram, Slack, Facebook Messenger, Whatsapp, Microsoft Bot, Alexa, Google Assistant..._)

Si te interesa conocer un poco el porqué de este proyecto, a continuación doy un poco de contexto. Si tanto texto te aburre, te agradeceré al menos que [**pruebes nuestro bot**](https://cryptoadvisor.club/es) y nos hagas llegar tus impresiones. ☺️

#### ¿Porqué un _side project_?

[Dejé Uvinum]({{< ref "/content/post/2020/05/el-de-cuando-sali-de-uvinum.md" >}}), hace ya unos 5 meses, con dos propósitos claros en mente: **recuperar tiempo para mí** 😇 (reciclar conocimientos, recuperar algunas aficiones y buenos hábitos, reflexionar sobre mi futuro...) y **empezar a desarrollar una idea de negocio** a la que veníamos dando vueltas desde hace un tiempo con _Albert Lombarte_, amigo, socio y compañero de aventuras varias. 

Durante los meses de junio y julio nos enfocamos en **mejorar nuestro conocimiento** del ecosistema en el que nos moveremos, investigando otros proyectos similares, y en **validar algunas hipótesis** que habíamos elaborado, llevando a cabo una serie de entrevistas. Ha sido un proceso muy interesante: hemos aprendido un montón gracias a experiencias de primera mano relacionadas con las problemáticas que trataremos de resolver, y hemos podido acotar nuestra idea inicial de negocio. 👌

Nuestra intención es lanzar el proyecto en [modo _bootstrapping_](https://es.wikipedia.org/wiki/Bootstrapping_(negocios)), así que una de las implicaciones es que deberíamos ser capaces de **construir y lanzar por nosotros mismos la versión inicial del proyecto**, el {{< abbr "MVP" "Minimum Viable Product">}}.

Y aunque este proyecto no tiene nada que ver con las criptomonedas, los chatbots / asistentes virtuales sí tendrán un peso muy relevante. Ni Albert Lombarte ni yo habíamos trabajado antes en un producto de este tipo, y al poco de empezar a investigar ya vimos que tendríamos que hincar los codos para empaparnos de una serie de conceptos que **poco o nada tenían que ver con la UX "tradicional"**: interfaces gráficas, forma, color, contraste, formularios, layouts... versus _intents_, NLP, conversaciones, y unos pocos elementos interactivos en determinadas plataformas (botones en Telegram, menús en Slack, cards en FB Messenger...).

Nos planteamos 3 opciones:
 
1) Empezar a buscar, leer, aprender y probar montándonos un _sandbox_ genérico donde poner en práctica lo que aprendíamos.
2) Meternos en faena ya sobre el nuevo proyecto. Ir aprendiendo, resolviendo y reescribiendo a medida que aprendíamos cómo funcionaban las herramientas, las librerías, las técnicas adecuadas para mantener conversaciones, analizar e identificar intents, etc.
3) Aprender y ponerlo en práctica en un proyecto real, un _playground_ que nada tuviera que ver con el proyecto definitivo, pero que tuviera cuerpo y forma, algún sentido, no un mero _sandbox_ de pruebas.

Optamos por la segunda opción, por una cuestión de _separation of concerns_: nuestro interés en el momento en que empecemos el desarrollo del nuevo proyecto debe orientarse al máximo a **la parte lógica del desarrollo del MVP**, no a sus detalles técnicos. Y puestos a usar un playground para aprender, mejor darle un sentido y hacer algo que pudiera sernos útil, no?. 

Aprovechando la idea de un proyecto que inicié hará cosa de 3 años, para probar una nueva librería de machine learning en PHP ([_Stock Forecast_ en Github](https://github.com/obokaman-com/stock-forecast)) pensamos que un bot que actuara como "asistente virtual" para ofrecer información, recordatorios y consejos de compra podría requerir casos de uso suficientemente variados y complejos como para que pudiéramos sacarle partido a la experiencia. Además, durante los últimos meses había estado haciendo algunas pruebas con algoritmos de inversión automatizada como {{< abbr "AIM" "Automatic Investment Management">}} ({{< abbr "GAD" "Gestión Automatizada del Dinero" >}} en castellano) o Twinvest de Lichello, que junto a los algoritmos predictivos que usaba en _Stock Forecast_ estaban dando resultados interesantes. Y si pudiera automatizar todos esos cálculos, cruzar los datos de una cartera completa, hacer backtesting con mediciones reales?... Y bueno, ya sabes, aquello de _eat your own dog food_, no? 😜 Y de paso hemos tenido ocasión de pelearnos con lambdas, frustrarnos con las posibilidades reales de las librerías y plataformas de NLP disponibles hoy en día 😒, descubrir varias iniciativas _NoCode_ interesantes, montar mi primera app en producción con un flujo completo de desarrollo, integración y despliegue completamente basado en contenedores 🐳... **¡Aprendiendo!** ✅

Por otro lado, y a modo de refuerzo de la opción que escogimos, creo que este tipo de _side projects_ (objetivo de aprendizaje, _scope_ muy acotado) son una **fuente inestimable de exploración e inspiración**, y permiten **mejorar nuestra opcionalidad**, incrementar a un coste relativamente bajo oportunidades futuras de éxito. No en vano así surgieron en su día [Obolog](https://www.genbeta.com/web/obolog-plataforma-espanola-de-creacion-de-blogs-totalmente-reformada) o [Splitweet](https://computerhoy.com/noticias/internet/hootsuite-compra-start-espanola-splitweet-2493). 😅

De modo que mientras terminamos esta fase y nos preparamos para empezar, ahora sí,  con el desarrollo del nuevo proyecto, **nos encantaría escuchar tu feedback sobre CryptoAdvisor.Club**:
- Más información: [cryptoadvisor.club](https://cryptoadvisor.club/es)
- El bot: [https://t.me/cryptoadvisorclubbot](https://t.me/cryptoadvisorclubbot)
