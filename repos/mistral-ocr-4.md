---
title: mistral-ocr-4
url: https://mistral.ai/news/ocr-4
tags: [ocr, document-conversion, vision, mistral, self-hosted]
added: 2026-08-10
added_by: Emiliano
---

OCR de Mistral orientado a document intelligence: además del texto devuelve bounding boxes, clasificación de bloques (títulos, tablas, ecuaciones, firmas) y confidence scores inline. Model id `mistral-ocr-4-0`.

## Por qué vale la pena

- **Precio**: USD 4 por 1.000 páginas vía API (USD 2 con el descuento de Batch API), USD 5 por 1.000 en Document AI. Es el punto que hizo que Emiliano lo pasara al canal.
- **170 idiomas en 10 grupos lingüísticos**, cubriendo lenguas de bajos recursos donde la competencia se degrada: hindi, japonés, georgiano, bengalí, armenio, hebreo, griego, gujarati, tamil, malayalam, kannada, telugu, además de europeas, medio-orientales y del sudeste asiático.
- **Salida estructurada, no un blob de texto**: la clasificación de bloques + bounding boxes es lo que permite armar pipelines de extracción confiables.
- **Confidence score inline** para rutear a revisión humana solo lo dudoso.
- **Benchmarks**: 85.20 en OlmOCRBench y 93.07 en OmniDocBench, con 72% de win rate promedio en evaluación humana contra sistemas competidores (el propio anuncio aclara que estos benchmarks tienen artifacts de scoring que a veces penalizan output correcto).
- **Self-hosted en un único container** para soberanía de datos; también en Mistral Studio, Amazon SageMaker y Microsoft Foundry.
- Formatos: PDF, DOC, PPT y OpenDocument.

## Comparación útil

Para PDFs con texto nativo conviene evaluar primero [[pdf-inspector]], que resuelve local en <200ms sin costo por página. Mistral OCR 4 gana en escaneados, manuscritos y multilingüe raro.

**Licencia**: producto comercial (API + deployment self-hosted enterprise)
