---
title: openshorts
url: https://github.com/mutonby/openshorts
tags: [video, generative, self-hosted, python, mcp]
added: 2026-09-02
added_by: Emiliano
---

Plataforma de video con IA que corta videos largos en shorts 9:16: detección de momentos, face tracking, subtítulos y doblaje, más generación de UGC con actores IA. Self-hosted con Docker.

## Por qué vale la pena

- **Se puede correr entero en tu máquina** con `docker compose up`, sin cuenta ni SaaS de por medio — el dashboard queda en `localhost:5175`.
- **Trae servidor MCP propio** (`mcp_server.py`, con `server.json` del registro MCP `2025-12-11`) y un skill de agente en `skills/openshorts`, así que se puede manejar desde Claude Code en vez de por UI.
- **Stack de piezas conocidas y reemplazables**: FastAPI + Gemini 3.1 Flash-Lite para elegir momentos, faster-whisper para transcribir, YOLOv8 + MediaPipe + OpenCV para el face tracking, yt-dlp, FFmpeg y Remotion para render.
- **Muy activo**: 3.829 stars, 400 commits propios y último push del 2-sep-2026 (el mismo día que lo miramos).
- Soporte opcional de GPU NVIDIA vía `docker-compose.override.yml` + NVIDIA Container Toolkit.

## Uso básico

```bash
git clone https://github.com/mutonby/openshorts.git && cd openshorts
cp .env.example .env
docker compose up --build        # dashboard en http://localhost:5175
claude mcp add --transport http openshorts http://localhost:8000/mcp
```

(El README dice `cd OpenShorts` después del clone, pero el directorio que se crea es `openshorts` — el comando está mal.)

## Advertencias

- **La licencia no es MIT limpia, aunque el badge diga eso.** El `LICENSE` es MIT **con una excepción**: los 24 archivos bajo `cloud/` (billing, metering, api_keys, oauth, analytics…) están bajo la "OpenShorts Commercial License" source-available — podés self-hostear para uso personal o interno, pero **no ofrecerlo a terceros como servicio hosted, ni revender, ni remover o eludir el billing/metering**. Es una cláusula anti-competencia tipo BSL. GitHub no la puede clasificar y devuelve `NOASSERTION`.
- **No es gratis en la práctica**: la API key de Gemini es requerida para todas las features de IA (podés apuntar `LLM_BASE_URL` a Ollama, pero solo para el picker de momentos). fal.ai, ElevenLabs y Upload-Post son requeridas para AI Shorts, doblaje y publicación.
- **Es el funnel de un SaaS pago**: hosted desde $12/mes con free tier de 20 min/mes y watermark. Buena parte del README es marketing comparativo contra Opus Clip, CapCut, Vizard, Klap y Descript.
- **Todos los números son del vendor, sin verificación independiente**: 5-8 min por video de 8 min en CPU vs ~50 s en su GPU, ~$0.65/video en modo Low Cost y ~$2 en Premium.
- **Sin releases ni tags**, solo `main` — para un repo de 89 MB con Docker eso complica la reproducibilidad. El CI viene mixto (varias corridas en failure el 1 y 2 de sep).
- **Un solo dev real**: GitHub atribuye 7 contributors, pero 87 de los últimos 100 commits tienen un author sin cuenta de GitHub asociada. Los 1.005 forks están inertes.
- Es técnicamente un fork de `kamilstanuch/Autocrop-vertical` (YOLOv8+FFmpeg, 336 stars), aunque reescrito por completo.
- `docs/` tiene solo dos archivos y son legales (aviso DSA y sección DMCA de Upload-Post), lo que sugiere exposición a reclamos de contenido del servicio hosted.

Relacionado: [[minimax-h3]] y [[fluxrt]] para generación de video, [[ai-avatar-system]] para el lado de avatares.

**Licencia**: MIT para el core, con `cloud/` bajo "OpenShorts Commercial License" (source-available, prohíbe ofrecerlo como servicio a terceros)
