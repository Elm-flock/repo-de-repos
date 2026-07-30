---
title: harlequin
url: https://github.com/tconbeer/harlequin
tags: [cli, sql, tui, python, mit]
added: 2026-07-30
added_by: Emiliano
---

SQL IDE para la terminal, escrito en Python. Reemplazo "drop-in" del CLI de DuckDB, de SQLite, de `psql`, etc., que suma features de IDE (autocompletado, catálogo de datos navegable, syntax highlighting, exportación) dentro de una TUI. No es IA, pero es tooling de terminal que suma.

## Por qué vale la pena

- **Adaptadores por plug-in**: built-in trae DuckDB y SQLite3; instalables aparte Postgres, MySQL/MariaDB, ODBC y S3, más docenas de bases vía adaptadores de la comunidad.
- **TUI sobre Textual** (mismo ecosistema que Rich); corre en Linux, macOS y Windows.
- **Catálogo de datos navegable** en panel lateral, temas y key-bindings personalizables, perfiles vía archivo de config.
- **Integración con Django** vía el paquete `django-harlequin`.

## Uso básico

```bash
uv tool install harlequin
# con adaptadores: uv tool install 'harlequin[postgres,mysql,s3]'
# alternativas: pip install harlequin  ·  brew install harlequin
```

**Licencia**: MIT
