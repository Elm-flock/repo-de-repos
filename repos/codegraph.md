---
title: codegraph
url: https://github.com/colbymchenry/codegraph
tags: [mcp, code-search, coding-agent, typescript, colbymchenry, mit]
added: 2026-07-21
added_by: Emiliano
---

Índice local de conocimiento de código que expone símbolos, llamadas, dependencias y blast radius a agentes mediante MCP.

## Por qué vale la pena

- **Contexto directo para agentes**: responde consultas semánticas con código y rutas de llamadas relevantes, evitando recorridos repetidos con grep y lecturas archivo por archivo.
- **Índice siempre actualizado**: `codegraph init` crea el grafo y un watcher sincroniza altas, cambios y borrados automáticamente.
- **100% local**: el índice vive en `.codegraph/` y no requiere un servicio administrado ni enviar el código fuera de la máquina.
- **Soporte multilenguaje amplio**: analiza desde TypeScript, Python, Rust, Go y Java hasta Swift, CUDA, Solidity, COBOL, Terraform y Nix.
- **Integración automática**: configura su server MCP en Claude Code, Cursor, Codex, OpenCode, Hermes Agent, Gemini, Antigravity y Kiro.
- **Benchmark reproducible**: sobre 7 repos reales y medianas de 4 corridas por variante, el proyecto reporta 58% menos tool calls, 22% menos tiempo y casi cero lecturas de archivos con Opus 4.8.

## Uso básico

```bash
npm install -g @colbymchenry/codegraph
codegraph install
cd tu-proyecto
codegraph init
```

El instalador standalone incluye su propio runtime de Node.js; la alternativa npm sirve si Node ya está disponible.

**Licencia**: MIT
