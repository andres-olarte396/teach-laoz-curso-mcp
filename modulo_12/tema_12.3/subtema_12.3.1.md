# Subtema 12.3.1: Rúbrica de Evaluación

¿Cómo saber si tu proyecto está listo?

## Checklist de Entrega

### 1. Protocolo MCP (30%)

- [ ] Los 3 servidores implementan `list_tools`, `call_tool`.
- [ ] Al menos un servidor implementa `resources` (logs o docs).
- [ ] Al menos un servidor usa `prompts`.
- [ ] Los errores se reportan correctamente (no crashes silenciosos).

### 2. Calidad de Código (25%)

- [ ] Estructura limpia de carpetas.
- [ ] Uso correcto de tipos (TypeScript interfaces / Python Pydantic models).
- [ ] Manejo de errores (try/catch, validación de inputs).
- [ ] Código comentado donde es complejo.

### 3. Arquitectura y Docker (20%)

- [ ] `docker-compose up` funciona a la primera sin intervención manual.
- [ ] Los servidores son independientes (no comparten código spaghetti).
- [ ] Las variables de entorno (API Keys) estàn en `.env`, no en el código.

### 4. Cliente / Host (15%)

- [ ] El cliente se conecta exitosamente a los servidores.
- [ ] Mantiene el historial de conversación.
- [ ] Muestra el feedback de las herramientas al usuario.

### 5. Documentación (10%)

- [ ] `README.md` claro con instrucciones de :
  - Prerrequisitos.
  - Instalación.
  - Ejemplos de uso.

## Entregables

Un repositorio GitHub conteniendo:

- `/servers` (código de los 3 servidores)
- `/client` (código del dashboard)
- `docker-compose.yml`
- `README.md`
- Link a video de demostración (Loom/YouTube).
