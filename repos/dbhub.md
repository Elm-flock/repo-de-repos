---
title: dbhub
url: https://github.com/bytebase/dbhub
tags: [mcp, sql, claude-code, typescript, mit]
added: 2026-09-23
added_by: Guille
---

Servidor MCP de Bytebase que conecta agentes a PostgreSQL, MySQL, MariaDB, SQL Server, Oracle y SQLite gastando pocos tokens de contexto. Es el ejemplo de base de datos que usa la documentación oficial de Claude Code.

## Por qué vale la pena

- **Pocas tools**: por defecto expone sólo `execute_sql` y `search_objects`, que ocupan ~1,4k tokens. Según una medición de la propia Bytebase, MCP Toolbox ocupa ~19k y Supabase MCP ~19,3k. Opcionalmente suma `explain_sql`, `health_check` y tools SQL parametrizadas definidas en `dbhub.toml`.
- **Read-only en dos capas**: un clasificador de keywords más el modo read-only del motor (`BEGIN READ ONLY` en Postgres, `START TRANSACTION READ ONLY` en MySQL/MariaDB).
- **Multi-conexión** en un TOML con hot reload, túneles SSH (incluido ProxyJump multi-hop), SSL/TLS, `max_rows` y `query_timeout`.
- Transports `stdio` y `http`, con un Workbench web. Soporta la spec MCP 2026-07-28 stateless, con fallback a la de 2025.
- **Tracción real**: 3.5k stars, ~116k descargas en npm en el último mes y ~160k pulls en Docker Hub. v1.3.1 (21-sep-2026), 36 contributors.
- Viene como bundle `.mcpb` para Claude Desktop y como plugin de Claude Code con `/dbhub:setup` y `/dbhub:explore`. El bundle y el plugin arrancan en read-only.

## Uso básico

```bash
claude mcp add --transport stdio db -- npx -y @bytebase/dbhub --dsn "postgresql://readonly:pass@host:5432/db"
npx @bytebase/dbhub@latest --demo    # SQLite de ejemplo
```

Requiere Node ≥22.5. También está como imagen Docker: `bytebase/dbhub`.

**Trampas:**
- **Instalado a mano, `execute_sql` no es read-only por defecto** y no hay flag de CLI para activarlo: hay que poner `readonly = true` en la entrada de la tool `execute_sql` del `dbhub.toml`.
- **En modo `http` escucha en `0.0.0.0` y sin autenticación por defecto.** Usar `--host 127.0.0.1` o `--auth-token`.
- El read-only no frena funciones de roles privilegiados (`pg_read_file`, `COPY … TO PROGRAM`, `dblink`). En MySQL/MariaDB el DDL lo frena sólo el clasificador de keywords. Conectar siempre con un usuario de mínimos privilegios.
- El conector de Oracle se agregó en la v1.3.0 (19-sep-2026): está verde.
- Los drivers son dependencias opcionales y pueden fallar al instalar con `npx`.

Relacionado: [[harlequin]] es el IDE SQL de terminal para humanos, [[motherduck]] tiene su propio MCP para DuckDB, y [[kravn]] es un gateway para gobernar servidores MCP como este en una organización.

**Licencia**: MIT
