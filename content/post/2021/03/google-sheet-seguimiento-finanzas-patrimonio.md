+++
date = 2021-03-02T09:50:15Z
image = "/images/2021/03/header.jpg"
slug = "google-sheet-seguimiento-finanzas-patrimonio"
tags = ["finanzas", "inversión","criptomonedas","herramientas"]
title = "Google Sheet para facilitar seguimiento de tus finanzas y patrimonio"
description = "He compartido un Google Sheet similar al que uso para hacer seguimiento en el tiempo de la evolución a grandes rasgos de ahorros e inversiones."

+++

Algunos sabéis ya de **mi afición por hacerme listas**, _Notions_ y _Google Sheets_ para todo (oigo a Nico y Albert López reírse desde aquí 😅). Desde el roadmap de un side project, a mis _to-do_ personales, calendarios de publicación automatizados, seguimiento de carteras, de gastos de casa, de la evolución de la hipoteca VS el rendimiento del alquiler... 

> TL;DR (Si no quieres leerte el artículo entero)
> 
> He montado **un Google Sheet con el que poder hacer seguimiento en el tiempo de la evolución a grandes rasgos de tus ahorros y tus inversiones**.
> 
> 👇 Lo comparto aquí por si puede ser útil para otros. <!--more-->
> 
> 📊 [**Registro y estado de patrimonio &raquo;**](https://bit.ly/gsheet-patrimonio) 
> 
> Puedes hacer una copia en tu Google Drive y editar con tus propios datos.

### Un poco de contexto. Mi plan de inversión.

Hace unos años empecé a pensar en serio en planificar mi jubilación (probablemente demasiado tarde, aunque lo importante es empezar 🤷‍♂️). **¿Qué tendría que estar haciendo ahora para encontrarme en la mejor posición posible dentro de 20-25 años?**

Entre otras cosas, la respuesta incluía **tener una buena estrategia de ahorro e inversión**, así que me puse a ello y tras leer y tratar de aprender de la experiencia de otras personas de mi entorno, pensé en un sistema: 
- que fuera **sencillo** y **cómodo**.
- que en lo posible **no requiriera de una "gestión activa"** por mi parte.
- que **se adaptara a distintas circunstancias** personales y familiares (que fuera válido para aquel momento o pasados 10 años).


En realidad no tiene mucha miga. Concluí que debía:

1. Definir y separar **un % de ahorro "no invertido"**, disponible para cualquier emergencia o para poder vivir durante al menos un año sin disponer de ingresos recurrentes. Nulo o mínimo riesgo: depósito o cuenta de ahorro.
2. Centrarme principalmente en hacer **aportaciones periódicas automáticamente a fondos indexados** (soy un cliente feliz de [**Indexa Capital**](https://indexacapital.com/es/esp/t/yHI9Gm) 👈 _enlace de invitación_).
3. Dedicar un porcentaje pequeño a **activos de alto riesgo**, entre los que englobo **startups** (_criterio_: conocer muy bien al equipo o el sector, y la posibilidad de aprendizaje) y **criptomonedas** (criterio: de nuevo aprender y aprovechar la oportunidad a futuro que traerá, _creo_, la adopción masiva que está por llegar en los próximos años).\
   [CryptoAdvisor.Club](https://cryptoadvisor.club/es), la herramienta que lanzamos a finales del año pasado, me ayuda precisamente a invertir en criptomonedas aplicando [algunas buenas prácticas](https://cryptoadvisor.club/es/algoritmo-inversion-criptos).
4. En general, **evitar invertir en bolsa** (en la medida que requiere una gestión activa: selección de los activos, monitorización, decidir cuándo y cómo entrar y salir, etc.), o hacerlo bajo un sistema que me "proteja" de decisiones impulsivas (así conocí GAD de Lichello, de la mano de Albert Lombarte). 

### El dashboard de seguimiento en Google Sheet

Para hacer seguimiento de todo ello y monitorizar la evolución, la representatividad de cada categoría, etc. desde hace un par de años vengo usando un dashboard muy parecido a este: 📊 [**Registro y estado de patrimonio &raquo;**](https://bit.ly/gsheet-patrimonio)

Consta de las siguientes secciones:

#### 1. Pestañas de Gráficas e Informes

{{< figure src="/images/2021/03/pestana-graficos.png" caption="Algunas gráficas sobre la distribución de activos y su evolución" >}}

Los datos de estas pestañas **se actualizan automáticamente**. 

En la pestaña gráficas podrás ver la evolución de tu patrimonio agregado por tipo de activo (barras apiladas), la distribución actual (gráfico circular) y una gráfica de rendimiento VS aportaciones de fondos y criptomonedas.

En la pestaña Informe encontrarás un registro mensual, con un snapshot de los datos detallados. El documento tiene un script (lo puedes ver en Herramientas > Editor de secuencias de comandos) que se puede configurar para su ejecución automática 1 vez al mes. Este script toma los datos de la fila nº 2 (datos actuales) y los copia en una nueva fila, de forma que **si actualizas periódicamente los saldos, la hoja generará automáticamente ese histórico cada mes**. Yo suelo marcarme un recordatorio para actualizar los datos una o dos veces al mes.

#### 2. Pestaña de Cuentas

En esta pestaña simplemente tienes que **incluir tus cuentas y actualizar los saldos** (columna naranja). Los datos se recogerán automáticamente en la pestaña Informes. Si tienes algún inmueble, puedes incluirlo también aquí e ir actualizando su valor a mercado.

#### 3. Pestaña Inversiones

{{< figure width="500" src="/images/2021/03/pestana-inversiones.png" caption="Aportaciones, valor actual y rendimiento de tus inversiones" >}}

Esta pestaña incluye tus inversiones, ya sea en fondos, acciones o criptomonedas. **Las aportaciones se actualizarán automáticamente** a partir de los datos que se registren en la siguiente pestaña. Aquí **lo que debes actualizar periódicamente es su valor actual**. Eso te permitirá ver el rendimiento acumulado en esta pestaña, y permitirá actualizar dicha información en los informes y gráficas.

#### 4. Pestaña Aportaciones de Inversión

Aquí **deberás registrar las aportaciones que hagas a los diferentes activos que hayas listado en la pestaña anterior**. De hecho verás que el desplegable en cada fila de esta pestaña es una lista dinámica con los activos listados en la pestaña anterior. Los valores que incluyas en esta lista afectarán a la columna "aportaciones" de la pestaña anterior, y se computarán las aportaciones del mes en curso para los cálculos de la pestaña Informes y las gráficas de evolución de rendimiento de pestaña Gráficos.

#### 5. Bonus track: Rebalanceo de criptomonedas

{{< figure width="400" src="/images/2021/03/pestana-rebalanceo.png" caption="Herramienta de rebalanceo de cartera de criptomonedas" >}}

En la última pestaña encontrarás una herramienta muy sencilla que te permitirá calcular qué operaciones deberías hacer si, dado un importe que quieras aportar a tu cartera de criptomonedas, quieres **asegurarte de que el balance y la representatividad de cada moneda se mantienen en línea con tus objetivos**, independientemente de la evolución reciente de su valor. Por tanto, tomará también de forma dinámica el valor actual de cada criptomoneda de la pestaña anterior. 

Puedes editar el importe de la aportación en la celda naranja, o incluso puedes dejar el valor a cero si no quieres hacer ninguna aportación adicional, pero quieres saber qué transacciones deberías realizar para **rebalancear tu cartera** para seguir la distibución que te hayas marcado como objetivo.

---

{{< center >}}
<p>👉 📊 <a href="https://bit.ly/gsheet-patrimonio"><strong>Registro y estado de patrimonio &raquo</strong></a> 👈</p>
{{< /center >}}

Normalmente me lleva no más de 5 minutos al mes llevarlo al día, y me resulta bastante útil sobre todo para hacer seguimiento en cuestión de rendimiento de las inversiones y de la distribución.

**¿Te sirve? Cualquier aportación o mejora que se te ocurra, compártela.** 😉 
