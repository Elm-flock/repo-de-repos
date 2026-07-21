---
title: kravn
url: https://github.com/addlayerio/kravn
tags: [mcp, gateway, self-hosted, enterprise, sso, typescript]
added: 2026-07-20
added_by: Emiliano
---

Gateway self-hosted de MCP (Model Context Protocol) pensado para organizaciones reguladas que necesitan adoptar herramientas de IA sin sacar datos de su infraestructura.

## Por qué vale la pena

- **Self-hosted de verdad**: Docker o Kubernetes, sin dependencias externas ni salida de datos ("no data egress, no third-party dependency").
- **Identidad enterprise integrada desde el inicio**: SAML, OAuth2/OIDC SSO, SCIM 2.0 y RBAC — no son un agregado posterior.
- **Bootstrap zero-config**: SQLite embebido y keys auto-generadas para arrancar rápido; después soporta PostgreSQL, MySQL o SQL Server con migraciones automáticas.
- **Gateway MCP real**: conecta servers MCP upstream y re-expone sus tools de forma global o vía endpoints virtuales compuestos; soporta OAuth 2.1 para clientes remotos como Claude.
- **Arquitectura clara**: monorepo TypeScript (pnpm + Nx) con backend Fastify, consola de operador y chat de usuario en Vue 3.

## Uso básico

```bash
docker compose up --build
# o
helm install kravn ./charts/kravn
```

Configuración runtime (políticas de seguridad, rate limits, federación) vía web UI, no archivos de config estáticos.

**Licencia**: Business Source License 1.1 — self-hosting libre para uso interno; servicios hosteados comerciales requieren licencia aparte. Pasa a Apache 2.0 a los 4 años del release.
