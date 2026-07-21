---
title: unlimited-ocr
url: https://github.com/baidu/Unlimited-OCR
tags: [ocr, vision, cuda, python, baidu, mit]
added: 2026-07-21
added_by: Emiliano
---

Modelo de Baidu para OCR y parsing de documentos extensos en una sola ejecución, con soporte para imágenes individuales, lotes de páginas y PDFs.

## Por qué vale la pena

- **Parsing long-horizon**: procesa múltiples páginas en una misma secuencia con contexto de hasta 32.768 tokens.
- **Dos modos de imagen**: `gundam` usa crops a 640 px sobre base 1024 para una imagen; `base` trabaja a 1024 px y soporta múltiples páginas.
- **Tres rutas de inferencia**: funciona con Transformers, vLLM o SGLang, incluyendo APIs compatibles con OpenAI para los dos últimos.
- **Ecosistema disponible**: publica pesos en Hugging Face, ModelScope y Baidu Cloud, además de una demo en Hugging Face Spaces.
- **Integraciones de comunidad**: vLLM mantiene una receta y una imagen Docker específica; `ms-swift` agregó soporte de entrenamiento.
- **Entorno reproducible documentado**: la referencia fija Python 3.12.3, CUDA 12.9 y versiones concretas de PyTorch, Transformers y PyMuPDF.

## Uso básico

```bash
docker pull vllm/vllm-openai:unlimited-ocr
```

Para inferencia directa con Transformers se carga `baidu/Unlimited-OCR` con `trust_remote_code=True`, `torch.bfloat16` y una GPU NVIDIA.

**Licencia**: MIT
