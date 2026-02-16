# Subtema 3.2.2: Structured Output: outputSchema y Resultados Tipados

Por defecto, la salida de una herramienta es texto libre para que el LLM lo lea. Pero a veces queremos que la salida sea procesable por el Host (ej: una herramienta que devuelve coordenadas GPS para pintar un mapa).

## El Concepto

Igual que definimos `inputSchema` para lo que entra, podemos definir `outputSchema` para lo que sale.

## Definición

```json
{
  "name": "get_coordinates",
  "inputSchema": { "city": "string" },
  "outputSchema": {
    "type": "object",
    "properties": {
      "lat": { "type": "number" },
      "lon": { "type": "number" }
    }
  }
}
```

## Respuesta Estructurada

Cuando la herramienta se ejecuta, en lugar de devolver solo texto en `content`, devuelve un objeto JSON en `data`.

```json
{
  "result": {
    "content": [{ "type": "text", "text": "Coordenadas encontradas." }],
    "data": {
      "lat": 40.4168,
      "lon": -3.7038
    }
  }
}
```

Esto permite construir interfaces ricas en el Host (mapas, gráficos) que consumen estos datos directamente.
