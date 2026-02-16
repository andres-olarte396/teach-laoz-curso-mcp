# Subtema 9.2.3: Implementación Completa: Servidor MCP con OAuth 2.1

Implementar OAuth completo desde cero es complejo. Se recomienda usar librerías o un Gateway.

## Ejemplo Conceptual (Python / FastAPI)

```python
from fastapi import FastAPI, Depends, HTTPException
from fastapi.security import OAuth2AuthorizationCodeBearer
from fastmcp import FastMCP

app = FastAPI()
oauth2_scheme = OAuth2AuthorizationCodeBearer(
    authorizationUrl="auth",
    tokenUrl="token"
)

# Servidor MCP (lógica de negocio)
mcp = FastMCP("SecureServer")

async def verify_token(token: str = Depends(oauth2_scheme)):
    # Validar firma del JWT
    user = decode_jwt(token)
    if not user:
        raise HTTPException(status_code=401)
    return user

@app.get("/sse")
async def handle_sse(token: str = Depends(verify_token)):
    # Si llega aquí, está autenticado.
    # Iniciar conexión SSE del MCP.
    pass

# Endpoints OAuth (simplificados)
@app.get("/auth")
def auth_endpoint(): ...

@app.post("/token")
def token_endpoint(): ...
```

Lo importante es que el endpoint `/sse` (el handshake inicial) esté protegido. Una vez establecida la conexión, se asume que es segura (siempre sobre HTTPS).
