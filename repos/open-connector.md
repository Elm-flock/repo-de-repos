---
title: open-connector
url: https://github.com/oomol-lab/open-connector
tags: [gateway, mcp, cli, agents, self-hosted, apache-2.0]
added: 2026-07-30
added_by: Emiliano
---

Auth gateway open source que conecta 1000+ proveedores SaaS (10.000+ acciones prearmadas) a agentes de IA. Conectás las cuentas del usuario una vez y exponés un catálogo compartido de acciones vía SDK, CLI, MCP, HTTP y OpenAPI, gestionando credenciales, OAuth, scopes, schemas, políticas y logs de ejecución en un runtime inspeccionable. Se posiciona explícitamente como alternativa self-hostable a Composio.

## Por qué vale la pena

- **Cinco métodos de integración** sobre el mismo gateway: SDK (cliente HTTP en TypeScript), CLI (`oo connector`, relay de agente local), MCP (`/mcp`), HTTP/OpenAPI (`/v1/actions/*` + `/openapi.json`) y Web Console para administración/debug.
- **Escala**: 1000+ proveedores y 10.000+ acciones prearmadas (GitHub, Gmail, Notion, BigQuery, Google Analytics, Supabase, Airtable, Slack, etc.); ~3.5k estrellas.
- **Auth flexible**: maneja API keys, OAuth2, credenciales custom y proveedores no-auth.
- **Deploy self-hosteable**: local (Docker/Node), Fly.io (persistencia SQLite), Cloudflare Workers (D1/R2) o runtime hosteado por OOMOL con OAuth gestionado.
- **Diferencial vs Composio**: open source y self-hostable, con exposición MCP nativa (Composio es mayormente SaaS/gestionado).

## Uso básico

```bash
docker compose up
# Consola:      http://localhost:3000
# Endpoint MCP: http://localhost:3000/mcp
```

**Licencia**: Apache 2.0
