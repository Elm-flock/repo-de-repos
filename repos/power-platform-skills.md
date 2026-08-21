---
title: power-platform-skills
url: https://github.com/microsoft/power-platform-skills
tags: [skill, coding-agent, claude-code, plugin, microsoft, mit]
added: 2026-08-21
added_by: Emiliano
---

Marketplace oficial de plugins de Microsoft para Claude Code y GitHub Copilot CLI, que empaqueta expertise de desarrollo en Power Platform: Power Pages, model-driven apps, canvas apps, Power Automate, code apps, mobile apps y MCP apps.

## Por qué vale la pena

- **91 archivos `SKILL.md` en 7 plugins**: power-pages 32, mobile-apps 23, code-apps 15, power-automate 10, canvas-apps 4, model-apps 4, mcp-apps 2. Es volumen real de conocimiento empaquetado, no un template.
- **Stack explícito por plugin**, no genérico: power-pages cubre React/Angular/Vue/Astro; model-apps es React + TypeScript + Fluent vía PAC CLI; mobile-apps es Expo + React Native vía Power Apps Wrap; canvas-apps trabaja sobre `.pa.yaml` con `CanvasAuthoringMcpServer`.
- **Muy activo**: creado el 21-ene-2026, 747 stars, 29 contributors y 445+ PRs mergeados. Último commit el mismo día que se cargó esta entrada.
- Sirve como **referencia de cómo Microsoft estructura un marketplace de plugins** para Claude Code, más allá de que uses Power Platform o no.

## Uso básico

```bash
# dentro de una sesión de Claude Code o Copilot CLI
/plugin marketplace add microsoft/power-platform-skills
/plugin install power-pages@power-platform-skills
```

Se instala desde `main` con auto-update; no hay releases publicados.

**Advertencia de seguridad**: el README recomienda correrlo con `--dangerously-skip-permissions` / `--allow-all-tools`. Eso desactiva la confirmación de herramientas para toda la sesión — no es una recomendación que convenga seguir a ciegas en un repo con credenciales o infra.

**Otras trampas:**
- Sin licencia de Microsoft y un tenant de Power Platform, no sirve para nada: requiere el CLI `pac` y un environment.
- El nombre de install difiere del directorio en dos plugins: `code-apps-preview` → `plugins/code-apps`, y `mobile-app` (singular) → `plugins/mobile-apps`.
- `canvas-apps` necesita **.NET 10 SDK**; `power-automate` necesita Node 18+ y Azure CLI.
- 91 issues abiertos para 7 meses de vida.

Relacionado: [[skill-recorder]] para generar skills propias, [[skillsmp]] para descubrirlas.

**Licencia**: MIT
