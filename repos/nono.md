---
title: nono
url: https://github.com/nolabs-ai/nono
tags: [sandbox, agents, security, rust, apache-2.0]
added: 2026-09-02
added_by: Juan Martin
---

Sandbox para correr agentes de IA con enforcement a nivel de kernel (Landlock en Linux, Seatbelt en macOS), sin daemon, sin contenedor y sin VM. Escrito en Rust por el equipo detrás de Sigstore.

## Por qué vale la pena

- **No necesita contenedor ni VM**: aplica restricciones al proceso directamente vía primitivas del kernel, así que arranca sin overhead de imagen ni daemon corriendo.
- **Perfiles reutilizables por herramienta**: `nono search opencode` busca en un registry (`registry.nono.sh`) y los perfiles se extienden en vez de escribirse de cero.
- **3.922 stars y 88 contributors** en 7 meses (creado 31-ene-2026), con 30 releases — la v0.75.0 salió el 1-sep-2026.
- **Bindings oficiales en 4 lenguajes**: `nono-py`, `nono-ts`, `nono-go`, más `langchain-nono` (backend de sandbox para LangChain Deep Agents) y una GitHub Action (`agent-sign`).
- **Adopción de terceros verificable**: `guarddog` de DataDog lo usa en sus evals para escanear paquetes maliciosos; `kubefence` embebe el binario; está empaquetado en `numtide/llm-agents.nix`.

## Uso básico

```bash
curl -fsSL https://nono.sh/install.sh | sh
brew install nono                                        # está en homebrew-core
nono search opencode
nono run --profile nolabs-ai/opencode -- opencode
nono profile init opencode --extends nolabs-ai/opencode   # perfil propio
```

**Advertencia importante sobre el aislamiento**: es más débil de lo que sugiere la palabra "sandbox", y la doc del propio proyecto lo admite — es control de capacidades **a nivel de proceso**, "no crea un límite separado de kernel ni de hardware". Gaps documentados: `stat`/`access` no se interceptan (se puede enumerar el filesystem), los file descriptors ya abiertos bypassean seccomp, el filtro seccomp solo cubre `openat`/`openat2`, **Landlock no puede filtrar por IP** (solo puertos TCP), y no aísla namespaces de PID ni de usuario. Si querés un límite real de kernel, [[dory]] o [[docker-sandboxes]] usan microVM.

Otras dos trampas: es pre-1.0 declarado ("API changes may still occur") y el proyecto **migró de namespace dos veces** (`lukehinds/nono` → `always-further/nono` → `nolabs-ai/nono`), así que hay URLs viejas circulando y los perfiles del registry viejo hay que reinstalarlos. Windows solo vía WSL2; Linux requiere 5.13+ para Landlock.

**Licencia**: Apache-2.0
