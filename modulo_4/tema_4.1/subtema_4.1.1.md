# Subtema 4.1.1: El Modelo de Recursos: URIs, Tipos MIME y Contenido

## ¿Qué es un Resource?

Si las **Tools** son los "verbos" de MCP (hacer cosas), los **Resources** son los "sustantivos" (leer cosas).

Un Resource es cualquier dato que el servidor quiera exponer al Host para que el LLM lo lea como contexto.

Ejemplos:

- Archivos del sistema.
- Logs de una aplicación.
- Filas de una base de datos.
- La captura de pantalla actual.

## Identificación por URI

Cada recurso debe tener una **URI (Uniform Resource Identifier)** única.

`schema://path/to/resource`

- No tiene por qué ser una URL `http://` o `file://` real.
- Puede ser un esquema personalizado: `postgres://users/1`, `app-logs://latest`.

## Contenido y Tipos MIME

Al leer un recurso, el servidor devuelve dos cosas clave aparte del contenido:

1.  **URI:** Para confirmar qué se leyó.
2.  **MIME Type:** Para que el Host sepa cómo interpretarlo.

### Tipos de Contenido

MCP soporta dos formas de enviar el cuerpo del recurso:

1.  **Text (`text`):** Para código, logs, JSON, XML.

    ```json
    {
      "uri": "file:///var/log/syslog",
      "mimeType": "text/plain",
      "text": "Feb 15 10:00:00 server systemd[1]: Started..."
    }
    ```

2.  **Binary (`blob`):** Para imágenes, PDFs, zips. Se envía codificado en **Base64**.
    ```json
    {
      "uri": "file:///home/user/photo.jpg",
      "mimeType": "image/jpeg",
      "blob": "base64_encoded_string_here..."
    }
    ```
