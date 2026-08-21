---
title: anthropic-sdk-csharp
url: https://github.com/anthropics/anthropic-sdk-csharp
tags: [llm, api, dotnet, anthropic, mit]
added: 2026-08-21
added_by: Emiliano
---

SDK oficial de Anthropic para C# / .NET, mantenido por Anthropic, con integración nativa del `IChatClient` de `Microsoft.Extensions.AI`.

## Por qué vale la pena

- **Es el oficial**: hasta ahora en .NET se usaban SDKs comunitarios. Esto habilita integrar Claude en aplicaciones enterprise .NET sin depender de un wrapper de terceros.
- **`IChatClient` de `Microsoft.Extensions.AI`** significa que se enchufa al mismo abstraction layer que ya usan Semantic Kernel y el resto del stack de IA de Microsoft — se puede swapear provider sin reescribir.
- **Cobertura amplia de target frameworks**: netstandard2.0+, net8.0 y net9.0. El netstandard2.0 permite usarlo desde proyectos viejos.
- **Packages hermanos por plataforma**: `Anthropic.Vertex`, `Anthropic.Bedrock`, `Anthropic.Aws` y `Anthropic.Foundry`.
- Última versión **12.42.0** del 19-ago-2026, ~3.4M descargas acumuladas en NuGet.

## Uso básico

```bash
dotnet add package Anthropic
```

**Dos confusiones a evitar**:
- El package se llama **`Anthropic`**, no `Anthropic.SDK` — este último es el SDK **no oficial** de `tghamm`, que aclara explícitamente que no está afiliado a Anthropic.
- Las versiones **3.x y anteriores** del package eran el SDK comunitario de tryAGI (hoy renombrado `tryAGI.Anthropic`); el oficial arranca en **v10+**.

**Está en beta a pesar del número de versión**: la doc dice textualmente que aunque versione 10+, durante la beta pueden haber breaking changes en releases minor o patch. Pinear versión si va a producción.

Docs: `platform.claude.com/docs/en/api/sdks/csharp`.

**Licencia**: MIT
