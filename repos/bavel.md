---
title: bavel
url: https://github.com/ignaciochiappero/bavel
tags: [voice, translation, offline, docker, gemma, apache-2.0]
added: 2026-08-12
added_by: Denis
---

Fork de [gemma-translator](gemma-translator.md) orientado a uso en desktop/reuniones: mismo stack local (Moonshine STT + Gemma 4 vía LiteRT-LM + moonshine-voice TTS), más escucha de pestaña, transcripción streaming, sesiones persistentes y Docker.

## Por qué vale la pena

- **Escuchar pestaña (Meet, etc.)**: captura el audio de un tab del browser (no tu mic); traduce o transcribe en vivo. Atajo **T**.
- **Modo Transcripción**: subtítulos streaming con Moonshine incremental (~1 s), sin traducción ni voz — útil para seguir una sola persona.
- **Sesiones SQLite**: historial de charlas (guardar / recargar / nueva); en Docker viven en el volume `translator-data`.
- **Docker one-shot**: `docker compose up -d --build` (o `run.bat` en Windows); modelo ~5 GB se descarga una vez y sobrevive rebuilds. Pedí ≥8 GB RAM al Docker Desktop.
- **Mantiene el appliance Pi** del upstream (`deploy-pi.sh`, STLs) y suma tests (pytest backend mockeado + Vitest frontend).
- Repo chico (~4★) pero útil si el original se queda corto para meetings; conviene linkear ambos en el grafo Obsidian.

## Uso básico

```bash
docker compose up -d --build
# abrir http://localhost:3000
# o nativo: ./setup.sh && ./download_model.sh && ./start.sh
```

Modos: **Traducción** | **Transcripción**. Python 3.12+ si vas sin Docker.

**Licencia**: Apache 2.0
