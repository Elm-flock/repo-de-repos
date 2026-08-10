---
title: lifeos
url: https://github.com/danielmiessler/LifeOS
tags: [agents, claude-code, skill, productivity, typescript, mit]
added: 2026-08-10
added_by: Guille
---

Harness de IA de propósito general de Daniel Miessler (el de Fabric), pensado como capa de contexto personal sobre un coding agent: captura quién sos, qué te importa y a dónde vas, y usa eso para ayudarte a moverte de "Current State" a "Ideal State". TypeScript + Bash, corre sobre Claude Code (path más testeado) pero se declara harness-agnostic.

## Por qué vale la pena

- **La instalación es un prompt**, no un script: le pegás `Read https://ourlifeos.ai/install and install LifeOS for me` a tu agente y él hace el setup pidiendo permiso antes de tocar algo. También hay one-liner para Claude Code en macOS/Linux.
- **Se construye sobre primitivas universales** (hooks, skills, context files, routing agéntico) en vez de features de un vendor — el README es explícito en no listar lo que el harness ya da solo (subagentes, por ejemplo).
- **Ruteo por intención**: decís "research this" y dispara el workflow correcto, con memoria persistente entre sesiones y self-improvement (el sistema se modifica según lo que aprende).
- **Se instala como una única skill autocontenida** que empaqueta toda la librería (research, security, writing, art).
- **Recovery pensado**: `USER/` nunca se toca en upgrades, settings mergean en vez de sobreescribir, todo versionado en git.
- Complementario a Fabric, no reemplazo: Fabric son patterns (*qué* preguntarle a la IA), LifeOS es infra (*cómo* opera tu asistente).

## Ojo

Trae vocabulario propio bastante cargado (TELOS, the Algorithm, Arbol, Bunker, ISA System, Cortex, Synapse, Atlas, Ledger, "Euphoric Surprise") y bastante marketing en el README. Vale la pena para robar ideas de arquitectura de harness; adoptarlo entero es otra decisión. Requiere un harness capaz + [bun](https://bun.sh).

**Licencia**: MIT
