---
title: fluxrt
url: https://github.com/tensorforger/FluxRT
tags: [realtime, generative, diffusion, cuda, python, unlicense]
added: 2026-08-05
added_by: Denis
---

Pipeline de edición de video/webcam en tiempo real con **FLUX.2-klein-4B** (instruct image editing), optimizado para GPUs consumer. Alternativa a Stream Diffusion con conditioning por imagen de referencia y prompts interactivos.

## Por qué vale la pena

- **Latencia usable en vivo**: a 512×512 reporta ~20–40 FPS / ~0.2 s e2e en RTX 5090 y ~15–30 FPS / ~0.3 s en RTX 4090.
- **Spatial KV Cache** propio para rectified flow: reusa tokens entre frames (texto, referencia y regiones espaciales estáticas); en la práctica solo recomputea ~20–50% de tokens. En 576×320, cache ON pasa de 20→50 FPS con poco movimiento.
- **Instruct editing + referencias nativas de FLUX.2**: no es solo estilo genérico; sirve para try-on, VTubing y workflows con imagen de ropa/referencia en vivo.
- **Salida a apps reales**: GUI con virtual webcam (OBS/Zoom/Chrome/TouchDesigner/Resolume); en Windows también Spout (`FluxRTOutput`). Plugin para Daydream Scope.
- **Extensiones concretas**: TAEF2 (decode rápido), Flow Upscaler 2×, int8 para ~24 GB VRAM, LoRA, LivePortrait para lip transfer.
- **API de integración**: `StreamProcessor` con shared memory + multiproceso (I/O, inferencia, scheduler de frames interpolados con RIFE).

## Uso básico

Requisitos: NVIDIA RTX 4090+ (mín. ~20 GB VRAM con int8; 32 GB recomendado), CUDA 12.8, Python 3.12, conda o uv, git-lfs. Modelos: `FLUX.2-klein-4B` + `RIFE-safetensors` (clones en la raíz del repo).

```bash
git clone https://github.com/tensorforger/FluxRT
cd FluxRT
# Linux: sh scripts/install.sh  |  Windows: scripts/install.bat
conda activate fluxrt
python scripts/run_gui.py          # o --int8
# python scripts/run_gradio_demo.py
# python scripts/process_local_video.py --input in.mp4 --output out.mp4 --prompt "..."
```

En Linux la virtual cam necesita `v4l2loopback`; en Windows, OBS.

**Licencia**: Unlicense
