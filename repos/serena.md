---
title: serena
url: https://github.com/oraios/serena
tags: [mcp, code-search, coding-agent, language-server, python, mit]
added: 2026-08-10
added_by: Denis
---

Toolkit MCP que le da a un agente de coding capacidades de IDE: retrieval semántico, edición, refactor y debugging a nivel de símbolo, explotando la estructura relacional del código en vez de números de línea y grep. Se enchufa a cualquier cliente que hable MCP.

## Por qué vale la pena

- **Diseño agent-first**: abstracciones de alto nivel (find symbol, find referencing symbols, replace symbol body, insert before/after symbol) en lugar de line numbers y search & replace, que es lo que hace que un rename cross-file no se rompa a mitad de camino.
- **40+ lenguajes** vía language servers (LSP) en el backend por defecto: Python, TypeScript/JavaScript, Java, C#, C/C++, Go, Rust, Kotlin, Swift, PHP, Ruby, Elixir, Zig, Terraform, Solidity, etc.
- **Backend alternativo con plugin de JetBrains** (pago, con trial): agrega move de símbolo/archivo/directorio, inline, propagate deletions, type hierarchy, búsqueda en dependencias del proyecto y query de proyectos externos — cosas que el LSP no da.
- **Sistema de memorias** para workflows largos.
- **Ahorra tokens** además de errores: la edición simbólica evita releer archivos enteros.
- Compatible con Claude Code, Codex, OpenCode, Gemini CLI, VSCode/Cursor/JetBrains, Claude Desktop, OpenWebUI.

## Uso básico

Seguir el Quick Start del repo — el README avisa explícitamente de **no instalarlo desde un marketplace de MCP o de plugins**, porque traen comandos de instalación viejos y subóptimos.

Nota de Denis en Slack: no alcanza con instalarlo, **hay que activarlo por proyecto** (los pasos están en el repo).

**Licencia**: MIT (el plugin de JetBrains es aparte y pago)
