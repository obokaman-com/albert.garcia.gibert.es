+++
date = 2020-10-29T11:13:15Z
image = "/images/2020/10/cryptoadvisorclub-screenshot.png"
slug = "criptoadvisor-como-se-hizo"
tags = ["proyectos", "criptomonedas", "cryptoadvisor"]
title = "El making of de CryptoAdvisor.Club"

+++
Anteriormente te explicaba [los motivos que nos llevaron a lanzar CryptoAdvisor.Club]({{< ref "/content/post/2020/10/nuevo-proyecto-playground-chatbots-cryptoadvisor.md" >}}), el asistente virtual para la inversión en criptomonedas. 

En este artículo te comparto algunos detalles técnicos sobre **el stack y las herramientas que hemos utilizado para construir el bot de [CryptoAdvisor.Club](https://cryptoadvisor.club/es)**.

#### El _stack_ técnico

- Es una aplicación en **PHP 7.4**, con Symfony. CQRS, DDD, eventos...
- Usamos intensivamente la librería **[BotMan](https://botman.io/)**, con algunos drivers propios para modificar algunos comportamientos a la hora de interactuar con menús y botones.
- Varios workers se encargan tanto de los **procesos periódicos** (sincronización de precios y tratamiento de datos) como de consumir y tratar los **eventos** que se generan en la aplicación (eventos de dominio varios, analítica, sistema de feedback que sincroniza las sesiones de feedback con threads en nuestro Slack...)
- **MySql 8.0** ahora. **DynamoDB** mientras estuvimos en Lambdas en AWS.

#### Entorno y servicios complementarios

##### Infraestructura
- **Ansible** y **Terraform** nos permiten provisionar y configurar el servidor y algunos servicios de AWS que utilizamos. Poco que decir: imprescindibles para **abstraer y automatizar cualquier tema relacionado con servicios de infraestructura**.
- La aplicación corre en contenedores de **Docker**, tanto en el entorno de desarrollo como en producción. Usamos **Github Actions** para automatizar el build del contenedor que se usará en producción con la versión actualizada del código, pushearla al registry que tenemos en AWS, y hacer el pull de ese contenedor desde el servidor de producción, integrando también la ejecución de los tests, notificación a New Relic, Slack, etc.
- Usamos [**ngrok**](https://ngrok.com/) para **crear una URL pública que sirva de túnel a nuestro entorno local**. Esto es imprescindible para poder llevar a cabo las pruebas durante el desarrollo. Tenemos varios bots de pruebas que usan estas URL públicas como webhooks. Los comandos para levantar y parar la aplicación en desarrollo **automatizan** la ejecución de ngrok en segundo plano, la notificación de la URL resultante a Telegram y copian la URL pública de ngrok al portapapeles. [_He compartido el script en un Gist aquí_ »](https://gist.github.com/obokaman-com/07e66dcfcbcbe09bce50c970fabac079).

{{< figure src="/images/2020/10/ngrok.png" caption="Ngrok" >}}

##### Monitorización y Analítica
- [**New Relic**](https://newrelic.com/) nos permite **monitorizar la performance de la aplicación** a un muy bajo nivel: tiempos de respuesta, tracing de transacciones, requests, queries SQL... con lo que es muy útil para **identificar cuellos de botella o posibles optimizaciones a la aplicación**. También usamos el sistema de alertas, conectado a nuestro canal de Slack.
- Usamos [**Chatbase**](https://chatbase.com/products/virtual-agent-analytics/) (de Google) como **sistema de analítica** para entender mejor el uso del chat por parte de los usuarios: qué intents hacen matching con el sistema, qué interacciones quedan sin respuesta válida y disparan los fallbacks, ver los diferentes _funnels_ de uso... Ha resultado ser **una herramienta muy útil para "afinar" los intents abiertos del sistema** y ajustarlos a los usos reales de los usuarios. 

{{< figure src="/images/2020/10/chatbase.png" caption="Session flow en Chatbase" >}}

#### Otras herramientas 

- La landing del proyecto (https://cryptoadvisor.club) **es una página de Notion**. Con Cloudflare haciendo de proxy y **los workers que ofrecen como servicio gratuíto**, [modificamos request y response para poder servir el contenido desde nuestro propio dominio](https://twitter.com/obokaman/status/1314146211776126976) y con URL personalizadas para cada idioma, hacer que la página sea visible e indexable por parte de buscadores, etc.
- También en [**Notion**](https://notion.so) es donde gestionamos nuestras tareas, recogemos información interesante o documentamos cualquier cosa. _I_ ❤️ _Notion._
- Usamos **[PoEditor](https://poeditor.com/) para gestionar las traducciones**. Permite la exportación de los ficheros en más de 20 formatos, muchos de los cuales son directamente compatibles con Symfony. En su versión gratuíta se pueden gestionar hasta 1000 cadenas distintas.
- En [**Slack**](https://slack.com) centralizamos tema alertas y **también el sistema de soporte y feedback**: los usuarios disponen de un comando especial para compartir feedback con nosotros, que **inicia un thread en nuestro canal de soporte** y nos permite charlar con ellos directamente desde el propio bot.

#### Otras cosas interesantes que hemos probado

##### Lambdas
- Probamos por un tiempo, y **terminamos descartando**, montarlo mediante **lambdas en AWS**, por una cuestión de costes e idoneidad. Las Lambdas, mientras no estén en un Security Group, tienen acceso a internet _by default_. En el momento en qué tuvimos que añadirlas a un SG para que tuvieran conectividad con otros servicios a los que queríamos dar cierta capa de seguridad, si queríamos que siguieran teniendo conexión a Internet, debíamos habilitar un Internet Gateway y un NAT Gateway. Terminábamos pagando más del doble por estos servicios que por las propias Lambdas.
- Lo interesante del asunto es que **pudimos probar Lambdas con PHP, mediante [bref.sh](https://bref.sh/)**, una librería que se integra con [**Serverless**](https://www.serverless.com/) y facilita enormemente todo el proceso de deploy y la integración con frameworks como Symfony, ya sea para servir una aplicación completa a través de HTTP, para ejecutar comandos de aplicación a demanda en remoto o para configurar eventos que programen la ejecución periódica de determinadas funciones.

##### Plataformas y librerías para {{< abbr "NLP" "Natural Language Processing" >}}
- [**Dialogflow**](https://dialogflow.cloud.google.com/) (de Google, antiguamente Api.ai), es una **plataforma de comprensión de lenguaje natural** pensada para facilitar el diseño de interfaces conversacionales. Aunque empezamos a trabajar con ella e integramos algunos intents más complejos a través suyo, terminamos quitándola de la ecuación.{{< breakline >}}{{< breakline >}}
Al final no dejaba de ser una manera sofisticada de implementar cosas que podíamos conseguir igual, sin añadir más capas de complejidad ni dependencias de servicios externos, con expresiones regulares y condiciones, que teníamos igualmente que implementar en su plataforma 🤷‍♂️, y que doblaban (_o más_) los tiempos de respuesta del bot.{{< breakline >}}{{< breakline >}}
En cualquier caso es un servicio interesante con el que es posible **montar un chatbot sin necesidad de implementar ninguna lógica relacionada directamente con la parte conversacional**, y la posibilidad de complementar información con llamadas a webhooks propios, o integrarse con múltiples plataformas desde un único lugar.{{< breakline >}}{{< breakline >}}
- [**DeepPavlov**](https://deeppavlov.ai/) es un **framework open source en Python para montar AI conversacionales**. Es uno de los proyectos más interesantes que he conocido este tiempo. Permite implementar sistemas abiertos de preguntas y respuestas, reconocimiento de entidades, de clasificación automática de intents, detección de palabras malsonantes... en base a textos que podemos ofrecer por nuestro lado para entrenar a los modelos con nuestro caso de uso específico. [Prueba alguna de las demos](https://demo.deeppavlov.ai/#/mu/ner) porque vale la pena.

{{< figure src="/images/2020/10/deep-pavlov-example.png" caption="Intent detection con Deep Pavlov" >}}

##### Integración y automatización de servicios
- Inicialmente usamos también [**Integromat**](https://www.integromat.com/) para **automatizar un flujo de recogida > tratamiento > ingestión de datos** a nuestra API desde las APIs de terceros, pero terminamos descartándolo por tema costes. Sólo en lo que se refiere a llamadas a APIs hablábamos de unas 800 llamadas cada minuto. Teniendo en cuenta que el coste de Integromat es por "operaciones", y cada pipe tenía al menos 4 operaciones:{{< breakline >}}1. llamada API externa{{< breakline >}}2. conversión de formato{{< breakline >}}3. transformación del contenido{{< breakline >}}4. llamada a nuestra API{{< breakline >}}{{< breakline >}}Hablábamos de **unos pocos millones de operaciones al día**. Podíamos optimizar algunos de los pasos intermedios, pero seguiría quedando lejos de las 40.000 operaciones mensuales que incluye un plan (de pago) estándar de Integromat. 🙄

👉 _Bonus point_: Todos estos servicios disponen de versiones gratuitas que, al menos de momento, cubren nuestras necesidades.
