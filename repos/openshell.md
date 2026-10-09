---
title: openshell
url: https://github.com/NVIDIA/OpenShell
tags: [sandbox, agents, security, rust, nvidia, apache-2.0]
added: 2026-10-09
added_by: Emiliano
---

Runtime y sandbox de NVIDIA para correr flotas de agentes autónomos con políticas declarativas de archivos, red y procesos aplicadas a nivel kernel (Landlock y seccomp). **No requiere GPU ni hardware NVIDIA, pero sigue en 0.x, la actualización desde 0.0.x obliga a recrear todos los sandboxes, y la telemetría viene activada.**

## Por qué vale la pena

- **Políticas verificadas antes de aplicarse**: un "prover" valida formalmente cada cambio de política antes de aprobarlo. La política por defecto niega toda la red.
- **Credenciales que no se filtran al agente**: sólo se inyectan en requests a endpoints aprobados. Drivers para Vault, un credstore en base de datos y secrets de Kubernetes.
- **Varios backends**: Docker 28+, Podman 5.x, Kubernetes 1.29+ vía Helm y MicroVM con libkrun (KVM o Hypervisor.framework). GPU opcional con `--gpu N`.
- **Perfiles de provider listos** para Claude Code, Codex, Copilot, Cursor, Anthropic, OpenAI, OpenRouter, Bedrock, Vertex AI y otros. El tutorial inicial usa [[opencode]] con un modelo gratis de OpenRouter.
- SDKs en Python (`openshell` en PyPI), TypeScript, Go y Rust. 15,5k stars; último stable v0.1.2 (28-sep-2026), con releases semanales.
- Comunidad: `NVIDIA/NemoClaw` (22,7k stars) corre Hermes, LangChain Deep Agents y OpenClaw adentro de OpenShell; `langchain-ai/openshell-deepagent`; un operador para OpenShift; y un curso gratis de NVIDIA DLI disponible en español.

## Uso básico

```bash
curl -LsSf https://raw.githubusercontent.com/NVIDIA/OpenShell/main/install.sh | sh   # fijar versión: OPENSHELL_VERSION=v0.1.2
openshell sandbox create --name demo
openshell sandbox create --from <imagen-oci> -- claude
openshell provider profile import -f providers/github.yaml --global
OPENSHELL_TELEMETRY_ENABLED=false
```

**Trampas:**
- Requiere kernel Linux 6.2+ con Landlock ABI 3; si no lo encuentra, falla cerrado. En macOS corre dentro de la VM de Docker Desktop. No soporta Mac Intel; en Windows (WSL2) es experimental.
- La imagen por defecto es un Ubuntu mínimo sin ningún agente: hay que armarse una imagen propia.
- El SDK de TypeScript está en GitHub Packages, no en npmjs. El snap choca con el snap de Docker.

Otros sandboxes para agentes en este repo: [[nono]] (Landlock/Seatbelt sin daemon ni contenedor) y [[docker-sandboxes]] (microVMs). [[nooa]] recomienda correr su código generado acá adentro.

**Licencia**: Apache-2.0
