---
title: gemma4-transcribe
url: https://github.com/hanneshapke/gemma4-transcribe
tags: [speech-to-text, gemma, audio, python, javascript, apache-2.0]
added: 2026-08-21
added_by: Emiliano
---

Demo mínima que transcribe voz usando el **audio nativo de Gemma 4**, sin modelo ASR aparte: recorder en el browser + backend FastAPI que llama a `google/gemma-4-E2B-it`.

## Por qué vale la pena

- **El valor es la referencia, no el producto**: muestra cómo invocar audio nativo en Gemma 4 vía `pipeline("any-to-any", ...)` de `transformers`, sin encadenar Whisper + LLM. Las variantes E2B y E4B aceptan audio directamente.
- **Escala honesta**: **4 stars, 0 forks, creado y pusheado el mismo día (09-abr-2026)**. Es un scratch demo de una tarde, no software mantenido — sirve para copiar el patrón, no para depender de él.
- **6 archivos en total**: `server.py` (4 KB) y un componente JSX (27 KB). React 18 por CDN con Babel transpilando en el browser, sin build step — se lee de punta a punta en minutos.
- **API de dos endpoints**: `GET /` sirve la SPA, `POST /transcribe` toma `multipart/form-data` webm y devuelve `{"text": "..."}`.
- Tiene **demo mode** con transcripciones simuladas, así que se puede explorar el frontend sin cargar el modelo.

## Uso básico

```bash
git clone https://github.com/hanneshapke/gemma4-transcribe.git && cd gemma4-transcribe
brew install ffmpeg          # o: apt install ffmpeg
uv sync && uv run server.py  # http://localhost:8080
```

**ffmpeg es dependencia dura del sistema**: convierte el `.webm` del browser a `.wav` porque librosa/soundfile no leen webm. Requiere Python 3.10+, `uv`, y GPU con VRAM suficiente para Gemma 4 E2B (en CPU corre, lento).

Detalle curioso: `pillow` y `torchvision` están en las dependencias sólo para satisfacer imports incondicionales de `Gemma4Processor` y `Gemma4VideoProcessor`, no porque se usen.

Relacionado: [[bavel]] y [[gemma-translator]], otros usos de Gemma para voz offline.

**Licencia**: Apache-2.0
