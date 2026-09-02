---
title: dory
url: https://github.com/Augani/dory
tags: [sandbox, docker, cli, swift, gpl-3.0]
added: 2026-09-02
added_by: Francisco
---

Runtime local completo para macOS en Apple Silicon: motor Docker nativo, Compose, k3s, VMs Linux con escritorio y sandboxes de agentes con políticas. Pensado como reemplazo de Docker Desktop / OrbStack.

## Por qué vale la pena

- **Los sandboxes de agentes son VMs headless dedicadas**, no namespaces: sin archivos del host por defecto, non-root, mounts read-only y política de red `none` por defecto (o `outbound` con allowlist). Aislamiento más fuerte que [[nono]].
- **Trae el stack entero**: Docker 29 API/CLI, Buildx, BuildKit, Compose v2, k3s con presets v1.34/v1.35/v1.36, y VMs de Ubuntu 24.04 LTS GNOME, Debian 13 Xfce, Kali Xfce y Alpine headless.
- **Sin cuenta, sin cloud, sin telemetría y sin tier comercial** — el README es explícito: no requiere Docker Desktop, gestor de VM externo, cuenta, control plane en la nube ni licencia paga para uso comercial.
- **Migración desde lo que ya tenés**: importa de Docker Desktop, OrbStack, Colima, Rancher Desktop y Podman. Crea el contexto Docker `dory` apuntando a `~/.dory/dory.sock`, así que el CLI de Docker existente sigue funcionando.
- Expone un modo MCP read-only y un `llms-full.txt` para que los agentes lo operen.

## Uso básico

```bash
brew install --cask Augani/dory/dory
dory sandbox run --json --network none --rollback -- /bin/sh -lc 'uname -a'
dory sandbox run --json --mount "$PWD:/workspace" -- /bin/sh -lc 'ls /workspace'
dory sandbox create my-project --workspace .
dory sandbox capabilities my-project --json
```

**Las advertencias**: es **solo Apple Silicon con macOS 14+** — el README aclara que ni los downloads ni el cask traen build para Intel. **Bus factor 1**: un único contributor (`Augani`, 909 commits) sobre 1.561 stars, y va por la 0.4.x. Y hay una inconsistencia concreta: el README documenta la 0.4.6 y linkea su `.dmg`, pero ese URL da 404 y el último release publicado es **v0.4.5 (13-ago-2026)** — los docs van adelante del release real. Varios componentes (Kubernetes, Linux Machines, escritorios) se descargan aparte, la app base no los trae.

**Licencia**: GPL-3.0
