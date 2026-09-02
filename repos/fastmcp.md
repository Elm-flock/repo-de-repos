---
title: fastmcp
url: https://github.com/PrefectHQ/fastmcp
tags: [mcp, framework, python, apache-2.0]
added: 2026-09-02
added_by: Guille
---

Framework Python completo para MCP: servidores, clientes y "apps" (UIs interactivas que se renderizan dentro de la conversación). Es la capa alta que se apoya sobre el SDK oficial, no un reemplazo.

## Por qué vale la pena

- **Es el estándar de facto por volumen**: 83.9M de descargas/mes en PyPI (1.68M/día). Para comparar, el SDK oficial `mcp` está en 317M/mes.
- **27.495 stars y 282 contributors**, con v4.0.0 GA el 31-ago-2026 y v4.0.1 al día siguiente.
- **Decorador y listo**: `@mcp.tool` sobre una función tipada genera el schema del tool solo, sin escribir JSON Schema a mano.
- **Se apila sobre el SDK oficial, no compite**: FastMCP 4 está construido sobre la revisión de protocolo MCP `2026-07-28` y sobre el SDK oficial de Python v2.
- **Contraparte oficial en TypeScript** del mismo equipo: `PrefectHQ/fastmcp-ts` (npm `@prefecthq/fastmcp-ts`, Apache-2.0).

## Uso básico

```bash
uv add fastmcp
```

```python
from fastmcp import FastMCP
mcp = FastMCP("Demo 🚀")

@mcp.tool
def add(a: int, b: int) -> int:
    """Add two numbers"""
    return a + b

if __name__ == "__main__":
    mcp.run()
```

## Las dos historias de fastmcp, que conviene no confundir

- **fastmcp 1.0 está extinto bajo ese nombre.** El fastmcp original de Jeremiah Lowin fue donado al SDK oficial de Python en dic-2024 (commit "Integrate FastMCP") y vivió ahí como `mcp.server.fastmcp` durante toda la línea `mcp` 1.x. El 25-ene-2026 el SDK renombró `FastMCP` → `MCPServer`, y en `mcp` 2.x el módulo viejo es un stub que tira `ModuleNotFoundError`. **Si tenés código estilo FastMCP 1.0 sobre el SDK oficial, hay que pinnear `mcp<2` o migrar a `MCPServer`.**
- **fastmcp 2.x+ es el proyecto independiente y el único FastMCP vivo**, hoy mantenido por **Prefect** (PrefectHQ) con Lowin y Nate Nowack. Ojo que la URL vieja `jlowin/fastmcp` redirige acá.

## Advertencias

- **Cadencia de majors agresiva**: 1.x → 2.x (abr-2025) → 3.x → 4.x (ago-2026) en menos de dos años. La señal de que los upgrades no son triviales es que hay guías de migración separadas para cada salto.
- **Breaking changes reales en 4.0**: sampling y roots iniciados por el servidor eliminados, `ctx.elicit()` solo para protocolo viejo, APIs deprecadas de 3.x borradas, campos de modelos MCP pasados a snake_case, y las background tasks movidas al paquete aparte `fastmcp-tasks`.
- **Colisión de nombres**: `punkpeye/fastmcp` (3.259 stars, TypeScript, MIT) es un framework MCP **distinto y sin relación** con el mismo nombre.
- El packaging está partido en `fastmcp` / `fastmcp-slim` / `fastmcp-tasks`, lo que puede dar sorpresas al resolver extras.
- El claim del README de que "alguna versión de FastMCP mueve el 70% de los MCP servers" no es verificable. El de descargas sí lo es.
- Hay producto comercial del mismo equipo (**Prefect Horizon**, gateway MCP enterprise con SSO y RBAC por tool), pero FastMCP sigue Apache-2.0.

Relacionado: [[mcpwasm]] y [[open-connector]] para otras piezas del ecosistema MCP; [[orcarouter]] del lado de gateways.

**Licencia**: Apache-2.0 (distinta del SDK oficial, que es MIT)
