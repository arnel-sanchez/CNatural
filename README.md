# CNatural

## Descripción de la Base de Datos
### Entidades
* PRODUCTO que contiene su Nombre(String 50) requerido, el ID requerido, la Cantidad(int) no puede ser menor que cero, Diseño(String 50) puede ser null.
* VENTAS que contiene Cantidad(int) requerido, Fecha(DateTime) requerido, Precio(double) requerido.
* INVERSIÓN que contiene su Cantidad(int) requerido, Precio(double) requerido, Fecha de Encargo(DateTime) requerido, Fecha de Llegada(DateTime) requerido.
* COMPRADOR que contiene su Móvil(Requerido, necesario validar el número de móvil), su Nombre(String 50) puede ser null, Dirección(String 100) requerido.
* CONTABILIDAD que contiene Fecha(DateTime) requerido, Dinero Invertido(double) requerido mayor o igual que cero, Dinero Ganado(double).

### Relaciones
* Un PRODUCTO puede tener o ninguna o muchas VENTAS
* Una VENTA puede ser de 1 PRODUCTO
* Un COMPRADOR puede estar asociado a una o muchas VENTAS
* Una VENTA puede ser de un sólo COMPRADOR
* Un PRODUCTO puede ser parte de una o muchas INVERSIONES
* Una INVERSIÓN puede ser de un PRODUCTO
* Una CONTABILIDAD puede ser de una o muchas INVERSIONES
* Una INVERSIÓN puede ser de una CONTABILIDAD
* Una CONTABILIDAD puede ser de una o muchas VENTAS
* Una VENTA puede ser de una CONTABILIDAD

### Modificaciones en tiempo de ejecución
* Cuando se hace una venta se debe disminuir en la cantidad de la venta la cantidad del producto existente en base de datos, si ese número da negativo lanzar un error.
* Cuando se hace una inversión, el día que llega el producto se debe aumentar la cantidad de ese producto.
* La Contabilidad se debe generar el día 1 de cada mes

### Vistas
* La vista PRODUCTOS, contiene una tabla con los productos, donde cada producto tendrá un botón de edición, debe tener filtro por nombre y por diseño.
* La vista COMPRADOR, contiene una tabla con todos los compradores, debe permitir editar cada comprador, debe tener un filtro por el nombre, por el móvil y por la dirección.
* La vista INVERSIÓN, contiene una tabla con todas las inversiones, debe permitir editar una inversión, y si se edita la cantidad se debe actualizar la cantidad del producto en Stock en caso de que la fecha actual sea mayor a la fecha de llegada y se debe actualizar la contabilidad en caso de tenerla si se edita la cantidad y el precio, debe tener un filtro por fecha de llegada y por fecha de encargo.
* La vista de VENTAS, contiene una tabla con todas las ventas, debe permitir editar una venta, y si edita la cantidad del producto se debe actualizar la cantidad en Stock, debe tener un filtro por fecha y un buscador con autocompletamiento por cliente.
* CONTABILIDAD, debe tener unas gráficas donde se muestre las ventas, las inversiones y los resultados finales del mes, debe tener un selector por fechas.

# Detalles Técnicos
* Sólo se puede acceder al sistema si estás loggeado.
* Sólo un usuario loggeado puede crear un usuario nuevo.
* Para la autenticación utiliza Identity y aplica Scaffolder para que se autogenere.
* Cuando se crea la contabilidad se debe mandar un email utilizando el SMTP de Gmail a los admins reportándole que ya está la contabilidad del mes pasado lista.
* Cuando se reporta un venta o una compra se le debe enviar un email a los demás admins reportando de los cambios.
* Debes utilizar PostgreSQL como motor de base de datos.
* Si te decides a hacerlo como API Rest te recomiendo usar una plantilla React(te la puedo dar) que te será muy cómodo el frontend, pero complejizas un poco la autenticación porque vas a tener que hacerla a mano, si vas a hacer una Aplicación Web se te va a complicar un poco el frontend. Puedes meterle coco a eso como mejor te sea.
