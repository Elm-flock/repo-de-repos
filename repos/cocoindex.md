---
title: cocoindex
url: https://github.com/cocoindex-io/cocoindex
tags: [rag, data-pipeline, agents, python, rust, apache-2.0]
added: 2026-07-21
added_by: Guille
---

Motor incremental para mantener actualizado el contexto de agentes y aplicaciones RAG sin reprocesar el corpus completo ante cada cambio.

## Por qué vale la pena

- **Procesamiento por delta**: detecta cambios en fuentes, código y transformaciones, e invalida sólo los resultados afectados.
- **Lineage de punta a punta**: cada vector, fila o nodo generado puede rastrearse hasta el byte de origen, útil para depuración y auditoría.
- **Python declarativo sobre un core Rust**: los flows se escriben como funciones Python mientras el motor gestiona paralelismo, caché, reintentos, backoff y dead-letter queues.
- **Fuentes y destinos variados**: cubre repos, Slack, PDFs, audio, video, bases de datos y colas; puede escribir en stores relacionales, vectoriales, grafos, warehouses y Kafka.
- **Casos concretos incluidos**: trae más de 20 ejemplos para índices de código, RAG de PDFs, knowledge graphs, extracción estructurada y pipelines CSV a Kafka.
- **Escala medible por el cambio**: el proyecto reporta frescura sub-segundo y hasta 10x menos cómputo cuando el delta es una fracción pequeña del corpus.

## Uso básico

```bash
pip install -U cocoindex
```

Los pipelines se definen en Python y se ejecutan una vez para el backfill; las corridas posteriores recalculan sólo los archivos o registros modificados. Requiere Python 3.10-3.13.

**Licencia**: Apache 2.0
