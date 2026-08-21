---
title: ideogram
url: https://ideogram.ai
tags: [image-generation, generative, design, open-weights, saas]
added: 2026-08-10
added_by: Emiliano
---

Generador de imágenes cuyo diferencial concreto es el **texto legible dentro de la imagen**: carteles, logos, posters y piezas tipográficas con las palabras bien escritas. Es el caso de uso donde el resto de los modelos sigue fallando.

## Por qué vale la pena

- **Renderizado de texto con 90-95% de precisión** en el modelo 3.0, contra 30-40% de Midjourney y Stable Diffusion — la razón por la que vale tenerlo aparte de tu generador habitual.
- **Ideogram 4.0 (03-jun-2026) liberó pesos**: Diffusion Transformer single-stream de **9.3B params**, 34 capas, text encoder **Qwen3-VL-8B-Instruct congelado**, generación nativa a 2048px. Corre en **una sola GPU de 24 GB**.
- **Control de layout por JSON**: bounding boxes en coordenadas normalizadas 0-1000, o sea que la composición se puede automatizar en vez de rezarle al prompt. Reportan 0.97 de OCR en inglés (X-Omni) y 0.69 mIoU en 7Bench.
- **Modos de estilo**: Realistic, Design, Anime, 3D Render.
- **Magic Prompt** (mejora automática del prompt) y **Describe** (reverse-engineering del prompt a partir de una imagen).
- **API con precio por imagen**, no por créditos: desde USD 0.03 en modo Turbo hasta USD 0.09 en Quality — predecible para automatizar.
- **Precio de suscripción**: free tier de 10 prompts/día (~40 imágenes), Basic USD 7/mes (400 prompts), Plus USD 15/mes (1.000), Pro USD 42/mes (3.000).
- El update Live Action de feb-2026 agregó clips animados de hasta 120 segundos.

## Uso básico

Web en <https://ideogram.ai> o API. Emiliano lo pasó al canal como "para generar imágenes es un lujo".

Para correrlo local: código de inferencia en `ideogram-oss/ideogram4` (Python, Apache-2.0) y pesos en la org `ideogram-ai` de HuggingFace — `ideogram-4-fp8` (9B), `ideogram-4-nf4` y `ideogram-4-nf4-diffusers` (5B, nf4 sólo CUDA). No hay repo de precisión completa publicado.

**Cuidado con la licencia de los pesos**: el model card de `ideogram-4-fp8` los etiqueta como **"Ideogram 4 Non-Commercial"**, en contradicción con Wikipedia y varios blogs que afirman que todo el release 4.0 es Apache-2.0. Leer el LICENSE del repo de pesos antes de asumir uso comercial.

**Licencia**: SaaS propietario; código de inferencia 4.0 Apache-2.0, pesos "Ideogram 4 Non-Commercial" (verificar)
