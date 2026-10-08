# Modelo Entidad-Relación — Tajinaste S.A.

## 1. Descripción de las entidades

### Vivero

Representa cada uno de los viveros pertenecientes a la empresa Tajinaste S.A. En cada vivero existen diferentes zonas donde se almacenan o gestionan los productos y donde pueden trabajar los empleados.

**Atributos:**

- `id_vivero`: identificador único del vivero (Clave Primaria).
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

- `id_zona`: identificador único de la zona (Clave Primaria).
- `georreferenciación`: atributo compuesto que agrupa las coordenadas geográficas de la zona. Se divide en:
  - `latitud`: coordenada de latitud.
  - `longitud`: coordenada de longitud.

**Ejemplo:**

Una zona podría tener:

- `id_zona = 10`
- `georreferenciación = (28.4638, -16.2521)`

---

### Producto

Representa los productos que vende Tajinaste S.A., como plantas, productos de jardinería o elementos de decoración.

**Atributos:**

- `id_producto`: identificador único del producto (Clave Primaria).
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

- `id_empleado`: identificador único del empleado (Clave Primaria).
- `nombre`: nombre del empleado.
- `apellido`: apellido del empleado.

*(Nota: Las asignaciones a viveros o puestos se gestionan mediante las relaciones correspondientes).*

**Ejemplo:**

Un empleado podría ser:

- `id_empleado = 100`
- `nombre = "Carlos"`
- `apellido = "Gómez"`

---

### Puesto

Representa el puesto o función que puede desempeñar un empleado dentro de la empresa.

**Atributos:**

- `id_puesto`: identificador único del puesto (Clave Primaria).
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

- `id_pedido`: identificador único del pedido (Clave Primaria).
- `fecha_pedido`: fecha en la que se realizó el pedido (necesario para el cálculo mensual de bonificaciones).
- `importe_total`: atributo derivado (representado con línea discontinua) que representa el coste total del pedido calculado a partir de los productos y sus cantidades.

**Ejemplo:**

Un pedido podría tener:

- `id_pedido = 500`
- `fecha_pedido = 2026-10-08`

---

### Cliente

Representa a los clientes que realizan compras en Tajinaste S.A.

**Atributos:**

- `id_cliente`: identificador único del cliente (Clave Primaria).
- `nombre`: nombre del cliente.
- `apellido`: apellido del cliente.
- `es_tajinaste_plus`: valor booleano que indica si el cliente pertenece al programa de fidelización.
- `fecha_ingreso`: fecha en la que el cliente se unió al programa.

**Ejemplo:**

Un cliente podría ser:

- `id_cliente = 25`
- `nombre = "María"`
- `apellido = "Pérez"`
- `es_tajinaste_plus = true`
- `fecha_ingreso = 2025-05-12`

---

### Bonificación

Representa las bonificaciones que puede obtener un cliente en función de sus compras.

**Atributos:**

- `id_bono`: identificador único de la bonificación (Clave Primaria).
- `descuento`: porcentaje o valor de descuento asociado a la bonificación.
- `fecha_asignación`: mes o fecha en la que se otorga la bonificación según el volumen de compras.

**Ejemplo:**

Una bonificación podría ser:

- `id_bono = 4`
- `descuento = 10%`
- `fecha_asignación = Octubre 2026`

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

---

## Es asignado — Vivero / Empleado

Relaciona las entidades `Vivero` y `Empleado`.

Representa la asignación de un empleado a un vivero.

La cardinalidad indicada es:

- Un vivero puede tener de `0` a `N` empleados asignados.
- Un empleado puede estar asignado a `0` o `1` vivero en un momento dado.

Por tanto, la relación es **1:N**.

**Ejemplo:**

El vivero 1 puede tener varios empleados asignados, mientras que el empleado 1 puede estar asignado como máximo a un vivero.

---

## Hace tarea en

Relaciona las entidades `Empleado` y `Zona`.

Representa que un empleado puede desempeñar tareas en una determinada zona.

La cardinalidad indicada es:

- Un empleado puede hacer tareas en `0` a `N` zonas.
- Una zona puede tener `0` a `N` empleados realizando tareas.

Por tanto, la relación es **N:N**.

**Ejemplo:**

Un empleado puede trabajar en la zona exterior y en el almacén, y el almacén puede tener varios empleados trabajando en él.

---

## Es asignado — Zona / Producto

Relaciona las entidades `Zona` y `Producto`.

Representa que los productos son asignados a determinadas zonas del vivero.

**Atributos de relación:**
- `cantidad`: Indica el stock o número de unidades disponibles de un producto específico en una zona concreta.

La cardinalidad indicada es:

- Una zona puede tener de `0` a `N` productos asignados.
- Un producto puede estar asignado a `0` a `N` zonas.

Por tanto, la relación es **N:N**.

**Ejemplo:**

La zona "Almacén" puede contener macetas y herramientas, registrando la cantidad exacta de cada una mediante el atributo de la relación.

---

## Tiene

Relaciona las entidades `Producto` y `Pedido`.

Representa los productos que forman parte de los pedidos realizados por los clientes.

**Atributos de relación:**
- `cantidad`: Indica cuántas unidades de un producto específico se han incluido en el pedido.

La cardinalidad indicada es:

- Un producto puede aparecer en `0` a `N` pedidos.
- Un pedido puede contener `0` a `N` productos.

Por tanto, la relación es **N:N**.

**Ejemplo:**

El producto "Rosal rojo" puede aparecer en muchos pedidos diferentes, y la relación guarda la cantidad de rosales comprados en cada pedido.

---

## Se encarga de

Relaciona las entidades `Empleado` y `Pedido`.

Representa al empleado responsable de gestionar un pedido.

La cardinalidad indicada es:

- Un empleado puede encargarse de `0` a `N` pedidos.
- Un pedido puede tener `0` o `1` empleado responsable.

Por tanto, es una relación **1:N**, ya que un empleado puede gestionar muchos pedidos, mientras que un pedido puede tener como máximo un empleado responsable.

**Ejemplo:**

El empleado 100 puede gestionar los pedidos 500 y 501, garantizando que cada pedido tenga un único responsable.

---

## Hace

Relaciona las entidades `Cliente` y `Pedido`.

Representa que un cliente realiza pedidos en Tajinaste S.A.

La cardinalidad indicada en el modelo es:

- Un cliente puede realizar de `0` a `N` pedidos.
- Un pedido es realizado obligatoriamente por `1` y sólo `1` cliente.

Por tanto, según el diagrama, la relación es **1:N**.

**Ejemplo:**

Un cliente puede realizar varios pedidos a lo largo del tiempo, pero un recibo de compra pertenece a una única persona.

---

## Desempeña

Relaciona las entidades `Empleado` y `Puesto`.

Representa el puesto que desempeña un empleado a lo largo del tiempo.

**Atributos de relación:**
- `fecha_inicio`: Fecha en la que el empleado comenzó en ese puesto.
- `fecha_fin`: Fecha en la que el empleado dejó ese puesto.

La cardinalidad indicada es:

- Un empleado puede desempeñar de `0` a `N` puestos en su histórico.
- Un puesto puede ser desempeñado por `0` a `N` empleados.

Por tanto, la relación es **N:N**.

**Ejemplo:**

Un empleado puede haber sido "Jardinero" de 2024 a 2025, y "Encargado" de 2025 en adelante.

---

## Obtiene

Relaciona las entidades `Cliente` y `Bonificación`.

Representa las bonificaciones que obtiene un cliente en función de sus compras en el programa Tajinaste Plus.

La cardinalidad indicada es:

- Un cliente puede obtener de `0` a `N` bonificaciones.
- Una bonificación puede ser obtenida por `0` a `N` clientes.

Por tanto, la relación es **N:N**.

**Ejemplo:**

Un cliente puede obtener diferentes bonificaciones mensuales, y una misma política de descuento del 10 % puede ser obtenida por diferentes clientes ese mes.

---

# 3. Resumen de cardinalidades

| Relación | Entidad 1 | Cardinalidad | Entidad 2 | Cardinalidad | Relación Global |
|---|---|---:|---|---:|---:|
| Hay en | Vivero | 0..N | Zona | 0..N | **N:N** |
| Es asignado | Vivero | 0..N | Empleado | 0..1 | **1:N** |
| Hace tarea en | Empleado | 0..N | Zona | 0..N | **N:N** |
| Es asignado | Zona | 0..N | Producto | 0..N | **N:N** |
| Tiene | Producto | 0..N | Pedido | 0..N | **N:N** |
| Se encarga de | Empleado | 0..N | Pedido | 0..1 | **1:N** |
| Hace | Cliente | 0..N | Pedido | 1..1 | **1:N** |
| Desempeña | Empleado | 0..N | Puesto | 0..N | **N:N** |
| Obtiene | Cliente | 0..N | Bonificación | 0..N | **N:N** |

# 4. Resumen del modelo

El modelo permite representar íntegramente la organización de la red de viveros de Tajinaste S.A. y cumplir con sus requerimientos de negocio. Se ha estructurado para soportar el control detallado del inventario (registrando el stock por zonas mediante atributos en las relaciones), el seguimiento de la productividad del personal (incluyendo el historial temporal de puestos) y la operativa de ventas. 

Asimismo, integra la lógica necesaria para el programa de fidelización Tajinaste Plus, permitiendo asociar bonificaciones temporales a las compras mensuales calculadas mediante atributos derivados en los pedidos. Las entidades se han normalizado correctamente trasladando las claves foráneas a las relaciones estructurales correspondientes. Las relaciones N:N permiten representar situaciones complejas como el histórico de puestos o el inventario distribuido.
