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
