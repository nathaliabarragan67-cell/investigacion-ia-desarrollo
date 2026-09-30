# Ficha 04: Security Best Practices (MCP)

**Referencia:** Model Context Protocol. (s. f.). *Security Best Practices* (versión de la documentación 2026-07-28). https://modelcontextprotocol.io/docs/2026-07-28/tutorials/security/security_best_practices

**Fecha de lectura:** 23 de septiembre de 2026

## Resumen (en mis palabras)

Esta página reúne los riesgos de seguridad de las implementaciones de MCP y las medidas para reducirlos, y está pensada para leerse junto con la especificación de autorización. Para cada ataque explica cómo funciona, qué riesgos trae y qué mitigación exige, usando un lenguaje de obligaciones (MUST para lo obligatorio y SHOULD para lo recomendado). Entre los ataques están el "confused deputy" (un servidor intermediario que un atacante aprovecha para saltarse el consentimiento del usuario), el reenvío de tokens sin validar, hacer que un cliente consulte direcciones internas (SSRF), adivinar identificadores de estado y ejecutar comandos maliciosos en servidores locales. Cierra con la minimización de permisos: pedir al inicio solo lo básico y ampliar cuando haga falta. Su público son los desarrolladores de flujos de autorización, los operadores de servidores y los especialistas en seguridad.

## Aportes

- Noté que casi todos los riesgos vienen de cómo se conectan las piezas (servidores intermediarios, tokens, URLs, comandos de arranque) y no de lo que "piensa" el modelo. Esto amplía lo que entendí en la ficha 03: dar acceso a una IA es conectar sistemas, y cada conexión es una superficie de ataque.
- El consentimiento aparece como un requisito concreto de diseño. La pantalla de consentimiento debe mostrar el nombre del cliente, los permisos que pide y la dirección a la que se enviarán los tokens; y antes de conectar un servidor local, el cliente debe mostrar el comando exacto que va a ejecutar, sin recortarlo. Esto deja claro qué significa pedir permiso "bien".
- La minimización de permisos (scopes) enlaza con mi conclusión de la ficha 03: más acceso implica más daño posible si algo se filtra. La página propone empezar con permisos mínimos de lectura, subir solo cuando se intenta una operación privilegiada, y evitar errores comunes como los permisos comodín (`*`, `all`).
- Como el protocolo de esta versión no mantiene sesiones, el estado entre llamadas se maneja con identificadores (por ejemplo, el de un carrito o flujo de trabajo), y la página advierte que tener ese identificador no equivale a estar autenticado: el servidor debe comprobar a quién pertenece. Me pareció un ejemplo claro de una decisión de diseño que trae un riesgo nuevo.
- La mayoría de las obligaciones recaen en quienes implementan (servidores intermediarios, clientes, operadores y servidores de autorización). Al usuario le toca aprobar, pero la página pone la carga en que el software le muestre información veraz para que pueda decidir bien. Esta es mi lectura de la estructura de la página.

## Limitaciones

- Es muy técnica y asume conocimientos de OAuth (client ID estático, PKCE, audiencia de tokens, varios RFC). Varios ataques, como el confused deputy y los mix-up, no los entendí a fondo, así que resumí solo lo que sí pude seguir.
- Se centra en la autorización entre clientes y servidores. No encontré en ella temas como la inyección de instrucciones maliciosas en lo que lee el modelo, ni qué debe confirmar el usuario cada vez que la IA usa una herramienta. Sobre ese último punto, el consentimiento que sí desarrolla es el de conectar clientes y servidores.
- Deja varias decisiones al criterio de quien implementa. Por ejemplo, las protecciones contra SSRF dependen del entorno de red, cuántos permisos incluir en cada solicitud depende de la evaluación del servidor, y la defensa contra los mix-up solo funciona si los servidores de autorización son honestos y envían el dato correcto.
- La propia página reconoce un caso en que el cliente pide todos los permisos por defecto: si el servidor no indica qué permisos pedir, el cliente debe solicitar todos los que el servidor lista, porque los clientes generales no conocen el dominio. Esto contradice en parte la recomendación de mínimo privilegio que ella misma hace.
- Indica qué medidas aplicar, pero no cómo comprobar que quedaron bien implementadas (pruebas, auditorías). Tampoco muestra casos reales ni qué tan frecuentes son estos ataques.
- Está ligada a una versión de la especificación (2026-07-28). Para los identificadores de sesión remite a la versión anterior (2025-11-25), así que parte del contenido cambia entre versiones.

## Mi opinión

Esta lectura me muestra que la seguridad también es parte del diseño que hay que comunicarle a una IA. Una IA que construya un sistema con conexiones a datos y herramientas implementará lo que se le especifique. Mi hipótesis es que, si no le digo que los permisos deben empezar al mínimo, que debe validar de quién es cada identificador o que debe pedir consentimiento antes de ejecutar algo, probablemente no lo hará por su cuenta; esto lo puedo probar en mi experimento, pidiéndole a una IA que construya algo con y sin restricciones de seguridad escritas y comparando los resultados. La forma de la página me parece un buen modelo: casi cada riesgo trae una condición verificable y un nivel de obligación (MUST o SHOULD), y eso se parece a la especificación clara y comprobable que me faltaba en las fichas anteriores.

Aun así, pienso que la página sirve más para quien implementa que para quien diseña y delega. No explica cómo transformar estas reglas en requisitos que una IA pueda seguir, ni cómo comprobar después que los cumplió. Además, deja decisiones abiertas que alguien tendrá que tomar con criterio propio, y esa es justo la parte del diseño que no se puede delegar.

Mi conclusión provisional se actualiza: comunicarle un diseño a una IA implica instrucciones bien estructuradas (ficha 02), acceso a las fuentes y herramientas correctas (ficha 03), restricciones de seguridad escritas como requisitos verificables (esta ficha) y una forma de comprobar el resultado. Esa última parte sigue pendiente en mi investigación.
