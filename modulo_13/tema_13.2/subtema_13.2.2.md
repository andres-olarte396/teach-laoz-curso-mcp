# Subtema 13.2.2: FAQ y Troubleshooting

## Errores Comunes

### 1. "Connection refused" o "Transport closed"

- **Causa:** El servidor crasheó al inicio o no está escuchando en stdio/http.
- **Solución:** Ejecuta el comando del servidor manualmente en tu terminal para ver si imprime errores de Python/Node antes de conectarlo a Claude.

### 2. El LLM alucina herramientas que no existen

- **Causa:** Confusión de contexto o descripciones de herramientas pobres.
- **Solución:** Mejora los docstrings de tus herramientas. Sé explícito sobre qué hace y qué NO hace la herramienta.

### 3. "Tool execution timeout"

- **Causa:** Tu herramienta tardó demasiado (> 60s).
- **Solución:** Optimiza el código o devuelve una respuesta asíncrona "Job started, check status later".

## Preguntas Frecuentes

**P: ¿Puedo usar MCP con GPT-4 en OpenAI?**
R: Sí, si usas una aplicación Host que soporte MCP (como un script custom con el SDK `client`). La app de ChatGPT oficial **no** soporta MCP nativamente aún (a fecha 2024), pero Claude Desktop sí.

**P: ¿Es seguro exponer mi base de datos?**
R: Solo si implementas **autenticación** y **tool confirmation**. Por defecto, MCP confía en el Host. Usa el modo "human-in-the-loop" para operaciones críticas.

**P: ¿Dónde encuentro más servidores?**
R: En el repositorio oficial: [github.com/modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers)
