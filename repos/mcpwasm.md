---
title: mcpwasm
url: https://github.com/MauricioPerera/mcpwasm
tags: [mcp, wasm, sandbox, self-hosted, javascript, mit]
added: 2026-08-10
added_by: Emiliano
---

"Static MCP": tus tools son archivos, no servidores. Las tools se publican como contenido estático verificado por hash y se ejecutan sandboxeadas on demand. La analogía del README: lo que el static hosting le hizo al web server ("no corras Apache, publicá HTML"), esto se lo hace al MCP server.

## Por qué vale la pena

- **Cero infraestructura del lado del publisher**: el MCP server se materializa por request desde los archivos y desaparece al responder (instancia efímera, definición durable).
- **Sandbox real para código de terceros**: cada `tool.js` corre aislado en QuickJS-wasm sobre Cloudflare Workers. El único puente del sandbox a los internals de la plataforma es una capability que el host inyecta explícitamente: sin capability, sin acceso. La comparación que usa es "php-wasm pero para tools MCP".
- **Verificación por hash**: fetchea `/llms.txt`, verifica cada `tool_sha256` y recién entonces ejecuta.
- **Convierte cualquier sitio estático en MCP server**, sin cuenta, sin deploy y sin infra de ninguno de los dos lados.
- **Tres modos de uso**: runtime local (stdio, el que no necesita nada), gateway hosteado multi-tenant en Cloudflare Workers, y librería embebible (`@rckflr/mcpwasm`) para armar tu propio host.
- Se integra con el estándar [llms-txt-skills](https://github.com/MauricioPerera/llms-txt-skills) vía dos extensiones adoptadas en la spec: executable skills (v0.4, con *origin memory*) y skill attestations (v0.4).

## Uso básico

```bash
npx -y @rckflr/mcpwasm https://usuario.github.io
```

En un cliente MCP (Claude Code, Cursor, Cline):

```json
{
  "mcpServers": {
    "misitio": {
      "command": "npx",
      "args": ["-y", "@rckflr/mcpwasm", "https://usuario.github.io"]
    }
  }
}
```

Proyecto muy chico en tracción (unidades de estrellas) — la idea es más interesante que la adopción por ahora. Llegó al canal vía el video "mcpwasm: Herramientas MCP Estáticas en Sandbox WebAssembly".

**Licencia**: MIT
