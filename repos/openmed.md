---
title: openmed
url: https://github.com/maziyarpanahi/openmed
tags: [healthcare, nlp, privacy, on-device, python, apache-2.0]
added: 2026-08-10
added_by: Guille
---

IA clínica open source que corre 100% on-device: de-identificación de PHI y extracción de entidades médicas sin que el dato del paciente salga del equipo. "Tu data, tu modelo, tu hardware."

## Por qué vale la pena

- **De-identificación con 55+ tipos de PHI**, incluyendo los 18 identificadores de HIPAA Safe Harbor más entidades extendidas, con detección context-aware y keyword boosting.
- **Validadores de formato incorporados** (SSN, NIR, CPF/CNPJ, etc.) — no es solo un NER que adivina.
- **Reportes de auditoría firmados**: qué se encontró y qué política se aplicó. Release gates que **fallan cerrado** cuando falta evidencia, en vez de dejar pasar.
- **Catálogo de 2.000+ modelos Apache-2.0** de 33M a 568M params, con dominios especializados (químicos, enfermedades, genómica, oncología, farmacovigilancia). 34 idiomas model-backed.
- **Cinco runtimes**: Python/PyTorch (CPU y NVIDIA), MLX en Apple Silicon (24–33× más rápido que CPU), OpenMedKit para iOS/Android vía ONNX, browser con WebGPU/Transformers.js, y servicios REST/gRPC en tu VPC.
- **Sin API keys ni acuerdos con vendors**: Apache 2.0 y listo — lo cual es exactamente el bloqueo típico en cualquier proyecto de salud.

## Uso básico

```bash
pip install openmed
```

```python
from openmed import deidentify
note = "Patient Casey Example (MRN 00123) called from 555-0100."
print(deidentify(note))
# → "Patient [NAME] ([ID]) called from [PHONE]."
```

Sitio: <https://openmed.life>

**Licencia**: Apache 2.0
