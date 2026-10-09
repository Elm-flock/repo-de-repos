---
title: coderabbit
url: https://www.coderabbit.ai
tags: [code-review, coding-agent, cli, ci-cd, saas]
added: 2026-10-09
added_by: Emiliano
---

SaaS de code review con IA: revisa cada PR/MR con resumen, walkthrough, comentarios línea por línea y chat con `@coderabbitai`, y también revisa local antes del commit con extensión de IDE y CLI. **El plan Free no revisa PRs, sólo los resume, y el código se comparte con OpenAI y/o Anthropic.** Llegó al canal por un video patrocinado de BettaTech.

## Por qué vale la pena

- **Todas las plataformas de Git**: GitHub (cloud y Enterprise Server), GitLab (cloud y self-managed), Azure DevOps y Bitbucket (Cloud y Data Center).
- **Lee `CLAUDE.md`, `AGENTS.md` y `.cursorrules`** y los aplica como guidelines del review. Integra más de 50 linters y herramientas SAST (ESLint, Ruff, ShellCheck, Trivy, Checkov, TruffleHog, etc.).
- **CLI para agentes**: `cr review --agent` devuelve NDJSON, y hay plugins oficiales para Claude Code, Codex, Cursor, Gemini y Antigravity.
- **Gratis para open source** con features de Team, entre 1 y 10 reviews de PR por hora según las stars del repo.
- **Precios** (USD por developer/mes, anual o mensual; sólo se cobra a quien abre PRs):
  - Essentials: 24 o 30. 5 reviews por hora, hasta 150 archivos.
  - Team: 48 o 60. 8 por hora, 300 archivos, generación de tests y resolución de merge conflicts.
  - Advanced: 72 o 90. Suma security review y análisis de blast radius.
  - El exceso se paga a USD 0,25 por archivo. Los videos viejos que hablan de "Pro" se refieren al actual Essentials.
- Config por repo en `.coderabbit.yaml` con perfiles `quiet`, `chill` (default) o `assertive`.

## Uso básico

```bash
curl -fsSL https://cli.coderabbit.ai/install.sh | sh    # o: brew install coderabbit
cr auth login
cr review --uncommitted
cr review --agent                                       # para agentes de código
claude plugin install coderabbit                        # plugin de Claude Code
```

En el PR: `@coderabbitai review`, `full review`, `autofix`, `generate unit tests`, `pause`/`resume`. Poner `@coderabbitai ignore` en la descripción para saltear un PR.

**Trampas:**
- **Privacidad**: dicen que no entrenan con tu código, pero clonan el repo completo en un sandbox en la nube y guardan caché cifrada, embeddings y "learnings". Sólo en self-hosted se puede apagar toda la retención, y self-hosted es Enterprise con 500+ seats.
- **Antecedente de seguridad**: Kudelski Security encontró un RCE vía un `.rubocop.yml` malicioso en un PR, que exponía la clave privada de la GitHub App con escritura potencial a repos privados. Se arregló en una semana (ene-2025).
- Cada push que dispara un review incremental consume cupo. Más una "Fair Usage Policy" que puede espaciar reviews. Los PRs de más de 300 archivos no se soportan en ningún plan.
- El perfil `assertive` es ruidoso según sus propias docs; arrancar con `chill` o `quiet`.
- El viejo `ai-pr-reviewer` (MIT) ya no está público. Alternativa open source madura: `The-PR-Agent/pr-agent` (MIT, 13k stars).

Para pedir review a Codex desde Claude Code sin otro SaaS: [[codex-plugin-cc]].

**Licencia**: SaaS propietario (CodeRabbit Inc.); algunos repos auxiliares de la org son MIT o Apache-2.0
