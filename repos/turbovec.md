---
title: turbovec
url: https://github.com/RyanCodrai/turbovec
tags: [vector-search, rag, quantization, rust, python, mit]
added: 2026-07-21
added_by: Emiliano
---

Índice vectorial local basado en TurboQuant, implementado en Rust con bindings Python, para reducir memoria y acelerar búsqueda aproximada en pipelines RAG.

## Por qué vale la pena

- **Compresión concreta**: un corpus de 10 millones de vectores que ocupa 31 GB en float32 entra en 4 GB con la configuración reportada por el proyecto.
- **Ingesta online**: agrega vectores sin etapa de entrenamiento, ajuste de parámetros ni reconstrucción completa al crecer el índice.
- **Kernels SIMD propios**: usa NEON en ARM y AVX-512BW con fallback AVX2 en x86; reporta 10-19% más velocidad que FAISS FastScan en ARM.
- **Filtros dentro del kernel**: acepta allowlists o bitmasks y evita puntuar bloques sin candidatos permitidos, sin sobreconsulta ni pérdida adicional de recall.
- **Persistencia e IDs estables**: `IdMapIndex` permite altas, borrado O(1), búsqueda y serialización conservando IDs externos.
- **Integraciones listas**: ofrece reemplazos para stores en memoria de LangChain, LlamaIndex, Haystack y Agno.

## Uso básico

```bash
pip install turbovec
# o desde Rust
cargo add turbovec
```

Admite índices de 2 o 4 bits y carga/escritura desde disco para reutilizarlos entre procesos.

**Licencia**: MIT
