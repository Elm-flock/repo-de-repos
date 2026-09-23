---
title: muse-code
url: https://dev.meta.ai/products/muse-code
tags: [coding-agent, cli, multi-agent, meta, saas]
added: 2026-09-23
added_by: Emiliano
---

Agente de código de terminal de Meta, en beta, multi-agente y movido por su modelo propietario Muse Spark (hoy 1.3). **El CLI es cerrado y pago, y exige cuenta de Meta**: lo único open source es el SDK.

## Por qué vale la pena

- **Barato para probar**: el plan Everyday cuesta $5/mes (10-50 prompts cada 5 h), High $15 (5×) y Power $50 (20×). Por API, `muse-spark-1.3` sale $1.25 input / $4.25 output por millón de tokens, con 1M de contexto.
- **Agentes de fondo persistentes** y un event log local "replay-exact" que permite retomar una sesión después de un crash.
- **Subagentes en worktrees aislados**, más skills incluidas `/plan`, `/grill` y `/goal`.
- **Entrada multimodal, incluido video.**
- SDK abierto `@muse-code/sdk` (MIT, Developer Preview) para manejarlo desde código. Integraciones de la comunidad: la GUI `helicon` y el proxy `CLIProxyAPI`, que lo expone como API compatible OpenAI.

## Uso básico

```bash
curl -fsSL https://dev.meta.ai/install.sh | bash   # instala el launcher `muse` en ~/.local/bin
muse
```

**Trampas:**
- **El plan de $5 se agota rápido**: el video de Fazt Code que lo trajo al canal tiene un capítulo "Después de 30-40 min: cuota agotada".
- **No hay Windows nativo**: el launcher sólo acepta macOS y Linux, en arm64 y x86_64. El video lo instala vía WSL, aunque la página oficial promete Windows.
- **La variante barata de la API (`-contributor`, $0.10 / $0.20) usa tus datos para entrenar.**
- Algunos blogs dicen que el CLI es open source y gratis durante el rollout. No lo pudimos confirmar: la página oficial sólo muestra planes pagos y no hay repo público.

Relacionado: [[muse-glimmer]] es el modelo open-weights de Meta destilado de Muse Spark. Alternativas abiertas: [[opencode]], [[pi]], [[deepseek-harness]].

**Licencia**: propietaria (términos de servicio de Meta); el SDK `meta-models/muse-code-sdk` es MIT
