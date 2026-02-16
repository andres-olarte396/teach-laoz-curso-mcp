# Subtema 4.1.3: Resource Templates: URIs Dinámicos con Parámetros

Imagina que tienes una base de datos con 1 millón de usuarios. No puedes enviar 1 millón de elementos en `resources/list`.

Para esto existen los **Resource Templates**. Le dicen al LLM: "No te voy a dar la lista completa, pero si conoces el ID, puedes construir la URI tú mismo".

## Definición del Template

Los templates usan la sintaxis **RFC 6570** (URI Template).

```json
{
  "uriTemplate": "db://users/{user_id}/profile",
  "name": "Perfil de Usuario",
  "description": "Obtiene el perfil completo de un usuario dado su ID",
  "mimeType": "application/json"
}
```

## Uso por el LLM

El LLM ve esta plantilla y entiende que si necesita el perfil del usuario 55, debe pedir leer:
`db://users/55/profile`

El servidor recibe `resources/read` con esa URI exacta, parsea el `55`, hace la consulta y devuelve los datos.

Esto hace a los recursos infinitamente escalables.
