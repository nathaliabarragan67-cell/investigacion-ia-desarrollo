# Versión B: libre con reglas (control)

**Fecha de ejecución:** 20 de octubre de 2026 (las capturas muestran 20/10/2026, 5:07 p. m.).
**Modelo y opciones activadas:** los mismos que en la versión A, en un chat nuevo e incógnito.

## Prompt

Desviación del protocolo: este texto lleva una frase que no estaba en el texto congelado. Después de "y ningún otro" agregué "y este se pregunta", para que la app preguntara el color. El resto es idéntico al texto congelado.

```text
Hazme una app para registrar los pedidos de mi restaurante. Vendemos arroz chino, arroz paisa, pollo frito y bebidas. Los arroces cuestan $50.000 la caja, $42.000 la media y $32.000 el personal; el pollo frito $38.000 completo, $22.000 medio y $12.000 cuarto; la bebida personal $4.000. El arroz chino siempre tiene que llevar color, amarillo o café, y ningún otro y este se pregunta. El total lo tiene que calcular la app, nadie lo escribe. Cada producto solo se puede vender en sus propias presentaciones y la cantidad debe ser un número entero mayor que cero. Si es domicilio hace falta el barrio y un teléfono de exactamente 10 dígitos; si es para recoger, el nombre de quien recoge. Si algo está mal, que muestre un mensaje y no guarde el pedido. Cada pedido guardado lleva un número consecutivo, la hora y el total, y no debe guardarse dos veces si se hace doble clic. Los pedidos tienen que seguir ahí al cerrar y reabrir la app. Que funcione abriendo un solo archivo en el navegador, sin instalar nada.
```

## Lo que respondió la IA

- Mensajes míos hasta la primera entrega: 1. No pedí correcciones.
- Preguntas de la IA: 0.
- Entregó un solo archivo, [`app-pedidos.html`](app-pedidos.html).
- Su explicación (sin el código): los precios y presentaciones están en la app y el total lo calcula ella; cada producto solo ofrece sus propias presentaciones. Al elegir arroz chino aparece la pregunta del color, obligatoria, con solo amarillo o café. La cantidad debe ser un entero mayor que cero y se pueden agregar varios productos al pedido y quitarlos antes de guardar. Domicilio pide barrio y teléfono de 10 dígitos; recoger pide el nombre. Los errores salen en un mensaje rojo y no se guarda el pedido. Cada pedido queda con número consecutivo, fecha, hora y total. Dijo que el doble clic no duplica porque el botón se bloquea un instante, y que los pedidos se guardan en el navegador y equipo donde se usa la app. Aclaró que no incluyó botones para editar o anular pedidos porque no se pidieron.

## Lo que agregó sin que se lo pidieran

Botón "Quitar" por línea del pedido, suma de cantidades cuando se repite la misma línea, mensaje de error si el navegador no deja guardar, y un aviso en verde al guardar con el número y el total. No agregó resumen del día, estados de entrega ni exportaciones.

## Resultados de las seis pruebas

| # | Qué hice | Qué pasó | Resultado |
|---|---|---|---|
| 1 | 2 Arroz chino caja Amarillo + 1 bebida | Total $104.000 | ✔ |
| 2 | Arroz chino sin color; elegir un color distinto; agregar Arroz paisa | Sin color: "El arroz chino debe llevar color: amarillo o café." y no se agrega. El selector de color solo ofrece Amarillo y Café, así que no se puede elegir "Rojo". El Arroz paisa no pide color | ✔ |
| 3 | Teléfono "12345" y con letras; recoger sin nombre; domicilio sin barrio; guardar sin productos | "12345": "El teléfono debe tener exactamente 10 dígitos (solo números)." Con letras: rechazado. Recoger sin nombre: "Falta el nombre de quien recoge." Domicilio sin barrio: "Falta el barrio para el domicilio." Sin productos: "Agrega al menos un producto al pedido." | ✔ |
| 4 | Pollo frito en "Caja"; cantidad 0 y negativa | El pollo solo ofrece Completo, Medio y Cuarto. Cantidad 0 o negativa: "La cantidad debe ser un número entero mayor que cero." | ✔ |
| 5 | Guardar un pedido, cerrar la pestaña y volver a abrir | En el mismo navegador, el pedido sigue en la lista con número, hora y total. En una ventana de incógnito (otra sesión) no aparece | ✔ |
| 6 | Doble clic rápido en "Guardar" | El botón se bloquea mientras guarda; se guardó un solo pedido | ✔ |

**Total: 6/6.**

## Observaciones

- **Precios:** el catálogo está una sola vez en el código y se usa para validar al agregar y de nuevo al guardar.
- **Validaciones:** el teléfono debe cumplir exactamente 10 dígitos numéricos; la cantidad, un entero positivo.
- **Persistencia:** usa el almacenamiento del navegador; si falla, muestra un error y no guarda. Los datos viven en ese navegador y equipo.
- **Doble clic:** tiene una protección explícita (el botón se deshabilita unos 1,2 segundos mientras guarda).
- **Consecutivo:** toma el número más alto existente y le suma 1; no se reinicia por día.
- **Errores:** cuando hay varios, se muestran juntos en un solo mensaje.
- **Alcance:** no permite editar ni anular pedidos.
