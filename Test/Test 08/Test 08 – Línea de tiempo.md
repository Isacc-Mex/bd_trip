## Test 08 – Línea de tiempo
---
 
#### Objetivo

Mostrar el orden cronológico en el que un usuario agrega productos a su carrito.

#### Descripción

Dado un id_carrito, se obtiene la secuencia temporal de selección de productos.

#### Resultado esperado

- ID del carrito
- ID del producto
- Nombre del producto
- Fecha y hora de agregación
- Orden de selección

#### Consideraciones técnicas

Tabla principal:
carrito_detalle

Ordenamiento:
ORDER BY fecha_agregado ASC

#### Evidencias

![Test 08 - Linea del tiempo" ](test8.png)

#### Estatus:
Exitosa.