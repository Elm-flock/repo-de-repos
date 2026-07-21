---
title: claude-statusline
url: https://github.com/nilbuild/claude-statusline
tags: [cli, claude-code, statusline, shell, nilbuild, mit]
added: 2026-07-21
added_by: Denis
---

Statusline mínima para Claude Code que muestra modelo, uso de contexto, límites, directorio y estado de Git durante una sesión.

## Por qué vale la pena

- **Límites visibles en la terminal**: consulta los datos de rate limit para mostrar el consumo sin salir de Claude Code.
- **Contexto operativo**: combina modelo y ventana de contexto con directorio, branch y estado de Git.
- **Instalación reversible**: guarda una copia de la statusline previa y la restaura al desinstalar.
- **Implementación pequeña**: la visualización es un script shell y el paquete npm sólo se ocupa de instalarlo y configurar Claude Code.
- **Dependencias comunes**: usa `jq` para JSON, `curl` para límites y `git` para la información del repositorio.

## Uso básico

```bash
npx @kamranahmedse/claude-statusline
```

Para quitarla y restaurar la configuración anterior: `npx @kamranahmedse/claude-statusline --uninstall`.

**Licencia**: MIT
