---
title: sdd-builder
url: https://github.com/juanklagos/spec-driven-development-template
tags: [coding-agent, spec-driven, mcp, multi-agent, mit]
added: 2026-07-30
added_by: Emiliano
---

Template + toolkit educativo y práctico de spec-driven development (SDD). Regla central: no hay código antes de un `spec.md` aprobado y un `plan.md` consistente. Combina guías bilingües (ES/EN) con scripts de enforcement, reglas de agente, un servidor MCP y un modo "sidecar" (`spec/`) desplegable sobre bases de código existentes. Autor: Juan Carlos Álvarez Lagos.

## Por qué vale la pena

- **Bundles de spec numerados** con approval gates + logbook (`bitacora/`) de decisiones.
- **Enforcement vía GitHub Actions** (SDD Validate) que bloquea implementación hasta pasar el gate.
- **Builder visual (SDD Desk)** para componer especificaciones + dashboards/tracking de dependencias.
- **Servidor MCP** para workflows guiados e integración con GitHub Spec Kit.
- **Multi-agente** (Claude, Cursor, Copilot, Gemini) y doc **bilingüe ES/EN**.

## Uso básico

Guía visual y setup en <https://juanklagos.github.io/spec-driven-development-template/>. Se puede clonar como template o montar el modo sidecar sobre un repo existente.

**Licencia**: MIT
