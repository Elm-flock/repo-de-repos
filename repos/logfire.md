---
title: logfire
url: https://pydantic.dev/logfire
tags: [observability, agents, python, typescript, rust, mit]
added: 2026-08-21
added_by: Guille
---

Plataforma de observabilidad para apps de LLM/agentes (y apps en general) del equipo de Pydantic, construida sobre OpenTelemetry, con traces, métricas y logs consultables por **SQL**.

## Por qué vale la pena

- **Free tier usable de verdad**: 10M spans/logs/métricas por mes, 30 días de retención, sin tarjeta de crédito. Al llegar al límite **pausa la ingesta** en vez de facturarte — no hay sorpresa a fin de mes.
- **Traces consultables por SQL**, no un query language propietario. Reduce mucho la curva para debuggear una cadena de agentes.
- **3 SDKs propios** (Python, JS/TS incluyendo Next.js, Cloudflare Workers y Deno, y Rust) y cualquier otro lenguaje vía OTLP: Go, Java, .NET, Ruby, PHP, Elixir, Swift.
- **No hay lock-in de datos**: ingiere OTLP estándar y puede reenviar a otro endpoint OTLP-compatible.
- Precios: Team **$49/mo** (10M incluidos, **$2 por millón extra**, 5 seats), Growth **$249/mo** con hasta 90 días de retención y seats/proyectos ilimitados.
- Trae **AI Gateway**: podés usar tus propias credenciales de provider **sin markup**, o las suyas con 5% (Team) / 3% (Growth).

## Uso básico

```bash
pip install logfire     # también: npm i logfire  /  cargo add logfire
```

**Qué es open source y qué no**: los SDKs son MIT (`pydantic/logfire` ~4.4k stars, `pydantic/logfire-rust`, `pydantic/logfire-js`), pero el **backend y la UI son propietarios**. El self-hosting es sólo Enterprise: el Helm chart está abierto pero las imágenes del server son cerradas. Enterprise ofrece tres modelos de deploy: Cloud, Dedicated single-tenant en GCP, y self-hosted en tu Kubernetes.

Relacionado: [[cocoindex]] para el lado de pipelines de datos/RAG que después querés observar.

**Licencia**: SDKs MIT; backend y UI propietarios
