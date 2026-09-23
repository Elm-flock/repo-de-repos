---
title: meet2notes
url: https://github.com/estebanstifli/Meet2Notes
tags: [speech-to-text, audio, on-device, self-hosted, python, mit]
added: 2026-09-23
added_by: Denis
---

Asistente de reuniones local-first: graba, transcribe, separa hablantes (diarización) y arma notas con un LLM local, desde una UI web en `127.0.0.1`. **Es alpha, de un solo autor (Esteban García), con 14 stars y 2 meses de vida.**

## Por qué vale la pena

- **Diarización incluida y open source**, que es lo que le falta a [[meetily]] (ahí es una feature de la versión PRO). Por defecto usa Sherpa-ONNX, con Pyannote Community-1 o `diarize` como alternativas.
- **Catálogo de modelos intercambiables**:
  - ASR: Faster Whisper (tiny a large-v3, `small` por defecto), NVIDIA Parakeet TDT 0.6B v3, Nemotron ASR 0.6B y VibeVoice ASR BitNet.
  - Notas: LLM local vía llama.cpp (LFM2.5 1.2B Q4 por defecto, Qwen3 0.6B/1.7B o un GGUF propio) o remoto vía LiteLLM (Ollama, LM Studio o endpoints compatibles con OpenAI).
- **Búsqueda sobre reuniones pasadas**: embeddings BGE-M3 en SQLite + sqlite-vec, combinados con FTS5.
- **Servidor MCP stdio de sólo lectura** (desde la v0.6.0) para consultar las reuniones desde Claude Desktop, Codex, VS Code o Cursor.
- **Corre en Linux**, a diferencia de Meetily, que en Linux hay que compilar. La CI corre en Ubuntu, Windows y macOS con Python 3.11 y 3.13, y trae instalador para Linux con backend CPU o CUDA.
- Webhooks con firma HMAC, API de plugins, 9 formatos de nota y sin telemetría declarada.

## Uso básico

```bash
git clone https://github.com/estebanstifli/Meet2Notes.git && cd Meet2Notes
./install.sh --ai-backend cpu     # o --ai-backend cuda
.venv/bin/meet2notes --no-browser # http://127.0.0.1:8765
```

En Windows se instala con `install-update.bat`. También está en Pinokio. No está publicado en PyPI.

**Trampas:**
- En Linux, capturar el audio del sistema (el otro lado de la llamada) puede exigir configurar PulseAudio/PipeWire y ALSA a mano (`~/.asoundrc`, `libasound2-plugins`). El propio doc aclara que la captura está testeada sólo con drivers simulados.
- Pyannote Community-1 es un modelo gated en Hugging Face: hay que aceptar condiciones y usar un token. Cada modelo del catálogo tiene su propia licencia.
- El actualizador hace `git pull` a tags `vX.Y.Z` y necesita un checkout limpio.

Relacionado: [[meetily]] es la opción madura de la categoría (29.7k stars), [[gemma4-transcribe]] transcribe con el audio nativo de un LLM.

**Licencia**: MIT (los modelos que descarga tienen licencias propias)
