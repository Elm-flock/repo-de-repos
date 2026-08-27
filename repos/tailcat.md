---
title: "tailcat"
url: "https://github.com/tailscale/tailcat"
tags: [cli, networking, wireguard, p2p, golang, tailscale]
added: "2026-08-27"
added_by: "Denis Hugo Perafan"
---

Como netcat pero sobre el data plane de Tailscale (magicsock + WireGuard + DERP), sin usar el control plane de Tailscale. No requiere cuenta de Tailscale ni acceso root/admin — es una librería y CLI en userspace que no toca rutas ni DNS del sistema.

## Por qué vale la pena

- Intercambio de metadata de conexión totalmente out-of-band: un lado corre `tailcat` (servidor) y obtiene un token corto; el otro lado usa ese token para conectarse, sin coordinación central.
- Todo el tráfico va cifrado end-to-end con WireGuard; el bootstrap inicial pasa por un relay DERP (gratuito y rate-limited por defecto, `https://tailcat.dev/derpmap.json`) y luego magicsock intenta upgrade a conexión P2P directa vía NAT traversal.
- Usable como CLI (`cmd/tailcat`) o como librería Go (`github.com/tailscale/tailcat`).
- Soporta más que pipes stdin/stdout: forward de puertos TCP locales (`--serve=8080`), servidor SSH sin auth, proxy SOCKS5 sobre el túnel, exit node, y comandos `ping --until-direct` / `parse` / `resolve` para depurar tokens y DERP.
- Demo experimental en el navegador compilado a WebAssembly (https://tailscale.github.io/tailcat/), interoperable con la CLI.

## Uso básico

```sh
go install github.com/tailscale/tailcat/cmd/tailcat@latest
```

```sh
# servidor
$ tailcat
# 🐈 Server listening with new address: tcomFwWCCcjS5nKNqAod034nWoJZW0LZqDhhC8U_dKdnDRYQ8uNGFpGQEu

# cliente
$ echo hello | tailcat tcomFwWCCcjS5nKNqAod034nWoJZW0LZqDhhC8U_dKdnDRYQ8uNGFpGQEu
```

**Licencia**: BSD-3-Clause
