---
title: pdf-inspector
url: https://github.com/firecrawl/pdf-inspector
tags: [pdf, document-conversion, markdown, rust, python, mit]
added: 2026-08-10
added_by: Francisco
---

Librería Rust de Firecrawl para clasificar y extraer texto de PDFs sin OCR. Detecta si un PDF es text-based o escaneado y, si tiene texto nativo, lo convierte a Markdown limpio en menos de 200ms — evitando pagar servicios de OCR para el ~54% de PDFs que no lo necesitan.

## Por qué vale la pena

- **Clasificación en ~10-50ms**: distingue TextBased / Scanned / ImageBased / Mixed muestreando content streams, con score de confianza (0.0-1.0) y ruteo a OCR por página.
- **Benchmark en opendataloader-bench** (200 PDFs, sin OCR, M4 Pro): 0.875 overall / 0.915 reading order / 0.814 tablas, corriendo el corpus completo en 0.470s. Comparado: liteparse 0.873 en 0.750s, pymupdf4llm 0.735 en 17.1s, markitdown 0.589 en 16.2s.
- **Detección de tablas dual**: por rectángulos del PDF y heurística por alineación de texto — maneja tablas financieras, footnotes y tablas que continúan entre páginas.
- **Layout multi-columna** con orden de lectura automático y soporte RTL; fuentes CID (ToUnicode CMap para Type0/Identity-H, UTF-16BE, UTF-8, Latin-1).
- **Detecta encodings de fuente rotos** y los marca, para que el caller haga fallback a OCR en vez de devolver basura.
- **Bindings**: Python (maturin/PyPI), Node.js (`@firecrawl/pdf-inspector`) y WebAssembly de browser (`@firecrawl/pdf-inspector-wasm`, con CMaps embebidos y sin round trip al server).
- Rust puro, sin modelos ML ni servicios externos: una sola dependencia (`lopdf`).

## Uso básico

```bash
pip install pdf-inspector     # o: npm i @firecrawl/pdf-inspector | cargo add pdf-inspector
```

```python
import pdf_inspector
result = pdf_inspector.process_pdf("document.pdf")
print(result.pdf_type)   # "text_based", "scanned", "image_based", "mixed"
print(result.markdown)
```

**Licencia**: MIT
