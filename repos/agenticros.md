---
title: agenticros
url: https://github.com/agenticros/agenticros
tags: [robotics, agents, skill, claude-code, typescript, apache-2.0]
added: 2026-08-21
added_by: Denis
---

Plugin/bridge para ROS 2 que expone las capacidades del robot como *skills* consumibles por agentes de IA: Claude Code, Claude Desktop/Dispatch, Codex, Gemini, OpenClaw, Hermes y MCP.

## Por qué vale la pena

- **Cierra el gap entre agente y hardware**: en vez de generar código ROS y esperar que compile, el agente invoca skills que ya encapsulan la acción del robot.
- **Skills concretas, una por repo**: `navigate-to`, `find`, `detect-humans`, `start-slam`, `follow-me-ros`, `moveit-pick`, `dock-to-charger`, `followme`, `jarvis`. La org tiene ~15 repos y un marketplace de skills en `agenticros-skills`.
- **CLI publicado y en uso**: npm `agenticros` v0.7.13 (~4.2k descargas/mes), Node.js ≥20. No es un proof of concept abandonado — último push 20-ago-2026.
- Anunciado en **ROS Discourse el 31-mar-2026**, así que tiene visibilidad en la comunidad ROS y no sólo en el mundo de agentes.
- Topics del repo (`physical-ai`, `robotics`, `ros`, `anthropic`, `claude-code`) reflejan el cruce que ocupa: es de los pocos que conecta un coding agent con la capa de control de un robot real.

## Uso básico

```bash
npm i -g agenticros
```

Store de skills en `skills.agenticros.com`. ~140 stars, creado el 01-mar-2026, mantenido por Chris Matthieu.

**Advertencia de licencia**: el repo principal es Apache-2.0, pero **`agenticros-skills` no tiene archivo de licencia** (SPDX null). Revisar antes de usar una skill del marketplace en algo propietario.

**Licencia**: Apache-2.0 (el repo de skills no declara licencia)
