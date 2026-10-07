# Modelo Entidad-Relación — Tajinaste S.A.

## 1. Descripción de las entidades

### Vivero

Representa cada uno de los viveros pertenecientes a la empresa Tajinaste S.A. En cada vivero existen diferentes zonas donde se almacenan o gestionan los productos y donde pueden trabajar los empleados.

**Atributos:**

- `id_vivero`: identificador único del vivero.
- `latitud`: coordenada geográfica de latitud del vivero.
- `longitud`: coordenada geográfica de longitud del vivero.

**Ejemplo:**

Un vivero podría tener:

- `id_vivero = 1`
- `latitud = 28.4636`
- `longitud = -16.2518`

---

### Zona

Representa una zona concreta dentro de un vivero. Por ejemplo, una zona puede ser un almacén, una zona exterior o un invernadero.

**Atributos:**

- `id_zona`: identificador único de la zona.
- `latitud`: coordenada geográfica de la zona.
- `longitud`: coordenada geográfica de la zona.

**Ejemplo:**

Una zona podría tener:

- `id_zona = 10`
- `latitud = 28.4638`
- `longitud = -16.2521`

---

### Producto

Representa los productos que vende Tajinaste S.A., como plantas, productos de jardinería o elementos de decoración.

**Atributos:**

- `id_producto`: identificador único del producto.
- `nombre`: nombre del producto.
- `precio`: precio de venta del producto.

**Ejemplo:**

Un producto podría ser:

- `id_producto = 25`
- `nombre = "Rosal rojo"`
- `precio = 15.50`

El dominio de `nombre` es texto y el de `precio` es un valor numérico positivo.

---

### Empleado

Representa a los trabajadores de Tajinaste S.A.

**Atributos:**

- `id_empleado`: identificador único del empleado.
- `nombre`: nombre del empleado.
- `apellido`: apellido del empleado.
- `id_puesto`: identificador del puesto asociado al empleado.
- `id_vivero`: identificador del vivero al que está asignado.

**Ejemplo:**

Un empleado podría ser:

- `id_empleado = 100`
- `nombre = "Carlos"`
- `apellido = "Gómez"`
- `id_puesto = 3`
- `id_vivero = 2`

Los atributos `nombre` y `apellido` son valores de texto, mientras que los identificadores son valores numéricos que permiten identificar cada elemento.

---

### Puesto

Representa el puesto o función que puede desempeñar un empleado dentro de la empresa.

**Atributos:**

- `id_puesto`: identificador único del puesto.
- `nombre`: nombre del puesto.

**Ejemplo:**

Un puesto podría ser:

- `id_puesto = 3`
- `nombre = "Vendedor"`

Otros ejemplos podrían ser "Jardinero", "Encargado" o "Responsable de almacén".

---

### Pedido

Representa un pedido realizado por un cliente a Tajinaste S.A.

**Atributos:**

- `id_pedido`: identificador único del pedido.
- `id_cliente`: identificador del cliente que realiza el pedido.
- `id_empleado`: identificador del empleado responsable de gestionar el pedido.

**Ejemplo:**

Un pedido podría tener:

- `id_pedido = 500`
- `id_cliente = 25`
- `id_empleado = 100`

---

### Cliente

Representa a los clientes que realizan compras en Tajinaste S.A.

**Atributos:**

- `id_cliente`: identificador único del cliente.
- `nombre`: nombre del cliente.
- `apellido`: apellido del cliente.

**Ejemplo:**

Un cliente podría ser:

- `id_cliente = 25`
- `nombre = "María"`
- `apellido = "Pérez"`

---

### Bonificación

Representa las bonificaciones que puede obtener un cliente en función de sus compras.

**Atributos:**

- `id_bono`: identificador único de la bonificación.
- `descuento`: porcentaje o valor de descuento asociado a la bonificación.

**Ejemplo:**

Una bonificación podría ser:

- `id_bono = 4`
- `descuento = 10%`

Esto podría representar una bonificación del 10 % para un cliente.

---

# 2. Descripción de las relaciones

## Hay en

Relaciona las entidades `Vivero` y `Zona`.

Representa que una zona se encuentra dentro de un vivero.

La cardinalidad indicada en el modelo es:

- Un vivero puede tener de `0` a `N` zonas.
- Una zona puede estar asociada de `0` a `N` viveros.

Por tanto, según el modelo representado, la relación es **N:N**.

**Ejemplo:**

Un vivero puede contener las zonas:

- Zona exterior
- Almacén
- Invernadero

Y una zona puede aparecer asociada a diferentes viveros según el modelo.

---

## Es asignado — Vivero / Empleado

Relaciona las entidades `Vivero` y `Empleado`.

Representa la asignación de un empleado a un vivero.

La cardinalidad indicada es:

- Un vivero puede tener de `0` a `N` empleados asignados.
- Un empleado puede estar asignado a `0` o `1` vivero.

Por tanto, la relación es **1:N**.

**Ejemplo:**

El vivero 1 puede tener varios empleados:

- Empleado 1
- Empleado 2
- Empleado 3

Mientras que el empleado 1 puede estar asignado como máximo a un vivero en el modelo.

---

## Hace tarea

Relaciona las entidades `Empleado` y `Zona`.

Representa que un empleado puede desempeñar tareas en una determinada zona.

La cardinalidad indicada es:

- Un empleado puede hacer tareas en `0` a `N` zonas.
- Una zona puede tener `0` a `N` empleados realizando tareas.

Por tanto, la relación es **N:N**.

**Ejemplo:**

Un empleado puede trabajar en:

- Zona exterior
- Almacén

Y una zona puede tener varios empleados trabajando en ella.

---

## Es asignado — Zona / Producto

Relaciona las entidades `Zona` y `Producto`.

Representa que los productos son asignados a determinadas zonas del vivero.

La cardinalidad indicada es:

- Una zona puede tener de `0` a `N` productos asignados.
- Un producto puede estar asignado a `0` a `N` zonas.

Por tanto, la relación es **N:N**.

**Ejemplo:**

La zona "Almacén" puede contener:

- Macetas
- Fertilizante
- Herramientas

Mientras que un mismo producto puede encontrarse en diferentes zonas.

---

## Tiene

Relaciona las entidades `Producto` y `Pedido`.

Representa los productos que forman parte de los pedidos realizados por los clientes.

La cardinalidad indicada es:

- Un producto puede aparecer en `0` a `N` pedidos.
- Un pedido puede contener `0` a `N` productos.

Por tanto, la relación es **N:N**.

**Ejemplo:**

El producto "Rosal rojo" puede aparecer en muchos pedidos diferentes.

Un pedido puede contener:

- 2 Rosales rojos
- 1 Maceta
- 3 Sacos de tierra

---

## Se encarga de

Relaciona las entidades `Empleado` y `Pedido`.

Representa al empleado responsable de gestionar un pedido.

La cardinalidad indicada es:

- Un empleado puede encargarse de `0` a `N` pedidos.
- Un pedido puede tener `0` o `1` empleado responsable.

Por tanto, es una relación **1:N**, ya que un empleado puede gestionar muchos pedidos, mientras que un pedido puede tener como máximo un empleado responsable.

**Ejemplo:**

El empleado 100 puede gestionar:

- Pedido 500
- Pedido 501
- Pedido 502

Pero cada uno de estos pedidos tiene como máximo un empleado responsable.

---

## Hace

Relaciona las entidades `Cliente` y `Pedido`.

Representa que un cliente realiza pedidos en Tajinaste S.A.

La cardinalidad indicada en el modelo es:

- Un cliente puede realizar de `0` a `N` pedidos.
- Un pedido aparece asociado de `1` a `N` clientes según la cardinalidad representada.

Por tanto, según el diagrama, la relación es **N:N**.

**Ejemplo:**

Un cliente puede realizar varios pedidos a lo largo del tiempo.

---

## Desempeña

Relaciona las entidades `Empleado` y `Puesto`.

Representa el puesto que desempeña un empleado.

La cardinalidad indicada es:

- Un empleado puede desempeñar de `0` a `N` puestos.
- Un puesto puede ser desempeñado por `0` a `N` empleados.

Por tanto, la relación es **N:N**.

**Ejemplo:**

Un empleado puede desempeñar diferentes puestos y un mismo puesto puede ser desempeñado por diferentes empleados.

---

## Obtiene

Relaciona las entidades `Cliente` y `Bonificación`.

Representa las bonificaciones que obtiene un cliente en función de sus compras.

La cardinalidad indicada es:

- Un cliente puede obtener de `0` a `N` bonificaciones.
- Una bonificación puede ser obtenida por `0` a `N` clientes.

Por tanto, la relación es **N:N**.

**Ejemplo:**

Un cliente puede obtener diferentes bonificaciones:

- 5 % de descuento
- 10 % de descuento
- 15 % de descuento

Y una misma bonificación del 10 % puede ser obtenida por diferentes clientes.

---

# 3. Resumen de cardinalidades

| Relación | Entidad 1 | Cardinalidad | Entidad 2 | Cardinalidad |
|---|---|---:|---|---:|
| Hay en | Vivero | 0..N | Zona | 0..N |
| Es asignado | Vivero | 0..N | Empleado | 0..1 |
| Hace tarea | Empleado | 0..N | Zona | 0..N |
| Es asignado | Zona | 0..N | Producto | 0..N |
| Tiene | Producto | 0..N | Pedido | 0..N |
| Se encarga de | Empleado | 0..N | Pedido | 0..1 |
| Hace | Cliente | 0..N | Pedido | 1..N |
| Desempeña | Empleado | 0..N | Puesto | 0..N |
| Obtiene | Cliente | 0..N | Bonificación | 0..N |

# 4. Resumen del modelo

El modelo permite representar la organización de los viveros de Tajinaste S.A., sus zonas, los productos disponibles, los empleados y los puestos que desempeñan. También permite representar los pedidos realizados por los clientes, los empleados responsables de dichos pedidos y las bonificaciones obtenidas por los clientes.

Las relaciones N:N permiten representar situaciones en las que un elemento puede estar relacionado con múltiples elementos del otro conjunto, como ocurre con los productos y los pedidos, los empleados y las zonas o los clientes y las bonificaciones.
