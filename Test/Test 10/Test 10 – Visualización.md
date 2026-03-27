## Test 10 – Visualización

#### Objetivo
Generar una visualización (dashboard) que permita analizar los pagos en función de su origen.

#### Descripción
Se construyó una visualización utilizando **Navicat**, aprovechando sus herramientas de gráficos integradas para representar la distribución de los pagos según su origen.

#### Herramienta utilizada

- **Navicat Data Visualization**

#### Requerimientos cumplidos

- Clasificación de pagos por origen  
- Total de pagos por cada origen  
- Importe total acumulado por origen  
- Visualización clara mediante gráficos  

#### Consulta base utilizada 

#### Evidencias

![Test 10 - Visualizacion]([grafica_navicat_pagos_por_origen.png))

#### Estatus:
Exitosa.

#### Consulta base utilizada 
```sql
SELECT 
    origen_pago,
    COUNT(*) AS total_pagos,
    SUM(importe) AS monto_total
FROM pagos
GROUP BY origen_pago;

#### Evidencias

Se debe incluir evidencia visual del resultado de la consulta ejecutada.

![Test 10 - Visualizacion" ](test1_230550.png)

#### Estatus:
Exitosa.
