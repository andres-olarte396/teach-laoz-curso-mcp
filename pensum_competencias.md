# PENSUM DE COMPETENCIAS: Model Context Protocol (MCP) - De Cero a Experto

## PERFIL DE EGRESO

Al finalizar este curso, el estudiante será capaz de:

1. **Diseñar e implementar servidores MCP** completos en TypeScript y Python que expongan herramientas, recursos y prompts siguiendo la especificación oficial, con validación de esquemas y manejo robusto de errores.
2. **Construir clientes y hosts MCP** que descubran servicios, negocien capacidades y orquesten múltiples servidores simultáneamente con enrutamiento inteligente de invocaciones.
3. **Seleccionar y configurar transportes MCP** (stdio, SSE, Streamable HTTP) justificando la elección con criterios de localidad, escalabilidad, latencia y seguridad según el escenario de despliegue.
4. **Implementar seguridad end-to-end** en sistemas MCP incluyendo OAuth 2.1 con PKCE, validación de entradas, rate limiting, y mitigación de amenazas específicas (tool poisoning, prompt injection, DNS rebinding).
5. **Arquitectar ecosistemas multi-servidor** con patrones de gateway, federation y aggregation, integrando MCP con frameworks de agentes de IA y plataformas cloud.
6. **Desplegar y operar servidores MCP en producción** con observabilidad completa (métricas, logs, alertas), containerización, CI/CD y estrategias de versionado para compatibilidad.
7. **Evaluar críticamente** implementaciones MCP existentes, identificando vulnerabilidades, ineficiencias y oportunidades de mejora basándose en la especificación y mejores prácticas de la industria.

## MATRIZ DE COMPETENCIAS POR MODULO

| Módulo | Competencia Específica (Saber Hacer) | Resultado de Aprendizaje (Evidencia) |
| :--- | :--- | :--- |
| **Módulo 0: Diagnóstico y Nivelación** | Configurar un entorno de desarrollo completo para MCP con Node.js, Python, Claude Desktop y MCP Inspector operativos. | Entorno funcional verificado con servidor MCP de ejemplo ejecutándose en Claude Desktop. |
| **Módulo 1: Fundamentos del Protocolo MCP** | Explicar la arquitectura MCP (Host/Client/Server), construir mensajes JSON-RPC válidos y trazar el ciclo de vida completo de una conexión. | Documento técnico con análisis de los 3 roles, 5 mensajes JSON-RPC construidos manualmente y diagrama de secuencia del ciclo de vida. |
| **Módulo 2: Mecanismos de Transporte** | Implementar servidores MCP funcionales en los tres transportes (stdio, SSE, Streamable HTTP) y justificar la selección según contexto. | Tres implementaciones de servidor (una por transporte) con tests de conectividad y documento de análisis comparativo. |
| **Módulo 3: Primitivas Core - Tools** | Diseñar herramientas MCP con validación de esquemas, anotaciones semánticas, structured output y reporte de progreso. | Servidor MCP de gestión de base de datos SQLite con 5+ herramientas CRUD, tests unitarios y documentación de API. |
| **Módulo 4: Primitivas Core - Resources y Prompts** | Exponer recursos por URI con suscripciones, crear prompts parametrizables con datos dinámicos e implementar autocompletado. | Servidor MCP de documentación técnica con 10+ recursos, 3+ prompts dinámicos, suscripciones y autocompletado funcional. |
| **Módulo 5: Primitivas Avanzadas** | Implementar flujos de sampling (server solicita al LLM), elicitation (formularios al usuario) y logging estructurado con progreso. | Mini-proyecto que demuestra un flujo completo: herramienta que usa sampling para enriquecer resultados, elicitation para confirmar acciones, y logging con progreso. |
| **Módulo 6: SDK TypeScript** | Construir servidores y clientes MCP profesionales en TypeScript usando APIs de alto y bajo nivel, con tests unitarios e integración. | Servidor MCP de API Gateway conectando 3+ APIs externas, cliente multi-servidor, y suite de tests con cobertura >80%. |
| **Módulo 7: SDK Python** | Construir servidores FastMCP con decoradores, gestión de lifecycle, composición de servidores y clientes Python completos. | Servidor MCP de Machine Learning con pipeline completo (datos, entrenamiento, predicción, métricas), tests pytest y deployment multi-transporte. |
| **Módulo 8: Integraciones y Hosts** | Configurar MCP en Claude Desktop, IDEs y frameworks de agentes; construir un host MCP personalizado funcional. | Configuración verificada en 3+ hosts, host personalizado con interfaz de chat funcional, e integración con LangChain o OpenAI Agents SDK. |
| **Módulo 9: Seguridad y Autorización** | Implementar OAuth 2.1 completo, identificar y mitigar amenazas MCP, y aplicar auditoría de seguridad de 20 puntos. | Servidor MCP con autenticación OAuth 2.1, reporte de análisis de amenazas con 5+ vectores identificados y mitigados, checklist de auditoría completada. |
| **Módulo 10: Arquitecturas Avanzadas** | Diseñar y construir arquitecturas multi-servidor con patrones de gateway, federation y agentes autónomos sobre MCP. | Sistema multi-servidor con gateway centralizado, agente autónomo funcional con bucle tool-use, y análisis del ecosistema de servidores comunitarios. |
| **Módulo 11: MCP en Producción** | Desplegar servidores MCP containerizados con observabilidad, CI/CD y estrategias de versionado para producción. | Servidor MCP dockerizado con métricas Prometheus, dashboard Grafana, pipeline CI/CD funcional y estrategia de versionado documentada. |
| **Módulo 12: Proyecto Integrador** | Sintetizar todos los conocimientos en un ecosistema MCP completo con múltiples servidores, gateway, host web, testing y documentación. | Ecosistema MCP funcional con 3+ servidores, gateway OAuth, host web, tests (>80% cobertura), Docker Compose, documentación técnica y video demo. |

## COMPETENCIAS TRANSVERSALES

| Competencia Transversal | Módulos Donde se Desarrolla | Indicadores |
| :--- | :--- | :--- |
| **Pensamiento Arquitectónico** | 1, 2, 8, 10, 12 | Justifica decisiones de diseño con trade-offs claros. |
| **Seguridad por Diseño** | 3, 5, 9, 10, 12 | Valida entradas, aplica mínimo privilegio, documenta amenazas. |
| **Testing Riguroso** | 6, 7, 11, 12 | Escribe tests antes o junto con implementación; cobertura >80%. |
| **Comunicación Técnica** | Todos | Documenta código, escribe ADRs, presenta decisiones claramente. |
| **Debugging Sistemático** | 2, 6, 7, 8 | Usa herramientas de debugging (Inspector, logs) metódicamente. |
