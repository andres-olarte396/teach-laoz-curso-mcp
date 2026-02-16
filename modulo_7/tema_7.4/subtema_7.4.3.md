# Subtema 7.4.3: Proyecto Práctico: Servidor MCP de Machine Learning

Vamos a construir un servidor que expone un modelo de clasificación de texto (Sentiment Analysis) simple.

## Requisitos

1.  **Modelo:** Usar `textblob` o un pipeline simple de `scikit-learn` (pre-entrenado para no complicarnos).
2.  **Tool `analyze_sentiment(text)`:** Devuelve polaridad y subjetividad.
3.  **Resource `stats://model`:** Devuelve métricas de precisión del modelo (fijas).
4.  **Prompt `improve_sentiment`:** Toma un texto negativo y pide al LLM que lo reescriba para ser más positivo.

## Esqueleto

```python
from fastmcp import FastMCP
from textblob import TextBlob

mcp = FastMCP("SentimentBot")

@mcp.tool()
def analyze(text: str) -> str:
    """Analiza el sentimiento de un texto."""
    blob = TextBlob(text)
    return f"Polaridad: {blob.sentiment.polarity}, Subjetividad: {blob.sentiment.subjectivity}"

@mcp.resource("stats://model")
def get_stats() -> str:
    return '{"accuracy": 0.85, "model": "TextBlob-Simple"}'

@mcp.prompt()
def improve_sentiment(text: str) -> str:
    return f"El siguiente texto tiene sentimiento negativo. Reescríbelo para que sea positivo pero mantenga el significado:\n\n{text}"

if __name__ == "__main__":
    mcp.run()
```

## Tarea

Implementa esto, instálalo en Claude Desktop y prueba a decirle:
_"Analiza esta frase: 'Odio este producto'. Luego usa el prompt de mejora para arreglarla."_
