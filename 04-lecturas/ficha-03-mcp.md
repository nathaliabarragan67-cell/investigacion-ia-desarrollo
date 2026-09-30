# Ficha 03: What is the Model Context Protocol (MCP)?

**Referencia:** Model Context Protocol. (s. f.). *What is the Model Context Protocol (MCP)?* (versión de la documentación 2026-07-28). https://modelcontextprotocol.org/docs/2026-07-28/getting-started/intro

**Fecha de lectura:** 22 de septiembre de 2026

## Resumen (en mis palabras)

Esta página es la introducción oficial al Model Context Protocol (MCP), un estándar abierto para conectar aplicaciones de IA con sistemas externos como archivos, bases de datos, herramientas y flujos de trabajo. Usa la comparación con un puerto USB-C: así como un solo tipo de conector sirve para muchos dispositivos, MCP busca que una aplicación de IA se conecte a muchas fuentes de la misma forma. Menciona ejemplos como agentes que acceden a Google Calendar y Notion, o Claude Code generando una aplicación web a partir de un diseño de Figma. Explica qué gana cada actor (desarrolladores, aplicaciones de IA y usuarios finales) y aclara que varios clientes lo soportan, entre ellos Claude, ChatGPT, VS Code y Cursor, por lo que se construye una vez y se integra en muchos lugares. Las instrucciones técnicas las deja para otras secciones de la documentación.

## Aportes

- La idea central es que MCP separa dos cosas: el modelo que razona y las herramientas o datos con los que actúa. En lugar de programar una integración distinta para cada IA y cada servicio, se define una conexión estándar. Esto significa que elegir bien las herramientas del sistema incluye decidir qué puede ver y hacer la IA.
- El ejemplo de Claude Code generando una aplicación web usando un diseño de Figma es lo que más se acerca a mi pregunta de investigación. La página solo menciona el ejemplo, pero esto sugiere que la IA puede leer el diseño desde la herramienta donde vive, y que comunicar un diseño podría ser darle acceso a la fuente y no traducirlo a un prompt largo.
- Distingue tres tipos de cosas a las que una IA se puede conectar: datos (archivos, bases de datos), herramientas (buscadores, calculadoras) y flujos de trabajo (prompts especializados). Me parece una forma útil de clasificar qué necesita saber y hacer una IA para construir algo.
- Que sea un protocolo abierto y con muchos clientes (Claude, ChatGPT, VS Code, Cursor) probablemente reduce el riesgo de quedar atado a un solo proveedor; esa es mi lectura, la página no lo afirma. Esto conecta con la ficha 02, donde noté que los detalles de la guía de OpenAI son específicos de su plataforma.

## Limitaciones

- Es solo una página de introducción: explica qué es MCP y para qué sirve, pero no cómo funciona por dentro. La arquitectura, la creación de servidores y clientes y la seguridad quedan en otras secciones que no leí.
- Está escrita por el propio proyecto, así que su tono es promocional. Lista beneficios y ejemplos atractivos, pero no menciona límites, costos, fallos ni casos en que la integración no funcione bien.
- No dice quién creó MCP. Según su anuncio original (https://www.anthropic.com/news/model-context-protocol), lo presentó Anthropic en noviembre de 2024. Es la misma empresa que desarrolla Claude y Claude Code, que aparecen como ejemplos en la página, lo que refuerza el tono promocional. Este dato lo encontré citado en fuentes secundarias y falta contrastarlo leyendo el anuncio original.

- **Fuente complementaria:** Anthropic. (25 de noviembre de 2024). *Introducing the Model Context Protocol*. https://www.anthropic.com/news/model-context-protocol
  
- No responde cómo comunicar un diseño a una IA. MCP resuelve la conexión con herramientas y datos, no cómo redactar requisitos, dividir un sistema en partes ni verificar lo que la IA construyó. Eso queda fuera de su alcance.
- Los ejemplos (Blender con impresora 3D, chatbots empresariales conectados a varias bases de datos) se presentan sin detalles, y no deja claro qué tan confiables son en la práctica.
- La seguridad solo se menciona como un enlace. Dar a una IA acceso a calendarios, archivos o bases de datos implica riesgos de privacidad y de acciones no deseadas que la página no desarrolla.

## Mi opinión

Creo que MCP responde una parte de mi pregunta de investigación, pero no toda. Si la habilidad valiosa es diseñar el sistema y elegir las herramientas correctas, MCP muestra que elegir herramientas también es decidir a qué tiene acceso la IA. Una IA que puede leer mi diseño en Figma, mi base de datos o mi documentación tiene más contexto para construir bien que una a la que solo le doy un prompt.

Aun así, pienso que MCP es un canal y no el mensaje. Conecta a la IA con mis herramientas, pero no hace que mi diseño sea claro, completo ni verificable. Si el diseño de Figma es ambiguo, la IA lo construirá ambiguo. Por eso esta ficha se suma a las anteriores de una forma complementaria: la ficha 02 mostró cómo se redactan las instrucciones (estructura, roles, ejemplos, pruebas) y esta muestra cómo se le da acceso al entorno. Me falta la tercera pieza, que es cómo especificar y verificar lo que la IA construye.

Mi conclusión provisional es que comunicarle un diseño a una IA tiene tres partes: instrucciones bien estructuradas, acceso a las fuentes y herramientas correctas, y una forma de comprobar el resultado. Para seguir con la investigación, me interesaría leer sobre cómo escribir especificaciones y criterios de aceptación que una IA pueda seguir, y sobre la seguridad en MCP, porque dar más acceso a la IA también aumenta lo que puede salir mal.
