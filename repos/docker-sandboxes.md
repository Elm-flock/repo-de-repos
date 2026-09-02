---
title: docker-sandboxes
url: https://docs.docker.com/ai/sandboxes
tags: [sandbox, coding-agent, docker, cli, security]
added: 2026-09-02
added_by: Juan Martin
---

CLI `sbx` de Docker Inc. que corre agentes de coding (Claude Code, Codex, Gemini CLI, OpenCode) dentro de microVMs con kernel, filesystem, red y daemon Docker propios.

## Por qué vale la pena

- **Es un CLI aparte, no una feature de Docker Desktop**: la doc de instalación es explícita en que no necesitás Docker Desktop ni Docker Engine para usar `sbx`.
- **Aislamiento por hypervisor, no por namespaces** — la doc lo tabula así contra las alternativas basadas en contenedores. Cinco capas: kernel separado, proxy de red deny-by-default, Docker Engine aislado, workspace clonado opt-in (`--clone`) e inyección de credenciales por headers.
- **Gratis, incluido uso comercial.** Lo único pago es el governance a nivel de organización (políticas centralizadas), que va por suscripción separada.
- **Ritmo de release alto**: 160 releases desde el 3-mar-2026; último estable v0.39.0 (19-ago-2026), con RCs semanales (v0.42.0-rc4 el 2-sep-2026).
- Entornos declarativos vía `.sbxenv.yaml` (marcado experimental) para reproducir el sandbox por proyecto.

## Uso básico

```bash
brew trust docker/tap && brew install docker/tap/sbx     # macOS
winget install -h Docker.sbx                             # Windows
curl -fsSL https://get.docker.com | sudo SBX=1 sh        # Ubuntu
sudo usermod -aG kvm $USER && newgrp kvm                 # Linux: hace falta KVM
sbx login
sbx run claude
sbx ls / sbx prune / sbx secret set
```

**Las trampas, que salen de la propia página de seguridad de Docker**:

- **El modo por defecto no aísla tus archivos**: "el agente edita los mismos archivos que ves en tu host". Eso incluye git hooks, configs de CI y `Makefile` que se ejecutan implícitamente y **no aparecen en `git diff`**. El workspace clonado es opt-in.
- **Los MCP servers stdio locales corren FUERA de la VM**, con permisos y aislamiento del host, no del sandbox.
- Los dominios permitidos por defecto incluyen wildcards amplios: `*.googleapis.com` cubre muchos servicios más allá de las APIs de IA.
- Las skills compartidas son un store read-write entre sandboxes: uno puede modificar instrucciones o scripts que otro agente use después.
- **Propietario** y pre-1.0 de facto: 309 issues abiertas, varias features marcadas experimentales, y sin build para Intel Mac (macOS pide Sonoma 14+ en Apple Silicon).

Alternativas en este repo: [[nono]] (más liviano, aislamiento a nivel de proceso), [[dory]] (microVM pero solo macOS y GPL). Para aislar por git worktree en vez de por VM, [[orca]].

**Licencia**: propietaria (Copyright © 2026 Docker Inc., all rights reserved)
