# Diagramas e Ilustraciones del Curso MCP

Este directorio contiene todos los diagramas SVG e ilustraciones del curso "Model Context Protocol (MCP) - De Cero a Experto".

## Índice de Diagramas

### General

| Diagrama                                        | Descripción                                             |
| :---------------------------------------------- | :------------------------------------------------------ |
| [Mapa del Curso](general/mapa_curso_visual.svg) | Roadmap visual de los 13 módulos organizados por mes    |
| [Ecosistema MCP](general/ecosistema_mcp.svg)    | Vista panorámica: modelos, hosts, protocolo, servidores |

### Módulo 0: Diagnóstico y Nivelación

| Diagrama                                                    | Descripción                                  | Se usa en     |
| :---------------------------------------------------------- | :------------------------------------------- | :------------ |
| [Estructura JSON](modulo_0/json_estructura.svg)             | Árbol de tipos de datos JSON con ejemplo MCP | subtema_0.1.1 |
| [HTTP Request-Response](modulo_0/http_request_response.svg) | Ciclo completo request→response con headers  | subtema_0.1.2 |
| [API REST Recursos](modulo_0/api_rest_recursos.svg)         | Verbos HTTP mapeados a operaciones CRUD      | subtema_0.1.3 |

### Módulo 1: Fundamentos del Protocolo MCP

| Diagrama                                                                        | Descripción                                       | Se usa en     |
| :------------------------------------------------------------------------------ | :------------------------------------------------ | :------------ |
| [Problema N×M](modulo_1/problema_nxm.svg)                                       | N×M vs N+M con analogía USB                       | subtema_1.1.2 |
| [Arquitectura Host/Client/Server](modulo_1/arquitectura_host_client_server.svg) | Los 3 roles de MCP con sus relaciones             | subtema_1.2.1 |
| [Ciclo de Vida](modulo_1/ciclo_vida_conexion.svg)                               | Estados de conexión con detalle de inicialización | subtema_1.2.3 |
| [Mensajes JSON-RPC](modulo_1/json_rpc_mensajes.svg)                             | Anatomía de Request, Response y Notification      | subtema_1.3.1 |

### Módulo 2: Mecanismos de Transporte

| Diagrama                                                        | Descripción                                   | Se usa en     |
| :-------------------------------------------------------------- | :-------------------------------------------- | :------------ |
| [Transporte stdio](modulo_2/transporte_stdio.svg)               | Host→subprocess con stdin/stdout/stderr       | subtema_2.1.1 |
| [Transporte SSE](modulo_2/transporte_sse.svg)                   | Arquitectura dual: SSE + POST                 | subtema_2.2.2 |
| [Streamable HTTP](modulo_2/transporte_streamable_http.svg)      | Endpoint unificado con 3 modos                | subtema_2.3.1 |
| [Comparativa Transportes](modulo_2/comparativa_transportes.svg) | Tabla visual: stdio vs SSE vs Streamable HTTP | subtema_2.4.1 |

### Módulo 3: Primitivas Core — Tools

| Diagrama                                                            | Descripción                                              | Se usa en       |
| :------------------------------------------------------------------ | :------------------------------------------------------- | :-------------- |
| [Anatomía de Tool](modulo_3/anatomia_tool.svg)                      | Estructura: name, description, inputSchema, outputSchema | subtema_3.1.1   |
| [Flujo tools/list → tools/call](modulo_3/flujo_tools_list_call.svg) | Secuencia completa de descubrimiento e invocación        | subtema_3.1.2-3 |
| [Anotaciones](modulo_3/tool_anotaciones.svg)                        | readOnlyHint, destructiveHint, openWorldHint             | subtema_3.2.1   |

### Módulo 4: Resources y Prompts

| Diagrama                                              | Descripción                                  | Se usa en       |
| :---------------------------------------------------- | :------------------------------------------- | :-------------- |
| [Modelo de Resources](modulo_4/modelo_resources.svg)  | URI → Resource con tipos MIME y contenido    | subtema_4.1.1   |
| [Flujo de Prompts](modulo_4/flujo_prompts.svg)        | Definición → Resolución → Mensajes multi-rol | subtema_4.2.1-2 |
| [Suscripciones](modulo_4/suscripciones_resources.svg) | Subscribe → cambio → notificación → re-read  | subtema_4.1.4   |

### Módulo 5: Primitivas Avanzadas

| Diagrama                                            | Descripción                                           | Se usa en       |
| :-------------------------------------------------- | :---------------------------------------------------- | :-------------- |
| [Flujo Sampling](modulo_5/flujo_sampling.svg)       | Flujo inverso Server→Client→LLM con human-in-the-loop | subtema_5.1.1   |
| [Elicitation](modulo_5/elicitation_formularios.svg) | Formularios dinámicos con tipos y validaciones        | subtema_5.3.1   |
| [Logging y Progreso](modulo_5/logging_progreso.svg) | Niveles de log y reporte de progreso                  | subtema_5.4.1-2 |

## Paleta de Colores

| Color       | Hex                   | Uso                         |
| :---------- | :-------------------- | :-------------------------- |
| Azul oscuro | `#01579b`             | Headers, fondos principales |
| Azul medio  | `#0288d1`             | Protocolo, Client           |
| Azul claro  | `#4fc3f7`             | Fondos de componentes       |
| Verde       | `#4caf50`             | Server, éxito               |
| Naranja     | `#ff9800`             | Advertencia, anotaciones    |
| Rojo        | `#f44336`             | Errores, destructivo        |
| Púrpura     | `#9c27b0`             | LLM                         |
| Gris        | `#263238` / `#546e7a` | Texto                       |
