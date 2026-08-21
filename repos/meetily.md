---
title: meetily
url: https://github.com/Zackriya-Solutions/meetily
tags: [speech-to-text, audio, on-device, rust, typescript, mit]
added: 2026-08-21
added_by: Denis
---

App de escritorio (Tauri) que graba micrófono + audio del sistema, transcribe localmente con whisper.cpp o NVIDIA Parakeet, y resume con Ollama o un provider por API. No necesita cloud.

## Por qué vale la pena

- **Local de punta a punta si querés**: transcripción con whisper.cpp o Parakeet en tu máquina, y resumen con Ollama. Es la opción para reuniones que no pueden salir de la empresa.
- **Captura audio del sistema, no sólo el micrófono** — o sea graba también a los demás participantes, sin bot que entre a la llamada.
- **Aceleración por GPU compilada según plataforma**: Metal + CoreML en macOS, CUDA (NVIDIA) y Vulkan (AMD/Intel) en Windows y Linux.
- **El más maduro de su categoría**: 29.7k stars, creado en dic-2024, ~477.000 descargas acumuladas de assets entre todos los releases.
- Providers de resumen intercambiables: Ollama (local, el recomendado), Claude, Groq, OpenRouter o cualquier endpoint OpenAI-compatible.
- La v0.4.0 sumó modelos Qwen 3.5 incorporados, resúmenes multi-idioma, y pasó la telemetría a **opt-in**.

## Uso básico

Instaladores prearmados sólo para **Windows** (`.exe`/`.msi`) y **macOS Apple Silicon** (`.dmg`), con updater de Tauri. En **Linux hay que compilar**:

```bash
git clone https://github.com/Zackriya-Solutions/meeting-minutes
cd meeting-minutes/frontend && pnpm install && ./build-gpu.sh
```

(El repo se renombró de `meeting-minutes` a `meetily`; el clone viejo sigue redirigiendo.)

**Trampas importantes:**
- **El branch principal está parado desde el 05-jun-2026** (~11 semanas), con 349 issues y 134 PRs abiertos.
- **La diarización de hablantes está en conflicto entre fuentes**: la descripción del repo la anuncia y los topics incluyen `sortformer`, pero el README dice dos veces que está *planeada para la versión PRO*. Verificar antes de adoptarlo para reuniones multi-hablante.
- **Meetily PRO corre sobre otro codebase**: las features de pago (templates, export a PDF/DOCX, auto-join, calendario) no van a aterrizar en la versión open source.
- "Import & Enhance" está marcado Beta.

Código tomado de whisper.cpp, Screenpipe y transcribe-rs.

Relacionado: [[pocket-tts]] para el camino inverso (texto a voz), [[gemma4-transcribe]] para transcribir con audio nativo de un LLM.

**Licencia**: MIT
