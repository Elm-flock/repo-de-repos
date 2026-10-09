---
title: warp
url: https://github.com/warpdotdev/warp
tags: [cli, coding-agent, multi-agent, rust, agpl-3.0]
added: 2026-10-09
added_by: Guille
---

Warp empezó como terminal moderna para desarrollo con agentes y hoy vende primero **Warp Factories**: "software factories" en la nube que corren flotas de agentes de código sobre el SDLC. La terminal sigue existiendo, es gratis y desde abril de 2026 su cliente es open source. **Lo abierto es sólo el cliente: server, Drive, auth y la orquestación de agentes cloud siguen siendo propietarios, y Factories está en early access cerrado.**

## Por qué vale la pena

- **Cliente open source**: 65k stars, en Rust, abierto el 28-abr-2026. OpenAI figura como "founding sponsor" del repo. Ya hay forks: `zerx-lab/zap` (local-first), `the1812/warp-offline` y `mxcl/vorp` (sin las features "bonus").
- **Oz**, la plataforma de agentes cloud (lanzada en feb-2026): corre Claude Code y Codex en la nube. Factories se monta encima, definida como código (`factory.yaml` más agents, automations, runners, skills y webhooks), con un agente "Foreman" que coordina y se integra con Slack, Linear, Jira, GitHub y GitLab.
- **Terminal para agentes de terceros**: toolbar para Claude Code, Codex, Gemini CLI y Kiro CLI. Desde el 23-sep-2026 se puede usar el plan de ChatGPT con el agente de Warp.
- **Precios** (USD/mes):
  - Free: terminal completa, Agent CLI y BYO inference (sólo para individuos y orgs de hasta 10 personas).
  - Build: 20, con 20 de uso de agente a tarifa API. Max: 200, con 200 de uso.
  - Business: 50 por usuario, hasta 25 asientos, SAML SSO.
  - Factories pay-as-you-go: 0 de base, con el uso facturado 20% por encima de la tarifa API.
- macOS, Linux (deb, rpm, Arch, AppImage; x64 y ARM64) y Windows 10/11. Releases semanales.

## Uso básico

```bash
brew install --cask warp          # o: winget install Warp.Warp
curl -fsSL https://app.warp.dev/download/agent-cli | bash    # Agent CLI
```

Repos abiertos relacionados en la org: `oz-agent-worker` (MIT, workers self-hosted), `oz-sdk-python` y `oz-sdk-typescript` (Apache-2.0) y `claude-code-warp` (MIT).

**Trampas:**
- Drive sync, los agentes con modelos hosteados y las features de equipo dependen del backend de Warp y de una cuenta.
- Los GitHub Releases sólo muestran builds dev; los stable se bajan de warp.dev.
- AGPL: si modificás el cliente y lo distribuís o lo hosteás, tenés que liberar los cambios. Para contribuir hay que firmar un CLA.

En el canal surgió como ejemplo de "ambientes aislados de desarrollo" en la nube. Alternativas locales para correr varios agentes: [[orca]] y [[herdr]].

**Licencia**: AGPL-3.0 el cliente, MIT los crates de UI (`warpui_core`, `warpui`); server y servicios cloud propietarios
