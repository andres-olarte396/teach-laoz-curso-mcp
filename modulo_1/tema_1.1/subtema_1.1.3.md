# Subtema 1.1.3: Principios de Diseño: Localidad, Seguridad y Composabilidad

MCP no es solo un protocolo técnico; tiene una filosofía sobre cómo debe interactuar la IA con el mundo.

## 1. Localidad del Servidor (Server Locality)

MCP está diseñado para asumir que **el usuario controla sus datos**.

- Por defecto, los servidores MCP corren **localmente** en la máquina del usuario (o en su infraestructura privada).
- El modelo de IA (Host) se conecta a estos servidores locales.
- Esto significa que no tienes que enviar tus credenciales de base de datos a un tercero. Tus claves de API se quedan contigo.

## 2. Consentimiento del Usuario (User Consent)

La seguridad es primordial cuando una IA puede ejecutar código.

- **Human-in-the-loop:** El protocolo está diseñado para que los Hosts (como Claude Desktop) pidan permiso al usuario antes de ejecutar acciones sensibles o enviar datos a un servidor.
- El protocolo incluye mecanismos de `sampling` donde el servidor puede pedir explícitamente la revisión del usuario.

## 3. Composabilidad (Composability)

Un sistema de IA no debería depender de un monolito.

- MCP fomenta la creación de herramientas **pequeñas y especializadas**.
- Un "Sqlite Server" solo sabe hablar SQL. Un "Filesystem Server" solo sabe leer archivos.
- El Host puede conectar **múltiples servidores simultáneamente**.
- El LLM tiene acceso al conjunto unido de todas las herramientas, permitiéndole crear flujos de trabajo complejos (ej: "Lee este archivo, extrae los datos, y guárdalos en la base de datos").

## 4. Agnosticismo de Modelo

MCP no está atado a Claude. Cualquier modelo de lenguaje (OpenAI, Llama, Mistral) puede ser "enseñado" a hablar MCP, ya que al final se reduce a estructuras JSON estándar.
