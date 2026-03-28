## Test 03: Compras en el año 2026
---

#### Objetivo
Validar la correcta asignación y persistencia de fechas en transacciones.

#### Precondiciones
- Sistema permite manipulación de fechas
- Base de datos preparada

#### Flujo del proceso
1. Configurar fecha en **2026**
2. Ejecutar flujo de compra completo
3. Repetir hasta generar **100 compras**

#### Validaciones
- Campo fecha correcto
- Consistencia entre pedido y pago
- Persistencia en base de datos

#### Resultado esperado
- 100 compras con fecha en 2026
- Integridad de datos

#### Posibles errores
- Fechas incorrectas
- Problemas de formato
- Rechazos del sistema

#### Evidencias

Se debe incluir evidencia visual del resultado de la consulta ejecutada.

![Test 03 - Compras en el año 2026" ](https://github.com/Isacc-Mex/bd_trip/blob/main/Test/Test%2003/carritos_test3.png)

#### Estatus:
Exitosa.
