---
title: agent-teams
url: https://github.com/egdev6/agent-teams
tags: [agents, multi-agent, plugin, typescript, copilot]
added: 2026-08-21
added_by: Emiliano
---

Monorepo pnpm + extensión de VS Code para crear, componer y desplegar agentes custom de GitHub Copilot a partir de "kits" reutilizables y perfiles de equipo, con dashboard React embebido.

## Por qué vale la pena

- **Lo primero y más importante: no tiene licencia.** La API de GitHub devuelve `license: null` y `/LICENSE` da 404; el README declara un aviso propietario/privado. Es **visible pero no reutilizable legalmente** — sirve para mirar el diseño, no para tomar código.
- **Modelo de composición en 4 capas** que es la idea interesante: Core → Kits → Project Profile (`.agent-teams/project.profile.yml`) → Team Profile (`.agent-teams/teams/<id>.yml`), todo validado con JSON Schema vía AJV.
- **`MergeEngine` con 4 estrategias** (`team-priority`, `profile-priority`, `kit-priority`, `explicit-only`) y **3 modos de array** (`replace`, `concat`, `union`). Es la parte que vale robar como patrón para cualquier sistema de perfiles de agentes.
- **Formato de kit definido**: `kit.yml` + `agents/` con placeholders `{{...}}` + `context-packs/`. Trae un kit de ejemplo: `testing-vitest` (`vitest-worker`, `test-orchestrator`).
- **Participantes de chat dinámicos** en Copilot, incluido un `@router` que rutea por intención.
- Webview React con 12 páginas (Dashboard, Profile Editor, Team Manager, Agent Manager, Skills Browser, Context Packs, Import/Export, Agent Wizard…). ~900 KB de TypeScript: es sustancial para sus 4 stars.
- **README y producto en español**, si eso importa para el equipo.

## Uso básico

```bash
git clone https://github.com/egdev6/agent-teams.git && cd agent-teams && pnpm install
# VS Code → Run and Debug → "Run Extension Watch"
pnpm -C packages/extension package
```

Requiere Node ≥18, pnpm ≥8, VS Code ≥1.85. Toolchain: Biome, changesets, commitlint, lefthook.

**Estado**: self-describe como "v1.0.0, Beta, Marzo 2026" y el último push es del 04-abr-2026 — ~4 meses y medio parado. No está publicado en el Marketplace de VS Code.

Relacionado: [[gentle-ai]] para composición de agentes con otra filosofía.

**Licencia**: sin licencia (todos los derechos reservados)
