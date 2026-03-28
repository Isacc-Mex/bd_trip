## Tabla: personas

#### Descripción:
Esta tabla almacena la información personal de los individuos dentro del sistema, incluyendo datos como nombre, apellidos, fecha de nacimiento y género.


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

#### Datos

Esta tabla almacena información personal de los usuarios o clientes del sistema, incluyendo:

- Nombre completo
- Fecha de nacimiento
- Género
- Información de identificación básica

#### trigger_personas_AFTER_INSERT
Descripción:
Trigger que registra automáticamente que se ha insertado una nueva persona.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `personas_AFTER_INSERT` AFTER INSERT ON `personas` FOR EACH ROW BEGIN
    INSERT INTO bitacora VALUES(DEFAULT, "personas", "Insert", 
    session_user(), concat_ws(" ",
    "Se ha insertado un nuevo persona del tipo:", new.tipo,
    "con el ID: ", new.id), now());
END

```

#### trigger_personas_AFTER_UPDATE
Descripción:
Trigger que registra automáticamente que se ha actualizado una persona.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `personas_AFTER_UPDATE` AFTER UPDATE ON `personas` FOR EACH ROW BEGIN
    INSERT INTO bitacora VALUES(DEFAULT, "persona", "Update", 
    session_user(), concat_ws(" ",
    "Se ha actualizado la persona con el ID: ", old.id), now());
END

```

#### trigger_personas_AFTER_DELETE
Descripción:
Trigger que registra automáticamente que se ha eliminado una persona .

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `personas_AFTER_DELETE` AFTER DELETE ON `personas` FOR EACH ROW BEGIN
INSERT INTO bitacora VALUES(DEFAULT, "personas", "Delete", 
    session_user(), concat_ws(" ",
    "Se ha  eliminado uan persona con el ID: ", old.id), now());
END

```
---

## Tabla: persona_fisica

#### Descripción:
Esta tabla almacena la información personal de los individuos dentro del sistema, incluyendo datos como nombre, apellidos, fecha de nacimiento y género.

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

#### Datos

Esta tabla almacena información personal de los usuarios del sistema, incluyendo:

- Titulo de cortesia
- Nombre
- Género
- Fecha de nacimiento
- Apellidos

#### trigger_persona_fisica_AFTER_INSERT
Descripción:
Trigger que registra automáticamente que se ha insertado una nueva persona física.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `persona_fisica_AFTER_INSERT` AFTER INSERT ON `persona_fisica` FOR EACH ROW BEGIN
    INSERT INTO bitacora VALUES(DEFAULT, "persona_fisica", "Insert", 
    session_user(), concat_ws(" ",
    "Se ha insertado una nueva persona física llamada:", 
    CONCAT_WS(" ",new.titulo_cortesia, new.nombre, new.primer_apellido,
    new.segundo_apellido),
    "con el ID: ", new.id), now());
END

```

#### trigger_persona_fisica_AFTER_UPDATE
Descripción:
Trigger que registra automáticamente que se ha actualizado una persona fisica.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `persona_fisica_AFTER_UPDATE` AFTER UPDATE ON `persona_fisica` FOR EACH ROW BEGIN
INSERT INTO bitacora VALUES(DEFAULT, "persona_fisica", "Update", 
    session_user(), concat_ws(" ",
    "Se ha actualizado la persona fisica con el ID: ", old.id), now());
END

```

#### trigger_persona_fisica_AFTER_UPDATE
Descripción:
Trigger que registra automáticamente que se ha actualizado una persona fisica.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `persona_fisica_AFTER_UPDATE` AFTER UPDATE ON `persona_fisica` FOR EACH ROW BEGIN
INSERT INTO bitacora VALUES(DEFAULT, "persona_fisica", "Update", 
    session_user(), concat_ws(" ",
    "Se ha actualizado la persona fisica con el ID: ", old.id), now());
END

```

#### trigger_persona_fisica_AFTER_DELETE
Descripción:
Trigger que registra automáticamente que se ha eliminado a una persona fisica.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `persona_fisica_AFTER_DELETE` AFTER DELETE ON `persona_fisica` FOR EACH ROW BEGIN
    INSERT INTO bitacora VALUES(DEFAULT, "persona_fisica", "delete", 
    session_user(), concat_ws(" ",
    "Se ha eliminado a la persona fisica con id:", old.id), now());
END

```
---

## Tabla: persona_moral

#### Descripción:
Esta tabla almacena la información de las personas morales dentro del sistema.

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

#### Datos

Esta tabla almacena información legal y administrativa de las empresas registradas en el sistema, incluyendo:

- Razón social
- Tipo de sociedad
- Estatus
- Información jurídica y patrimonial

#### trigger_persona_moral_AFTER_INSERT
Descripción:
Trigger que registra automáticamente que se ha insertado una nueva persona moral.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `persona_moral_AFTER_INSERT` AFTER INSERT ON `persona_moral` FOR EACH ROW BEGIN
    INSERT INTO bitacora VALUES(DEFAULT, "persona_moral", "Insert", 
    session_user(), concat_ws(" ",
    "Se ha insertado un nueva persona moral llamada:", new.razon_social,
    "con el ID: ", new.id), now());
END

```
#### trigger_persona_moral_AFTER_UPDATE
Descripción:
Trigger que registra automáticamente que se ha actualizado una persona moral.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `persona_moral_AFTER_UPDATE` AFTER UPDATE ON `persona_moral` FOR EACH ROW BEGIN
    INSERT INTO bitacora VALUES(DEFAULT, "persona_moral", "Update", 
    session_user(), concat_ws(" ",
    "Se ha actualizado la persona moral con el ID: ", old.id), now());
END

```

#### trigger_persona_moral_AFTER_DELETE
Descripción:
Trigger que registra automáticamente que se ha eliminado a UNA persona moral.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `persona_moral_AFTER_DELETE` AFTER DELETE ON `persona_moral` FOR EACH ROW BEGIN
    INSERT INTO bitacora VALUES(DEFAULT, "persona_moral", "Delete", 
    session_user(), concat_ws(" ",
    "Se ha eliminado a la persona moral con el ID: ",
    old.id), now());
END

```
---

## Tabla: usuarios

#### Descripción:
Esta tabla almacena la información de acceso de los usuarios del sistema, incluyendo sus credenciales, estado y relación con la persona física.

| Campo                 | Tipo             | Llave | Descripción                                              |
|-----------------------|------------------|-------|----------------------------------------------------------|
| persona_fisica_id     | INT UNSIGNED     | PK    | Identificador de la persona física asociada              |
| nickname              | VARCHAR(80)      |       | Nombre de usuario único                                  |
| contrasenia           | VARCHAR(300)     |       | Contraseña del usuario (almacenada de forma segura)      |
| fecha_registro        | DATETIME         |       | Fecha de registro del usuario                            |
| fecha_ultimo_ingreso  | DATETIME         |       | Última vez que el usuario ingresó                        |
| estatus               | ENUM             |       | Estado del usuario (Activo, Inactivo, etc.)              |

---

#### Datos

Esta tabla almacena información de autenticación y control de acceso de los usuarios, incluyendo:

- Nickname
- Contraseña
- fecha_registro
- fecha_ultimo_ingreso

#### trigger_usuarios_AFTER_INSERT
Descripción:
Trigger que registra automáticamente que se ha creado un nuevo usuario.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `usuarios_AFTER_INSERT` AFTER INSERT ON `usuarios` FOR EACH ROW BEGIN
	INSERT INTO bitacora VALUES(default, "usuarios",
    "Insert", session_user(), concat_ws(" ", "Se ha creado un nuevo
    usuario con el nickname:", new.nickname, "asociado a la persona 
    física con id:",  new.persona_fisica_id, "con estado:", new.estatus),
    now());
END

```

#### trigger_usuarios_AFTER_UPDATE
Descripción:
Trigger que registra automáticamente que se ha actualizado un usuario.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `usuarios_AFTER_UPDATE` AFTER UPDATE ON `usuarios` FOR EACH ROW BEGIN
	INSERT INTO bitacora VALUES(default, "usuarios",
    "Update", session_user(), concat_ws(" ", "Se ha actualizado el
    usuario con el nickname:", new.nickname, "asociado a la persona 
    física con id:",  new.persona_fisica_id, "con estado:", new.estatus),
    now());
END

```

#### trigger_usuarios_AFTER_DELETE
Descripción:
Trigger que registra automáticamente que se ha eliminado un usuario.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `usuarios_AFTER_DELETE` AFTER DELETE ON `usuarios` FOR EACH ROW BEGIN
	INSERT INTO bitacora VALUES(default, "usuarios",
    "Delete", session_user(), concat_ws(" ", "Se ha eliminado el
    usuario con el nickname:", old.nickname, "asociado a la persona 
    física con id:",  old.persona_fisica_id, "con estado:", old.estatus),
    now());
END

```
---

## Tabla: clientes

#### Descripción:
Esta tabla almacena información adicional sobre los clientes del sistema, incluyendo su tipo de frecuencia de compra, monto acumulado y estado dentro del sistema.

| Campo                     | Tipo               | Llave | Descripción                                              |
|---------------------------|--------------------|-------|----------------------------------------------------------|
| id                        | INT UNSIGNED       | PK    | Identificador único del cliente                          |
| persona_id                | INT UNSIGNED       | UNI   | Identificador único de la persona asociada               |
| tipo_frecuencia           | ENUM               |       | Tipo de cliente según su frecuencia de compra            |
| monto_acumulado_compras   | DOUBLE             |       | Monto total acumulado de compras del cliente             |
| estatus                   | ENUM               |       | Estado del cliente (Activo, Inactivo, Bloqueado)         |
| fecha_registro            | DATETIME           |       | Fecha en que se registró el cliente                      |

---

#### Datos

Esta tabla almacena información relacionada con el comportamiento de compra de los clientes, incluyendo:

- Frecuencia de compra
- Monto acumulado de adquisiciones
- Estado dentro del sistema

#### trigger_clientes_AFTER_INSERT
Descripción:
Trigger que registra automáticamente que se ha insertado un nuevo cliente asociado a una persona.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `clientes_AFTER_INSERT` AFTER INSERT ON `clientes` FOR EACH ROW BEGIN
    INSERT INTO bitacora VALUES(DEFAULT, "clientes", "Insert", 
    session_user(), concat_ws(" ",
    "Se ha insertado un nuevo cliente asociado a la persona con id : ", 
    new.persona_id), now());
END

```

#### trigger_clientes_AFTER_UPDATE
Descripción:
Trigger que registra automáticamente que se ha actualizado un cliente asociado a una persona.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `clientes_AFTER_UPDATE` AFTER UPDATE ON `clientes` FOR EACH ROW BEGIN
    INSERT INTO bitacora VALUES(DEFAULT, "clientes", "Update", 
    session_user(), concat_ws(" ",
    "Se ha actualizado el cliente asociado a la persona con el ID: ", 
    old.persona_id), now());
END

```

#### trigger_clientes_AFTER_DELETE
Descripción:
Trigger que registra automáticamente que se ha eliminado un cliente asociado a una persona.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `clientes_AFTER_DELETE` AFTER DELETE ON `clientes` FOR EACH ROW BEGIN
    INSERT INTO bitacora VALUES(DEFAULT, "clientes", "Delete", 
    session_user(), concat_ws(" ",
    "Se ha eliminado un cliente asociado a la persona con id : ", 
    old.persona_id), now());
END

```
---

## Tabla: proveedores

#### Descripción:
Esta tabla almacena la información de los proveedores del sistema, incluyendo su tipo, estado y métricas relacionadas con los productos suministrados.

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

#### Datos
Esta tabla almacena información relacionada con los proveedores del sistema, incluyendo:

- Tipo de proveedor según volumen de operación
- Cantidad de productos suministrados
- Monto acumulado de transacciones
- Última fecha de actividad

#### trigger_proveedores_AFTER_INSERT
Descripción:
Trigger que registra automáticamente que se ha insertado un nuevo proveedor asociado a una persona.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `proveedores_AFTER_INSERT` AFTER INSERT ON `proveedores` FOR EACH ROW BEGIN
 INSERT INTO bitacora VALUES(DEFAULT, "proveedores", "Insert", 
    session_user(), concat_ws(" ",
    "Se ha insertado un nuevo proveedor asociado a la persona con id : ", new.persona_id), now());
END

```

#### trigger_proveedores_AFTER_UPDATE
Descripción:
Trigger que registra automáticamente que se ha actualizado un proveedor asociado a una persona.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `proveedores_AFTER_UPDATE` AFTER UPDATE ON `proveedores` FOR EACH ROW BEGIN
    INSERT INTO bitacora VALUES(DEFAULT, "proveedores", "Update", 
    session_user(), concat_ws(" ",
    "Se ha actualizado el proveedor asociado a la persona con el ID: ",
    old.persona_id), now());
END

```

#### trigger_proveedores_AFTER_DELETE
Descripción:
Trigger que registra automáticamente que se ha eleminado UN proveedor asociado a una persona.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `proveedores_AFTER_DELETE` AFTER DELETE ON `proveedores` FOR EACH ROW BEGIN
INSERT INTO bitacora VALUES(DEFAULT, "proveedores", "Delete", 
    session_user(), concat_ws(" ",
    "Se ha eleminado el proveedor asociado a la persona con el ID: ",
    old.persona_id), now());
END

```
---

## Tabla: divisas
---

#### Descripción:
Esta tabla almacena las divisas utilizadas en el sistema, incluyendo su nombre, símbolo y tasa de cambio, permitiendo manejar diferentes monedas en las transacciones.

| Campo          | Tipo            | Llave | Descripción                                      |
|----------------|-----------------|-------|--------------------------------------------------|
| id             | INT UNSIGNED    | PK    | Identificador único de la divisa                 |
| nombre         | VARCHAR(50)     |       | Nombre de la divisa (ej. Peso, Dólar)            |
| simbolo        | VARCHAR(5)      |       | Símbolo de la divisa (ej. $, USD, MXN)           |
| tasa_cambio    | DOUBLE          |       | Valor de conversión respecto a una moneda base   |
| estatus        | ENUM            |       | Estado de la divisa (Activa o Inactiva)          |
| fecha_registro | DATETIME        |       | Fecha en que se registró la divisa               |

---

#### Datos
Esta tabla almacena información sobre las monedas disponibles en el sistema, incluyendo:

- Nombre de la divisa
- Símbolo representativo
- Tasa de cambio
- Estado de disponibilidad

#### trigger_divisas_AFTER_INSERT
Descripción:
Trigger que registra automáticamente que se ha insertado una nueva divisa.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `divisas_AFTER_INSERT` AFTER INSERT ON `divisas` FOR EACH ROW BEGIN
    INSERT INTO bitacora VALUES(DEFAULT, "divisas", "Insert", 
    session_user(), concat_ws(" ", "Se ha insertado una nueva divisa con id:", 
    new.id, "con nombre: ", new.nombre
    ), now());
END

```

#### trigger_divisas_AFTER_UPDATE
Descripción:
Trigger que registra automáticamente que se ha actualizado una divisa.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `divisas_AFTER_UPDATE` AFTER UPDATE ON `divisas` FOR EACH ROW BEGIN
    INSERT INTO bitacora VALUES(DEFAULT, "divisas", "Update", 
    session_user(), concat_ws(" ", "Se ha actualizado la divisa con id:", 
    new.id, "con nombre: ", new.nombre
    ), now());
END

```

#### trigger_divisas_AFTER_DELETE
Descripción:
Trigger que registra automáticamente que se ha eliminado una divisa.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `divisas_AFTER_DELETE` AFTER DELETE ON `divisas` FOR EACH ROW BEGIN
    INSERT INTO bitacora VALUES(DEFAULT, "divisas", "Delete", 
    session_user(), concat_ws(" ", "Se ha eliminado una divisa con id:", 
    old.id, "con nombre: ", old.nombre
    ), now());
END

```
--- 

## Tabla: categorias

#### Descripción:
Esta tabla almacena las categorías de los productos dentro del sistema, permitiendo organizar los productos de forma jerárquica mediante categorías padre.

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

#### Datos
Esta tabla almacena información sobre la clasificación de productos, incluyendo:

- Nombre y descripción de la categoría
- Estado de la categoría
- Cantidad de productos asociados
- Relación jerárquica entre categorías

#### trigger_categorias_AFTER_INSERT
Descripción:
Trigger que registra automáticamente que se ha creado una nueva categoria.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `categorias_AFTER_INSERT` AFTER INSERT ON `categorias` FOR EACH ROW BEGIN
INSERT INTO bitacora VALUES(DEFAULT, "categorias", "Insert", 
    session_user(), concat_ws(" ",
    "Se ha creado una nueva categoria con id: ", new.id, " nombrada:", 
    new.nombre), now());
END

```

#### trigger_categorias_AFTER_UPDATE
Descripción:
Trigger que registra automáticamente que se ha actualizado una categoria.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `categorias_AFTER_UPDATE` AFTER UPDATE ON `categorias` FOR EACH ROW BEGIN
	INSERT INTO bitacora VALUES(DEFAULT, "categorias", "Update", 
    session_user(), concat_ws(" ",
    "Se ha actualizado la categoria con id: ", new.id), now());
END

```

#### trigger_categorias_AFTER_DELETE
Descripción:
Trigger que registra automáticamente que se ha eliminado una categoria.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `categorias_AFTER_DELETE` AFTER DELETE ON `categorias` FOR EACH ROW BEGIN
INSERT INTO bitacora VALUES(DEFAULT, "categorias", "Delete", 
    session_user(), concat_ws(" ",
    "Se ha eliminado la categoria con id: ", old.id), now());
END

```

---

## Tabla: productos

#### Descripción:
Esta tabla almacena la información de los productos disponibles en el sistema, incluyendo sus características, precios, tipo y estado en inventario.

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

#### Datos

Esta tabla almacena información detallada de los productos disponibles en el sistema, incluyendo:

- Nombre, marca y modelo
- Precios de venta (menudeo y mayoreo)
- Tipo de producto
- Estado en inventario
- Identificadores únicos como código de barras y SKU

#### trigger_productos_AFTER_INSERT
Descripción:
Trigger que registra automáticamente que se ha insertado un nuevo producto.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `productos_AFTER_INSERT` AFTER INSERT ON `productos` FOR EACH ROW BEGIN
    INSERT INTO bitacora VALUES(DEFAULT, "productos", "Insert", 
    session_user(), concat_ws(" ",
    "Se ha insertado un nuevo producto llamado:", new.nombre,
    "con el ID: ", new.id), now());
END

```

#### trigger_productos_AFTER_UPDATE
Descripción:
Trigger que registra automáticamente que se ha actualizado un producto.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `productos_AFTER_UPDATE` AFTER UPDATE ON `productos` FOR EACH ROW BEGIN
    INSERT INTO bitacora VALUES(DEFAULT, "productos", "Update", 
    session_user(), concat_ws(" ",
    "Se ha actualizado el producto con el ID: ", old.id), now());
END

```

#### trigger_productos_AFTER_DELETE
Descripción:
Trigger que registra automáticamente que se ha eliminado un producto.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `productos_AFTER_DELETE` AFTER DELETE ON `productos` FOR EACH ROW BEGIN
   INSERT INTO bitacora VALUES(DEFAULT, "productos", "Delete", 
    session_user(), concat_ws(" ",
    "Se ha  eliminado el producto con el ID: ", old.id), now());
END

```
---

## Tabla: productos_categorias

#### Descripción:
Esta tabla establece la relación entre las categorías y los productos, permitiendo que un producto pertenezca a una o varias categorías.

| Campo          | Tipo             | Llave | Descripción                                      |
|----------------|------------------|-------|--------------------------------------------------|
| categoria_id   | INT UNSIGNED     | PK    | Identificador de la categoría                    |
| producto_id    | INT UNSIGNED     | PK    | Identificador del producto                       |
| estatus        | ENUM             |       | Estado de la relación (Activo o Inactivo)        |
| fecha_registro | DATETIME         |       | Fecha en que se creó la relación                 |

---

#### Datos
Esta tabla almacena la relación entre productos y categorías, permitiendo:

- Asignar múltiples categorías a un producto
- Organizar productos de forma flexible
- Controlar el estado de la relación

#### trigger_productos_categorias_AFTER_INSERT
Descripción:
Trigger que registra automáticamente que se asociado un producto a una categoria.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `productos_categorias_AFTER_INSERT` AFTER INSERT ON `productos_categorias` FOR EACH ROW BEGIN
    DECLARE v_nombre_producto VARCHAR(255);
    DECLARE v_nombre_categoria VARCHAR(255);

    SELECT nombre  INTO v_nombre_producto  FROM productos   WHERE id = NEW.producto_id;
    SELECT nombre  INTO v_nombre_categoria  FROM categorias WHERE id = NEW.categoria_id;

    INSERT INTO bitacora  VALUES ( DEFAULT,'productos_categorias','Insert', SESSION_USER(),
        CONCAT('Se ha asociado el producto id: ', NEW.producto_id,' con el nombre de: ', v_nombre_producto,
            ' con la categoría id: ', NEW.categoria_id,' con el nombre de: ', v_nombre_categoria),NOW());
END

```

#### trigger_productos_categorias_AFTER_UPDATE
Descripción:
Trigger que registra automáticamente que se ha actualizado un producto asociado a una categoria.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `productos_categorias_AFTER_UPDATE` AFTER UPDATE ON `productos_categorias` FOR EACH ROW BEGIN
    DECLARE v_nombre_producto VARCHAR(255);
    DECLARE v_nombre_categoria VARCHAR(255);

    SELECT nombre  INTO v_nombre_producto  FROM productos   WHERE id = NEW.producto_id;
    SELECT nombre  INTO v_nombre_categoria  FROM categorias WHERE id = NEW.categoria_id;

    INSERT INTO bitacora  VALUES ( DEFAULT,'productos_categorias','Update', SESSION_USER(),
        CONCAT('Se actualizado el producto id: ', NEW.producto_id,' con el nombre de: ', v_nombre_producto,
            ' a la categoría id: ', NEW.categoria_id,' con el nombre de: ', v_nombre_categoria),NOW());
END

```

#### trigger_productos_categorias_AFTER_DELETE
Descripción:
Trigger que registra automáticamente que se ha eliminado un producto asociado a una categoria.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `productos_categorias_AFTER_DELETE` AFTER DELETE ON `productos_categorias` FOR EACH ROW BEGIN
    DECLARE v_nombre_producto VARCHAR(255);
    DECLARE v_nombre_categoria VARCHAR(255);

    SELECT nombre  INTO v_nombre_producto  FROM productos   WHERE id = OLD.producto_id;
    SELECT nombre  INTO v_nombre_categoria  FROM categorias WHERE id = OLD.categoria_id;

    INSERT INTO bitacora  VALUES ( DEFAULT,'productos_categorias','Delete', SESSION_USER(),
        CONCAT('Se ha eliminado la asociación del producto id: ', OLD.producto_id,' con el nombre de: ', v_nombre_producto,
            ' con la categoría id: ', OLD.categoria_id,' con el nombre de: ', v_nombre_categoria),NOW());
END

```
---

## Tabla: carritos

#### Descripción:
Esta tabla almacena la información general de los carritos de compra generados en el sistema, incluyendo la sesión del usuario, cantidad de productos, monto estimado y estado del carrito.

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

#### Datos
Esta tabla almacena información general de los carritos de compra, incluyendo:

- Relación con la sesión del usuario
- Cantidad total de productos
- Monto estimado de compra
- Estado del carrito dentro del sistema


#### trigger_carrito_AFTER_INSERT
Descripción:
Trigger que registra automáticamente que se ha insertado un nuevo carrito.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `carrito_AFTER_INSERT` AFTER INSERT ON `carritos` FOR EACH ROW BEGIN
    DECLARE v_divisa VARCHAR(50) DEFAULT NULL;
    SET v_divisa = (SELECT nombre FROM divisas WHERE id= new.divisa_id);
    INSERT INTO bitacora VALUES(DEFAULT, "carritos", "Insert", 
    session_user(), concat_ws(" ", "Se ha insertado un nuevo carrito con id:", 
    new.id, " durante la sesión con id:", new.id, "usando como divisa:", v_divisa
    ), now());
END

```

#### trigger_carrito_AFTER_UPDATE
Descripción:
Trigger que registra automáticamente que se ha actualizado el carrito.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `carrito_AFTER_UPDATE` AFTER UPDATE ON `carritos` FOR EACH ROW BEGIN
    DECLARE v_divisa VARCHAR(50) DEFAULT NULL;
    SET v_divisa = (SELECT nombre FROM divisas WHERE id= new.divisa_id);
    INSERT INTO bitacora VALUES(DEFAULT, "carritos", "Update", 
    session_user(), concat_ws(" ", "Se ha actualizado el carrito con id:", 
    new.id, " durante la sesión con id:", new.id, "usando como divisa:", v_divisa
    ), now());
END

```

#### trigger_carrito_AFTER_DELETE
Descripción:
Trigger que registra automáticamente que se ha elminado un carrito.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `carrito_AFTER_DELETE` AFTER DELETE ON `carritos` FOR EACH ROW BEGIN
    DECLARE v_divisa VARCHAR(50) DEFAULT NULL;
    SET v_divisa = (SELECT nombre FROM divisas WHERE id= old.divisa_id);
    INSERT INTO bitacora VALUES(DEFAULT, "carritos", "Delete", 
    session_user(), concat_ws(" ", "Se ha elminado el carrito con id:", 
    old.id, " durante la sesión con id:", old.id, "usando como divisa:", v_divisa
    ), now());
END

```


---

## Tabla: carrito_detalle

#### Descripción:
Esta tabla almacena los productos que han sido agregados a un carrito de compras, incluyendo la cantidad, precio y estado del producto dentro del carrito.

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

#### Datos
Esta tabla almacena información relacionada con el carrito de compras, incluyendo:

- Productos agregados
- Cantidad de cada producto
- Precio al momento de agregarlo
- Estado del producto dentro del carrito

#### trigger_carrito_detalle_AFTER_INSERT
Descripción:
Trigger que registra automáticamente que se ha insertado un nuevo detalle de carrito.

```sql
CREATE DEFINER=`root`@`localhost` TRIGGER `carrito_detalle_AFTER_INSERT` AFTER INSERT ON `carrito_detalle` FOR EACH ROW BEGIN
    INSERT INTO bitacora VALUES(DEFAULT, "carrito_detalle", "Insert", 
    session_user(), concat_ws(" ",
    "Se ha insertado un nuevo detalle de carrito asociado al carrito con id:", new.carrito_id,
    "con el producto_id: ", new.producto_id), now());
END

```

#### trigger_carrito_detalle_AFTER_UPDATE
Descripción:
Trigger que registra automáticamente que se ha actualizado el detalle de carrito.

```sql
CREATE DEFINER=`root`@`localhost` TRIGGER `carrito_detalle_AFTER_INSERT` AFTER INSERT ON `carrito_detalle` FOR EACH ROW BEGIN
    INSERT INTO bitacora VALUES(DEFAULT, "carrito_detalle", "Insert", 
    session_user(), concat_ws(" ",
    "Se ha insertado un nuevo detalle de carrito asociado al carrito con id:", new.carrito_id,
    "con el producto_id: ", new.producto_id), now());
END

```

#### trigger_carrito_detalle_AFTER_DELETE
Descripción:
Trigger que registra automáticamente que se ha eliminado el detalle de carrito.

```sql
CREATE DEFINER=`root`@`localhost` TRIGGER `carrito_detalle_AFTER_DELETE` AFTER DELETE ON `carrito_detalle` FOR EACH ROW BEGIN
    INSERT INTO bitacora VALUES(DEFAULT, "carrito_detalle", "Delete", 
    session_user(), concat_ws(" ",
    "Se ha eliminado el detalle de carrito asociado al carrito con id:", old.carrito_id,
    "con el producto_id: ", old.producto_id), now());
END

```
---

## Tabla: pedidos

#### Descripción:
Esta tabla almacena la información de los pedidos generados a partir de los carritos de compra, incluyendo el total de productos, importe total, estado del pedido y su aprobación.

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

#### Datos

Esta tabla almacena información relacionada con los pedidos realizados en el sistema, incluyendo:

- Relación con el carrito de compra
- Cantidad total de productos
- Importe total
- Estado del pedido
- Aprobación del pedido

#### trigger_pedidos_after_insert
Descripción:
Trigger que registra automáticamente que se ha creado un nuevo pedido.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `pedidos_after_insert` AFTER INSERT ON `pedidos` FOR EACH ROW BEGIN
    INSERT INTO bitacora 
    VALUES (
        DEFAULT,
        'pedidos',
        'Insert',
        SESSION_USER(),
        CONCAT('Nuevo pedido creado con id: ', NEW.id),
        NOW()
    );
END

```

#### trigger_pedidos_after_update
Descripción:
Trigger que registra automáticamente que se ha actualizado un pedido.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `pedidos_after_update` AFTER UPDATE ON `pedidos` FOR EACH ROW BEGIN
    INSERT INTO bitacora 
    VALUES (
        DEFAULT,
        'pedidos',
        'Update',
        SESSION_USER(),
        CONCAT('Pedido actualizado id: ', NEW.id),
        NOW()
    );
END

```

#### trigger_pedidos_after_delete
Descripción:
Trigger que registra automáticamente que se ha elimina un pedido.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `pedidos_after_delete` AFTER DELETE ON `pedidos` FOR EACH ROW BEGIN
    INSERT INTO bitacora 
    VALUES (
        DEFAULT,
        'pedidos',
        'Delete',
        SESSION_USER(),
        CONCAT('Pedido eliminado id: ', OLD.id),
        NOW()
    );
END

```
---

## Tabla: metodos_pago

#### Descripción:
Esta tabla almacena la información de las tarjetas bancarias asociadas a los usuarios del sistema, permitiendo gestionar los métodos de pago disponibles para realizar transacciones.

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

#### Datos
Esta tabla almacena información sobre las tarjetas bancarias de los usuarios, incluyendo:

- Número de tarjeta
- Tipo de red bancaria
- Tipo de cuenta
- Titular
- Estado de la tarjeta

#### trigger_mp_insert
Descripción:
Trigger que registra automáticamente que se ha creado un metodo de pago.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `mp_insert` AFTER INSERT ON `metodos_pago` FOR EACH ROW INSERT INTO bitacora VALUES(DEFAULT,'metodos_pago','Insert',
SESSION_USER(), CONCAT('Metodo pago creado id:',NEW.id), NOW())

```

#### trigger_mp_update
Descripción:
Trigger que registra automáticamente que se ha actualizado un metodo de pago.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `mp_update` AFTER UPDATE ON `metodos_pago` FOR EACH ROW INSERT INTO bitacora VALUES(DEFAULT,'metodos_pago','Update',
SESSION_USER(), CONCAT('Metodo pago actualizado id:',NEW.id), NOW())

```

#### trigger_mp_delete
Descripción:
Trigger que registra automáticamente que se ha eliminado un metodo de pago.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `mp_delete` AFTER DELETE ON `metodos_pago` FOR EACH ROW INSERT INTO bitacora VALUES(DEFAULT,'metodos_pago','Delete',
SESSION_USER(), CONCAT('Metodo pago eliminado id:',OLD.id), NOW())

```
---

## Tabla: transacciones_financieras

#### Descripción:
Esta tabla almacena los movimientos financieros del sistema, incluyendo compras, ventas y otros tipos de operaciones, así como el origen del pago, monto y estado de la transacción.

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

#### Datos
Esta tabla almacena información sobre las transacciones financieras realizadas en el sistema, incluyendo:

- Tipo de operación (compra, venta, etc.)
- Origen del pago
- Monto de la transacción
- Estado de aprobación

#### trigger_tf_insert
Descripción:
Trigger que registra automáticamente que se ha creado una transacciòn.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `tf_insert` AFTER INSERT ON `transacciones_financieras` FOR EACH ROW INSERT INTO bitacora VALUES(DEFAULT,'transacciones_financieras','Insert',
SESSION_USER(), CONCAT('Transaccion creada id:',NEW.id), NOW())

```

#### trigger_tf_update
Descripción:
Trigger que registra automáticamente que se ha actualizado una transacciòn.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `tf_update` AFTER UPDATE ON `transacciones_financieras` FOR EACH ROW INSERT INTO bitacora VALUES(DEFAULT,'transacciones_financieras','Update',
SESSION_USER(), CONCAT('Transaccion actualizada id:',NEW.id), NOW())

```

#### trigger_tf_delete
Descripción:
Trigger que registra automáticamente que se ha eliminado una transacciòn.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `tf_delete` AFTER DELETE ON `transacciones_financieras` FOR EACH ROW INSERT INTO bitacora VALUES(DEFAULT,'transacciones_financieras','Delete',
SESSION_USER(), CONCAT('Transaccion eliminada id:',OLD.id), NOW())

```
---

## Tabla: sesiones

#### Descripción:
Esta tabla almacena la información de las sesiones de los usuarios dentro del sistema, permitiendo registrar el origen de acceso, tipo de dispositivo, sistema operativo y duración de la sesión.

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
#### Datos

Esta tabla almacena información sobre las sesiones de los usuarios, incluyendo:

- Origen de acceso
- Tipo de dispositivo utilizado
- Sistema operativo
- Ubicación aproximada (país)
- Duración de la sesión

#### trigger_sesiones_AFTER_INSERT
Descripción:
Trigger que registra automáticamente que se ha creado un nueva sesion.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `sesiones_AFTER_INSERT` AFTER INSERT ON `sesiones` FOR EACH ROW BEGIN
	DECLARE v_usuario VARCHAR(100) DEFAULT NULL;
	SET v_usuario = (select nickname from usuarios WHERE persona_fisica_id = new.usuario_id);
	INSERT INTO bitacora VALUES(default, "sesiones",
    "Insert", session_user(), concat_ws(" ", "Se ha creado un nueva
    sesion con id:", new.id , "asociado al usuario con nickname:",  v_usuario,
    "con estado:", new.estatus),
    now());
END

```

#### trigger_sesiones_AFTER_UPDATE
Descripción:
Trigger que registra automáticamente que se ha actualizado una sesión.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `sesiones_AFTER_UPDATE` AFTER UPDATE ON `sesiones` FOR EACH ROW BEGIN
	declare v_usuario VARCHAR(100) DEFAULT NULL;
	SET v_usuario = (select nickname from usuarios WHERE persona_fisica_id = new.usuario_id);
	INSERT INTO bitacora VALUES(default, "sesiones",
    "Update", session_user(), concat_ws(" ", "Se ha actualizado la sesión
     con id:", new.id , "asociada  al usuario con nickname:",  v_usuario,
    "con estado:", new.estatus),
    now());
END

```

#### trigger_sesiones_AFTER_DELETE
Descripción:
Trigger que registra automáticamente que se ha eliminado una sesión.

```sql

CREATE DEFINER=`root`@`localhost` TRIGGER `sesiones_AFTER_DELETE` AFTER DELETE ON `sesiones` FOR EACH ROW BEGIN
	DECLARE v_usuario VARCHAR(100) DEFAULT NULL;
	SET v_usuario = (select nickname from usuarios WHERE persona_fisica_id = old.usuario_id);
	INSERT INTO bitacora VALUES(default, "sesiones",
    "Delete", session_user(), concat_ws(" ", "Se ha eliminado la sesión
     con id:", old.id , "asociada  al usuario con nickname:",  v_usuario,
    "con estado:", old.estatus),
    now());
END

```
---

## Tabla: bitacora

#### #### Descripción:
Esta tabla almacena el registro de operaciones realizadas en la base de datos, permitiendo llevar un control de inserciones, eliminaciones y actualizaciones, así como el usuario que realizó cada acción.

| Campo        | Tipo          | Llave | Descripción                                           |
|--------------|--------------|-------|-------------------------------------------------------|
| id           | INT UNSIGNED | PK    | Identificador único del registro                      |
| tabla        | VARCHAR(100) |       | Nombre de la tabla afectada                           |
| operacion    | ENUM         |       | Tipo de operación (Insert, Delete, Update)            |
| usuario      | VARCHAR(100) |       | Usuario que realizó la operación                      |
| descripcion  | TEXT         |       | Descripción adicional de la operación                 |
| fecha_hora   | DATETIME     |       | Fecha y hora en que ocurrió la operación              |

---

#### Datos

Esta tabla almacena información de auditoría del sistema, incluyendo:

- Tipo de operación realizada  
- Tabla afectada  
- Usuario responsable  
- Fecha y hora del evento

#### Triggers

No se implementaron triggers en esta base de datos.

## Funciones 
---
#### calucla_antiguedad

**Descripción:** 
Calcula la antigüedad en años a partir de una fecha de registro.

```sql
CREATE DEFINER=`root`@`localhost` FUNCTION `calcula_antiguedad`(v_fecha_registro DATE) RETURNS int
    DETERMINISTIC
BEGIN
       
RETURN floor(datediff(NOW(),v_fecha_nacimiento)/365.25);
END
```
**Uso:**
Se utiliza para calcular el tiempo en años desde una fecha hasta la actualidad.
---
#### calcula_edad

**Descripción:** 
Calcula la edad de una persona en años a partir de su fecha de nacimiento.

```sql
CREATE DEFINER=`root`@`localhost` FUNCTION `calcula_edad`(v_fecha_nacimiento DATE) RETURNS int
    DETERMINISTIC
BEGIN
       
RETURN floor(datediff(NOW(),v_fecha_nacimiento)/365.25);
END
```

**Uso:**
Se utiliza para obtener la edad actual de una persona con base en su fecha de nacimiento.
---
#### elige_cantidad

**Descripción:** 
Genera una cantidad aleatoria basada en probabilidades predefinidas, simulando un comportamiento realista de selección de cantidades.

```sql
CREATE FUNCTION elige_cantidad()
RETURNS INT
DETERMINISTIC
BEGIN
    DECLARE v_random INT;

    SET v_random = genera_numero_aleatorio_rangos(1, 1000);

    RETURN CASE
        WHEN v_random <= 820 THEN 1
        WHEN v_random <= 940 THEN 2
        WHEN v_random <= 980 THEN 3
        WHEN v_random <= 995 THEN 4
        ELSE 5
    END;
END;
```

**Uso:**
Se utiliza para asignar cantidades de forma probabilística, por ejemplo en simulaciones de compras o generación de datos de prueba.
---
#### elige_dispositivo

**Descripción:** 
Genera un tipo de dispositivo de forma aleatoria basado en probabilidades predefinidas, simulando el comportamiento real de acceso de los usuarios.

```sql
CREATE DEFINER=`root`@`localhost` FUNCTION `elige_dispositivo`() RETURNS varchar(50) CHARSET utf8mb4
    DETERMINISTIC
BEGIN
 DECLARE v_random INT;

    -- Genera número aleatorio entre 1 y 100
    SET v_random = genera_numero_aleatorio_rangos(1,100);

    RETURN
        CASE
            WHEN v_random BETWEEN 1 AND 65 THEN 'Smart Phone'
            WHEN v_random BETWEEN 66 AND 77 THEN 'Laptop'
            WHEN v_random BETWEEN 78 AND 92 THEN 'PC'
            WHEN v_random BETWEEN 93 AND 94 THEN 'Tablet'
            WHEN v_random = 95 THEN 'Smart TV'
            ELSE 'Voice Assistant'
        END;
END
```
**Uso:**
Se utiliza para asignar de manera aleatoria el tipo de dispositivo desde el cual un usuario accede al sistema, útil para simulaciones y análisis de comportamiento.
---
#### elige_divisa

**Descripción:** 
Selecciona de forma aleatoria una divisa existente en la tabla `divisas`, devolviendo su identificador.

```sql
CREATE DEFINER=`root`@`localhost` FUNCTION `elige_divisa`() RETURNS int
    READS SQL DATA
BEGIN
    DECLARE v_id INT;
    SELECT d.id
      INTO v_id FROM divisas d  
      ORDER BY RAND() LIMIT 1;
    RETURN v_id;

END
```

**Uso:**
Se utiliza para asignar una divisa aleatoria en operaciones del sistema, como simulaciones de compras o generación de datos.
---
#### elige_pais

**Descripción:** 
Genera un código de país de forma aleatoria basado en una distribución probabilística, simulando la procedencia geográfica de los usuarios.

```sql
CREATE DEFINER=`root`@`localhost` FUNCTION `elige_pais`() RETURNS varchar(2) CHARSET utf8mb4
    NO SQL
BEGIN
 DECLARE v_rand INT;

    -- 1..10000 para manejar decimales en porcentajes
    SET v_rand = FLOOR(1 + RAND() * 10000);

    RETURN CASE
        WHEN v_rand <= 9510 THEN 'MX'  -- 95.10%
        WHEN v_rand <= 9860 THEN 'US'  -- +3.50% = 98.60%
        WHEN v_rand <= 9920 THEN 'CA'  -- +0.60% = 99.20%
        WHEN v_rand <= 9950 THEN 'CO'  -- +0.30% = 99.50%
        WHEN v_rand <= 9970 THEN 'ES'  -- +0.20% = 99.70%
        WHEN v_rand <= 9985 THEN 'GT'  -- +0.15% = 99.85%
        WHEN v_rand <= 9990 THEN 'DE'  -- +0.05% = 99.90%
        ELSE 'OT'                      -- +0.10% = 100%
    END;
END
```

**Uso:**
Se utiliza para asignar un país de origen a usuarios o sesiones dentro del sistema, útil para análisis geográfico y simulación de datos.
---
#### elige_plataforma

**Descripción:** 
Selecciona de forma aleatoria el origen de acceso de un usuario dentro del sistema, utilizando una lista predefinida de opciones.

```sql
CREATE DEFINER=`root`@`localhost` FUNCTION `elige_plataforma`() RETURNS varchar(50) CHARSET utf8mb4
    DETERMINISTIC
BEGIN
	DECLARE v_plataforma_elegida VARCHAR(50);
    SET v_plataforma_elegida= 
	ELT(genera_numero_aleatorio_rangos(1,3),
"Plataforma", "Liga Externa", "Campaña Publicitaria");

RETURN v_plataforma_elegida;
END
```

**Uso:**
Se utiliza para asignar el origen de acceso de un usuario o sesión, útil para análisis de tráfico y marketing.
---
#### elige_producto

**Descripción:** 
Selecciona un producto de forma aleatoria. Si se proporciona una categoría, el producto se elige únicamente dentro de esa categoría. En caso contrario, se selecciona cualquier producto disponible en el sistema.

```sql
CREATE DEFINER=`root`@`localhost` FUNCTION `elige_producto`(v_categoria VARCHAR(80)) RETURNS int
    READS SQL DATA
BEGIN
    DECLARE v_id INT;
    DECLARE v_existe INT DEFAULT 0;

    -- Si se proporciona una categoría, validar si existe
    IF v_categoria IS NOT NULL THEN
        SELECT COUNT(*)
        INTO v_existe
        FROM categorias
        WHERE nombre = v_categoria;

        -- Si no existe, detener ejecución
        IF v_existe = 0 THEN
            SIGNAL SQLSTATE '45000'
            SET MESSAGE_TEXT = 'La categoria ingresada no existe';
        END IF;
    END IF;

    -- Si la categoría es NULL → producto aleatorio
    IF v_categoria IS NULL THEN
        SELECT p.id
        INTO v_id
        FROM productos p
        ORDER BY RAND()
        LIMIT 1;

    ELSE
        -- Producto aleatorio de la categoría indicada
        SELECT p.id
        INTO v_id
        FROM productos p
        JOIN productos_categorias pc 
            ON p.id = pc.producto_id
        JOIN categorias c 
            ON pc.categoria_id = c.id
        WHERE c.nombre = v_categoria
        ORDER BY RAND()
        LIMIT 1;
    END IF;

    RETURN v_id;
END
```

**Uso:**
Se utiliza para asignar productos de manera aleatoria en simulaciones de compras o generación de datos, pudiendo filtrar por categoría para mayor control.
---
#### elige_sesion

**Descripción:** 
Selecciona una sesión activa de forma aleatoria dentro del sistema. Solo se consideran aquellas sesiones que tienen una fecha de inicio registrada.

```sql
CREATE DEFINER=`root`@`localhost` FUNCTION `elige_sesion`() RETURNS int
    READS SQL DATA
BEGIN
    DECLARE v_id INT;

    SELECT id INTO v_id
    FROM sesiones
    WHERE fecha_inicio IS NOT NULL
    ORDER BY RAND()
    LIMIT 1;

    IF v_id IS NULL THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'No hay sesiones disponibles';
    END IF;

    RETURN v_id;
END
```

**Uso:**
Se utiliza para asignar una sesión existente en procesos de simulación o pruebas, garantizando que la sesión sea válida (con fecha de inicio).
---
#### elige_sistema_operativo

**Descripción:** 
Selecciona un sistema operativo de forma aleatoria en función del tipo de dispositivo proporcionado, utilizando distribuciones probabilísticas para simular el uso real de tecnologías.

```sql
CREATE DEFINER=`root`@`localhost` FUNCTION `elige_sistema_operativo`(v_dispositivo VARCHAR(50)) RETURNS varchar(50) CHARSET utf8mb4
    DETERMINISTIC
BEGIN
 DECLARE v_random INT;

    SET v_random = genera_numero_aleatorio_rangos(1,100);
    RETURN
    CASE

        -- SMARTPHONE
        WHEN v_dispositivo = 'Smart Phone' THEN
            CASE
                WHEN v_random <= 82 THEN 'Android'
                ELSE 'iOS'
            END

        -- LAPTOP y DESKTOP
        WHEN v_dispositivo IN ('Laptop','PC') THEN
            CASE
                WHEN v_random <= 75 THEN 'Windows'
                WHEN v_random <= 95 THEN 'MacOS'
                ELSE 'Linux'
            END

        -- TABLET
        WHEN v_dispositivo = 'Tablet' THEN
            CASE
                WHEN v_random <= 55 THEN 'iOS'
                ELSE 'Android'
            END

        -- SMART TV
        WHEN v_dispositivo = 'Smart TV' THEN
            CASE
                WHEN v_random <= 60 THEN 'Android TV'
                WHEN v_random <= 85 THEN 'Tizen'
                ELSE 'WebOS'
            END

        -- ASISTENTE DE VOZ
        WHEN v_dispositivo = 'Voice Assistant' THEN
            CASE
                WHEN v_random <= 50 THEN 'Alexa OS'
                WHEN v_random <= 90 THEN 'Google Home'
                ELSE 'Apple Homekit'
            END

        ELSE 'Desconocido'

    END;
END
```

**Uso:**
Se utiliza para asignar un sistema operativo a un dispositivo dentro del sistema, permitiendo simular datos realistas para análisis tecnológico.
---
#### elige_usuario

**Descripción:** 
Selecciona de forma aleatoria un usuario activo dentro del sistema, garantizando que solo se consideren registros con estatus válido.

```sql
CREATE DEFINER=`root`@`localhost` FUNCTION `elige_usuario`() RETURNS int
    READS SQL DATA
BEGIN
    DECLARE v_id INT;
    SELECT u.persona_fisica_id
      INTO v_id FROM usuarios u  WHERE u.estatus = "Activo"
      ORDER BY RAND() LIMIT 1;
    RETURN v_id;

END
```

**Uso:**
Se utiliza para obtener un usuario válido en procesos de simulación, pruebas o generación de datos dentro del sistema.
---
#### fn_duracion_sesion

**Descripción:** 
Calcula la duración de una sesión en formato de tiempo (HH:MM:SS) a partir de la diferencia entre la fecha de inicio y la fecha de fin.

```sql
CREATE DEFINER=`root`@`localhost` FUNCTION `fn_duracion_sesion`(
    fecha_inicio DATETIME,
    fecha_fin DATETIME
) RETURNS time
    DETERMINISTIC
BEGIN
    RETURN SEC_TO_TIME(TIMESTAMPDIFF(SECOND, fecha_inicio, fecha_fin));
END
```

**Uso:**
Se utiliza para medir el tiempo que un usuario permanece activo en una sesión, útil para análisis de comportamiento y métricas de engagement.
---
#### fn_tiempo_compra  

**Descripción:**  
Genera una nueva fecha y hora sumando un intervalo aleatorio de entre 1 y 10 minutos a una fecha base. Se utiliza para simular tiempos de compra o variaciones en registros temporales.

```sql
CREATE DEFINER=`root`@`localhost` FUNCTION `fn_tiempo_compra`(fecha_base DATETIME) RETURNS datetime
    DETERMINISTIC
BEGIN
    RETURN DATE_ADD(fecha_base, INTERVAL FLOOR(1 + RAND()*10) MINUTE);
END
```
**Uso:**
Se utiliza para simular el momento en que se realiza una compra a partir de una fecha base, agregando un tiempo aleatorio.
---
#### genera_numero_aleatorio_rangos  

**Descripción:**  
Genera un número entero aleatorio dentro de un rango definido, incluyendo tanto el límite inferior como el límite superior.

```sql
CREATE DEFINER=`root`@`localhost` FUNCTION `genera_numero_aleatorio_rangos`(v_limite_inferior INT,v_limite_superior INT) RETURNS int
    DETERMINISTIC
BEGIN
  RETURN FLOOR(v_limite_inferior + (RAND() * (v_limite_superior
  - v_limite_inferior + 1)));
END
```

**Uso:**
Se utiliza para generar valores aleatorios en un rango específico, útil en pruebas, simulaciones, generación de datos ficticios o lógica que requiera variabilidad controlada dentro de ciertos límites.
---
#### limpiar_caracteres_especiales  

**Descripción:**  
Limpia un texto eliminando caracteres especiales y normalizando letras con acentos o caracteres propios del español. Convierte caracteres acentuados a su forma básica y elimina cualquier símbolo que no sea letra, número, guion o punto.

```sql
CREATE DEFINER=`root`@`localhost` FUNCTION `limpiar_caracteres_especiales`(p_texto TEXT) RETURNS text CHARSET utf8mb4
    DETERMINISTIC
BEGIN

    DECLARE v_texto TEXT;

    SET v_texto = p_texto;

    -- Normalización básica (acentos)
    SET v_texto = REPLACE(v_texto, 'á', 'a');
    SET v_texto = REPLACE(v_texto, 'é', 'e');
    SET v_texto = REPLACE(v_texto, 'í', 'i');
    SET v_texto = REPLACE(v_texto, 'ó', 'o');
    SET v_texto = REPLACE(v_texto, 'ú', 'u');

    SET v_texto = REPLACE(v_texto, 'Á', 'A');
    SET v_texto = REPLACE(v_texto, 'É', 'E');
    SET v_texto = REPLACE(v_texto, 'Í', 'I');
    SET v_texto = REPLACE(v_texto, 'Ó', 'O');
    SET v_texto = REPLACE(v_texto, 'Ú', 'U');

    SET v_texto = REPLACE(v_texto, 'ñ', 'n');
    SET v_texto = REPLACE(v_texto, 'Ñ', 'N');
    SET v_texto = REPLACE(v_texto, 'ü', 'u');
    SET v_texto = REPLACE(v_texto, 'Ü', 'U');

    -- Expresión regular:
    -- elimina cualquier caracter que NO sea letra, número o espacio o punto
    SET v_texto = REGEXP_REPLACE(v_texto, '[^A-Za-z0-9-.]', '');

    RETURN v_texto;
END
```

**Uso:**
Se utiliza para limpiar y estandarizar textos antes de almacenarlos o procesarlos, por ejemplo en nombres, direcciones o datos de entrada de usuarios.
---
#### saluda  

**Descripción:**  
Devuelve un mensaje de saludo fijo desde una función en SQL. Es una función simple utilizada principalmente para pruebas o demostraciones.

```sql
CREATE DEFINER=`root`@`localhost` FUNCTION `saluda`() RETURNS varchar(50) CHARSET utf8mb4
    DETERMINISTIC
BEGIN

RETURN "Hola desde una función SQL";
END
```

**Uso:**
Se utiliza para verificar el correcto funcionamiento de funciones en la base de datos, realizar pruebas básicas o como ejemplo didáctico para entender la creación y ejecución de funciones en SQL.
---
## Procesos
---

#### aux_finaliza_pedido_individual  

**Descripción:**  
Procedimiento almacenado que finaliza un pedido a partir de un carrito específico. Calcula el total de productos y el importe, genera el pedido correspondiente, registra la transacción financiera y actualiza el estado del carrito.

```sql
CREATE DEFINER=`root`@`localhost` PROCEDURE `aux_finaliza_pedido_individual`(IN p_carrito_id INT)
BEGIN
    DECLARE v_total DECIMAL(10,2);
    DECLARE v_total_prod INT;
    DECLARE v_f_ultimo_item DATETIME;
    DECLARE v_usuario_id INT;
    DECLARE v_metodo_id INT;
    DECLARE v_pedido_id INT;

    -- A. Obtener datos del carrito y fecha del último producto
    SELECT 
        IFNULL(SUM(precio_unitario * cantidad), 0), 
        IFNULL(SUM(cantidad), 0), 
        MAX(fecha_registro) 
    INTO v_total, v_total_prod, v_f_ultimo_item
    FROM carrito_detalle
    WHERE carrito_id = p_carrito_id AND estatus = 'Activo';

    -- B. Solo proceder si hay productos
    IF v_total > 0 THEN
        
        -- C. Encontrar al dueño del carrito (Relación Carritos -> Sesiones -> Usuarios)
        SELECT s.usuario_id INTO v_usuario_id
        FROM sesiones s JOIN carritos c ON s.id = c.sesion_id
        WHERE c.id = p_carrito_id;

        -- D. Buscar el método de pago del usuario (Relación Usuarios -> Metodos_Pago)
        SELECT id INTO v_metodo_id FROM metodos_pago 
        WHERE usuario_id = v_usuario_id LIMIT 1;

        -- E. INSERTAR PEDIDO (Relación Pedidos -> Carritos)
        INSERT INTO pedidos(
            carrito_id, 
            total_productos, 
            importe_total, 
            fecha_registro, 
            estatus, 
            aprobacion
        )
        VALUES (
            p_carrito_id, 
            v_total_prod, 
            v_total, 
            DATE_ADD(v_f_ultimo_item, INTERVAL 30 SECOND), 
            'Pagado', 
            1
        );
        
        SET v_pedido_id = LAST_INSERT_ID();

        -- F. INSERTAR TRANSACCIÓN (Relación Transacciones -> Pedidos Y Metodos_Pago)
        -- Ajusta el nombre de la columna 'pedido_id' si en tu tabla se llama distinto
        INSERT INTO transacciones_financieras(
            metodo_pago_id, 
            tipo, 
            monto, 
            fecha_registro, 
            estatus
        )
        VALUES (
            v_metodo_id, 
            'Compra', 
            v_total, 
            DATE_ADD(v_f_ultimo_item, INTERVAL 1 MINUTE), 
            'Aprobado'
        );

        -- G. ACTUALIZAR CARRITO (Cierre del ciclo)
        UPDATE carritos SET estatus = 'Convertido' WHERE id = p_carrito_id;

    END IF;
END
```
**Uso:**
Se utiliza para automatizar el proceso de cierre de compra de un carrito específico (p_carrito_id), generando el pedido correspondiente, registrando la transacción financiera y actualizando el estado del carrito a "Convertido".
---
#### crear_usuarios  

**Descripción:**  
Procedimiento almacenado que genera automáticamente usuarios a partir de los registros de la tabla `persona_fisica`. Construye un nickname único basado en el nombre y apellido, asigna una contraseña temporal y registra el usuario en la base de datos evitando duplicados.

```sql
CREATE DEFINER=`root`@`localhost` PROCEDURE `crear_usuarios`()
BEGIN
    DECLARE v_id_pf BIGINT;
    DECLARE v_nombre VARCHAR(100);
    DECLARE v_apellido VARCHAR(100);

    DECLARE v_base_nick VARCHAR(255);
    DECLARE v_nick_final VARCHAR(255);
    DECLARE v_pass_temp VARCHAR(255);

    DECLARE v_sufijo INT;
    DECLARE v_existe INT;

    DECLARE done INT DEFAULT 0;

    -- Cursor: recorre todas las personas físicas
    -- (si quieres solo las que NO tienen usuario, ya lo filtramos dentro)
    DECLARE cur CURSOR FOR
        SELECT pf.id, pf.nombre, pf.primer_apellido
        FROM persona_fisica pf;

    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = 1;

    OPEN cur;

    read_loop: LOOP
        FETCH cur INTO v_id_pf, v_nombre, v_apellido;

        IF done = 1 THEN
            LEAVE read_loop;
        END IF;

        -- 1) Evita duplicar: si ya existe usuario para esta persona, saltar
        SELECT COUNT(*)
          INTO v_existe
          FROM usuarios u
         WHERE u.persona_fisica_id = v_id_pf;

        IF v_existe > 0 THEN
            ITERATE read_loop;
        END IF;

        -- 2) Construir nickname base: primera letra del nombre + '.' + primer apellido
        --    - lower()
        --    - limpiar caracteres especiales
        SET v_base_nick = LOWER(
            limpiar_caracteres_especiales(
                CONCAT(LEFT(TRIM(v_nombre), 1), '.', TRIM(v_apellido))
            )
        );

        -- opcional: quitar espacios que pudieron quedar (por si apellido compuesto raro)
        SET v_base_nick = REPLACE(v_base_nick, ' ', '');

        -- 3) Garantizar único: si ya existe, agregar sufijo incremental
        SET v_nick_final = v_base_nick;
        SET v_sufijo = 1;

        nick_loop: LOOP
            SELECT COUNT(*)
              INTO v_existe
              FROM usuarios u
             WHERE u.nickname = v_nick_final;

            IF v_existe = 0 THEN
                LEAVE nick_loop;
            END IF;

            SET v_sufijo = v_sufijo + 1;
            SET v_nick_final = CONCAT(v_base_nick, v_sufijo);  -- m.ramirez2, m.ramirez3, ...
        END LOOP;

        -- 4) Password temporal en texto plano (ejemplo)
        --    Puedes cambiar el patrón al que uses en clase
        SET v_pass_temp = CONCAT('Temp#', v_id_pf);

        -- 5) Insertar usuario
        INSERT INTO usuarios (persona_fisica_id, nickname, contrasenia,fecha_registro, estatus)
        VALUES (v_id_pf, v_nick_final, v_pass_temp, NOW(), default);

    END LOOP;

    CLOSE cur;
END
```

**Uso:**
Se utiliza para automatizar la creación de cuentas de usuario a partir de registros existentes de personas físicas.

#### finalizar_compra  

**Descripción:**  
Procedimiento almacenado que procesa la finalización de una compra a partir de un carrito. Calcula el total, genera una transacción financiera con datos simulados (origen, CLABE, convenio, estatus) y actualiza el estado del carrito.

**Parámetros:**  
- `p_carrito_id` (INT): Identificador del carrito que se desea finalizar  

**Retorna:**  
- *No retorna valores* (Procedimiento almacenado)  

```sql
CREATE DEFINER=`root`@`localhost` PROCEDURE `finalizar_compra`(
    IN p_carrito_id INT
)
BEGIN
    DECLARE v_total DECIMAL(10,2);

    DECLARE v_tipo VARCHAR(20);
    DECLARE v_origen VARCHAR(50);
    DECLARE v_metodo_pago INT;
    DECLARE v_estatus VARCHAR(20);

    DECLARE v_clabe CHAR(18);
    DECLARE v_convenio VARCHAR(50);

    --  Total del carrito
    SELECT IFNULL(SUM(cantidad * precio_unitario),0)
    INTO v_total
    FROM carrito_detalle
    WHERE carrito_id = p_carrito_id;

    --  Validación
    IF v_total = 0 THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'El carrito está vacío';
    END IF;

    --  Tipo fijo (más lógico en compras)
    SET v_tipo = 'Compra';

    --  Origen aleatorio (respetando ENUM EXACTO)
    SET v_origen = ELT(FLOOR(1 + (RAND() * 7)),
        'Tarjeta de Débito',
        'Tarjeta de Crédito',
        'Transferencia Bancaria',
        'Socio Comercial',
        'Tarjeta de Regalo',
        'Créditos Devolución',
        'Vales Despensa'
    );

    --  Método de pago real (mejor opción)
    SELECT id INTO v_metodo_pago
    FROM metodos_pago
    ORDER BY RAND()
    LIMIT 1;

    --  Estatus aleatorio
    SET v_estatus = ELT(FLOOR(1 + (RAND() * 4)),
        'Aprobado',
        'No Aprobado',
        'Pendiente',
        'Cancelado'
    );

    --  CLABE simulada (18 dígitos)
    SET v_clabe = LPAD(FLOOR(RAND()*100000000000000000),18,'0');

    --  Número de convenio
    SET v_convenio = CONCAT('CONV-', FLOOR(RAND()*100000));

    --  INSERT FINAL
    INSERT INTO transacciones_financieras (
        tipo,
        origen,
        clave_interbancaria,
        numero_convenio,
        monto,
        metodo_pago_id,
        estatus,
        fecha_registro,
        fecha_actualizacion
    )
    VALUES (
        v_tipo,
        v_origen,
        v_clabe,
        v_convenio,
        v_total,
        v_metodo_pago,
        v_estatus,
        NOW(),
        NOW()
    );

    --  Cerrar carrito
    UPDATE carrito
    SET estado = 'Finalizado'
    WHERE id = p_carrito_id;

END
```

**Uso:**
Se utiliza para completar el proceso de compra de un carrito (p_carrito_id), validando que tenga productos, generando una transacción financiera con datos simulados y actualizando el estado del carrito a "Finalizado". Es útil en pruebas de sistemas de e-commerce y simulaciones de procesos de pago.
---
#### limpiar_bd  

**Descripción:**  
Procedimiento almacenado que elimina los datos de varias tablas de la base de datos y reinicia sus contadores `AUTO_INCREMENT`. Incluye una validación de seguridad mediante contraseña para evitar ejecuciones accidentales.

```sql
CREATE DEFINER=`root`@`localhost` PROCEDURE `limpiar_bd`(reset_password varchar(20))
BEGIN
    -- Validar contraseña antes de ejecutar
    IF reset_password <> 'TI-evnd#2026' THEN
    
    SIGNAL SQLSTATE '45000'
    SET MESSAGE_TEXT = 'ERROR: Password de limpieza incorrecto. 
    Operación cancelada.';
    
    ELSE
        START TRANSACTION;
        -- Permitir DELETE sin WHERE (solo para práctica)
        SET SQL_SAFE_UPDATES = 0;
        DELETE FROM clientes;
        ALTER TABLE clientes AUTO_INCREMENT = 1;
        DELETE FROM proveedores;
        ALTER TABLE proveedores AUTO_INCREMENT = 1;
        DELETE FROM persona_fisica;
        DELETE FROM persona_moral;
        DELETE FROM personas;
        ALTER TABLE personas AUTO_INCREMENT = 1;
        DELETE FROM bitacora;
        ALTER TABLE bitacora AUTO_INCREMENT = 1;
        COMMIT;
    END IF;
END
```

**Uso:**
Se utiliza para limpiar completamente los datos de la base de datos en entornos de prueba o desarrollo, reiniciando las tablas principales.

---

#### limpiar_datos_compras  

**Descripción:**  
Procedimiento almacenado que elimina todos los datos relacionados con el proceso de compras, incluyendo carritos, pedidos, transacciones y métodos de pago. También limpia registros específicos de la bitácora y reinicia los valores `AUTO_INCREMENT` para mantener consistencia en pruebas.

```sql
CREATE DEFINER=`root`@`localhost` PROCEDURE `limpiar_datos_compras`()
BEGIN
    -- Desactivar llaves foráneas
    SET FOREIGN_KEY_CHECKS = 0;

    -- Eliminar datos
    DELETE FROM carrito_detalle;
    DELETE FROM carritos;
    ALTER TABLE carritos AUTO_INCREMENT = 1;

    DELETE FROM pedidos;
    ALTER TABLE pedidos AUTO_INCREMENT = 1;

    DELETE FROM transacciones_financieras;
    ALTER TABLE transacciones_financieras AUTO_INCREMENT = 1;

    DELETE FROM metodos_pago;
    ALTER TABLE metodos_pago AUTO_INCREMENT = 1;

    -- Limpiar bitácora
    DELETE FROM bitacora WHERE tabla = 'carritos';
    DELETE FROM bitacora WHERE tabla = 'carrito_detalle';
    DELETE FROM bitacora WHERE tabla = 'pedidos';
    DELETE FROM bitacora WHERE tabla = 'transacciones_financieras';
    DELETE FROM bitacora WHERE tabla = 'metodos_pago';

    -- Reiniciar auto_increment de bitácora
    ALTER TABLE bitacora AUTO_INCREMENT = 251;

    -- Activar llaves foráneas
    SET FOREIGN_KEY_CHECKS = 1;
END
```
**Uso:**
Se utiliza para reiniciar completamente los datos relacionados con compras en la base de datos, facilitando pruebas, simulaciones o reinicios de entorno.

---

#### rellenar_metodos_pago  

**Descripción:**  
Procedimiento almacenado que genera y asigna automáticamente métodos de pago a los usuarios existentes. Recorre la tabla de usuarios, obtiene el nombre del titular y crea registros simulados de tarjetas bancarias con datos aleatorios.

```sql
CREATE DEFINER=`root`@`localhost` PROCEDURE `rellenar_metodos_pago`()
BEGIN
    DECLARE v_done INT DEFAULT FALSE;
    DECLARE v_usuario_id INT;
    DECLARE v_nombre VARCHAR(100);
    
    DECLARE cur_usuarios CURSOR FOR 
        SELECT u.persona_fisica_id, pf.nombre 
        FROM usuarios u
        JOIN persona_fisica pf ON u.persona_fisica_id = pf.id;
        
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET v_done = TRUE;

    OPEN cur_usuarios;
    usuarios_loop: LOOP
        FETCH cur_usuarios INTO v_usuario_id, v_nombre;
        IF v_done THEN LEAVE usuarios_loop; END IF;

        INSERT INTO metodos_pago (
            usuario_id, 
            numero_tarjeta, 
            tipo_red_bancaria, 
            tipo_cuenta, 
            titular, 
            fecha_expiracion, 
            fecha_registro, 
            estatus
        )
        VALUES (
            v_usuario_id,
            CONCAT(FLOOR(1000 + RAND() * 8999), '0000', FLOOR(1000 + RAND() * 8999), '9999'),
            ELT(FLOOR(1 + RAND() * 3), 'Visa', 'Mastercard', 'American express'),
            'Debito',
            v_nombre,
            '12/28',
            NOW(),
            'Vigente'
        );
    END LOOP;
    CLOSE cur_usuarios;
    SELECT 'Tabla metodos_pago lista' AS Resultado;
END
```

**Uso:**
Se utiliza para poblar automáticamente la tabla metodos_pago con datos simulados para cada usuario existente.
---

#### simula_carritos  

**Descripción:**  
Procedimiento almacenado que simula la creación de múltiples carritos de compra con comportamiento realista. Genera carritos asociados a sesiones, agrega productos aleatorios (opcionalmente filtrados por categoría), define cantidades, estatus y fechas dentro del rango de la sesión, y calcula los totales finales.

```sql
CREATE DEFINER=`root`@`localhost` PROCEDURE `simula_carritos`(
    IN p_cuantos INT,
    IN p_total_productos INT,
    IN p_categoria VARCHAR(100)
)
BEGIN
    DECLARE v_i INT DEFAULT 1;
    DECLARE v_j INT DEFAULT 0;
    DECLARE v_intentos INT DEFAULT 0;
    DECLARE v_max_intentos INT DEFAULT 200;

    DECLARE v_sesion_id INT;
    DECLARE v_carrito_id INT;
    DECLARE v_divisa_id INT;

    DECLARE v_f_inicio_sesion DATETIME;
    DECLARE v_f_fin_sesion DATETIME;
    DECLARE v_fecha_item DATETIME;
    DECLARE v_segundos_sesion INT;

    DECLARE v_total_productos_actual INT;
    DECLARE v_producto_id INT;
    DECLARE v_precio_unitario DECIMAL(10,2);
    DECLARE v_estatus_item VARCHAR(20);

    DECLARE v_duracion_min INT;
    DECLARE v_tipo_usuario INT;

    DECLARE EXIT HANDLER FOR SQLEXCEPTION
    BEGIN
        ROLLBACK;
        RESIGNAL;
    END;

    carritos_loop: WHILE v_i <= p_cuantos DO
        START TRANSACTION;

        SET v_sesion_id = elige_sesion();
        SET v_divisa_id = elige_divisa();

        SELECT fecha_inicio, fecha_fin
        INTO v_f_inicio_sesion, v_f_fin_sesion
        FROM sesiones
        WHERE id = v_sesion_id;

        SET v_segundos_sesion = TIMESTAMPDIFF(
            SECOND,
            v_f_inicio_sesion,
            COALESCE(v_f_fin_sesion, DATE_ADD(v_f_inicio_sesion, INTERVAL 20 MINUTE))
        );

        SET v_duracion_min = v_segundos_sesion / 60;

        SET v_tipo_usuario = FLOOR(1 + RAND()*4);

        IF p_total_productos IS NULL OR p_total_productos <= 0 THEN

            IF v_tipo_usuario = 1 THEN
                IF v_duracion_min <= 10 THEN
                    SET v_total_productos_actual = 1;
                ELSE
                    SET v_total_productos_actual = genera_numero_aleatorio_rangos(1,2);
                END IF;

            ELSEIF v_tipo_usuario = 2 THEN
                IF v_duracion_min <= 10 THEN
                    SET v_total_productos_actual = genera_numero_aleatorio_rangos(1,2);
                ELSEIF v_duracion_min <= 25 THEN
                    SET v_total_productos_actual = genera_numero_aleatorio_rangos(2,4);
                ELSE
                    SET v_total_productos_actual = genera_numero_aleatorio_rangos(3,5);
                END IF;

            ELSEIF v_tipo_usuario = 3 THEN
                IF v_duracion_min <= 10 THEN
                    SET v_total_productos_actual = genera_numero_aleatorio_rangos(2,3);
                ELSEIF v_duracion_min <= 30 THEN
                    SET v_total_productos_actual = genera_numero_aleatorio_rangos(3,6);
                ELSE
                    SET v_total_productos_actual = genera_numero_aleatorio_rangos(5,8);
                END IF;

            ELSE
                IF v_duracion_min <= 15 THEN
                    SET v_total_productos_actual = genera_numero_aleatorio_rangos(2,4);
                ELSEIF v_duracion_min <= 40 THEN
                    SET v_total_productos_actual = genera_numero_aleatorio_rangos(4,7);
                ELSE
                    SET v_total_productos_actual = genera_numero_aleatorio_rangos(6,10);
                END IF;
            END IF;

        ELSE
            SET v_total_productos_actual = p_total_productos;
        END IF;

        INSERT INTO carritos (
            sesion_id, divisa_id, total_productos, monto_aproximado, fecha_creacion, estatus
        )
        VALUES (
            v_sesion_id, v_divisa_id, 0, 0.00, v_f_inicio_sesion, 'Activo'
        );

        SET v_carrito_id = LAST_INSERT_ID();
        SET v_j = 0;
        SET v_intentos = 0;

        detalle_loop: WHILE v_j < v_total_productos_actual AND v_intentos < v_max_intentos DO
            SET v_intentos = v_intentos + 1;

            SET v_fecha_item = DATE_ADD(
                v_f_inicio_sesion,
                INTERVAL FLOOR(RAND() * v_segundos_sesion) SECOND
            );

            SELECT p.id, p.precio_menudeo
            INTO v_producto_id, v_precio_unitario
            FROM productos p
            LEFT JOIN productos_categorias pc ON p.id = pc.producto_id
            LEFT JOIN categorias c ON pc.categoria_id = c.id
            WHERE p.estatus IN ('Activo','En existencia')
              AND (
                    p_categoria IS NULL 
                    OR p_categoria = '' 
                    OR c.nombre = p_categoria
                  )
              AND NOT EXISTS (
                    SELECT 1 FROM carrito_detalle cd
                    WHERE cd.carrito_id = v_carrito_id
                    AND cd.producto_id = p.id
              )
            ORDER BY RAND()
            LIMIT 1;

            IF v_producto_id IS NULL THEN
                LEAVE detalle_loop;
            END IF;

            IF v_tipo_usuario = 4 AND RAND() < 0.30 THEN
                SET v_estatus_item = 'Eliminado';
            ELSEIF RAND() < 0.10 THEN
                SET v_estatus_item = 'Eliminado';
            ELSE
                SET v_estatus_item = 'Activo';
            END IF;

            INSERT INTO carrito_detalle (
                carrito_id, producto_id, cantidad, precio_unitario,
                fecha_registro, fecha_actualizacion, estatus
            )
            VALUES (
                v_carrito_id,
                v_producto_id,
                elige_cantidad(),
                v_precio_unitario,
                v_fecha_item,
                CASE 
                    WHEN v_estatus_item = 'Eliminado'
                    THEN DATE_ADD(v_fecha_item, INTERVAL FLOOR(RAND()*60) SECOND)
                    ELSE NULL
                END,
                v_estatus_item
            );

            SET v_j = v_j + 1;

        END WHILE;

        IF NOT EXISTS (
            SELECT 1 FROM carrito_detalle
            WHERE carrito_id = v_carrito_id
            AND estatus = 'Activo'
        ) THEN
            UPDATE carrito_detalle
            SET estatus = 'Activo'
            WHERE carrito_id = v_carrito_id
            LIMIT 1;
        END IF;

        UPDATE carritos c
        LEFT JOIN (
            SELECT carrito_id,
                   SUM(cantidad) AS t_p,
                   SUM(cantidad * precio_unitario) AS t_m
            FROM carrito_detalle
            WHERE carrito_id = v_carrito_id
            AND estatus = 'Activo'
            GROUP BY carrito_id
        ) x ON c.id = x.carrito_id
        SET c.total_productos = IFNULL(x.t_p,0),
            c.monto_aproximado = IFNULL(x.t_m,0)
        WHERE c.id = v_carrito_id;

        COMMIT;
        SET v_i = v_i + 1;

    END WHILE;

END
```

**Uso:**
Se utiliza para generar datos simulados de carritos de compra en masa (p_cuantos), permitiendo controlar la cantidad de productos (p_total_productos) o dejar que el sistema los determine dinámicamente según el comportamiento del usuario y la duración de la sesión. Es ideal para pruebas de carga, análisis de comportamiento y simulaciones de e-commerce.

---

#### simula_carritos_v2  

**Descripción:**  
Procedimiento almacenado que genera carritos de compra simulados de forma simplificada. Crea carritos con productos aleatorios, asigna fechas dentro de un rango desde el inicio del año hasta la fecha actual y calcula automáticamente el total de productos y el monto aproximado.

```sql
CREATE DEFINER=`root`@`localhost` PROCEDURE `simula_carritos_v2`(
    IN p_cuantos INT,
    IN p_total_productos INT
)
BEGIN
    DECLARE v_i INT DEFAULT 1;
    DECLARE v_j INT;

    DECLARE v_carrito_id INT;
    DECLARE v_producto_id INT;
    DECLARE v_precio DOUBLE;
    DECLARE v_sesion_id INT;

    DECLARE v_fecha DATETIME;
    DECLARE v_inicio DATETIME;
    DECLARE v_fin DATETIME;

    IF p_cuantos IS NULL OR p_cuantos <= 0 THEN
        SET p_cuantos = 10;
    END IF;

    IF p_total_productos IS NULL OR p_total_productos <= 0 THEN
        SET p_total_productos = 3;
    END IF;

    SET v_inicio = STR_TO_DATE(CONCAT(YEAR(NOW()),'-01-01 00:00:00'), '%Y-%m-%d %H:%i:%s');
    SET v_fin = NOW();

    WHILE v_i <= p_cuantos DO

        SET v_fecha = DATE_ADD(
            v_inicio,
            INTERVAL FLOOR(RAND() * TIMESTAMPDIFF(SECOND, v_inicio, v_fin)) SECOND
        );

        --  sesión aleatoria
        SELECT id 
        INTO v_sesion_id
        FROM sesiones
        ORDER BY RAND()
        LIMIT 1;

        INSERT INTO carritos(
            sesion_id,
            divisa_id,
            total_productos,
            monto_aproximado,
            fecha_creacion,
            estatus
        )
        VALUES (
            v_sesion_id,
            1,
            0,
            0,
            v_fecha,
            'Activo'
        );

        SET v_carrito_id = LAST_INSERT_ID();
        SET v_j = 1;

        productos_loop: WHILE v_j <= p_total_productos DO

            SET v_producto_id = NULL;

            SELECT p.id, p.precio_menudeo
            INTO v_producto_id, v_precio
            FROM productos p
            WHERE NOT EXISTS (
                SELECT 1
                FROM carrito_detalle cd
                WHERE cd.carrito_id = v_carrito_id
                  AND cd.producto_id = p.id
            )
            ORDER BY RAND()
            LIMIT 1;

            IF v_producto_id IS NULL THEN
                LEAVE productos_loop;
            END IF;

            INSERT INTO carrito_detalle(
                carrito_id,
                producto_id,
                cantidad,
                precio_unitario,
                fecha_registro
            )
            VALUES (
                v_carrito_id,
                v_producto_id,
                FLOOR(1+RAND()*3),
                v_precio,
                v_fecha
            );

            SET v_j = v_j + 1;

        END WHILE;

        UPDATE carritos c
        JOIN (
            SELECT carrito_id,
                   SUM(cantidad) AS total,
                   SUM(cantidad * precio_unitario) AS monto
            FROM carrito_detalle
            WHERE carrito_id = v_carrito_id
            GROUP BY carrito_id
        ) x ON c.id = x.carrito_id
        SET c.total_productos = x.total,
            c.monto_aproximado = x.monto;

        SET v_i = v_i + 1;

    END WHILE;

END
```
**Uso:**
Se utiliza para generar rápidamente carritos de compra con productos aleatorios para pruebas o simulaciones. Permite definir cuántos carritos crear (p_cuantos) y cuántos productos incluir en cada uno (p_total_productos), facilitando la generación de datos para testing en sistemas de e-commerce.
---
#### simula_compras  

**Descripción:**  
Procedimiento almacenado que simula el proceso completo de compras a partir de carritos activos. Genera pedidos, asigna métodos de pago (reutilizando o creando nuevos), registra transacciones financieras y actualiza el estado de los carritos.

```sql
CREATE DEFINER=`root`@`localhost` PROCEDURE `simula_compras`(IN p_total INT)
BEGIN
    DECLARE v_done INT DEFAULT 0;
    DECLARE v_carrito_id INT;
    DECLARE v_usuario_id INT;
    DECLARE v_total DECIMAL(10,2);
    DECLARE v_cant_prod INT;
    DECLARE v_pedido_id INT;
    DECLARE v_metodo_pago_id INT;
    DECLARE v_existe_pedido INT;
    DECLARE v_count INT;

    DECLARE v_fecha_carrito DATETIME;
    DECLARE v_fecha_pedido DATETIME;
    DECLARE v_fecha_transaccion DATETIME;

    DECLARE v_origen VARCHAR(50);

    DECLARE cur_carritos CURSOR FOR
        SELECT c.id, s.usuario_id, c.fecha_creacion
        FROM carritos c
        INNER JOIN sesiones s ON c.sesion_id = s.id
        WHERE c.estatus = 'Activo'
        ORDER BY c.id
        LIMIT p_total;

    DECLARE CONTINUE HANDLER FOR NOT FOUND SET v_done = 1;

    OPEN cur_carritos;

    read_loop: LOOP
        FETCH cur_carritos INTO v_carrito_id, v_usuario_id, v_fecha_carrito;

        IF v_done = 1 THEN 
            LEAVE read_loop; 
        END IF;

        -- A. EVITAR DUPLICADOS
        SELECT COUNT(*) INTO v_existe_pedido 
        FROM pedidos 
        WHERE carrito_id = v_carrito_id;

        IF v_existe_pedido > 0 THEN
            UPDATE carritos SET estatus = 'Convertido' WHERE id = v_carrito_id;
            ITERATE read_loop;
        END IF;

        -- B. CALCULAR TOTAL
        SELECT 
            IFNULL(SUM(cantidad * precio_unitario), 0), 
            IFNULL(SUM(cantidad), 0)
        INTO v_total, v_cant_prod
        FROM carrito_detalle
        WHERE carrito_id = v_carrito_id 
          AND estatus = 'Activo';

        IF v_total <= 0 THEN 
            ITERATE read_loop; 
        END IF;

        -- C. FECHAS
        SET v_fecha_pedido = DATE_ADD(v_fecha_carrito, INTERVAL FLOOR(5 + RAND()*20) MINUTE);
        SET v_fecha_transaccion = DATE_ADD(v_fecha_pedido, INTERVAL FLOOR(1 + RAND()*5) MINUTE);

        -- D. CREAR PEDIDO
        INSERT INTO pedidos (
            carrito_id, total_productos, importe_total, fecha_registro, estatus, aprobacion
        )
        VALUES (
            v_carrito_id, v_cant_prod, v_total, v_fecha_pedido, 'Pagado', b'1'
        );

        SET v_pedido_id = LAST_INSERT_ID();

        -- E. MÉTODO DE PAGO (CORREGIDO)
        SET v_metodo_pago_id = NULL;

        -- contar métodos del usuario (NO rompe el cursor)
        SELECT COUNT(*) 
        INTO v_count
        FROM metodos_pago
        WHERE usuario_id = v_usuario_id;

        -- 70% reutiliza si existen
        IF v_count > 0 AND RAND() < 0.7 THEN
            SELECT id 
            INTO v_metodo_pago_id 
            FROM metodos_pago 
            WHERE usuario_id = v_usuario_id 
            ORDER BY RAND()
            LIMIT 1;
        END IF;

        -- si no hay o toca crear nuevo
        IF v_metodo_pago_id IS NULL THEN
            INSERT INTO metodos_pago (
                usuario_id,
                numero_tarjeta,
                tipo_red_bancaria,
                tipo_cuenta,
                titular,
                fecha_expiracion,
                fecha_registro,
                estatus
            )
            VALUES (
                v_usuario_id,
                LPAD(FLOOR(RAND() * 9999999999999999), 16, '0'),
                ELT(FLOOR(1 + RAND()*3), 'Visa', 'Mastercard', 'American Express'),
                ELT(FLOOR(1 + RAND()*2), 'Débito', 'Crédito'),
                CONCAT('Usuario_', v_usuario_id),
                '12/30',
                NOW(),
                'Vigente'
            );

            SET v_metodo_pago_id = LAST_INSERT_ID();
        END IF;

        -- F. ORIGEN DE PAGO
        SET v_origen = ELT(FLOOR(1 + RAND()*7),
            'Tarjeta de Débito',
            'Tarjeta de Crédito',
            'Transferencia Bancaria',
            'Socio Comercial',
            'Tarjeta de Regalo',
            'Créditos Devolución',
            'Vales Despensa'
        );

        -- G. TRANSACCIÓN
        INSERT INTO transacciones_financieras (
            tipo, origen, numero_convenio, monto, metodo_pago_id, estatus, fecha_registro
        )
        VALUES (
            'Compra',
            v_origen,
            CONCAT('PED-', v_pedido_id),
            v_total,
            v_metodo_pago_id,
            'Aprobado',
            v_fecha_transaccion
        );

        -- H. CERRAR CARRITO
        UPDATE carritos 
        SET estatus = 'Convertido' 
        WHERE id = v_carrito_id;

    END LOOP;

    CLOSE cur_carritos;

END
```
**Uso:**
Se utiliza para simular compras completas en un sistema de e-commerce, tomando carritos activos (p_total), generando pedidos, asignando métodos de pago y registrando transacciones.
---

#### simula_pedidos  

**Descripción:**  
Procedimiento almacenado que simula la generación de pedidos a partir de carritos activos. Selecciona carritos aleatorios, calcula el total de productos y el importe, y crea pedidos en estado pendiente, actualizando posteriormente el estado del carrito.

```sql
CREATE DEFINER=`root`@`localhost` PROCEDURE `simula_pedidos`(IN v_cuantos INT)
BEGIN
    DECLARE i INT DEFAULT 1;
    DECLARE v_carrito_id INT;
    DECLARE v_total DECIMAL(10,2);
    DECLARE v_total_productos INT;

    WHILE i <= v_cuantos DO

        START TRANSACTION;

        /* TOMAR CARRITO ALEATORIO */
        SELECT id INTO v_carrito_id
        FROM carritos
        WHERE estatus = 'Activo'
        ORDER BY RAND()
        LIMIT 1;

        /* CALCULAR TOTAL */
        SELECT 
            COUNT(*),
            IFNULL(SUM(cantidad * precio_unitario),0)
        INTO v_total_productos, v_total
        FROM carrito_detalle
        WHERE carrito_id = v_carrito_id;

        IF v_total_productos > 0 THEN

            INSERT INTO pedidos (
                carrito_id,
                total_productos,
                importe_total,
                fecha_registro,
                estatus,
                aprobacion
            )
            VALUES (
                v_carrito_id,
                v_total_productos,
                v_total,
                NOW(),
                'Pendiente',   --  AÚN NO PAGADO
                b'0'
            );

            UPDATE carritos
            SET estatus = 'Convertido'
            WHERE id = v_carrito_id;

            COMMIT;

        ELSE
            ROLLBACK;
        END IF;

        SET i = i + 1;

    END WHILE;

END
```
**Uso:**
Se utiliza para generar pedidos en estado "Pendiente" a partir de carritos activos, útil en pruebas donde se requiere simular órdenes sin procesar pagos. Permite crear múltiples pedidos (v_cuantos) de forma automatizada para testing o análisis.
---
#### simula_sesiones  

**Descripción:**  
Procedimiento almacenado que simula la creación de sesiones de usuarios con datos realistas. Genera información como dispositivo, plataforma, sistema operativo, país y fechas (registro, inicio y fin), distribuidas aleatoriamente dentro de un rango de tiempo.

```sql
CREATE DEFINER=`juan.catarino`@`%` PROCEDURE `simula_sesiones`(v_cuantos INT)
BEGIN
	DECLARE i INT DEFAULT 1;
    DECLARE v_dispositivo VARCHAR(50);
    DECLARE v_fecha_apertura DATETIME DEFAULT '2020-01-01 00:00:00';
    DECLARE v_fecha_hoy DATETIME DEFAULT NOW();
    DECLARE v_fecha_registro DATETIME;
    DECLARE v_fecha_inicio DATETIME;
    DECLARE v_fecha_fin DATETIME;
    DECLARE v_segundos_total INT;
    DECLARE v_duracion_segundos INT;

	WHILE i <= v_cuantos DO

        
        SET v_dispositivo = elige_dispositivo();

       
        SET v_segundos_total = TIMESTAMPDIFF(SECOND, v_fecha_apertura, v_fecha_hoy);

        SET v_fecha_registro = DATE_ADD(
            v_fecha_apertura,
            INTERVAL FLOOR(RAND() * v_segundos_total) SECOND
        );

        
        SET v_fecha_inicio = DATE_ADD(
            v_fecha_registro,
            INTERVAL FLOOR(5 + (RAND() * 115)) SECOND
        );

        
        SET v_duracion_segundos = 
            CASE 
                WHEN RAND() < 0.5 THEN FLOOR(180 + (RAND() * 120))   -- 3 a 5 min
                WHEN RAND() < 0.8 THEN FLOOR(300 + (RAND() * 180))   -- 5 a 8 min
                ELSE FLOOR(480 + (RAND() * 240))                     -- 8 a 12 min
            END;

       
        SET v_fecha_fin = DATE_ADD(
            v_fecha_inicio,
            INTERVAL v_duracion_segundos SECOND
        );

        INSERT INTO sesiones VALUES (
            DEFAULT,
            elige_usuario(),
            elige_plataforma(),
            v_dispositivo,
            elige_sistema_operativo(v_dispositivo),
            elige_pais(),
            v_fecha_registro,
            v_fecha_inicio,
            v_fecha_fin,
            'Activa'
        );

		SET i = i + 1;

	END WHILE;
END
```
**Uso:**
Se utiliza para generar sesiones de usuario simuladas (v_cuantos) con datos variados y realistas, incluyendo dispositivos, plataformas y duración de sesión. Es útil para pruebas, análisis de comportamiento de usuarios y simulaciones en sistemas web o aplicaciones.



