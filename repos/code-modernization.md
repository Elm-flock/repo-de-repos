---
title: code-modernization
url: https://github.com/anthropics/claude-plugins-official/tree/main/plugins/code-modernization
tags: [plugin, claude-code, coding-agent, anthropic, apache-2.0]
added: 2026-10-09
added_by: Lucas
---

Plugin oficial de Anthropic para Claude Code que moderniza codebases legacy en cualquier lenguaje, COBOL incluido. Recorre assessment, mapa del sistema, reglas de negocio extraídas del código, un plan que aprueba un humano, el build y una verificación que intenta probar que el código nuevo se comporta igual que el viejo. **Consume mucho uso: `extract-rules` lanzó entre 50 y 200 agentes en las corridas documentadas.**

## Por qué vale la pena

- **Veredicto por módulo, no "confiá en mí"**: re-ejecuta los tests desde cero, compara byte a byte viejo contra nuevo, prueba al menos 10 inputs nuevos y un canary, y marca cada módulo como PROVEN, PARTLY PROVEN o NOT PROVEN.
- **Corridas documentadas con números**: AWS CardDemo de COBOL/CICS/JCL a Java 21 (35 reglas, 213 tests, NOT PROVEN por 7 diferencias con registros malformados); Jetty de Java 8 a 17 (946 tests idénticos); osCommerce de PHP a FastAPI (17.727 casos idénticos, PROVEN). También AngularJS a React, Python 2 a 3, .NET Framework a .NET 10, Rails 3.2 a 7.1 y Jenkins a GitHub Actions.
- **Tres estrategias de build**: `uplift`, `transform` o `reimagine`. 13 comandos, 8 agentes y 6 workflows.
- **Tiempos en sistemas de decenas de miles de líneas**: preflight 3-4 min, assess 5-8, map y extract-rules 5-15 cada uno, y 15-30 min por módulo construido.
- Lo mostraron en una charla de Anthropic. El marketplace oficial donde vive tiene 315 plugins hoy, 40 de autoría de Anthropic.
- Comunidad: port a GitHub Copilot (`haukened/copilot-code-modernization`). Kit oficial aparte: `anthropics/code-migration-kit-with-claude-code`.

## Uso básico

```
/plugin install code-modernization@claude-plugins-official
/code-modernization:modernize
/code-modernization:modernize-preflight <name> --source <path>
/code-modernization:modernize-status <name>
```

Opcionales: `scc` o `cloc`, Python 3.8+ y el toolchain del stack. Recomiendan arrancar con un piloto de un solo módulo.

**Trampas:**
- Si el sistema viejo no se puede ejecutar localmente (mainframe), lo mejor que podés sacar es PARTLY PROVEN.
- La extracción de reglas no es determinista: dos corridas pueden dar reglas distintas.
- Que no toque el código legacy es por convención y reglas deny recomendadas; un script que abra archivos por su cuenta no queda cubierto. No hace commits.
- Telemetría de conteos activada por defecto, con un ping por versión y por máquina al iniciar sesión aunque no uses el plugin. Se apaga con `CODE_MODERNIZATION_TELEMETRY=0` o `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=1`.
- En Windows los hooks necesitan Git Bash.

Del mismo marketplace: [[claude-code-setup]].

**Licencia**: Apache-2.0
