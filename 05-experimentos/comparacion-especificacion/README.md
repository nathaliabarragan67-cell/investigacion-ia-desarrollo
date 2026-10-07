# Experimento: descripción libre vs. especificación estructurada

**Estado:** protocolo y criterios congelados. Las pruebas todavía no se han ejecutado; las secciones 5 y 6 se llenan después.

**Pregunta:** ¿cambia el resultado cuando a una IA le doy una descripción libre y cuando le doy una especificación hecha con una plantilla?

**App elegida:** registro de pedidos de un restaurante, con cuatro productos.

**Herramienta y modelo:** Claude en el chat de claude.ai (no Claude Code). Modelo: ______ (el que muestre el selector al momento de las pruebas; el mismo en las tres versiones).

**Las tres versiones:**
- **A. Descripción libre:** como la escribiría cualquiera, sin reglas.
- **B. Libre con reglas (control):** la misma información que C, pero escrita como un párrafo.
- **C. Especificación con la plantilla:** la información de B, estructurada, con lenguaje de requisitos, criterios de aceptación y la instrucción de preguntar antes de construir.

## Protocolo (para que la comparación sea justa)

- Congelo los criterios de aceptación (sección 1) **antes** de pedir nada, con un commit. Fecha en que los congelé: ______ (la del commit de este archivo).
- Uso la misma herramienta y el mismo modelo en las tres versiones, **cada una en una conversación nueva**, sin contexto de las otras y sin pegar los criterios en las versiones A y B.
- Orden de ejecución: A, luego B, luego C.
- Evalúo primero la **primera entrega**, sin correcciones. Si después pido arreglos, los cuento aparte (cuántos mensajes hicieron falta).
- Para probar, descargo el archivo `.html` y lo abro en mi propio navegador; no lo evalúo solo dentro del chat.
- Guardo cada versión en su carpeta (`v1-libre/`, `v2-libre-con-reglas/`, `v3-especificacion/`) y anoto lo que la IA preguntó o agregó sin que se lo pidiera.
- Los textos exactos de cada versión están en bloques de código para copiarlos sin cambios.

## Decisiones tomadas antes de ejecutar

- Si la IA hace preguntas, respondo siempre: "Haz lo que consideres mejor y dime qué supusiste", y cuento las preguntas.
- Hago las pruebas en chat incógnito (o con la memoria desactivada). Opciones activadas (búsqueda web, pensamiento extendido, estilo): ______
- Mismo modelo y mismas opciones en las tres versiones, en la misma sesión.
- Si la app guarda datos de una forma que no funciona al abrir el archivo en mi navegador, el criterio 5 cuenta como falla y lo anoto.
- Los resultados los anoto yo, sin ayuda del asistente con el que preparé este experimento, y analizo solo cuando tengo los seis criterios de las tres versiones.

## Catálogo del experimento

| Producto | Presentaciones y precios | Regla |
|---|---|---|
| Arroz Chino | Caja $50.000 / Media $42.000 / Personal $32.000 | Exige color: Amarillo o Café |
| Arroz Paisa | Caja $50.000 / Media $42.000 / Personal $32.000 | No lleva color |
| Pollo frito | Completo $38.000 / Medio $22.000 / Cuarto $12.000 | No lleva color |
| Bebida personal | $4.000 | Sin presentaciones |

## 1. Criterios de aceptación (congelados)

| # | Qué comprueba | Cómo lo pruebo | Resultado esperado |
|---|---|---|---|
| 1 | Total correcto | Registro 2 Arroz Chino Caja Amarillo + 1 Bebida | Total $104.000 |
| 2 | Regla del color | Intento guardar un Arroz Chino sin color, y otro con "Rojo". Luego agrego un Arroz Paisa | Rechaza los dos primeros; el Arroz Paisa no pide color |
| 3 | Datos de entrega | Domicilio con teléfono "12345" y luego con letras; después recoger sin nombre | Rechaza el teléfono que no tiene 10 dígitos o tiene letras; el domicilio exige barrio; recoger exige nombre |
| 4 | Entradas imposibles | Elijo Pollo frito "Caja", o pongo cantidad 0 o negativa | No lo permite |
| 5 | Registro persistente | Guardo un pedido, cierro y vuelvo a abrir la app | El pedido sigue en la lista con número consecutivo, hora y total |
| 6 | Sin duplicados por error | Hago doble clic rápido en "Guardar" | Se guarda un solo pedido |

Dato de proceso (no cuenta como pasa o falla): cuántos mensajes necesité hasta que cumplió todo.

## 2. Versión A: descripción libre

Escrita como la escribiría cualquiera, sin reglas ni validaciones:

Hazme una app para registrar los pedidos de mi restaurante. Vendemos arroz chino, arroz paisa, pollo frito y bebidas. Los arroces cuestan $50.000 la caja, $42.000 la media y $32.000 el personal; el pollo frito $38.000 completo, $22.000 medio y $12.000 cuarto; la bebida personal $4.000. Quiero anotar lo que pide el cliente, si es domicilio o para recoger, y ver el total. Que funcione abriendo un archivo en el navegador, sin instalar nada.


## 3. Versión B (control): las mismas reglas, pero en texto libre

Tiene la misma información que la especificación, escrita como un párrafo, sin estructura ni lenguaje de requisitos:

Hazme una app para registrar los pedidos de mi restaurante. Vendemos arroz chino, arroz paisa, pollo frito y bebidas. Los arroces cuestan $50.000 la caja, $42.000 la media y $32.000 el personal; el pollo frito $38.000 completo, $22.000 medio y $12.000 cuarto; la bebida personal $4.000. El arroz chino siempre tiene que llevar color, amarillo o café, y ningún otro. El total lo tiene que calcular la app, nadie lo escribe. Cada producto solo se puede vender en sus propias presentaciones y la cantidad debe ser un número entero mayor que cero. Si es domicilio hace falta el barrio y un teléfono de exactamente 10 dígitos; si es para recoger, el nombre de quien recoge. Si algo está mal, que muestre un mensaje y no guarde el pedido. Cada pedido guardado lleva un número consecutivo, la hora y el total, y no debe guardarse dos veces si se hace doble clic. Los pedidos tienen que seguir ahí al cerrar y reabrir la app. Que funcione abriendo un solo archivo en el navegador, sin instalar nada.

## 4. Versión C: especificación con la plantilla

Especificación: registro de pedidos

1. Objetivo y usuario.
Una persona que atiende pedidos de un restaurante los registra rápido y sin errores.

2. Alcance.
Incluye: registrar pedidos, validarlos, listarlos y conservarlos.
No incluye: pagos, usuarios, impresión ni conexión con otros sistemas.

3. Catálogo (fuente única de precios).
| Producto | Presentaciones y precios | Regla |
|---|---|---|
| Arroz Chino | Caja $50.000 / Media $42.000 / Personal $32.000 | Exige color: Amarillo o Café |
| Arroz Paisa | Caja $50.000 / Media $42.000 / Personal $32.000 | No lleva color |
| Pollo frito | Completo $38.000 / Medio $22.000 / Cuarto $12.000 | No lleva color |
| Bebida personal | $4.000 | Sin presentaciones |

4. Reglas de negocio.
- MUST: el Arroz Chino exige color Amarillo o Café; ningún otro color es válido.
- MUST: el total lo calcula el código a partir del catálogo; el usuario nunca lo escribe.
- MUST: cada producto solo admite sus propias presentaciones.
- MUST: la cantidad es un entero mayor que 0.

5. Datos de entrega y validaciones.
Domicilio: barrio obligatorio y teléfono de exactamente 10 dígitos.
Recoger: nombre obligatorio.
Cada error muestra un mensaje claro y no guarda el pedido.

6. Comportamiento.
Al guardar, el pedido recibe un número consecutivo, la hora y el total.
El botón de guardar se bloquea mientras guarda, para no duplicar el pedido.
La lista muestra todos los pedidos guardados.

7. Persistencia.
Los pedidos deben seguir ahí al cerrar y reabrir la app.

8. Restricciones técnicas.
Un solo archivo que se abre en el navegador, sin instalar nada y sin servidor.

9. Criterios de aceptación.
1. Al registrar 2 Arroz Chino Caja color Amarillo y 1 Bebida personal, el total mostrado DEBE ser $104.000.
2. La app DEBE rechazar un Arroz Chino sin color y uno con un color distinto de Amarillo o Café; el Arroz Paisa NO DEBE pedir color.
3. Un domicilio DEBE exigir barrio y un teléfono de exactamente 10 dígitos numéricos; recoger DEBE exigir nombre; los datos inválidos DEBEN rechazarse con un mensaje.
4. La app NO DEBE permitir una presentación que el producto no tiene (por ejemplo, Pollo frito en caja) ni cantidades menores o iguales a cero.
5. Un pedido guardado DEBE seguir en la lista al cerrar y reabrir la app, con consecutivo, hora y total.
6. Un doble clic rápido en "Guardar" DEBE guardar un solo pedido.

10. Proceso.
Si algo no está claro, pregunta antes de construir; no supongas.

## 5. Registro de pruebas

Marca ✔ cumple, ✘ falla o ~ parcial. Se llena después de ejecutar.

| # | Criterio | A: libre | B: libre con reglas | C: especificación | Observaciones |
|---|---|---|---|---|---|
| 1 | Total correcto | | | | |
| 2 | Regla del color | | | | |
| 3 | Datos de entrega | | | | |
| 4 | Entradas imposibles | | | | |
| 5 | Registro persistente | | | | |
| 6 | Sin duplicados | | | | |
| | **Total** | /6 | /6 | /6 | |

| Dato de proceso | A | B | C |
|---|---|---|---|
| Mensajes hasta cumplir todo | | | |
| Preguntas que hizo la IA antes de construir | | | |
| Cosas que agregó sin que se las pidiera | | | |

**Repeticiones (opcional).** Si repito cada versión en una conversación nueva, para ver cuánto varía:

| Versión | Primera ejecución | Repetición |
|---|---|---|
| A | /6 | /6 |
| B | /6 | /6 |
| C | /6 | /6 |

## 6. Qué cumplió, qué falló y qué cambiaría de la plantilla

Se llena después de las pruebas.

- **Versión A (libre):**
- **Versión B (libre con reglas):**
- **Versión C (especificación):**
- **A contra B (efecto de tener las reglas):**
- **B contra C (efecto de la estructura y los criterios explícitos):**
- **Qué falló aun con la especificación, y por qué creo que fue:**
- **Qué cambiaría de la plantilla:**
- **Conclusión provisional para mi pregunta de investigación:**

## Límites de este experimento

- Una sola prueba por versión no demuestra nada general; el resultado puede variar si repito.
- La versión A falla casi todos los criterios por omisión, porque nunca se le dijeron las reglas. La comparación informativa es B contra C, donde la información es la misma.
- La versión C además trae alcance, lenguaje MUST, los criterios escritos dentro de la especificación (incluido el caso exacto del criterio 1) y la instrucción de preguntar antes de construir. Si C supera a B, no sé cuál de esas diferencias lo explica.
- La herramienta puede imponer restricciones propias (por ejemplo, sobre cómo guarda datos una página dentro del chat) que afecten algunos criterios sin importar cómo escriba el pedido; lo anoto en observaciones si ocurre.
- Yo evalúo los resultados y sé qué versión es cuál; no es una evaluación a ciegas.
- El modelo evaluado es de la misma empresa que el asistente con el que preparé el experimento; por eso las pruebas se hacen en chats separados y los resultados los anoto yo.
- Los resultados valen solo para esta herramienta, este modelo y esta app; no los generalizo a otras.
