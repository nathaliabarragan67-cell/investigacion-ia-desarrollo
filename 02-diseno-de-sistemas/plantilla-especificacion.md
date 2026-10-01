# Plantilla de especificación para que una IA construya un sistema (versión inicial)

**Estado:** propuesta. La armé a partir de las fichas 02 a 04 y del experimento del contestador. Todavía no la he probado; la probaré con una app pequeña en `05-experimentos`.

**Hipótesis:** una IA construye mejor un sistema cuando la especificación dice qué debe decidir la IA, qué debe garantizar el código y cómo se comprueba cada regla.

## Secciones

1. **Objetivo y alcance.** Qué hace el sistema y qué no hace.
2. **Usuarios y situaciones.** Quién lo usa, casos típicos y casos raros. *(En el contestador, los fallos reales vinieron de casos raros.)*
3. **Datos.** Qué entra, qué se guarda y dónde.
4. **Reglas de negocio.** Una tabla con tres columnas:

   | Regla | Dónde vive (prompt, datos o código) | Cómo se verifica |
   |---|---|---|
   | [ej.: el producto debe existir en el catálogo] | [código] | [validación contra el catálogo] |

5. **Qué decide la IA y qué garantiza el código.** La IA interpreta lenguaje libre; el código garantiza lo que no puede fallar.
6. **Permisos y seguridad.** Permisos mínimos, y qué NO debe poder hacer el sistema. Cada requisito escrito con nivel de obligación (DEBE o DEBERÍA) y de forma verificable. *(Idea tomada de la ficha 04.)*
7. **Ejemplos.** Entradas y salidas esperadas, incluyendo casos que ya fallaron. *(Estructura de instrucciones de la ficha 02.)*
8. **Criterios de aceptación y pruebas.** Cómo compruebo, fuera del modelo, que lo construido cumple.

## Qué quiero comprobar

- ¿Mejora el resultado de la IA cuando uso esta plantilla frente a una descripción libre?
- ¿Cuáles secciones sirven y cuáles sobran?

*Los resultados se documentarán en `05-experimentos`, no aquí.*
