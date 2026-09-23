---
title: tgrep
url: https://github.com/microsoft/tgrep
tags: [code-search, cli, coding-agent, rust, microsoft, mit]
added: 2026-09-23
added_by: Emiliano
---

grep de Microsoft con índice de trigramas y arquitectura cliente/servidor, con CLI compatible con ripgrep. Está pensado para búsqueda regex en monorepos grandes, donde ripgrep tiene que recorrer todo el árbol en cada búsqueda.

## Por qué vale la pena

- **Ya lo usa GitHub Copilot CLI**: el changelog de la v1.0.79 (10-ago-2026) dice que en monorepos grandes usa tgrep en vez de ripgrep. No es un experimento suelto.
- **Benchmarks propios contra ripgrep** (24-ago-2026, sólo tiempo de búsqueda con el índice ya construido): media geométrica **14,6x en Windows, 8,6x en macOS y 2,8x en Linux**. El pico es gecko-dev (388K archivos) en macOS: 33,4 s contra 643 ms, o sea 51,9x. En Linux sobre Kubernetes gana ripgrep (0,93x).
- **Indexar es barato**: el kernel de Linux (94.634 archivos, índice de 990 MiB) se indexa en ~22-27 s con un pico de ~150-160 MiB de RAM.
- **Índice vivo**: índice en disco mapeado con mmap más un overlay en memoria, alimentado por un file watcher. El servidor habla JSON-RPC 2.0 sobre TCP.
- **Trae integración para agentes**: `AGENTS.md` y un `install-agent.sh` que instala tools MCP y hooks de arranque para Codex y [[pi]].
- Muy activo: v1.0.10 (21-sep-2026), 33 releases en 6 meses, 3.3k stars, 15 contributors. Binarios para Linux (musl), macOS y Windows, en x86_64 y ARM.

## Uso básico

```bash
brew install tgrep
tgrep index . && tgrep serve . &
tgrep "fn main" .
```

**Trampas:**
- **`cargo install tgrep` instala otro proyecto** (niamster/tgrep, que ocupa ese nombre en crates.io). Para compilar desde fuente: clonar y `cargo install --path tgrep-cli --locked`.
- Sin `tgrep serve` corriendo, el índice queda desactualizado después de cada edición. Un agente tiene que re-indexar o usar `--no-index`.
- Por defecto saltea archivos de más de 64 MiB, que se reportan como "sin match". Se desactiva con `--no-max-filesize`.
- Los flags de `index` y `serve` (`--exclude`, `--max-filesize`) tienen que coincidir: si difieren, el servidor puede sacar archivos del índice.
- Hay que agregar `.tgrep/` al `.gitignore`.
- En Linux la ganancia es mucho menor que en Windows o macOS. Los benchmarks corren en runners compartidos de GitHub, no en máquinas controladas.

Relacionado: [[codegraph]] y [[serena]] buscan por símbolo en vez de por texto, [[sourcegraph]] es la versión enterprise multi-repo, y [[rtk]] comprime el output de comandos como grep antes de que entre al contexto.

**Licencia**: MIT (contribuir exige firmar el CLA de Microsoft)
