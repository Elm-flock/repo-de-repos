---
title: opencode
url: https://github.com/anomalyco/opencode
tags: [coding-agent, cli, tui, agents, typescript, mit]
added: 2026-08-21
added_by: Lucas Mujica
---

Agente de coding open source para la terminal (TUI + CLI + app de escritorio + IDE + consola web) que corre contra cualquier proveedor de LLM del que tengas claves.

## Por qué vale la pena

- **199.9k stars**, ~456 contributors, **1.7 millones de descargas semanales** en npm. Es de los harnesses open source más usados que hay.
- **19 providers `@ai-sdk/*` incluidos**: anthropic, openai, google, google-vertex, amazon-bedrock, azure, groq, mistral, cerebras, cohere, deepinfra, perplexity, togetherai, xai, alibaba, vercel, gateway y openai-compatible. Más MCP y **ACP** (Agent Client Protocol).
- **Agente `plan` read-only de fábrica**: deniega ediciones y pregunta antes de correr bash. Se alterna con `build` (acceso total) apretando Tab. Es la separación que uno termina armando a mano en otros harnesses.
- **Monorepo Bun con 33 workspace packages** (`tui`, `desktop`, `server`, `sdk`, `plugin`, `enterprise`, `slack`, `console`, `codemode`, `protocol`…). El TUI se reescribió de Go/bubbletea a TypeScript sobre OpenTUI + Solid.
- App de escritorio en beta con `.dmg` (arm64/x64), `.exe`, `.deb`, `.rpm` y `.AppImage`.
- Releases varias veces por día: v1.18.20 y v1.18.21 salieron el mismo 21-ago-2026.

## Uso básico

```bash
brew install anomalyco/tap/opencode     # el tap va más al día que la formula oficial
curl -fsSL https://opencode.ai/install | bash
npm i -g opencode-ai@latest
```

**Cuidado con la confusión de nombres, que es real y grande:**

| Repo | Qué es | Estado |
|---|---|---|
| `anomalyco/opencode` | **El que la gente quiere.** TypeScript, 199.9k ★ | Activo, MIT |
| `sst/opencode` | Path viejo | Redirige al de arriba |
| `opencode-ai/opencode` | La implementación original en **Go**, 13.7k ★ | **Archivado** desde sep-2025 |
| `charmbracelet/crush` | Donde siguió el código Go, 27.6k ★ | Activo |
| `OpenCoder-llm/OpenCoder-llm` | Sin relación: un cookbook de code-LLMs | — |

El README del repo Go archivado lo dice: "el proyecto continuó bajo el nombre Crush, desarrollado por el autor original y el equipo de Charm". La org `sst` quedó como placeholder vacío apuntando a `anomalyco`.

**Otras cosas a saber:**
- **5.296 issues abiertos**, y varios releases por día: si necesitás reproducibilidad, pineá versión.
- El README avisa de desinstalar versiones anteriores a 0.1.x antes de instalar.
- La branch default es **`dev`**, no `main`.
- Hay un ecosistema grande de terceros **no afiliado** (awesome-opencode, opencode-antigravity-auth, oh-my-opencode-slim, opencode.nvim, opencode-plugin-openspec). El README pide que cualquier proyecto `opencode-*` aclare que no está afiliado.

Relacionado: [[pi]], [[codewhale]], [[rtk]] y [[deepseek-harness]] como otros harnesses de terminal; [[orca]] si lo que querés es correr varios en paralelo.

**Licencia**: MIT
