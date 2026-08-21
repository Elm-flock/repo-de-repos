---
title: orca
url: https://github.com/stablyai/orca
tags: [ide, coding-agent, multi-agent, cli, typescript, mit]
added: 2026-08-21
added_by: Emiliano
---

App de escritorio (Electron) que corre muchos agentes de coding CLI en paralelo, cada uno en su propio git worktree aislado, dentro de un editor basado en VS Code con terminales y Chromium embebido. Trae app de celular para dirigir agentes de forma remota.

## Por qué vale la pena

- **El worktree aislado por agente es el punto**: podés tener varios agentes trabajando en paralelo sobre el mismo repo sin que se pisen entre ellos.
- **~28 agentes soportados**, no dos o tres: Claude Code, Codex, Grok, Cursor, Copilot, OpenCode, Kimi, Amp, Pi, oh-my-pi, Devin, Goose, Cline, Continue, Droid, Kiro, Qwen Code, Crush, Antigravity, Hermes Agent, y "cualquier agente CLI".
- **Ritmo de release brutal**: 1.074 tags en 5 meses. v1.4.187 salió el 21-ago-2026, v1.4.186 el 20, v1.4.185 el 19. El repo avisa que un PR mergeado tarda 48-72hs en llegar a un release.
- **50.5k stars en 5 meses** (creado 17-mar-2026), ~333 contributors. Binarios firmados para macOS (arm64/x64), Windows y Linux (AppImage, deb, rpm, x64 y arm64).
- **No trae modelos**: usás tus propias suscripciones. No hay costo de inferencia adicional.
- Modo headless con `orca serve` para Linux sin escritorio, y app iOS + APK de Android para seguir agentes desde el celular.

## Uso básico

```bash
brew install --cask stablyai/orca/orca     # macOS
yay -S stably-orca-bin                    # Arch (AUR)
orca serve                                # headless en Linux
```

**Advertencia sobre el estado del proyecto**: **4.338 issues y 2.280 PRs abiertos** de 11.606 PRs totales. Es un backlog sin revisar enorme para un proyecto de 5 meses — creciendo mucho más rápido de lo que puede mantener. Recolecta telemetría anónima (hay opt-out documentado).

Llegó al canal por dos videos de Fazt; Juan Pablo Oller comentó que lo usa y que ya abandonó los IDE. Ojo que **no tiene nada que ver con [[orcarouter]]**, a pesar del nombre.

Relacionado: [[herdr]] para coordinar varios agentes desde la terminal.

**Licencia**: MIT (Lovecast Inc.)
