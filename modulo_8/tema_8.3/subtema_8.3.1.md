# Subtema 8.3.1: LangChain y LangGraph con MCP

![Frameworks de Agentes](../../../diagramas/modulo_8/frameworks_agentes.svg)

Si ya usas LangChain, MCP es una mina de oro: te da acceso instantáneo a miles de herramientas sin escribir wrappers.

## Adaptador MCP para LangChain

LangChain ha introducido soporte experimental para conectar clientes MCP.

```python
from langchain_mcp_adapters.tools import load_mcp_tools
from langchain_openai import ChatOpenAI
from mcp.client.stdio import StdioServerParameters

# 1. Definir cómo lanzar el servidor MCP

![Frameworks de Agentes](../../../diagramas/modulo_8/frameworks_agentes.svg)
server_params = StdioServerParameters(command="python", args=["server.py"])

# 2. Cargar herramientas MCP como Tools de LangChain

![Frameworks de Agentes](../../../diagramas/modulo_8/frameworks_agentes.svg)
tools = await load_mcp_tools(server_params)

# 3. Usarlas en un Agente

![Frameworks de Agentes](../../../diagramas/modulo_8/frameworks_agentes.svg)
llm = ChatOpenAI(model="gpt-4-turbo")
agent = create_react_agent(llm, tools)

print(agent.invoke({"input": "Usa la herramienta del servidor para sumar 5+5"}))
```

Esto democratiza el acceso a herramientas: ya no necesitas buscar si existe `LangChainToolForX`, solo necesitas un servidor MCP para X.

