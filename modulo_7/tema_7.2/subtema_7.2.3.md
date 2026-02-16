# Subtema 7.2.3: Composición de Servidores: mount() e import_server()

FastMCP permite construir servidores modulares combinando múltiples instancias.

## Montaje de Servidores (`mount`)

Imagina que tienes un servidor de Auth y uno de Database. Puedes unirlos en una sola App.

```python
from fastmcp import FastMCP

# Servidor 1
auth = FastMCP("Auth")
@auth.tool()
def login(user: str): return "Token..."

# Servidor 2
db = FastMCP("DB")
@db.tool()
def query(sql: str): return "Rows..."

# Servidor Principal
app = FastMCP("MainApp")

# Montar con prefijos para evitar colisiones
app.mount(auth, prefix="auth")
app.mount(db, prefix="db")

# Resultado:
# auth_login
# db_query
```

## Importación (`import_server`)

También puedes importar un servidor completo desde otro archivo o módulo remoto (experimental).

```python
# from my_utils import utils_server
# app.mount(utils_server)
```

Esto facilita enormemente la arquitectura de microservicios dentro de un mismo proceso.
