---
title: rea
url: https://github.com/morluto/rea
tags: [reverse-engineering, mcp, coding-agent, cli, typescript, mit]
added: 2026-10-07
added_by: Denis
---

MCP y CLI que le dan al agente de código herramientas de ingeniería inversa: binarios nativos, apps JS/Electron, assemblies .NET, APKs, firmware y sitios web. La idea es "vi una feature en esta app, explicame cómo funciona y armame una parecida para mi proyecto": el agente inspecciona sin código fuente, muestra la evidencia y reconstruye. Todo corre local.

## Por qué vale la pena

- **Un solo MCP para todo el stack de RE**: delega el análisis nativo profundo en Hopper, Ghidra 12.1.x (con JDK 21) o IDA Pro vía `mrexodia/ida-pro-mcp`. Si hay más de un motor instalado no elige solo: hay que fijarlo con `--provider` o `REA_ANALYSIS_PROVIDER`, y nunca cae a otro en silencio.
- **~133 herramientas en 12 familias**: inspección nativa (41: funciones, pseudocódigo, assembly, strings, referencias, call graphs), Mach-O/firmas/plists sin abrir Hopper, .NET (metadata y CIL sin cargar el assembly), APK con JADX, firmware con Binwalk/Unblob, observación de navegador por CDP y comparación de capturas de comportamiento.
- **JS/Electron sin motores ni ejecución**: `analyze-javascript-application` mapea módulos, imports, source maps, rutas, canales IPC y storage de un directorio o `.asar` sin correr la app y sin Hopper ni Ghidra.
- **Evidencia en vez de afirmaciones**: cada resultado trae ubicación, motor, confianza y limitaciones. Los chequeos de reconstrucción devuelven pass, fail o unknown, y la falta de evidencia no cuenta como pass. Aclara que no recupera el código fuente original.
- **Snapshots reutilizables**: guarda resultados y los reusa solo si coinciden los bytes del target, la operación, los parámetros y el motor, sin relanzar el proveedor.
- **Caso real**: en la reconstrucción de DX-Ball (juego de Windows a C mantenible) con el proveedor de Ghidra, una función reconstruida pasa 3.205 casos contra el x86 original y reproduce sus 63 bytes compilados.
- **Multi-agente**: el setup registra el MCP y una skill de workflow en Claude Code, Codex, Cursor, Gemini CLI, Windsurf, OpenCode, Antigravity, Copilot CLI y VS Code, entre otros. Muestra los cambios y hace backup de la config antes de aplicarlos.
- **Soporta CachyOS y Arch explícitamente**, además de Ubuntu 24.04+, Fedora 41+ y macOS 12+. En Linux, la demo de Hopper corre en un display virtual (Xvfb) sin tocar tu escritorio.

## Uso básico

```bash
npx rea-agents setup        # elige agentes, registra el MCP y opcionalmente instala Hopper (pide permiso)
# sin setup, para una app Electron/JS extraída o un .asar:
npx -y rea-agents@latest analyze-javascript-application /ruta/absoluta/app --json
rea doctor --provider ghidra --json   # chequeo acotado al motor que vas a usar
```

Después del setup, reiniciar el agente y pedir algo como "entendé cómo funciona la búsqueda en la app X, mostrame la evidencia y armá algo parecido para mi proyecto". Requiere Node 22.19+, 24.11+ o 26+.

**Trampas:**
- **Legal**: el propio repo aclara que es para investigación legítima y que la autorización corre por cuenta de quien lo usa. Muchas EULAs prohíben la ingeniería inversa: revisar antes de usarlo sobre software de terceros en trabajo de cliente.
- **Se mueve muy rápido**: pasó de v3.2.0 a v5.0.0 entre el 3 y el 7 de octubre de 2026, con dos majors en tres días. Fijar la versión si se integra en un flujo.
- **Hopper es comercial**: la demo tiene límites puestos por el vendor. Ghidra es gratis pero hay que instalarlo aparte, igual que IDA.
- **Windows** es experimental: solo Ghidra, con ejecutables PE x86-64 nativos en NTFS local.

**Licencia**: MIT
