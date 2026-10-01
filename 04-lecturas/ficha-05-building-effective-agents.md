# Ficha 05: Building effective agents

**Referencia:** Anthropic. (19 de diciembre de 2024). *Building effective agents* (última modificación según los metadatos de la página: 10 de agosto de 2026). https://www.anthropic.com/engineering/building-effective-agents

**Fecha de lectura:** 30 de septiembre de 2026

## Resumen (en mis palabras)

El artículo distingue dos tipos de "sistemas agénticos" según quién controla el camino: en un flujo de trabajo (workflow), el código predefinido orquesta a la IA y a las herramientas; en un agente, la IA decide por sí misma sus pasos y qué herramientas usar. A partir de ahí recorre patrones de flujos de trabajo cada vez más complejos (encadenar llamadas, enrutar según el tipo de entrada, paralelizar, un orquestador que reparte tareas y un evaluador que corrige) y termina en el agente, que describe como un modelo que usa herramientas en un ciclo, recibiendo resultados reales del entorno en cada paso. Su consejo central es empezar con lo más simple posible y añadir complejidad solo cuando mejore los resultados de forma demostrable. Cierra con dos ejemplos donde los agentes funcionan bien (atención al cliente y programación) y un apéndice sobre cómo diseñar bien las herramientas que usa el agente.

## Aportes

- La diferencia no está en qué tan "inteligente" es el sistema, sino en quién decide el siguiente paso: el código (flujo de trabajo) o el modelo (agente). Me sirve porque ordena una duda que tenía y la convierte en una pregunta de diseño.
- Cuándo usar cada uno. Los flujos de trabajo ofrecen predictabilidad y consistencia en tareas bien definidas. Los agentes sirven para problemas abiertos donde no se puede predecir cuántos pasos harán falta ni fijar una ruta, y exigen cierto grado de confianza en las decisiones del modelo, por lo que son más adecuados en entornos de confianza. Y antes de ambos, el artículo recuerda que muchas veces basta una sola llamada al modelo bien optimizada, con datos de apoyo y ejemplos.
- Qué advierte sobre la complejidad. Los sistemas agénticos suelen cambiar velocidad y costo por mejor desempeño, así que hay que preguntarse si ese cambio vale la pena. En los agentes, la autonomía implica más costo y el riesgo de que los errores se acumulen, por lo que recomienda pruebas extensas en entornos aislados y barreras de protección. También advierte que los marcos de desarrollo facilitan empezar, pero añaden capas que ocultan lo que se le envía y responde al modelo, dificultan la depuración y tientan a complicar de más.
- En el patrón de encadenamiento de prompts, el artículo menciona que se pueden agregar comprobaciones programáticas en los pasos intermedios (una "compuerta") para asegurar que el proceso sigue bien encaminado. Esto me llamó la atención porque se parece a lo que hice en mi contestador al mover la verificación al código.
- Dedica un apéndice a diseñar las herramientas del agente con el mismo cuidado que una interfaz para personas, y propone dificultar los errores desde el diseño (poka-yoke). Cuenta que en uno de sus proyectos dedicaron más tiempo a mejorar las herramientas que al prompt. Mi lectura es que el artículo trata las herramientas y su documentación como parte del diseño, no como un detalle.
- Presenta la atención al cliente como un caso natural para agentes (conversación, acceso a datos, acciones y un criterio de éxito medible), y dice que acciones como reembolsos pueden manejarse de forma programática. Mi nodo, a diferencia de ese ejemplo, no tiene herramientas.

## Limitaciones

- No habla de copilotos. Me sirve para entender qué es un agente y qué es un flujo de trabajo, pero la diferencia entre agente y copiloto necesita otra fuente.
- Lo escribe Anthropic, que fabrica modelos y herramientas para construir agentes: el propio artículo menciona su kit de desarrollo, su protocolo MCP (ficha 03) y ejemplos con sus modelos y sus propias implementaciones. Su consejo de simplicidad es sensato, pero los casos de éxito son suyos o de sus clientes y no muestra cifras (de costo, errores o desempeño) que permitan verificarlos.
- Es de diciembre de 2024. Una nota al inicio avisa que gran parte de las herramientas que describe han cambiado desde entonces y remite a una página sobre "Managed Agents", que no leí.
- La frontera entre flujo de trabajo y agente no es tan nítida como la presenta. El propio artículo reconoce que "agente" se define de varias maneras, y su patrón de orquestador y trabajadores se clasifica como flujo de trabajo aunque un modelo decide dinámicamente las subtareas.
- Insiste en medir y evaluar, pero no explica cómo diseñar esas evaluaciones, igual que me pasó con la guía de la ficha 02. De seguridad solo menciona pruebas aisladas y barreras de protección, sin detalle (tema de la ficha 04).

## Mi opinión

Creo que mi contestador se parece más a un flujo de trabajo que a un agente, aunque el nodo de n8n se llame "AI Agent". Mis razones:

- El camino lo define el código de n8n, no el modelo: ignorar mensajes repetidos, agrupar mensajes seguidos, armar el contexto, revisar si el restaurante está cerrado, llamar al modelo, validar, bloquear duplicados, guardar e imprimir. El modelo no elige ninguno de esos pasos.
- Según el flujo, ese nodo solo tiene conectados el modelo de lenguaje y una memoria de los últimos 10 mensajes de cada cliente. No tiene herramientas: no consulta la hoja, no guarda pedidos ni imprime. Esas acciones las hace el código, y solo después de validar lo que el modelo propone. En los términos del artículo, es un modelo "aumentado" con datos (el catálogo y el contexto del día) y memoria, dentro de un flujo.
- Incluso lo que el modelo pregunta depende en parte del código, porque una regla de "siguiente paso" calcula qué dato falta a partir del borrador guardado. Además, después del modelo hay un punto que enruta según el resultado (carta, pedido válido, falta un dato, conversación normal) y una validación que funciona como la compuerta que el artículo describe en el patrón de encadenamiento de prompts.

Donde sí hay algo de autonomía es en la conversación libre: el modelo decide cómo responder, cómo aclarar una ambigüedad y cuándo considera que el pedido está completo. Y justo ahí fallaba: dar por cerrado un pedido sin generar el bloque técnico, o pedir permiso para cerrar. Mi hipótesis es que cada falla se corrigió quitándole al modelo una decisión y pasándola al código, es decir, moviéndome de la mitad "agente" hacia la mitad "flujo de trabajo", lo cual concuerda con la advertencia del artículo sobre la predictibilidad y los errores acumulados. También se parece a la recomendación de empezar simple, aunque mi prompt de unos 49.000 caracteres muestra que la complejidad la fui agregando a medida que aparecían fallas, y no pude medir si cada cambio la justificaba (no tengo evaluaciones automáticas).

Esto aporta a mi pregunta de investigación una pieza nueva: cuánta autonomía darle a la IA es una decisión de diseño que hay que tomar y comunicar. Mi conclusión provisional es que, cuando los pasos se conocen de antemano, conviene un flujo de trabajo con verificación en el código, y que dejar a la IA dirigir sus propios pasos solo tiene sentido cuando no se pueden predecir y hay una forma de comprobar el resultado, como las pruebas automáticas en programación que el artículo menciona. Me quedan dos pendientes: entender qué es un copiloto y en qué se diferencia de un agente, y contrastar este artículo con la guía de agentes de otra empresa, porque esta fuente la escribe Anthropic.
