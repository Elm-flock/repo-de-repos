---
title: gentle-ai
url: https://github.com/Gentleman-Programming/gentle-ai
tags: [coding-agent, spec-driven, agents, multi-agent, mit]
added: 2026-07-30
added_by: Emiliano
---

Configurador de ecosistema para agentes de IA de código (no un instalador de agente). Equipa a agentes existentes (Claude Code, OpenCode, Cursor, etc.) con memoria persistente, workflows estructurados, skills curadas y revisión acotada, para convertirlos de "chatbots" en herramientas de desarrollo disciplinadas. Su enfoque arquitectónico es **Organic RDD** (Receipt-Driven Development). Autor: Gentleman Programming.

## Por qué vale la pena

- **Memoria persistente (Engram)** entre sesiones.
- **Routing multi-agente por resultado (outcome-first)**: directo si está acotado, delega si hace falta contexto, SDD solo bajo pedido explícito.
- **Content-bound receipts**: congela los bytes exactos antes de revisar → verificación basada en evidencia, no en la narración del agente.
- **Revisión nativa acotada** con verification gates en commit/push/PR/release.
- **Workflows SDD deterministas** con capacidad test-first; control nativo de identidad del repo y transiciones (trust verificable).

## Uso básico

Se instala sobre el agente que ya usás; ver el README del repo y `docs/architecture/the-organic-rdd-story.md` para la filosofía completa.

**Licencia**: MIT
