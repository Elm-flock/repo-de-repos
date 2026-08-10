---
title: graph-engineer
url: https://github.com/Ranteck/graph-engineer
tags: [skill, claude-code, codex, coding-agent, multi-agent, mit]
added: 2026-08-10
added_by: Denis
---

Skill de Claude Code que reparte roles entre dos modelos: Claude orquesta y arbitra, Codex escribe, se autocritica adversarialmente y arregla. La idea es que Codex no se corrija solo sin árbitro y que Claude preserve contexto para juicio en vez de gastarlo aplicando código.

## Por qué vale la pena

- **Ciclo de 8 nodos con aristas de retorno** (no un pipeline): PRE-FLIGHT → SPEC → IMPL → QUALITY GATE → CRITIQUE → DEBATE → REFACTOR → VERIFY, donde un QUALITY GATE fallido vuelve al último writer y **VERIFY vuelve a CRITIQUE**. Sin esas aristas es escribir una vez, revisar una vez, listo — bugs incluidos.
- **Estado explícito en `PROJECT_CONTEXT.md`**: cada arista es estado escrito, no memoria implícita de una conversación larga. Eso es lo que lo vuelve máquina de estados y no un chat.
- **Sub-loop de "debatable"** dentro de DEBATE: Claude reinyecta el finding a Codex con un contraargumento ("flagueaste X, pero Y porque Z — ¿lo sostenés?") y recién después decide si va a refactor o se descarta con justificación escrita.
- **QUALITY GATE es solo mecánico** (lint, format, typecheck, build) con retry capeado a 3 por activación; los tests funcionales y los criterios de aceptación son de VERIFY. Un VERIFY fallido se clasifica (defecto de implementación / de test / mismatch de contrato / ambiental) en vez de ir al fixer rápido.
- **Es implementación concreta de dos patrones que Anthropic sí documenta** — Orchestrator-Workers y Evaluator-Optimizer de *Building Effective Agents* — anidados. El repo aclara en `references/sources.md` qué es oficial y qué se le atribuye online a "graph engineering" sin serlo.

## Advertencia

El propio README lo marca como **design-stage: revisado adversarialmente pero todavía no dogfoodeado end-to-end**. El ciclo y el resolver del quality gate convergieron por review Claude↔Codex del diseño, no por correrlo contra una feature real en un repo real. Leer *Limitations / Risks* antes de tirarle `--write` a algo que importe.

Contexto en Slack: Emiliano pasó el video "¿Qué es esto del Graph Engineering?" y Denis linkeó el repo. Denis además comentó que lo que le encontró de útil fue el patrón de un `index.md` por carpeta (equivalente a un `AGENTS.md`/`CLAUDE.md` por directorio) más delegar a Codex por función, para ahorrar tokens y tener un pseudo-grafo.

**Licencia**: MIT
