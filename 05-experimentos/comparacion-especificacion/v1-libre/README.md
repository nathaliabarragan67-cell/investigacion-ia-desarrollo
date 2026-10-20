# Versión A: descripción libre

**Fecha de ejecución:** 19 de octubre de 2026. Pruebas completadas el 20 de octubre de 2026.
**Modelo y opciones activadas:** los registrados en el README principal del experimento.

## Prompt (exacto)

```text
Hazme una app para registrar los pedidos de mi restaurante. Vendemos arroz chino, arroz paisa, pollo frito y bebidas. Los arroces cuestan $50.000 la caja, $42.000 la media y $32.000 el personal; el pollo frito $38.000 completo, $22.000 medio y $12.000 cuarto; la bebida personal $4.000. Quiero anotar lo que pide el cliente, si es domicilio o para recoger, y ver el total. Que funcione abriendo un archivo en el navegador, sin instalar nada.
```

## Lo que respondió la IA

- Mensajes míos hasta la primera entrega: 1. No pedí correcciones.
- Preguntas de la IA: 0.
- Entregó un solo archivo, [`pedidos-restaurante.html`](pedidos-restaurante.html).
- Su explicación (sin el código): la app se abre con doble clic; el menú agrega productos con su tamaño y precio, con botones + y − para las cantidades; hay campos de nombre, teléfono (opcional), notas y tipo de pedido (recoger o domicilio, que pide dirección y valor del domicilio); el total se calcula solo; los pedidos guardados pasan a una lista del día con número, hora y detalle, y se pueden marcar como entregados o eliminar. Aclaró que los pedidos se guardan en el navegador y que se pierden si se cambia de equipo o se borran los datos. Al final ofreció cobrar el domicilio automáticamente, imprimir la comanda para cocina y exportar las ventas a Excel.

## Lo que agregó sin que se lo pidiera

Botones Entregado, Reabrir y Eliminar; resumen del día (pedidos, pendientes y total); valor del domicilio sumado al total; campo de notas; numeración por día. Además ofreció imprimir comandas, cobrar el domicilio automático y exportar a Excel.

## Resultados de las seis pruebas

| # | Qué hice | Qué pasó | Resultado |
|---|---|---|---|
| 1 | 2 Arroz chino caja + 1 bebida | Total $104.000. No existe campo de color, y aplica la regla definida antes de ejecutar | ✔ |
| 2 | Arroz chino sin color y con "Rojo" | No existe el campo de color; no se puede probar la regla | ✘ |
| 3 | Teléfono "12345" y teléfono con letras; recoger sin nombre; domicilio sin dirección | Guardó ambos teléfonos y el pedido de recoger sin nombre. Rechazó el domicilio sin dirección con "Falta la dirección del domicilio" | ✘ |
| 4 | Pollo frito en "Caja"; cantidad 0 y negativa | El pollo no tiene la presentación "Caja" en el menú, y al llegar a 0 la línea desaparece, por lo que no se puede guardar | ✔ |
| 5 | Guardar un pedido, cerrar la pestaña y volver a abrir el archivo | Los pedidos no siguen en la lista | ✘ |
| 6 | Doble clic rápido en "Guardar" | Se guardó un solo pedido | ✔ |

**Total: 3/6.**

## Observaciones

- **Doble clic:** al guardar, la app vacía el formulario; el segundo clic encuentra el pedido vacío y muestra "Agrega al menos un producto". No hay una protección específica contra el doble envío; el resultado se debe a ese efecto.
- **Persistencia:** el código guarda en el almacenamiento del navegador (`localStorage`). En mi prueba, los pedidos no volvieron al cerrar y reabrir el archivo; no investigué la causa. Según la regla definida antes de ejecutar, cuenta como falla.
- **Validación de teléfono:** no hay validación; acepta "12345" y letras.
- **Nombre:** si se deja vacío, el pedido se guarda como "Sin nombre".
- **Dirección y barrio:** la app pide "dirección", no "barrio".
- **Lista del día:** según el código, solo muestra los pedidos de la fecha actual.
- **Falla por omisión:** los criterios 2 y 3 fallan sobre todo porque la descripción nunca mencionó esas reglas.

