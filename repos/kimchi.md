---
title: kimchi
url: https://github.com/getkimchi/kimchi
tags: [coding-agent, cli, llm, saas, typescript, apache-2.0]
added: 2026-08-21
added_by: Emiliano
---

Agente de coding de terminal que delega cada fase de la tarea a un modelo distinto de un pool (casi todos open-weight), etiquetando cada request para atribuir costo y aplicar presupuesto.

## Por qué vale la pena

- **Un modelo por rol, con defaults explícitos**: orchestrator, planner y researcher usan `kimi-k2.6`; el pool de builder y reviewer combina kimi-k2.6 con `minimax-m2.7`; el explorer usa `nemotron-3-ultra-fp4`. La idea es no pagar modelo caro para tareas baratas.
- **Gobierno de gasto de verdad**: `/tags key:value` (hasta 10 tags de 64 chars) más tags automáticos de `model:` y `phase:`, con monitoreo de presupuesto y RBAC en el plan Teams.
- **`/ferment` es una máquina de estados real** (`draft→planned→running→paused→complete`) con event log append-only que guarda hashes de estado pre y post. No es un wrapper de prompts.
- **Precios de tokens publicados** (in/out por 1M): deepseek-v4-flash $0.14/$0.28, minimax-m3 $0.30/$1.20, nemotron-3-ultra-fp4 $0.60/$3.60, kimi-k2.7 $0.95/$4.00, glm-5.2-fp8 $1.40/$4.40.
- **Construido sobre el SDK de [[pi]]** (`@earendil-works/pi-coding-agent` 0.84.1, de Mario Zechner) con 4 dependencias parcheadas, no desde cero.
- Binarios compilados con `bun build --compile`, sin runtime: macOS, Linux y Windows, con `checksums.txt` SHA256.
- Compresión de output de bash estilo [[rtk]], con 60-90% de reducción de contexto reportada.

## Uso básico

```bash
brew install getkimchi/tap/kimchi
kimchi setup
```

Planes: Community $0, Coder **$20/mes** con $25 de crédito, Teams **$35/seat/mes** con $45, Enterprise con VPC self-hosted.

**Qué es open source y qué no**: el CLI es Apache-2.0, **el gateway y la consola son SaaS propietario**. Necesita `KIMCHI_API_KEY` y el catálogo de modelos se baja al arrancar desde su metadata service — no hay camino offline ni de modelos locales documentado. Hay BYOK, pero ruteado por su gateway.

**Otras trampas:**
- **v1.0.0 salió el 21-ago-2026, con horas de vida.** v0.1.97 a v1.0.0 pasaron en ~48hs. Cero track record de la línea 1.x.
- **La landing contradice al repo en los IDs de modelo**: el sitio anuncia Kimi K2.7 / MiniMax M3 / Nemotron-3-Super-FP4, el README trae kimi-k2.6 / minimax-m2.7 / nemotron-3-ultra-fp4. No citar la página de marketing.
- **No está en npm** (`@kimchi-dev/cli` da 404): sólo Homebrew o script de release.
- El LSP incorporado cubre únicamente `typescript-language-server` y `gopls`.
- `/teleport` no funciona en Windows. Contribuir requiere firmar CLA.

**Licencia**: CLI Apache-2.0 (CAST AI Group); gateway y consola propietarios
