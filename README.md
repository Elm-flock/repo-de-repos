# repo-de-repos

Repo compartido para guardar repos/herramientas interesantes que vamos encontrando, en formato Obsidian (carpeta de markdown) para que no se pierdan en favoritos individuales.

## Cómo agregar un repo

1. Copiá `templates/repo-template.md` a `repos/<nombre-corto>.md`.
2. Completá el frontmatter (`title`, `url`, `tags`, `added`, `added_by`).
3. Escribí una descripción corta: qué hace y por qué vale la pena guardarlo.
4. Commit y push.

## Por qué este formato

Un archivo por repo (no una lista corrida) para aprovechar backlinks y grafo de Obsidian, y porque un frontmatter estructurado es más fácil de parsear después por un script o un MCP — la idea a futuro es que esto alimente un integrador que capture lo que se charla en el canal de Slack del equipo.
