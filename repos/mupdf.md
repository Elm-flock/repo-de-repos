---
title: mupdf
url: https://mupdf.com
tags: [pdf, document-conversion, cli, c, python, agpl-3.0]
added: 2026-08-21
added_by: Emiliano
---

Librería en C de parsing y renderizado de PDF (fitz) **más** una suite de CLI (`mutool`) y visores. Rapidísima y muy completa — pero con una licencia que hay que leer antes de meterla en cualquier producto.

## 🚨 La licencia primero, porque es lo que decide todo

**AGPL-3.0-or-later, con licencia comercial paga de Artifex como alternativa.**

El `COPYING` es la AGPL v3 literal. La página de licencias de Artifex es explícita: *"no podés desplegar nuestro open source como parte de una aplicación o servicio basado en servidor sin divulgar el código fuente completo de tu propia aplicación bajo AGPL"*.

En la práctica el problema es el **§13 de la AGPL**: poner MuPDF detrás de una API interna, un endpoint SaaS o cualquier servicio de red con el que interactúen usuarios **dispara la obligación de liberar el código de *tu* aplicación**. Uso batch puramente interno sin interacción de red es un disparador más débil, pero es una decisión legal, no de ingeniería. Si toca superficie de producto, hay que presupuestar la licencia comercial (Artifex no publica precios: cotización por proyecto vía sales@artifex.com).

Lo mismo aplica a **todos** los bindings: `mupdf.js`, `MuPDF.NET`, `go-fitz`, y PyMuPDF.

## Por qué vale la pena igual

- **Velocidad**, según el benchmark del propio Artifex (8 PDFs, 7.031 páginas — self-benchmark, descontar en consecuencia): extracción de texto **8.01s** contra XPDF 27.42, PyPDF2 101.64 y PDFMiner 227.27. Copy/merge **3.05s** contra pikepdf 33.57 y PyPDF2 494.04.
- **`mutool` trae 19 subcomandos**: audit, bake, barcode, clean, convert, create, draw, extract, grep, info, merge, pages, poster, recolor, run, show, sign, trace, trim.
- **Conversión amplia**: raster (cbz, png, pnm, pgm, ppm, pam, pbm, pkm), print-raster (pcl, pclm, ps, pwg), vector (pdf, svg) y texto (html, xhtml, text, stext).
- Corre en Windows, macOS, Linux, BSD, Android e iOS. 18.7 MB de C.
- 1.28.2 del 03-ago-2026; ~2 releases de features por año más parches.

## Corrección importante sobre tablas

Llegó al canal como "mupdf lo recomiendo cuando tenés tablas", pero **el core en C y `mutool` no detectan estructura de tablas**. No existe un `mutool tables`; `mutool convert -F stext` te da texto posicionado, no tablas reconstruidas.

La detección de tablas vive en la capa **Python**:
- **PyMuPDF** — `Page.find_tables()` desde la 1.23.0, con estrategias `lines`, `lines_strict` y `text`, y objetos `Table` con `.extract()`, `.to_markdown()` y `.to_pandas()`. **Ojo**: el `TableFinder` está atado al ciclo de vida de la página — hay que extraer o copiar antes de reasignarla o los datos se invalidan silenciosamente.
- **pymupdf4llm** — es lo que realmente querés usar: markdown/JSON/TXT, páginas multi-columna, análisis de layout **sin GPU**, chunking e integraciones con LlamaIndex y LangChain. 21.5M descargas mensuales.

```bash
pip install pymupdf pymupdf4llm
python -c "import pymupdf4llm; print(pymupdf4llm.to_markdown('doc.pdf'))"
```

Ambos declaran en PyPI, textual: `Dual Licensed - GNU AFFERO GPL 3.0 or Artifex Commercial License`. Misma exposición que el core.

**Y la comparación contra [[markitdown]] no se sostiene como se dijo**: leyendo el converter de PDF de markitdown, importa `pdfplumber` junto a `pdfminer` y tiene `_to_markdown_table()` más reconstrucción heurística de tablas sin bordes (clusteriza palabras con tolerancia y de 5, agrupa columnas con gaps > 50pt). O sea **markitdown sí emite tablas markdown desde PDF**, y encima es MIT con 175k stars. La preferencia por MuPDF en PDFs con muchas tablas es plausible como juicio de calidad — el parser en C más la estrategia de líneas vectoriales es un enfoque genuinamente distinto al heurístico — pero no hay benchmark que lo respalde.

Relacionado: [[pdf-inspector]] para clasificar PDFs antes de procesarlos, [[markitdown]] como alternativa MIT.

**Licencia**: AGPL-3.0-or-later, o licencia comercial de Artifex
