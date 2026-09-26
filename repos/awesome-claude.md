---
title: awesome-claude
url: https://github.com/webfuse-com/awesome-claude
tags: [directory, claude-code, anthropic, mcp, cc0-1.0]
added: 2026-09-25
added_by: Denis
---

Lista curada de recursos sobre Claude: modelos, API, SDKs, Claude Code, MCP, extensiones, cursos y comunidad. Tiene ~77 links y la mayoría son oficiales de Anthropic. Sirve más como hoja de referencia rápida que como catálogo de herramientas de terceros. La arrancó Alvin Unreal (`alvinunreal/awesome-claude`) y hoy vive en la org de Webfuse, con sitio en awesomeclaude.ai.

## Por qué vale la pena

- **Tabla de modelos con datos operativos**: ID de API, precio por MTok, contexto y output máximo de cada modelo vigente, más las notas de migración que duelen. En la familia Claude 5, `budget_tokens` fijo, `temperature`/`top_p`/`top_k` y el prefill del último turno de assistant devuelven 400.
- **Todo lo oficial en un lugar**: 7 SDKs de cliente (Python, TS, Java, Go, Ruby, C#, PHP; ver [[anthropic-sdk-csharp]]), los 2 Agent SDKs, cookbook y quickstarts, acceso por Bedrock/Vertex/Azure, índice de system cards y 12 cursos gratis de Anthropic en Skilljar (API, Claude Code, MCP intro y avanzado, Bedrock, Vertex).
- **Puerta a las listas más grandes**: enlaza a `hesreallyhim/awesome-claude-code` (commands, `CLAUDE.md`, workflows), dos `awesome-claude-skills`, `VoltAgent/awesome-claude-code-subagents` (100+ subagentes) y `punkpeye/awesome-mcp-servers`. Para herramientas concretas conviene ir directo a esas.
- **Linux**: lista `claude-desktop-debian`, el port no oficial de Claude Desktop.

## Advertencia

- **Se actualiza poco y casi solo en modelos**: los commits de marzo a agosto de 2026 son actualizaciones de "Current Models" más un banner de `awesome-webmcp`, la otra lista de Webfuse. El último push es del 10 de agosto de 2026 y llega hasta Opus 5 y Sonnet 5, sin Opus 5.5 ni Fable 5.1. Verificar precios e IDs contra la doc oficial.
- La lista de Claude que figura en [[awesome]] (sindresorhus) es `awesome-claude-code`, no esta.

**Licencia**: CC0-1.0
