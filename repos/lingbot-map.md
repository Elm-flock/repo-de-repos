---
title: lingbot-map
url: https://github.com/Robbyant/lingbot-map
tags: [3d-reconstruction, image-to-3d, vision, cuda, python, apache-2.0]
added: 2026-08-21
added_by: Emiliano
---

Modelo feed-forward de reconstrucción 3D en streaming: le das un video o una carpeta de imágenes y devuelve poses de cámara + una nube de puntos densa, de forma incremental y sin optimización por escena.

## Por qué vale la pena

- **~20 FPS a 518×378** sobre secuencias de **más de 10.000 frames**, usando atención con paged-KV-cache (FlashInfer). El demo del repo procesa un recorrido interior de ~25.000 frames (13 minutos).
- **Feed-forward, sin optimización por escena**: la diferencia práctica con NeRF/3DGS es que no hay que entrenar nada por cada escena nueva.
- Paper "Geometric Context Transformer for Streaming 3D Reconstruction" (arXiv 2604.14141), 11 autores. Benchmarks publicados para KITTI, Oxford Spires, VBR, Droid-W, TUM-D, 7-scenes, ETH3D, Tanks and Temples y NRGBD.
- 16.6k stars en 4 meses (creado 15-abr-2026). 3 checkpoints en HuggingFace (`lingbot-map`, `-long`, `-stage1`), espejados en ModelScope.
- Visor en browser vía viser, más un renderer offline por batch para secuencias largas.

## Uso básico

```bash
conda create -n lingbot-map python=3.10 -y && conda activate lingbot-map
pip install torch==2.8.0 torchvision==0.23.0 --index-url https://download.pytorch.org/whl/cu128
pip install -e . && pip install flashinfer-python
python demo.py --model_path /path/to/lingbot-map.pt --video_path video.mp4 --fps 10
```

**Corrección respecto a cómo llegó al canal**: se compartió como "el gaussian splatting volvió", pero **no es gaussian splatting**. Las palabras `gaussian`, `splat` y `3DGS` no aparecen ni una vez en el README ni en el abstract; la representación de salida son nubes de puntos por unprojection de profundidad (linaje VGGT + DINOv2). El "video → 3D" sí es exacto.

**Requisitos y trampas:**
- **Necesita CUDA de NVIDIA**, no hay camino por CPU. Hay que compilar extensiones CUDA a mano.
- El renderer offline depende de NVIDIA Kaolin, que **no tiene wheels para PyTorch 2.9.x** — quedás pineado a torch 2.8.0+cu128 o a compilar Kaolin.
- Entrenado con 320 vistas; más allá de eso hay que usar `--keyframe_interval` o `--mode windowed`.
- El visor interactivo no aguanta secuencias muy largas. VRAM alta: el README linkea un fork de la comunidad para placas de 8 GB.
- Sin releases ni tags: sólo la rama `main`, y 3 contributors.

Relacionado: [[trellis-2]] e [[img2threejs]] para el camino imagen → 3D.

**Licencia**: Apache-2.0
