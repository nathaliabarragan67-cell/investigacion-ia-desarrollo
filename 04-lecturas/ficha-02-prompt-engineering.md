# Ficha 02: Prompt engineering (OpenAI API)

**Referencia:** OpenAI. (s. f.). *Prompt engineering*. OpenAI API Docs. https://developers.openai.com/api/docs/guides/prompt-engineering

**Fecha de lectura:** 20 de septiembre de 2026 

## Resumen 

Esta guía explica cómo escribir instrucciones para que un modelo de lenguaje dé resultados consistentes a través de la API de OpenAI. Plantea que un prompt no es un texto suelto, sino algo estructurado: los mensajes tienen roles (el `developer` define las reglas y el `user` aporta los datos de entrada) y se organizan en identidad, instrucciones, ejemplos y contexto. También cubre técnicas como dar ejemplos (few-shot), incluir información externa (RAG) y ajustar el estilo según el modelo: los de razonamiento aceptan metas generales, mientras que los GPT necesitan instrucciones precisas. Al final insiste en tratar los prompts como código: versionarlos, probarlos con evaluaciones y fijar una versión concreta del modelo en producción.

## Aportes

- La idea que más me llamó la atención es la analogía entre los roles y una función: el mensaje `developer` es como la definición de la función (reglas y lógica del sistema) y el mensaje `user` son los argumentos. Esto deja claro quién controla qué dentro de un sistema con IA.
- Propone guardar los prompts en el código de la aplicación, con pruebas, revisión y despliegue gradual, en lugar de tratarlos como texto suelto. Con esto el prompting pasa a ser parte de la ingeniería de software.
- Recomienda una estructura estándar para el mensaje (identidad, instrucciones, ejemplos y contexto) y poner al inicio lo que se repite en cada petición para aprovechar el caché y ahorrar costo y latencia.
- Distingue entre modelos de razonamiento, que funcionan como un compañero senior al que le das una meta, y modelos GPT, que funcionan como un compañero junior que necesita instrucciones explícitas.
- Como los resultados de un modelo no son deterministas y cambian entre versiones, recomienda fijar la versión del modelo y construir evaluaciones para medir el comportamiento. Esto se conecta directamente con mi pregunta de investigación.

## Limitaciones

- Es una guía escrita para la API de OpenAI. Los parámetros y ejemplos (`instructions`, rol `developer`, Responses API) son específicos de esa plataforma, y aunque las ideas generales sirven en otros modelos, los detalles no se trasladan directamente.
- La página parece actualizada por partes: mezcla modelos de distintas generaciones (`gpt-6-astra`, `gpt-5.5` y ejemplos de GPT-4.1) y en un punto todavía habla de GPT-5. Además, los prompts guardados como objetos reutilizables se están retirando y el endpoint `v1/prompts` cierra el 30 de noviembre de 2026, así que parte del contenido envejece rápido.
- Recomienda hacer evaluaciones, pero en esta página no explica cómo diseñarlas. Tampoco desarrolla cómo organizar varios agentes, manejar la memoria o decidir qué va en el prompt y qué en el código; esos temas los deriva a otras secciones de la documentación.
- Muestra qué hacer, pero casi no explica por qué funciona ni cuándo falla (por ejemplo, con instrucciones contradictorias o prompts muy largos).

## Mi opinión

Creo que la guía ayuda a entender que, si una IA va a construir un sistema, lo que yo escribo funciona como la especificación. La estructura de identidad, instrucciones, ejemplos y contexto se parece mucho a un documento de requisitos: quién es el agente, qué reglas sigue, cómo se ve un buen resultado y con qué información cuenta. Me parece valioso que proponga tratar el prompt como código, porque si la IA construye el sistema, mis instrucciones pasan a ser parte del sistema y merecen control de versiones, pruebas y revisión.

Aun así, pienso que por sí sola no alcanza para diseñar un sistema que una IA construya y mantenga en el tiempo. Esto no es un defecto de la guía sino de su alcance: es una guía de prompts, y un buen prompt es solo una pieza. Para el resto hace falta dividir el sistema en partes pequeñas y bien definidas, dejar criterios de aceptación claros y automatizar las pruebas, que es la forma de comprobar lo que la IA construyó.

Esto refuerza la pregunta que me dejó la ficha anterior: si la IA escribe cada vez más código, el valor parece moverse hacia saber especificar y verificar bien lo que se quiere construir. Mi conclusión provisional es que el prompt engineering es una base necesaria, pero diseñar para que una IA construya depende más de qué tan bien especifico y verifico el sistema que de cómo redacto cada prompt.
