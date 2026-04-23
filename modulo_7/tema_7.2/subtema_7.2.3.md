# Subtema 7.2.3: Composición de Servidores: mount() e import_server()

![Composición de Servidores](../../../diagramas/modulo_7/composicion_servidores.svg)

FastMCP permite construir servidores modulares combinando múltiples instancias.

## Montaje de Servidores (`mount`)

Imagina que tienes un servidor de Auth y uno de Database. Puedes unirlos en una sola App.

```python
from fastmcp import FastMCP

# Servidor 1

![Composición de Servidores](../../../diagramas/modulo_7/composicion_servidores.svg)
auth = FastMCP("Auth")
@auth.tool()
def login(user: str): return "Token..."

# Servidor 2

![Composición de Servidores](../../../diagramas/modulo_7/composicion_servidores.svg)
db = FastMCP("DB")
@db.tool()
def query(sql: str): return "Rows..."

# Servidor Principal

![Composición de Servidores](../../../diagramas/modulo_7/composicion_servidores.svg)
app = FastMCP("MainApp")

# Montar con prefijos para evitar colisiones

![Composición de Servidores](../../../diagramas/modulo_7/composicion_servidores.svg)
app.mount(auth, prefix="auth")
app.mount(db, prefix="db")

# Resultado:

![Composición de Servidores](../../../diagramas/modulo_7/composicion_servidores.svg)
# auth_login

![Composición de Servidores](../../../diagramas/modulo_7/composicion_servidores.svg)
# db_query

![Composición de Servidores](../../../diagramas/modulo_7/composicion_servidores.svg)
```

## Importación (`import_server`)

También puedes importar un servidor completo desde otro archivo o módulo remoto (experimental).

```python
# from my_utils import utils_server

![Composición de Servidores](../../../diagramas/modulo_7/composicion_servidores.svg)
# app.mount(utils_server)

![Composición de Servidores](../../../diagramas/modulo_7/composicion_servidores.svg)
```

Esto facilita enormemente la arquitectura de microservicios dentro de un mismo proceso.

