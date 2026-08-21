---
title: claude-code-setup
url: https://github.com/anthropics/claude-plugins-official/tree/main/plugins/claude-code-setup
tags: [plugin, claude-code, skill, coding-agent, anthropic, apache-2.0]
added: 2026-08-21
added_by: Lucas Mujica
---

Plugin oficial de Anthropic cuya skill principal (`claude-automation-recommender`) escanea un repo — manifests, dependencias, estructura, `.claude/` existente — y recomienda los 1-2 hooks, subagents, skills, plugins y MCP servers que mejor le calzan a *ese* proyecto.

## Por qué vale la pena

- **Recomendación específica del proyecto, no una lista genérica**: lee lo que hay y prioriza, en vez de tirarte el catálogo completo.
- **Read-only por diseño**: el front matter declara `tools: Read, Glob, Grep, Bash` — **sin Write ni Edit**. No te toca archivos, sólo sugiere.
- **`SKILL.md` de 11 KB + 5 archivos de referencia**: `hooks-patterns.md`, `mcp-servers.md`, `plugins-reference.md`, `skills-reference.md`, `subagent-templates.md`. Sirven como material de lectura por separado.
- **Vive en el marketplace oficial de plugins de Anthropic** (`anthropics/claude-plugins-official`, 33.7k stars, Apache-2.0), que hoy lista **286 plugins** — el repo entero vale la visita, no sólo este plugin.
- Validación externa concreta: Cherry Studio vendorea esta skill en su agente incorporado, con `NOTICE.md` documentando su única modificación.

## Uso básico

```
/plugin install claude-code-setup@claude-plugins-official
```

Se dispara con pedidos tipo "recomendá automatizaciones para este proyecto", "ayudame a configurar Claude Code", "qué hooks debería usar".

**Sobre el consumo de tokens** — Denis lo resumió en el canal como "gasta más tokens pero lo ultra recomiendo": el fork de Cherry Studio midió **20-40K tokens** de contexto para un repo mediano, y agregó un gate de "Phase 0: Confirm Before Scanning" que **el upstream no tiene** — el oficial arranca a escanear de una.

**Otras cosas a tener en cuenta:**
- Es sólo recomendador: presupuestá una segunda pasada para implementar lo que sugiera.
- El `SKILL.md` le indica al modelo usar web search más allá de las listas incluidas, así que la salida no es determinística y necesita red.
- Las listas de referencia son una foto curada, última actualización 28-may-2026: envejecen.

**Nota de identificación**: en el canal se lo mencionó como `/claude-code-recomender` y el link que circuló era de mcpmarket.com, un agregador de terceros. No hay evidencia en GitHub de que esta skill se haya llamado así nunca — arrancó como `claude-automation-recommender` desde su primer commit. Puede ser que Denis usara otra cosa, así que si el comportamiento no coincide con lo que él describió, vale volver a preguntarle.

Relacionado: [[skillsmp]] para buscar skills de terceros, [[power-platform-skills]] como otro marketplace de plugins.

**Licencia**: Apache-2.0
