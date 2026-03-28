## Indices Implementados
---

#### Tabla bitacora  

**Descripción:**  
La tabla `bitacora` almacena el historial de operaciones realizadas en la base de datos, incluyendo inserciones, actualizaciones y eliminaciones. Los índices en esta tabla permiten identificar registros de forma eficiente.

---

#### Índices

#### PRIMARY KEY (`id`)

```sql
PRIMARY KEY (`id`)
```
---

#### Tabla carrito_detalle 

**Descripción:**  
Listado completo de los índices definidos en la tabla `carrito_detalle`, utilizados para optimizar búsquedas, joins y validaciones dentro del sistema.

---

#### Índices

```sql
PRIMARY KEY (`carrito_id`,`producto_id`),
KEY `fk_carrito_idx` (`carrito_id`),
KEY `fk_producto2_idx` (`producto_id`),
KEY `idx_cd_estatus` (`estatus`),
KEY `idx_cd_fecha_registro` (`fecha_registro`)
```
---

#### Tabla carritos 

**Descripción:**  
Listado completo de los índices definidos en la tabla `carritos`, utilizados para optimizar búsquedas, relaciones y filtrado de carritos dentro del sistema.

---

#### Índices

```sql
PRIMARY KEY (`id`),
KEY `fk_divisa_idx` (`divisa_id`),
KEY `fk_sesion_idx` (`sesion_id`),
KEY `idx_carritos_estatus` (`estatus`)
```
---

#### Tabla categorias

**Descripción:**  
Listado completo de los índices definidos en la tabla `categorias`, utilizados para optimizar la identificación de categorías y la relación jerárquica entre ellas.

---

#### Índices

```sql
PRIMARY KEY (`id`),
KEY `fk_categoria_padre` (`categoria_padre_id`)
```
---

#### Tabla clientes

**Descripción:**  
Listado completo de los índices definidos en la tabla `clientes`, utilizados para optimizar la identificación de clientes y asegurar la relación única con la tabla `personas`.

---

#### Índices

```sql
PRIMARY KEY (`id`),
UNIQUE KEY `persona_id_UNIQUE` (`persona_id`)
```
---
#### Tabla divisas  

**Descripción:**  
Listado completo de los índices definidos en la tabla `divisas`, utilizados para optimizar la identificación de cada tipo de moneda en el sistema.

---

#### Índices

```sql
PRIMARY KEY (`id`)
```
---

#### Tabla metodos_pago

**Descripción:**  
Listado completo de los índices definidos en la tabla `metodos_pago`, utilizados para optimizar la relación con usuarios y el filtrado por estado de los métodos de pago.

---

#### Índices

```sql
PRIMARY KEY (`id`),
KEY `fk_usuario2_idx` (`usuario_id`),
KEY `idx_mp_estatus` (`estatus`)
```
---

#### Tabla pedidos 

**Descripción:**  
Listado completo de los índices definidos en la tabla `pedidos`, utilizados para optimizar la relación con carritos, así como consultas por estado y fechas.

---

#### Índices

```sql
PRIMARY KEY (`id`),
KEY `fk_carrito_idx` (`carrito_id`),
KEY `idx_pedidos_estatus` (`estatus`),
KEY `idx_pedidos_fecha_registro` (`fecha_registro`)
```
---

#### Tabla persona_fisica  

**Descripción:**  
Listado completo de los índices definidos en la tabla `persona_fisica`, utilizados para garantizar la unicidad de los registros y mantener la integridad con la tabla `personas`.

---

#### Índices

```sql
UNIQUE KEY `id_UNIQUE` (`id`)
```
---

#### Tabla persona_moral

**Descripción:**  
Listado completo de los índices definidos en la tabla `persona_moral`, utilizados para garantizar la unicidad de los registros y mantener la integridad con la tabla `personas`.

---

#### Índices

```sql
UNIQUE KEY `id_UNIQUE` (`id`)
```
---

#### Tabla personas

**Descripción:**  
Listado completo de los índices definidos en la tabla `personas`, utilizados para la identificación única de cada registro dentro del sistema.

---

#### Índices

```sql
PRIMARY KEY (`id`)
```
---

#### Tabla productos

**Descripción:**  
Listado completo de los índices definidos en la tabla `productos`, utilizados para garantizar la identificación única de productos y optimizar búsquedas por códigos clave.

---

#### Índices

```sql
PRIMARY KEY (`id`),
UNIQUE KEY `codigo_barras` (`codigo_barras`),
UNIQUE KEY `sku` (`sku`)
```
---

#### Tabla productos_categorias 

**Descripción:**  
Listado completo de los índices definidos en la tabla `productos_categorias`, utilizada para gestionar la relación entre productos y categorías.

---

#### Índices

```sql
PRIMARY KEY (`categoria_id`,`producto_id`),
KEY `fk_producto` (`producto_id`),
KEY `idx_pc_categoria_id` (`categoria_id`)
```
---

###3 Tabla proveedores

**Descripción:**  
Listado completo de los índices definidos en la tabla `proveedores`, utilizados para optimizar la identificación de proveedores y su relación con la tabla `personas`.

---

#### Índices

```sql
PRIMARY KEY (`id`),
KEY `fk_proveedpr_idx` (`persona_id`)
```
---

#### Tabla sesiones 

**Descripción:**  
Listado completo de los índices definidos en la tabla `sesiones`, utilizados para optimizar la relación con usuarios y consultas basadas en fechas de actividad.

---

#### Índices

```sql
PRIMARY KEY (`id`),
KEY `fk_usuarios1_idx` (`usuario_id`),
KEY `idx_sesiones_fecha_inicio` (`fecha_inicio`),
KEY `idx_sesiones_fecha_fin` (`fecha_fin`)
```
---

#### Tabla transacciones_financieras

**Descripción:**  
Listado completo de los índices definidos en la tabla `transacciones_financieras`, utilizados para optimizar consultas relacionadas con pagos, tipos de transacción, origen y análisis por fechas.

---

#### Índices

```sql
PRIMARY KEY (`id`),
KEY `fk_metodopago_idx` (`metodo_pago_id`),
KEY `idx_tf_tipo` (`tipo`),
KEY `idx_tf_origen` (`origen`),
KEY `idx_tf_metodo_pago_id` (`metodo_pago_id`),
KEY `idx_tf_fecha_registro` (`fecha_registro`)
```
---

#### Tabla usuarios

**Descripción:**  
Listado completo de los índices definidos en la tabla `usuarios`, utilizados para garantizar la unicidad de los registros y optimizar búsquedas por identificadores clave.

---

#### Índices

```sql
UNIQUE KEY `persona_fisica_id_UNIQUE` (`persona_fisica_id`),
UNIQUE KEY `nickname_UNIQUE` (`nickname`)
```
---






