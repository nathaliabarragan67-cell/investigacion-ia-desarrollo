# Experimento: descripción libre vs. especificación estructurada

**Pregunta:** ¿cambia el resultado cuando a una IA le doy una descripción libre y cuando le doy una especificación hecha con una plantilla?

**App elegida:** registro de pedidos de un restaurante, con cuatro productos.

**Herramienta y modelo:** Claude en el chat de claude.ai (no Claude Code). Modelo: ______ (el que muestre el selector al momento de cada prueba; debe ser el mismo en las tres versiones).

## Protocolo (para que la comparación sea justa)

- Congelo los criterios de aceptación (sección 1) **antes** de pedir nada y guardo el archivo con fecha, por ejemplo con un commit. Fecha en que los congelé: ______
- Uso la misma herramienta y el mismo modelo en las tres versiones, **cada una en una conversación nueva**, sin contexto de las otras y sin pegar los criterios en las versiones A y C.
- Orden de ejecución: A, luego C, luego B.
- Evalúo primero la **primera entrega**, sin correcciones. Si después pido arreglos, los cuento aparte (cuántos mensajes hicieron falta).
- Para probar, descargo el archivo `.html` y lo abro en mi propio navegador; no lo evalúo solo dentro del chat.
- Guardo cada versión en su carpeta (`v1-libre/`, `v2-libre-con-reglas/`, `v3-especificacion/`) y anoto lo que la IA preguntó o agregó sin que se lo pidiera.

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

Criterio extra de proceso (no cuenta como pasa o falla): cuántos mensajes necesité hasta que cumplió todo.

## 2. Versión A: descripción libre

Escrita como la escribiría cualquiera, sin reglas ni validaciones:

> Hazme una app para registrar los pedidos de mi restaurante. Vendemos arroz chino, arroz paisa, pollo frito y bebidas. Los arroces cuestan $50.000 la caja, $42.000 la media y $32.000 el personal; el pollo frito $38.000 completo, $22.000 medio y $12.000 cuarto; la bebida personal $4.000. Quiero anotar lo que pide el cliente, si es domicilio o para recoger, y ver el total. Que funcione abriendo un archivo en el navegador, sin instalar nada.

## 3. Versión C (control): las mismas reglas, pero en texto libre

Tiene la misma información que la especificación, pero escrita como un párrafo, sin estructura ni lenguaje de requisitos:

> Hazme una app para registrar los pedidos de mi restaurante. Vendemos arroz chino, arroz paisa, pollo frito y bebidas. Los arroces cuestan $50.000 la caja, $42.000 la media y $32.000 el personal; el pollo frito $38.000 completo, $22.000 medio y $12.000 cuarto; la bebida personal $4.000. El arroz chino siempre tiene que llevar color, amarillo o café, y ningún otro. El total lo tiene que calcular la app, nadie lo escribe. Cada producto solo se puede vender en sus propias presentaciones y la cantidad debe ser un número entero mayor que cero. Si es domicilio hace falta el barrio y un teléfono de exactamente 10 dígitos; si es para recoger, el nombre de quien recoge. Si algo está mal, que muestre un mensaje y no guarde el pedido. Cada pedido guardado lleva un número consecutivo, la hora y el total, y no debe guardarse dos veces si se hace doble clic. Los pedidos tienen que seguir ahí al cerrar y reabrir la app. Que funcione abriendo un solo archivo en el navegador, sin instalar nada.

## 4. Versión B: especificación con la plantilla

> **Especificación: registro de pedidos**
>
> **1. Objetivo y usuario.** Una persona que atiende pedidos de un restaurante los registra rápido y sin errores.
>
> **2. Alcance.** Incluye: registrar pedidos, validarlos, listarlos y conservarlos. No incluye: pagos, usuarios, impresión ni conexión con otros sistemas.
>
> **3. Catálogo (fuente única de precios).** [tabla del catálogo de arriba]
>
> **4. Reglas de negocio.**
> - MUST: el Arroz Chino exige color Amarillo o Café; ningún otro color es válido.
> - MUST: el total lo calcula el código a partir del catálogo; el usuario nunca lo escribe.
> - MUST: cada producto solo admite sus propias presentaciones.
> - MUST: la cantidad es un entero mayor que 0.
>
> **5. Datos de entrega y validaciones.** Domicilio: barrio obligatorio y teléfono de exactamente 10 dígitos. Recoger: nombre obligatorio. Cada error muestra un mensaje claro y no guarda el pedido.
>
> **6. Comportamiento.** Al guardar, el pedido recibe un número consecutivo, la hora y el total. El botón de guardar se bloquea mientras guarda, para no duplicar el pedido. La lista muestra todos los pedidos guardados.
>
> **7. Persistencia.** Los pedidos deben seguir ahí al cerrar y reabrir la app.
>
> **8. Restricciones técnicas.** Un solo archivo que se abre en el navegador, sin instalar nada y sin servidor.
>
> **9. Criterios de aceptación.** [los 6 criterios de la sección 1, redactados como requisitos MUST]
>
> **10. Proceso.** Si algo no está claro, pregunta antes de construir; no supongas.

## 5. Registro de pruebas

Marca ✔ cumple, ✘ falla o ~ parcial.

| # | Criterio | A: libre | C: libre con reglas | B: especificación | Observaciones |
|---|---|---|---|---|---|
| 1 | Total correcto | | | | |
| 2 | Regla del color | | | | |
| 3 | Datos de entrega | | | | |
| 4 | Entradas imposibles | | | | |
| 5 | Registro persistente | | | | |
| 6 | Sin duplicados | | | | |
| | **Total** | /6 | /6 | /6 | |

| Dato de proceso | A | C | B |
|---|---|---|---|
| Mensajes hasta cumplir todo | | | |
| Preguntas que hizo la IA antes de construir | | | |
| Cosas que agregó sin que se las pidiera | | | |

## 6. Qué cumplió, qué falló y qué cambiaría de la plantilla

- **Versión A (libre):**
- **Versión C (libre con reglas):**
- **Versión B (especificación):**
- **A contra C (efecto de tener las reglas):**
- **C contra B (efecto de la estructura y los criterios explícitos):**
- **Qué falló aun con la especificación, y por qué creo que fue:**
- **Qué cambiaría de la plantilla:**
- **Conclusión provisional para mi pregunta de investigación:**

## Límites de este experimento

- Una sola prueba por versión no demuestra nada general; el resultado puede variar si repito.
- La versión C tiene la misma información que la B, pero la B además trae alcance, lenguaje MUST, los criterios escritos dentro de la especificación y la instrucción de preguntar antes de construir; si B supera a C, no sé cuál de esas diferencias lo explica.
- La herramienta puede imponer restricciones propias (por ejemplo, sobre cómo guarda datos una página dentro del chat) que afecten algunos criterios sin importar cómo escriba el pedido; lo anoto en observaciones si ocurre.
