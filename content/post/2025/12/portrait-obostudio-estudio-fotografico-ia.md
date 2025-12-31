+++
date = 2025-12-13T18:00:00Z
author = "Albert Garcia"
title = "Cómo conseguí mi foto con Indiana Jones"
slug = "como-consegui-mi-foto-con-indiana-jones"
tags = ["proyectos", "inteligencia-artificial", "google-ai-studio", "side-project"]
description = "He montado un estudio fotográfico virtual que genera retratos manteniendo la identidad de múltiples personas. Te cuento cómo ha sido la experiencia con Google AI Studio."
image = "/images/2025/selfie-con-indy.jpg"
+++

¿No te hubiera gustado poder hacerte una foto con Harrison Ford y Sean Connery en el set de La Última Cruzada? O saludar a Marlon Brando en un descanso del rodaje de El Padrino. ¿Un selfie con el elenco del Señor de los Anillos? Montarme en el DeLorean con Marty McFly.

Cosas de friki, lo sé. Pero es que ahora no es tan difícil...

<!--more-->

{{< figure src="/images/2025/selfie-con-indie.jpg" caption="Entre toma y toma..." width="90%" >}}

Llevaba un tiempo intentando hacer este tipo de montajes con varias personas y no había manera. Con [Freepik](https://www.freepik.com/ai/image-generator), [Midjourney](https://www.midjourney.com/), [ChatGPT](https://chat.openai.com/)... si solo había un protagonista, los resultados eran decentes. Pero en cuanto metía a varias personas, la cosa se descontrolaba. A veces incluso con una sola.

Además hay un problema práctico: no siempre tienes una foto de grupo de base. A veces tienes fotos separadas de cada persona y quieres juntarlas en una misma escena. Eso ninguna herramienta lo hacía bien.

Así que me puse a experimentar con [Google AI Studio](https://aistudio.google.com/).

{{< figure src="/images/2025/portrait_3.jpg" caption="¿Eres un gallina?" width="90%" >}}

### Lo que me encontré

Las APIs de generación de imágenes que probé no ofrecen forma de "anclar" una identidad entre llamadas. Cada petición es independiente y stateless. Puedes describir a alguien con todo el detalle que quieras, pero el modelo interpreta esa descripción de nuevo cada vez. No hay manera de decirle "esta es Julia, recuérdala para la siguiente imagen".

Mi primer intento fue pasarle la foto de referencia junto con cada prompt. Si el modelo ve la cara, debería mantenerla, ¿no? Pues no del todo. Funcionaba a medias porque el modelo mezclaba la identidad con el contexto: la ropa, el fondo, la iluminación de la foto original contaminaban el resultado.

Lo que sí funcionó fue combinar ambas cosas. Pasar la foto de referencia junto con una descripción textual de los rasgos físicos de cada persona (estructura facial, tono de piel, forma de los ojos), sin ropa ni contexto. La imagen aporta la referencia visual y la descripción refuerza la identidad, anclándola con un nombre que luego puedes usar en el prompt. Esa combinación es lo que da la consistencia.

Y como las fotos con personajes famosos a veces se bloquean por los filtros de seguridad (falsos positivos, básicamente), el sistema permite generar 2, 4 u 8 versiones en paralelo. Las peticiones van concurrentes para no eternizarte esperando, y si alguna falla, te dice cuál y por qué. Así aumentas las probabilidades de obtener resultados válidos sin quedarte a ciegas.

{{< figure src="/images/2025/selfie-con-jack-sparrow.png" caption="Es \"CAPITÁN\" Jack Sparrow!" width="90%" >}}

### La sorpresa

No esperaba que [Google AI Studio](https://aistudio.google.com/) diera para tanto.

He usado [Lovable](https://lovable.dev/) para desarrollo web y trabajo con [Claude Code](https://docs.anthropic.com/en/docs/claude-code), así que tenía referencias de lo que se puede conseguir con vibe-coding. Pero la velocidad y la calidad de AI Studio me sorprendió. En unas cinco horas tenía la aplicación funcionando.

Durante las pruebas, Google lanzó Gemini 3 Pro. El salto en calidad fue notable, especialmente en dos cosas: la capacidad del modelo para reformular el prompt del usuario con terminología cinematográfica y fotográfica (tipo de lente, iluminación, textura), y el realismo de las imágenes generadas.

Actualmente uso Gemini 2.5 Flash para analizar las fotos e identificar personas, y Gemini 3 Pro tanto para optimizar el prompt como para generar las imágenes finales.

### Cómo funciona

{{< figure src="/images/2025/oboportrait-interface.png" caption="OboPortrait" width="90%" >}}

Subes fotos (de grupo o individuales), el sistema identifica a cada persona, les asignas un nombre para referenciarte a ellas en el prompt, describes la escena, y genera.

Todo funciona en el navegador. No hay backend. Las llamadas van directas a la API de Google con tu propia API key, así que tus fotos nunca pasan por ningún servidor mío. Quería algo que pudiera servir gratis desde GitHub Pages y olvidarme.

### Sobre el vibe-coding

Hace cinco años esto habría sido semanas de trabajo. Pero esas cinco horas requieren el mismo conocimiento de siempre: arquitectura, debugging, patrones, saber cuándo algo está bien hecho o es un desastre. La IA comprime el tiempo de ejecución, pero si no entiendes lo que genera, no puedes validarlo. Y si no puedes validarlo, estás jodido.

El tipo de trabajo cambia. Menos tiempo picando código, más tiempo decidiendo cómo tiene que funcionar algo. Sigue siendo trabajo, pero es distinto.

### Pruébalo

La app está en [portrait.obokaman.com](https://portrait.obokaman.com/). Necesitas una API key de Gemini con billing activado (el tier gratuito no incluye generación de imágenes). El código está en [GitHub](https://github.com/obokaman-com/portrait-studio/).

Si lo pruebas, cuéntame qué tal. Y si consigues esa foto con el elenco de tu peli favorita que siempre quisiste, me encantaría verla.
