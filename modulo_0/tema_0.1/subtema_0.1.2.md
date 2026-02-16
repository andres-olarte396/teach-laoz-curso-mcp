# Subtema 0.1.2: HTTP: Métodos, Headers y Ciclo Request-Response

## Introducción a HTTP

**HTTP (Hypertext Transfer Protocol)** es la base de la comunicación de datos en la World Wide Web. Aunque MCP puede funcionar sobre otros transportes (como `stdio`), el transporte via HTTP (Server-Sent Events) es esencial para conectar con servidores remotos.

## El Ciclo Request-Response

La comunicación HTTP sigue un modelo simple:

1. **Cliente (Client):** Envía una **Petición (Request)**.
2. **Servidor (Server):** Procesa la petición y envía una **Respuesta (Response)**.

## Métodos HTTP (Verbos)

Los métodos indican la acción que se desea realizar sobre un recurso.

- **GET:** Solicitar datos. No debe modificar el estado del servidor. (Ej: Leer una lista de recursos MCP).
- **POST:** Enviar datos para ser procesados. (Ej: Enviar una llamada a una herramienta MCP).
- **PUT:** Actualizar un recurso completo.
- **PATCH:** Actualizar parcialmente un recurso.
- **DELETE:** Eliminar un recurso.

## Headers (Encabezados)

Los headers son metadatos clave-valor que acompañan a la petición o respuesta.

### Headers Comunes

- `Content-Type`: Indica el tipo de medio del recurso (ej: `application/json`).
- `Authorization`: Credenciales para autenticar al cliente.
- `Accept`: Tipos de contenido que el cliente puede procesar.
- `User-Agent`: Identificación del cliente.

## Códigos de Estado (Status Codes)

Indican el resultado de la petición.

- **2xx (Éxito):** `200 OK` (Todo bien), `201 Created` (Recurso creado).
- **3xx (Redirección):** `301 Moved Permanently`.
- **4xx (Error del Cliente):** `400 Bad Request` (Solicitud malformada), `401 Unauthorized` (Falta autenticación), `404 Not Found` (Recurso no encontrado).
- **5xx (Error del Servidor):** `500 Internal Server Error` (Fallo en el servidor).

## Server-Sent Events (SSE)

Para MCP, es vital entender **SSE**. A diferencia del ciclo request-response tradicional donde el servidor cierra la conexión tras responder, en SSE el servidor mantiene la conexión abierta para enviar eventos asíncronos al cliente.

Esto permite que un servidor MCP envíe notificaciones (logs, cambios de estado) al cliente en tiempo real sobre una conexión HTTP estándar.
