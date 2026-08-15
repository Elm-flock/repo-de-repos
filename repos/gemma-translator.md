---
title: gemma-translator
url: https://github.com/google-gemma/gemma-translator
tags: [voice, translation, offline, gemma, raspberry-pi, apache-2.0]
added: 2026-08-12
added_by: Denis
---

Traductor de voz on-device y fully offline: **Gemma 4** (`gemma4-e2b` vía LiteRT-LM) + **Moonshine** STT/TTS. UI web estilo terminal pensada para pantallas chicas (p. ej. 480×320). Proyecto de Google Creative Lab (no producto oficial de Google). Upstream de [bavel](bavel.md).

## Por qué vale la pena

- **Offline real post-setup**: inferencia local con LiteRT-LM; sin cloud ni API keys después de bajar el modelo.
- **Kiosk de dos carriles**: dos personas/idiomas cara a cara; push-to-talk, revolver de idiomas, modos landscape (persona activa) y vertical (dos manos).
- **Appliance Pi**: target Raspberry Pi 5 8 GB + mic + speaker + display; `deploy-pi.sh` arma systemd + Chromium kiosk. Incluye STLs de carcasa en `stl/`.
- **Stack unificado**: un `start.sh` levanta LiteRT-LM (:9379), API Python (:3000) y frontend React/Vite (:5173 en dev).
- **Hecho con Antigravity** (según el README): buen ejemplo de referencia para demos edge de traducción por voz.

## Uso básico

```bash
chmod +x setup.sh download_model.sh start.sh deploy-pi.sh
./setup.sh            # venv + deps (Python 3.10+, Node 18+)
./download_model.sh   # gemma4-e2b → LiteRT-LM
./start.sh            # o ./start.sh --prod
# appliance: ./deploy-pi.sh
```

UI: `http://localhost:5173` (dev) o `:3000` (prod). Linux/macOS.

**Licencia**: Apache 2.0
