# CRONOGRAMA DETALLADO: Model Context Protocol (MCP) - De Cero a Experto

## RESUMEN TEMPORAL

- **Duración Total**: 20 Semanas (5 meses)
- **Carga Semanal**: 7-8 horas (flexible según ruta)
- **Horas Totales**: 142 horas

## CALENDARIO SEMANAL

### MES 1: FUNDAMENTOS Y PROTOCOLO

#### Semana 1: Nivelación y Entorno

- **Módulo 0, Temas 0.1-0.2**: JSON, HTTP, APIs REST, LLMs, problema de integración
- **Actividad Clave**: Consumir una API REST real y analizar las limitaciones de un LLM sin herramientas
- **Horas**: 5h teoría + 2h práctica

#### Semana 2: Entorno + Fundamentos MCP

- **Módulo 0, Tema 0.3 + Módulo 1, Tema 1.1**: Setup del entorno, historia y filosofía de MCP
- **Actividad Clave**: Instalar Claude Desktop, ejecutar primer servidor MCP de ejemplo con MCP Inspector
- **Horas**: 3h práctica + 4h teoría

#### Semana 3: Arquitectura del Protocolo

- **Módulo 1, Temas 1.2-1.3**: Host/Client/Server, JSON-RPC 2.0, métodos del protocolo
- **Actividad Clave**: Construir mensajes JSON-RPC manualmente y simular handshake de inicialización
- **Horas**: 4h teoría + 4h práctica

#### Semana 4: Versiones y Transportes I

- **Módulo 1, Tema 1.4 + Módulo 2, Tema 2.1**: Versiones de especificación, transporte stdio
- **Actividad Clave**: Implementar servidor MCP mínimo sobre stdio desde cero
- **Horas**: 3h teoría + 5h práctica

### MES 2: TRANSPORTES Y PRIMITIVAS CORE

#### Semana 5: Transportes II

- **Módulo 2, Temas 2.2-2.3.2**: SSE, Streamable HTTP, gestión de sesiones
- **Actividad Clave**: Implementar servidor MCP con Streamable HTTP y verificar con MCP Inspector
- **Horas**: 2h teoría + 6h práctica

#### Semana 6: Transportes III + Tools I

- **Módulo 2, Temas 2.3.3-2.4 + Módulo 3, Tema 3.1**: Resumability, selección de transporte, anatomía de herramientas
- **Actividad Clave**: Crear primera herramienta MCP con inputSchema y probar invocación completa
- **Horas**: 3h teoría + 5h práctica

#### Semana 7: Tools Avanzadas

- **Módulo 3, Temas 3.2-3.3.3**: Anotaciones, structured output, herramientas dinámicas, progreso
- **Actividad Clave**: Implementar herramienta con anotaciones, outputSchema y reporte de progreso
- **Horas**: 2h teoría + 6h práctica

#### Semana 8: Proyecto Tools + Resources I

- **Módulo 3, Tema 3.3.4 + Módulo 4, Tema 4.1**: Proyecto DB Server + modelo de recursos
- **Actividad Clave**: Entregar servidor MCP de gestión de base de datos SQLite funcional
- **Entregable**: Proyecto Práctico Módulo 3
- **Horas**: 2h teoría + 6h práctica

### MES 3: RESOURCES, PROMPTS Y SDKs

#### Semana 9: Resources + Prompts

- **Módulo 4, Temas 4.1.3-4.2**: Resource templates, suscripciones, definición y resolución de prompts
- **Actividad Clave**: Implementar servidor con recursos suscribibles y prompts dinámicos
- **Horas**: 2h teoría + 6h práctica

#### Semana 10: Completions + Primitivas Avanzadas

- **Módulo 4, Tema 4.3 + Módulo 5, Temas 5.1-5.2**: Autocompletado, sampling, roots
- **Actividad Clave**: Entregar proyecto de documentación técnica; implementar primer flujo de sampling
- **Entregable**: Proyecto Práctico Módulo 4
- **Horas**: 3h teoría + 5h práctica

#### Semana 11: Primitivas Avanzadas + SDK TypeScript I

- **Módulo 5, Temas 5.3-5.4 + Módulo 6, Tema 6.1**: Elicitation, logging, progreso, setup SDK TypeScript
- **Actividad Clave**: Implementar flujo completo elicitation + logging; crear primer servidor con SDK TypeScript
- **Horas**: 2h teoría + 6h práctica

#### Semana 12: SDK TypeScript II

- **Módulo 6, Temas 6.2-6.3**: Servidores avanzados en TypeScript, clientes MCP
- **Actividad Clave**: Construir servidor con herramientas dinámicas y cliente multi-servidor
- **Horas**: 1h teoría + 7h práctica

### MES 4: SDKs, INTEGRACIONES Y SEGURIDAD

#### Semana 13: SDK TypeScript III + SDK Python I

- **Módulo 6, Tema 6.4 + Módulo 7, Tema 7.1**: Testing TypeScript, FastMCP Python
- **Actividad Clave**: Entregar API Gateway en TypeScript; crear primer servidor FastMCP
- **Entregable**: Proyecto Práctico Módulo 6
- **Horas**: 2h teoría + 6h práctica

#### Semana 14: SDK Python II

- **Módulo 7, Temas 7.2-7.3**: Servidores Python avanzados, clientes Python
- **Actividad Clave**: Implementar composición de servidores y cliente Python completo
- **Horas**: 1h teoría + 7h práctica

#### Semana 15: SDK Python III + Integraciones I

- **Módulo 7, Tema 7.4 + Módulo 8, Tema 8.1**: Testing Python, Claude Desktop avanzado
- **Actividad Clave**: Entregar servidor ML en Python; configurar MCP remoto en Claude Desktop
- **Entregable**: Proyecto Práctico Módulo 7
- **Horas**: 2h teoría + 6h práctica

#### Semana 16: Integraciones II + Seguridad I

- **Módulo 8, Temas 8.2-8.3 + Módulo 9, Tema 9.1**: IDEs, frameworks de agentes, modelo de amenazas
- **Actividad Clave**: Integrar MCP con LangChain; analizar vectores de ataque en MCP
- **Horas**: 3h teoría + 5h práctica

### MES 5: SEGURIDAD, ARQUITECTURA Y PROYECTO FINAL

#### Semana 17: Seguridad II + Arquitecturas I

- **Módulo 9, Temas 9.2-9.3 + Módulo 10, Tema 10.1**: OAuth 2.1, mejores prácticas, composición de servidores
- **Actividad Clave**: Implementar OAuth 2.1 completo; construir patrón gateway
- **Horas**: 2h teoría + 6h práctica

#### Semana 18: Arquitecturas II + Producción

- **Módulo 10, Temas 10.2-10.3 + Módulo 11**: Agentes autónomos, ecosistema, producción completa
- **Actividad Clave**: Construir agente autónomo con MCP; desplegar servidor con Docker + observabilidad
- **Horas**: 2h teoría + 6h práctica

#### Semana 19: Proyecto Integrador - Diseño e Implementación

- **Módulo 12, Temas 12.1-12.2**: Diseño de arquitectura, implementación de servidores
- **Actividad Clave**: Entregar diseño de arquitectura aprobado; comenzar implementación de servidores
- **Horas**: 1h diseño + 7h implementación

#### Semana 20: Proyecto Integrador - Infraestructura, Testing y Presentación

- **Módulo 12, Temas 12.3-12.4**: Gateway, host web, tests, deployment, documentación, presentación
- **Actividad Clave**: Completar ecosistema, grabar video demo, presentar proyecto final
- **Entregable**: Proyecto Integrador Final completo
- **Horas**: 8h implementación + presentación

## HITOS Y ENTREGABLES

| Semana | Hito                                                    | Tipo                 |
| :----- | :------------------------------------------------------ | :------------------- |
| 2      | Entorno de desarrollo operativo con primer servidor MCP | Checkpoint           |
| 4      | Servidor stdio funcional implementado desde cero        | Evaluación Formativa |
| 8      | Proyecto: Servidor MCP de Base de Datos (Módulo 3)      | Proyecto Parcial     |
| 10     | Proyecto: Servidor MCP de Documentación (Módulo 4)      | Proyecto Parcial     |
| 13     | Proyecto: API Gateway en TypeScript (Módulo 6)          | Proyecto Parcial     |
| 15     | Proyecto: Servidor ML en Python (Módulo 7)              | Proyecto Parcial     |
| 17     | Servidor MCP con OAuth 2.1 funcional                    | Evaluación Formativa |
| 20     | Proyecto Integrador Final: Ecosistema MCP completo      | Evaluación Sumativa  |

## NOTAS PARA EL INSTRUCTOR

- **Semanas 1-4**: Ritmo deliberadamente pausado para consolidar fundamentos. No acelerar aunque el grupo parezca avanzado.
- **Semanas 5-12**: Ritmo intensivo de implementación. Asegurar que cada semana tenga código funcional entregado.
- **Semanas 13-16**: Semanas de máxima carga. Considerar sesiones de soporte adicional para proyectos.
- **Semanas 17-18**: Condensadas pero manejables porque los estudiantes ya dominan las bases.
- **Semanas 19-20**: Dedicadas exclusivamente al proyecto final. Ofrecer tutorías individuales.
- **Buffer implícito**: Las 142 horas en 20 semanas a 7-8h/semana incluyen ~18h de buffer distribuido para revisión y consolidación.
