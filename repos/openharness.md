---
title: openharness
url: https://github.com/HKUDS/OpenHarness
tags: [llm, agents, multi-agent, python, hkuds, mit]
added: 2026-07-21
added_by: Guille
---

Infraestructura abierta de agent harness en Python con tools, skills, memoria, permisos y coordinación multi-agente; incluye el agente personal `ohmo`.

## Por qué vale la pena

- **Harness completo e inspeccionable**: incluye loop con streaming, reintentos, ejecución paralela, conteo de tokens y seguimiento de costo.
- **43 tools integradas**: cubre archivos, shell, búsqueda, web y MCP; suma skills bajo demanda y plugins con skills, hooks y agentes.
- **Gobernanza configurable**: ofrece modos de permisos, reglas por path y comando, hooks `PreToolUse`/`PostToolUse` y aprobaciones interactivas.
- **Coordinación multi-agente**: permite crear subagentes, registrar equipos, asignar tareas y controlar el ciclo de vida de trabajos en background.
- **Contexto persistente**: descubre `CLAUDE.md`, compacta automáticamente, conserva `MEMORY.md` y permite reanudar sesiones largas.
- **Agente personal incluido**: `ohmo` funciona desde Slack, Telegram, Discord o Feishu y puede reutilizar suscripciones existentes de Claude Code o Codex.

## Uso básico

```bash
pip install openharness-ai
oh setup
oh
```

Para el agente personal: `ohmo init`, `ohmo config` y `ohmo gateway start`.

**Licencia**: MIT
