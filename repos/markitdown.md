---
title: markitdown
url: https://github.com/microsoft/markitdown
tags: [cli, document-conversion, markdown, python, microsoft, mit]
added: 2026-07-21
added_by: Emiliano
---

Utilidad Python de Microsoft para convertir documentos y archivos multimedia a Markdown estructurado, orientado a pipelines de LLMs y análisis de texto.

## Por qué vale la pena

- **Cobertura amplia**: convierte PDF, PowerPoint, Word, Excel, imágenes, audio, HTML, CSV, JSON, XML, ZIP, EPUB y URLs de YouTube.
- **Preserva estructura útil**: mantiene encabezados, listas, tablas y enlaces, priorizando una representación compacta para consumo por modelos.
- **Dependencias por formato**: permite instalar sólo los extras necesarios, por ejemplo `pdf`, `docx` y `pptx`, en lugar del paquete completo.
- **Extensible por plugins**: soporta plugins de terceros; el plugin `markitdown-ocr` agrega OCR sobre imágenes embebidas mediante modelos con visión.
- **Dos backends Azure opcionales**: Document Intelligence mejora layout/OCR y Content Understanding suma extracción de campos y soporte multimodal.
- **Superficie de seguridad explícita**: recomienda validar entradas no confiables y usar `convert_local()`, `convert_stream()` o `convert_response()` en vez del conversor permisivo cuando sea posible.

## Uso básico

```bash
pip install 'markitdown[all]'
markitdown documento.pdf -o documento.md
```

Requiere Python 3.10 o superior. Para una instalación mínima se pueden elegir extras: `pip install 'markitdown[pdf,docx,pptx]'`.

**Licencia**: MIT
