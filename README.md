🥦 Urban.Grocers – Backend
📘 Descripción general

El backend de Urban.Grocers gestiona el registro de usuarios, creación de pedidos, cálculo de costos de entrega, manejo de kits personalizados y conexión con los servicios de entrega y almacenes.
Este sistema garantiza un flujo de compra eficiente, flexible y automatizado.

⚙️ Funcionalidades principales
🧍 Registro y autorización de usuarios

Los usuarios pueden registrarse o comprar como invitados.

Campos requeridos: nombre, teléfono y dirección.

Campos opcionales: correo electrónico y comentarios.

Los datos pueden actualizarse y se permite realizar múltiples pedidos.

🛒 Carrito de compras

Muestra nombre, cantidad y precio total de cada artículo.

Permite agregar, eliminar o vaciar el carrito.

Incluye el costo de entrega si aplica.

El usuario debe indicar la hora de entrega (por defecto: hora actual del servidor).

El sistema valida la disponibilidad de los servicios de entrega.

🧩 Kits

Tres tipos de kits:

Para una situación (ej. “Para películas y series”, “Para pícnic”).

Prepara una receta (ej. pizza, pasta).

Crea tu propio kit (selección personalizada).

Cada artículo muestra su nombre, peso y precio.

Al seleccionarlo, aparece el botón “Carrito” con el total y el tiempo estimado de entrega.

Los kits personalizados pueden editarse, renombrarse o eliminarse.

En caso de error, se muestran mensajes de validación.

🚚 Servicios de entrega
Automático (POST /api/v1/orders)

Selecciona el servicio más económico disponible.
El envío cuesta $5 USD si:

Hay exceso de peso o cantidad.

El pedido total es menor a $7 USD.
De lo contrario, el envío es gratis.

Manual

El usuario puede consultar la disponibilidad y tarifas de cada servicio mediante su URL.
El costo depende de:

productsCount (número de artículos).

productsWeight (peso total en kg).

El monto total del pedido no afecta el costo en este método.

🏭 Almacenes

El sistema selecciona automáticamente el almacén que:

Tiene stock suficiente.

Está abierto al momento del pedido.

Resulta más económico.

No se permiten pedidos con productos parcialmente disponibles.

🔗 Endpoints principales
👤 Usuarios

POST /api/v1/users – Crear un usuario.

🧩 Kits

POST /api/v1/kits – Crear un kit.

GET /api/v1/kits – Obtener lista de kits.

PUT /api/v1/kits – Actualizar o renombrar un kit.

DELETE /api/v1/kits – Eliminar un kit.

GET /api/v1/kits/search – Buscar artículos en un kit.

🏭 Almacenes

GET /api/v1/warehouses – Obtener lista de almacenes.

POST /api/v1/warehouses/amount – Consultar cantidad disponible.

🚚 Servicios de entrega

GET /api/v1/couriers – Lista de servicios disponibles.

POST /api/v1/couriers/check – Verificar disponibilidad.

POST /speedy/v1/calculate – Calcular costo con Speedy.

POST /order-and-go/v1/delivery – Calcular costo con Order and Go.

POST /fast-delivery/v3.1.1/calculate-delivery.xml – Calcular costo con Fast Delivery.

POST /food-service/wsdl – Calcular costo con Food Service.

🛍️ Pedidos y carrito

POST /api/v1/orders – Crear o calcular pedido (con entrega).

GET /api/v1/orders/:id – Obtener artículos del carrito.

PUT /api/v1/orders/:id – Agregar artículos.

DELETE /api/v1/orders/:id – Eliminar carrito.

🧮 Ejemplo de cálculo (servicio Speedy)
Condición	hostDeliveryCost	clientDeliveryCost
≤10 artículos y ≤3 kg	4 USD	0 USD
>10 artículos o >3 kg	7 USD	9 USD

💡 En este método, el monto total del pedido no influye en el costo.

🧠 Lógica de negocio destacada

Validación de horarios de entrega.

Cálculo automático de tarifas y almacenes óptimos.

Restricciones de peso y cantidad por servicio.

Manejo de errores y mensajes de validación.

💻 Tecnologías sugeridas

Python / Node.js (según implementación).

REST API.

Base de datos relacional (PostgreSQL o MySQL).

Autenticación JWT.
