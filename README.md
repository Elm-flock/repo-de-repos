# repo-de-repos

Repo compartido para guardar repos/herramientas interesantes que vamos encontrando, en formato Obsidian (carpeta de markdown) para que no se pierdan en favoritos individuales.

## Cómo agregar un repo

1. Copiá `templates/repo-template.md` a `repos/<nombre-corto>.md`.
2. Completá el frontmatter (`title`, `url`, `tags`, `added`, `added_by`).
3. Escribí una descripción corta: qué hace y por qué vale la pena guardarlo.
4. Commit y push.

## Por qué este formato

Un archivo por repo (no una lista corrida) para aprovechar backlinks y grafo de Obsidian, y porque un frontmatter estructurado es más fácil de parsear después por un script o un MCP.

## Importar desde Slack

Hay una skill que lee el canal `flock-ai`, detecta herramientas que todavía no están cargadas, las investiga y escribe las entradas siguiendo `AGENTS.md`.

Setup, una sola vez por persona: corré `/mcp` en Claude Code y autenticá **claude.ai Slack**.

Después, cada vez que quieras traer lo nuevo:

```
/slack-import
```

Te deja los archivos escritos y un resumen de qué agregó y qué descartó, sin commitear — vos revisás y decidís.

El watermark y la lista de cosas ya descartadas viven en `slack-import-state.json`, versionado, así el equipo comparte el estado y nadie re-investiga lo mismo dos veces. La skill lee **sólo** ese canal, por ID, y sólo lee (nunca postea).

> **Corré esto cada 4-6 semanas.** El workspace retiene ~90 días de mensajes: lo que no se importa dentro de esa ventana se pierde y no hay forma de recuperarlo por API.
