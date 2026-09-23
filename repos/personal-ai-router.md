---
title: personal-ai-router
url: https://github.com/NVIDIA/Personal-AI-Router
tags: [inference, gateway, self-hosted, go, nvidia, apache-2.0]
added: 2026-09-23
added_by: Emiliano
---

NVIDIA Personal AI Router (PAIR): junta las máquinas de tu red (PCs con RTX, DGX Spark, Macs M4+) en un "cluster casero" y reparte cada request de Ollama o LM Studio a un nodo libre, detrás de un solo endpoint. **No suma VRAM ni parte modelos**: cada request corre entero en un nodo. Sirve para concurrencia, no para correr modelos más grandes.

## Por qué vale la pena

- **Pensado para multi-agente local**: en la demo de NVIDIA, 5 subagentes con Qwen 3.6 35B A3B tardaron 18 min en una laptop y 8 min 48 s en un cluster de 3 nodos. NVIDIA aclara que no es un benchmark oficial.
- **Endpoints compatibles con Ollama y con OpenAI** en el puerto por defecto del motor (p. ej. `11434/v1/chat/completions`): los clientes existentes no se tocan.
- **Seguridad razonable para una LAN**: descubrimiento por mDNS, pareo con PIN de 6 dígitos y mTLS entre nodos. Los prompts y archivos no salen de la red.
- **Open source y descarga pública sin registro**: Apache-2.0, 1.5k stars. Servicios en Go y app de escritorio en Electron. Hay instaladores para Windows, macOS y Linux (`.deb`), en x64 y ARM.
- Requisitos bajos: RTX serie 20 o superior, DGX Spark/GB10 o Mac M4+, 8 GB de RAM y 20 GB de disco.
- Roadmap sin fechas: llama.cpp, vLLM, EXO, ComfyUI, integración con Tailscale y scheduling consciente del KV cache.

## Uso básico

```bash
sudo apt install ./NVPAIR-Setup-0.1.1-amd64.deb   # Windows/macOS: instalador gráfico
curl http://127.0.0.1:11434/v1/chat/completions -H "Content-Type: application/json" \
  -d '{"model":"<modelo>","messages":[{"role":"user","content":"hola"}]}'
```

En máquinas sin escritorio se usa `nvpair-tui`.

**Trampas:**
- **Beta 0.1.x**: la v0.1.1 sólo corrige el build de la 0.1.0.
- **El scheduler mira carga y uso de GPU, no VRAM ni modelo de GPU**: en un cluster mixto puede mandar trabajo a la máquina lenta.
- Todavía no rutea requests OpenAI entre motores distintos (Ollama con LM Studio).
- Known issues: no detecta servicios colgados, macOS puede dejar de responder en la LAN estando sin cluster y Windows ARM es experimental. En Linux sólo hay `.deb`.
- **Licencia a revisar**: el repo es Apache-2.0, pero trae un `EULA.txt` marcado como *placeholder* que prohíbe redistribuir y modificar. No verificamos si el instalador oficial lo muestra.

Relacionado: [[orcarouter]] rutea por dificultad del prompt entre modelos de API, no entre máquinas. [[tailcat]] va sobre Tailscale, que está en el roadmap de PAIR.

**Licencia**: Apache-2.0 (con un EULA placeholder de NVIDIA en el instalador, ver trampas)
