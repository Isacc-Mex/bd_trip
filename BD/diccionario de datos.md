## Tabla: personas


| Campo            | Tipo           | Llave | Descripción                                     |
|------------------|----------------|-------|-------------------------------------------------|
| id               | INT UNSIGNED   | PK    | Identificador único de la persona               |
| titulo_cortesia  | VARCHAR(20)    |       | Título de cortesía (Sr., Sra., etc.)            |
| nombre           | VARCHAR(60)    |       | Nombre de la persona                            |
| primer_apellido  | VARCHAR(60)    |       | Primer apellido                                 |
| segundo_apellido | VARCHAR(60)    |       | Segundo apellido                                |
| fecha_nacimiento | DATE           |       | Fecha de nacimiento                             |
| genero           | ENUM           |       | Género de la persona (F, M, N/B)                |
---


## Tabla: persona_fisica

| Campo            | Tipo           | Llave | Descripción                                      |
|------------------|----------------|-------|--------------------------------------------------|
| id               | INT UNSIGNED   | PK    | Identificador único de la persona                |
| titulo_cortesia  | VARCHAR(20)    |       | Título de cortesía (Sr., Sra., etc.)             |
| nombre           | VARCHAR(60)    |       | Nombre de la persona                             | 
| primer_apellido  | VARCHAR(60)    |       | Primer apellido                                  |
| segundo_apellido | VARCHAR(60)    |       | Segundo apellido                                 |
| fecha_nacimiento | DATE           |       | Fecha de nacimiento                              |
| genero           | ENUM           |       | Género de la persona (F, M, N/B)                 |
---

## Tabla: persona_moral


| Campo                | Tipo               | Llave | Descripción                                              |
|----------------------|--------------------|-------|----------------------------------------------------------|
| id                   | INT UNSIGNED       | PK    | Identificador único de la empresa                        |
| razon_social         | VARCHAR(200)       |       | Nombre legal de la empresa                               |
| tipo                 | VARCHAR(100)       |       | Tipo de empresa (S.A., S. de R.L., etc.)                 |
| fecha_registro       | DATETIME           |       | Fecha en que se registró en el sistema                   |
| fecha_creacion       | DATE               |       | Fecha de constitución de la empresa                      |
| estatus              | ENUM               |       | Estado de la empresa (Activa, Inactiva, etc.)            |
| responsabilidad      | VARCHAR(100)       |       | Tipo de responsabilidad legal                            |
| capacidad_juridica   | VARCHAR(100)       |       | Capacidad legal de la empresa                            |
| patrimonio           | VARCHAR(100)       |       | Información sobre el patrimonio de la empresa            |

---

## Tabla: usuarios

#### Descripción:

| Campo                 | Tipo             | Llave | Descripción                                              |
|-----------------------|------------------|-------|----------------------------------------------------------|
| persona_fisica_id     | INT UNSIGNED     | PK    | Identificador de la persona física asociada              |
| nickname              | VARCHAR(80)      |       | Nombre de usuario único                                  |
| contrasenia           | VARCHAR(300)     |       | Contraseña del usuario (almacenada de forma segura)      |
| fecha_registro        | DATETIME         |       | Fecha de registro del usuario                            |
| fecha_ultimo_ingreso  | DATETIME         |       | Última vez que el usuario ingresó                        |
| estatus               | ENUM             |       | Estado del usuario (Activo, Inactivo, etc.)              |

---

## Tabla: clientes

| Campo                     | Tipo               | Llave | Descripción                                              |
|---------------------------|--------------------|-------|----------------------------------------------------------|
| id                        | INT UNSIGNED       | PK    | Identificador único del cliente                          |
| persona_id                | INT UNSIGNED       | UNI   | Identificador único de la persona asociada               |
| tipo_frecuencia           | ENUM               |       | Tipo de cliente según su frecuencia de compra            |
| monto_acumulado_compras   | DOUBLE             |       | Monto total acumulado de compras del cliente             |
| estatus                   | ENUM               |       | Estado del cliente (Activo, Inactivo, Bloqueado)         |
| fecha_registro            | DATETIME           |       | Fecha en que se registró el cliente                      |

---

## Tabla: proveedores

| Campo                 | Tipo               | Llave | Descripción                                              |
|-----------------------|--------------------|-------|----------------------------------------------------------|
| id                    | INT UNSIGNED       | PK    | Identificador único del proveedor                        |
| persona_id            | INT UNSIGNED       |       | Identificador de la persona asociada                     |
| tipo                  | ENUM               |       | Tipo de proveedor (Mayoreo, Menudeo o Mixto)             |
| estatus               | ENUM               |       | Estado del proveedor (Activo, Inactivo, etc.)            |
| fecha_registro        | DATETIME           |       | Fecha en que se registró el proveedor                    |
| total_productos       | INT                |       | Número de productos suministrados                        |
| monto_acumulado       | FLOAT              |       | Valor acumulado de los productos proporcionados          |
| fecha_ultima_compra   | DATETIME           |       | Fecha de la última transacción con el proveedor          |
---

## Tabla: divisas
---

| Campo          | Tipo            | Llave | Descripción                                      |
|----------------|-----------------|-------|--------------------------------------------------|
| id             | INT UNSIGNED    | PK    | Identificador único de la divisa                 |
| nombre         | VARCHAR(50)     |       | Nombre de la divisa (ej. Peso, Dólar)            |
| simbolo        | VARCHAR(5)      |       | Símbolo de la divisa (ej. $, USD, MXN)           |
| tasa_cambio    | DOUBLE          |       | Valor de conversión respecto a una moneda base   |
| estatus        | ENUM            |       | Estado de la divisa (Activa o Inactiva)          |
| fecha_registro | DATETIME        |       | Fecha en que se registró la divisa               |

---

## Tabla: categorias

| Campo              | Tipo               | Llave | Descripción                                                  |
|--------------------|--------------------|-------|--------------------------------------------------------------|
| id                 | INT UNSIGNED       | PK    | Identificador único de la categoría                          |
| nombre             | VARCHAR(100)       |       | Nombre de la categoría                                       |
| descripcion        | TEXT               |       | Descripción de la categoría                                  |
| fecha_registro     | DATETIME           |       | Fecha en que se registró la categoría                        |
| estatus            | ENUM               |       | Estado de la categoría (Activa, Inactiva, etc.)              |
| total_productos    | INT                |       | Número de productos asociados a la categoría                 |
| categoria_padre_id | INT UNSIGNED       |       |                                                              |

---

## Tabla: productos

| Campo            | Tipo               | Llave | Descripción                                              |
|------------------|--------------------|-------|----------------------------------------------------------|
| id               | INT UNSIGNED       | PK    | Identificador único del producto                         |
| nombre           | VARCHAR(150)       |       | Nombre del producto                                      |
| descripcion      | TEXT               |       | Descripción del producto                                 |
| marca            | VARCHAR(100)       |       | Marca del producto                                       |
| modelo           | VARCHAR(100)       |       | Modelo del producto                                      |
| precio_menudeo   | DECIMAL(10,2)      |       | Precio de venta al público                               |
| precio_mayoreo   | DECIMAL(10,2)      |       | Precio de venta al por mayor                             |
| tipo             | ENUM               |       | Tipo de producto (Perecedero o No Perecedero)            |
| estatus          | ENUM               |       | Estado del producto en inventario                        |
| codigo_barras    | VARCHAR(40)        | UNI   | Código de barras único del producto                      |
| sku              | VARCHAR(40)        | UNI   | Código SKU único del producto                            |

---

## Tabla: productos_categorias

| Campo          | Tipo             | Llave | Descripción                                      |
|----------------|------------------|-------|--------------------------------------------------|
| categoria_id   | INT UNSIGNED     | PK    | Identificador de la categoría                    |
| producto_id    | INT UNSIGNED     | PK    | Identificador del producto                       |
| estatus        | ENUM             |       | Estado de la relación (Activo o Inactivo)        |
| fecha_registro | DATETIME         |       | Fecha en que se creó la relación                 |

---

## Tabla: carritos

| Campo               | Tipo               | Llave | Descripción                                              |
|--------------------|--------------------|-------|----------------------------------------------------------|
| id                 | INT UNSIGNED       | PK    | Identificador único del carrito                          |
| sesion_id          | INT UNSIGNED       |       | Identificador de la sesión asociada al carrito           |
| divisa_id          | INT UNSIGNED       |       | Identificador de la divisa utilizada                     |
| total_productos    | INT UNSIGNED       |       | Cantidad total de productos en el carrito                |
| monto_aproximado   | DOUBLE UNSIGNED    |       | Monto total estimado del carrito                         |
| fecha_creacion     | DATETIME           |       | Fecha en que se creó el carrito                          |
| fecha_actualizacion| DATETIME           |       | Fecha de la última actualización                         |
| estatus            | ENUM               |       | Estado del carrito (Activo, Cancelado, etc.)             |

---

## Tabla: carrito_detalle

| Campo              | Tipo               | Llave | Descripción                                          |
|--------------------|--------------------|-------|------------------------------------------------------|
| carrito_id         | INT UNSIGNED       | PK    | Identificador del carrito                            |
| producto_id        | INT UNSIGNED       | PK    | Identificador del producto                           |
| cantidad           | INT UNSIGNED       |       | Cantidad del producto en el carrito                  |
| precio_unitario    | DOUBLE UNSIGNED    |       | Precio individual del producto                       |
| fecha_registro     | DATETIME           |       | Fecha en que se agregó el producto al carrito        |
| fecha_actualizacion| DATETIME           |       | Fecha de la última actualización                     |
| estatus            | ENUM               |       | Estado del producto (Activo, Eliminado, etc.)        |

---

## Tabla: pedidos

| Campo              | Tipo               | Llave | Descripción                                              |
|--------------------|--------------------|-------|----------------------------------------------------------|
| id                 | INT UNSIGNED       | PK    | Identificador único del pedido                           |
| carrito_id         | INT UNSIGNED       |       | Identificador del carrito asociado                       |
| total_productos    | INT UNSIGNED       |       | Cantidad total de productos en el pedido                 |
| importe_total      | DECIMAL(10,2)      |       | Monto total del pedido                                   |
| fecha_registro     | DATETIME           |       | Fecha en que se registró el pedido                       |
| fecha_actualizacion| DATETIME           |       | Fecha de la última actualización                         |
| estatus            | ENUM               |       | Estado del pedido (Pendiente, Enviado, Entregado, etc.)  |
| aprobacion         | BIT(1)             |       | Indica si el pedido ha sido aprobado (1 = sí, 0 = no)    |

---

## Tabla: metodos_pago

| Campo              | Tipo               | Llave | Descripción                                              |
|--------------------|--------------------|-------|----------------------------------------------------------|
| id                 | INT UNSIGNED       | PK    | Identificador único de la tarjeta                        |
| usuario_id         | INT UNSIGNED       |       | Identificador del usuario propietario de la tarjeta      |
| numero_tarjeta     | CHAR(16)           |       | Número de la tarjeta bancaria                            |
| tipo_red_bancaria  | ENUM               |       | Red bancaria (Visa, Mastercard, American Express)        |
| tipo_cuenta        | ENUM               |       | Tipo de cuenta (Débito, Crédito, etc.)                   |
| titular            | VARCHAR(100)       |       | Nombre del titular de la tarjeta                         |
| fecha_expiracion   | CHAR(5)            |       | Fecha de expiración (MM/YY)                              |
| fecha_registro     | DATETIME           |       | Fecha en que se registró la tarjeta                      |
| fecha_actualizacion| DATETIME           |       | Fecha de la última actualización                         |
| estatus            | ENUM               |       | Estado de la tarjeta (Vigente, Expirada, Desactivada)    |

---

## Tabla: transacciones_financieras

| Campo                 | Tipo                          | Llave | Descripción                                              |
|-----------------------|-------------------------------|-------|----------------------------------------------------------|
| id                    | INT UNSIGNED ZEROFILL         | PK    | Identificador único de la transacción                    |
| tipo                  | ENUM                          |       | Tipo de transacción (Compra, Venta, etc.)                |
| origen                | ENUM                          |       | Origen del pago (Tarjeta, Transferencia, etc.)           |
| clave_interbancaria   | CHAR(18)                      |       | CLABE interbancaria asociada                             |
| numero_convenio       | VARCHAR(50)                   |       | Número de convenio o referencia                          |
| monto                 | DECIMAL(10,2)                 |       | Monto de la transacción                                  |
| metodo_pago_id        | INT UNSIGNED ZEROFILL         |       | Identificador del método de pago                         |
| estatus               | ENUM                          |       | Estado de la transacción (Aprobado, Pendiente, etc.)     |
| fecha_registro        | DATETIME                      |       | Fecha en que se registró la transacción                  |
| fecha_actualizacion   | DATETIME                      |       | Fecha de la última actualización                         |

---

## Tabla: sesiones


| Campo             | Tipo               | Llave | Descripción                                              |
|-------------------|--------------------|-------|----------------------------------------------------------|
| id                | INT UNSIGNED       | PK    | Identificador único de la sesión                         |
| usuario_id        | INT UNSIGNED       |       | Identificador del usuario asociado                       |
| origen            | ENUM               |       | Origen de la sesión (Plataforma, Liga Externa, etc.)     |
| tipo_dispositivo  | ENUM               |       | Tipo de dispositivo utilizado                            |
| sistema_operativo | VARCHAR(50)        |       | Sistema operativo del dispositivo                        |
| codigo_pais       | CHAR(2)            |       | Código del país desde donde se accede                    |
| fecha_registro    | DATETIME           |       | Fecha de registro de la sesión                           |
| fecha_inicio      | DATETIME           |       | Fecha y hora de inicio de la sesión                      |
| fecha_fin         | DATETIME           |       | Fecha y hora de finalización de la sesión                |
| estatus           | ENUM               |       | Estado de la sesión (Activa, Finalizada, etc.)           |

---

## Tabla: bitacora

| Campo        | Tipo          | Llave | Descripción                                           |
|--------------|--------------|-------|-------------------------------------------------------|
| id           | INT UNSIGNED | PK    | Identificador único del registro                      |
| tabla        | VARCHAR(100) |       | Nombre de la tabla afectada                           |
| operacion    | ENUM         |       | Tipo de operación (Insert, Delete, Update)            |
| usuario      | VARCHAR(100) |       | Usuario que realizó la operación                      |
| descripcion  | TEXT         |       | Descripción adicional de la operación                 |
| fecha_hora   | DATETIME     |       | Fecha y hora en que ocurrió la operación              |

---