---
title: gemma-translator
url: https://github.com/google-gemma/gemma-translator
tags: [translation, speech-to-text, tts, on-device, raspberry-pi, gemma, litert-lm]
added: 2026-08-15
added_by: Denis
---

Traductor de voz on-device y offline de Google, pensado como appliance de hardware (Raspberry Pi 5 + pantalla chica) más que como app de escritorio. Corre `gemma4-e2b` local vía LiteRT-LM, con Moonshine para STT/TTS.

## Por qué vale la pena

- **100% local**: una vez descargado el modelo (`gemma4-e2b` vía LiteRT-LM), no necesita internet.
- **Pensado para kiosco físico**: UI retro-terminal optimizada para pantallas chicas (480x320), con `deploy-pi.sh` que arma un servicio systemd + Chromium en modo kiosko en una Raspberry Pi 5.
- **Modo conversación de dos carriles**: dos personas enfrentadas, cada una habla su idioma y escucha la traducción en el suyo (landscape "active person" o modos alternativos).
- **Stack**: frontend React/Vite + servidor Python (`http.server`) que orquesta LiteRT-LM y Moonshine.
- Requiere hardware específico (Pi 5 8GB + mic + speaker + display) — no es para correr en cualquier laptop sin adaptar.

## Uso básico

```bash
chmod +x setup.sh download_model.sh start.sh deploy-pi.sh
./setup.sh
./download_model.sh
./start.sh          # dev: UI en :5173, API/LiteRT-LM en :3000/:9379
./start.sh --prod   # sirve frontend compilado desde backend/server.py en :3000
```

Para deploy permanente en Raspberry Pi: `./deploy-pi.sh`.

Relacionado: [[utopiaia-translator]], que es una versión web (browser, WebGPU, sin instalación) del mismo concepto de "Gemma Translator".

**Licencia**: Apache 2.0
