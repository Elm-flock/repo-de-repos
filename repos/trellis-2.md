---
title: trellis-2
url: https://github.com/microsoft/TRELLIS.2
tags: [image-to-3d, generative, microsoft, python, mit]
added: 2026-07-30
added_by: Emiliano
---

Modelo generativo 3D de 4B parámetros (Microsoft) para generación **image-to-3D** de assets totalmente texturizados y de alta fidelidad. Ojo: es image-to-3D, no text-to-3D. Pesos en <https://huggingface.co/microsoft/TRELLIS.2-4B>.

## Por qué vale la pena

- **4B params** con DiTs "vanilla"; genera assets texturizados de alta resolución.
- **Representación O-Voxel** ("field-free" sparse voxel) que maneja topología arbitraria: superficies abiertas, geometría no-manifold y estructuras internas.
- **Materiales PBR completos** (base color, roughness, metallic, opacity), no solo malla + color.
- **Velocidad (H100)**: ~3 s a 512³, ~17 s a 1024³, ~60 s a 1536³.
- **Incluye codebase de entrenamiento completo** (entrenar desde cero o fine-tune con datasets propios).

## Uso básico

Requisitos: **≥24 GB VRAM**, probado en A100/H100, CUDA 12.4, Python 3.8+. Ver README del repo para pipeline de inferencia. El predecesor `microsoft/TRELLIS` (CVPR'25) es un modelo distinto y anterior.

**Licencia**: MIT (código y pesos)
