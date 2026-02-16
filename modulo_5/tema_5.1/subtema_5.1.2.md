# Subtema 5.1.2: Parámetros de Sampling: Messages, Model Preferences y System Prompt

La petición de Sampling es muy rica y permite configurar cómo debe comportarse el modelo.

## Estructura de `sampling/createMessage`

```json
{
  "method": "sampling/createMessage",
  "params": {
    "messages": [
      {
        "role": "user",
        "content": { "type": "text", "text": "Arregla este código..." }
      }
    ],
    "systemPrompt": "Eres un experto en Python seguidor de PEP8.",
    "includeContext": "none", // o "thisServer", "allServers"
    "maxTokens": 1000,
    "modelPreferences": {
      "hints": [{ "name": "claude-3-5-sonnet" }, { "name": "gpt-4o" }],
      "costPriority": 0.3, // 0-1 (Bajo costo es prioridad)
      "speedPriority": 0.8, // 0-1 (Velocidad es prioridad)
      "intelligencePriority": 0.9 // 0-1 (Inteligencia es prioridad)
    }
  }
}
```

### Model Preferences

El servidor no puede _exigir_ un modelo específico (porque el usuario podría no tener acceso), pero puede dar **pistas** (`hints`) y **prioridades**.

- Si `intelligencePriority` es alto, el Host intentará usar su modelo más capaz (ej: Opus/GPT-4).
- Si `speedPriority` es alto, podría usar Haiku/GPT-3.5.

### Contexto (`includeContext`)

El servidor puede pedir al Host que incluya contexto de _otros_ servidores en el prompt.

- `none`: Solo los mensajes enviados explícitamente.
- `thisServer`: Incluye recursos/prompts de este mismo servidor.
- `allServers`: (Peligroso/Pesado) Incluye contexto de todos los servidores conectados. Usualmente requiere aprobación explícita.
