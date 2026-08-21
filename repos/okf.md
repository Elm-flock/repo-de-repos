---
title: okf
url: https://github.com/GoogleCloudPlatform/knowledge-catalog/tree/main/okf
tags: [knowledge-base, markdown, agents, python, google, apache-2.0]
added: 2026-08-21
added_by: Emiliano
---

Formato vendor-neutral para representar conocimiento como un directorio de archivos markdown con frontmatter YAML, para que agentes y humanos curen contexto en git en vez de en un metadata store propietario.

## Por qué vale la pena

- **Es exactamente el formato de este repo.** Markdown + frontmatter YAML en una carpeta, versionado en git. Denis ya lo había planteado en el thread donde nació `repo-de-repos` ("y si le metemos okf?"). Si en algún momento se quiere formalizar, este es el estándar a seguir.
- **No es sólo spec: trae implementación.** Además de `SPEC.md` (1.006 líneas, v0.2) hay un paquete Python real, `reference_agent`, con subcomandos `enrich` y `visualize`, adaptador de BigQuery, crawler web por LLM, y generador de un visor HTML autocontenido con Cytoscape.js. Más 7 módulos de pytest y **4 bundles conformes prearmados** (ga4, stackoverflow, crypto_bitcoin, acme_retail) con su `viz.html` committeado.
- **Superficie obligatoria mínima**: `type` es la **única** clave siempre requerida. Recomendadas: `title`, `description`, `resource`, `tags`. Sólo dos nombres de archivo reservados: `index.md` y `log.md`.
- **Conformance deliberadamente permisiva**: el consumidor **no debe** rechazar un bundle por `type` desconocido, claves de frontmatter desconocidas, cross-links roto o `index.md` faltante. Es un no-objetivo explícito definir una taxonomía fija de tipos.
- **v0.2 (24-jul-2026) agregó** familias de procedencia, confianza y ciclo de vida (`sources`, `generated`, `verified`, `status`, `stale_after`) y el tipo `Attested Computation`. Dos cambios que rompen: `timestamp` → `generated.at`, y el heading `# Citations` pasó al frontmatter como `sources`.
- Segunda toolchain en `toolbox/mdcode/`: `kcmd`, "Metadata as Code Library, CLI and MCP Server" en TypeScript/Bun con SDK de MCP.

## Uso básico

```bash
cd okf && python3 -m venv .venv && .venv/bin/pip install -e .[dev]
.venv/bin/python -m reference_agent visualize --bundle ./bundles/ga4
```

**Cosas a tener en cuenta:**
- **El README del repo aclara: "This repository and its contents are not an official Google product."**
- **Cero releases, cero tags, no está en PyPI ni npm**: la instalación es editable desde fuente y nada más.
- Los ~8.8k stars son del monorepo `knowledge-catalog` entero (samples de Knowledge Catalog, ex-Dataplex). OKF es uno de tres directorios y sólo 8 commits tocaron `okf/`.
- El reference agent necesita credenciales de Google Cloud con billing (las queries de BigQuery las pagás vos) y `GEMINI_API_KEY` o Vertex AI.
- `toolbox/mdcode/package.json` declara ISC, inconsistente con el Apache-2.0 del repo.

**Dos aclaraciones sobre cómo llegó al canal:**
1. El framing de "Google rompió el RAG, la nueva memoria para IA es una simple carpeta" es **spin de terceros**. El anuncio original (12-jun-2026) describe la v0.1 y **no compara contra RAG ni vector databases** en ningún momento.
2. **"OKF" hoy nombra tres cosas distintas y sin relación**: este de Google, el de [[kdd]] (más estricto y mutuamente incompatible), y `pmaojo/okf-mcp`, donde significa "Obsidian-style Knowledge Format".

**Licencia**: Apache-2.0
