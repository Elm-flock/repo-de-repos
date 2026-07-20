# AGENTS.md

Convenciones para agregar o editar entradas en `repos/`. Un agente (o humano) que sume un repo nuevo debe seguir esto sin necesitar contexto adicional.

## Frontmatter

```yaml
---
title: ""       # nombre corto del repo, igual al nombre del archivo (sin .md)
url: ""         # URL canónica del repo (github/gitlab/etc), sin trailing slash
tags: []        # 3-6 tags en minúscula, kebab-case si son compuestos (ej: voice-cloning)
added: ""       # fecha ISO YYYY-MM-DD
added_by: ""    # nombre de quien lo agrega
---
```

- `title` y el nombre de archivo (`repos/<nombre-corto>.md`) deben coincidir.
- `tags` deben incluir: categoría principal (ej: `tts`, `cli`, `llm`), tecnología/runtime si es relevante (ej: `cpu`, `rust`), y organización/autor si es reconocible (ej: `kyutai`).
- Reusar tags existentes en otros `.md` de `repos/` antes de inventar uno nuevo, para mantener el grafo de Obsidian útil.
- No dejar campos vacíos ("") en el frontmatter final — completar todos antes de commitear.

## Cuerpo del archivo

Estructura recomendada, en este orden (omitir secciones que no apliquen, no dejar encabezados vacíos):

1. **Descripción corta** (1-2 líneas, sin encabezado): qué es y qué problema resuelve.
2. `## Por qué vale la pena` — bullets con los puntos fuertes/diferenciadores concretos (no genéricos tipo "es rápido y fácil de usar").
3. `## Uso básico` — instalación y comandos mínimos si aplica.
4. Licencia al final, en negrita: `**Licencia**: MIT`.

## Estilo

- Español, tono directo, sin relleno.
- Bullets con datos concretos (números, versiones, benchmarks) en vez de adjetivos vacíos.
- Si el repo tiene features "de la comunidad" (forks, ports a otros lenguajes, integraciones) mencionarlas — son útiles para decidir si conviene usarlo.

## Proceso

1. Copiar `templates/repo-template.md` a `repos/<nombre-corto>.md`.
2. Completar frontmatter.
3. Investigar el repo (README, releases, license) y escribir el cuerpo siguiendo la estructura de arriba.
4. Commit y push.
