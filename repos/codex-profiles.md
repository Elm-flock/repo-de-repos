---
title: codex-profiles
url: https://github.com/Ducksss/codex-profiles
tags: [cli, codex, openai, shell, mit]
added: 2026-10-09
added_by: Guille
---

CLI en Bash para tener perfiles nombrados de Codex CLI (por ejemplo personal y trabajo), cada uno con su propio `CODEX_HOME`, login, sesiones y config, y para atar cada directorio de proyecto a un perfil. No es un switcher de tokens: nunca lee ni copia tokens ni cookies. **La separación es sólo de estado local, no es un límite de seguridad ni de cuenta** (lo dice el README).

## Por qué vale la pena

- **Un perfil por `CODEX_HOME`**: `default` usa `~/.codex`, `work` usa `~/.codex-work`, y así. No hay magia: es la variable de entorno que Codex ya soporta, administrada por vos.
- **`workspace bind`**: atás un directorio a un perfil y `codex-profile run` elige solo.
- **En macOS** abre ventanas separadas de ChatGPT Desktop con estado local aparte, y tiene una app de barra de menú en Swift que muestra la cuota restante por perfil. Sólo se compila desde el código (`make menu-app`).
- Un único script de ~4.700 líneas que sólo usa herramientas estándar. Integración con bash, zsh y fish. macOS y Linux.

## Uso básico

```bash
npm install -g codex-profile          # singular: "codex-profiles" en npm es OTRO proyecto
# o: brew install Ducksss/tap/codex-profile
codex-profile setup work
codex-profile cli work exec "review this repo"
codex-profile workspace bind . work && codex-profile run
eval "$(codex-profile shell-init zsh --prompt --completions)"
```

**Trampas:**
- Los comandos de instalación standalone y Nix del README apuntan a v1.3.0, que no existe (404). Usá v1.2.0 (15-sep-2026).
- El login de ChatGPT Desktop y el del CLI son independientes, y la herramienta no verifica que sean la misma cuenta.
- Una vez por día consulta npm por updates (`CODEX_PROFILE_NO_UPDATE_CHECK=1` para apagarlo).
- 179 stars, un solo mantenedor, no oficial de OpenAI. Si lo que querés es switchear cuentas, hay alternativas más grandes: `Loongphy/codex-auth` (2,8k stars) y `Dicklesworthstone/coding_agent_account_manager` (Claude Code, Codex y Gemini).

Relacionado: [[codex-plugin-cc]] para usar Codex desde Claude Code.

**Licencia**: MIT
