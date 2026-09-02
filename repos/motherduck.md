---
title: motherduck
url: https://motherduck.com
tags: [sql, data-pipeline, saas, mcp, python]
added: 2026-09-02
added_by: Guille
---

Analytics serverless sobre DuckDB, con ejecución híbrida: las etapas de una query corren en tu laptop, en la nube, o repartidas entre las dos. Fundada por Jordan Tigani (ex-BigQuery).

## Por qué vale la pena

- **El dual execution es el diferencial**: no es "DuckDB hosteado", es un planner que parte la query entre local y cloud, así que los datos que ya tenés en la máquina no viajan.
- **Free tier usable sin tarjeta de crédito**: 10 GB de storage, 10 hs/mes de compute Pulse, hasta 3 usuarios y 2 service accounts.
- **Precios públicos y por segundo**: storage a $0.04/GB/mes; compute desde $0.60/CU-hora (Pulse, medido por query) hasta $24/h (Giga). El plan Business arranca en $250/org/mes + uso.
- **Una instancia DuckDB aislada por usuario**, sin clusters compartidos, con hasta 16 read-scaling replicas y zero-copy shares entre cuentas.
- **Endpoint MCP** para conectar Claude, ChatGPT o Cursor directo contra los datos, más Guides (contexto de negocio), Dives (visualizaciones) y Flights (pipelines Python agendados).
- **La org publica OSS real alrededor**: `mcp-server-motherduck` (MIT, 517 stars), `metabase_duckdb_driver` y `grafana-duckdb-datasource` (Apache-2.0), `duckdb-async` (MIT), conectores de Power Query y Tableau.

## Uso básico

```bash
pip install duckdb==1.5.5
```

```python
import duckdb
con = duckdb.connect('md:')                          # auth por browser
con = duckdb.connect('md:?motherduck_token=<token>') # auth por token
local_con.sql("ATTACH 'md:my_db'")                   # desde una conexión local
```

Requiere DuckDB 1.4.1–1.5.5 y Python 3.4+, sobre Linux x64 (glibc 2.31+) o macOS 11+.

**Lo que conviene tener presente**: el servicio es **propietario** y la extensión `motherduck` que hace el dual execution no es open source — ahí está el lock-in. El "Starting from $0" del plan Lite es el piso, no el plan: pasados los 10 GB o las 10 hs se factura por uso. Y **no hay región en Latinoamérica**: las 6 son de AWS (us-east-1, us-west-2, eu-west-1, eu-central-1, ap-northeast-1, ap-southeast-2) y una organización vive en una sola, así que desde acá lo más cerca es us-east-1.

No es un open-core hostil: DuckDB Labs (spin-off del CWI) co-creó MotherDuck y tiene equity, y deliberadamente no monetiza vía cloud service. Son empresas separadas. Entidad legal declarada: MotherDuck Corporation (Seattle, WA), ToS con fecha 10-feb-2026.

Relacionado: [[harlequin]] es una TUI SQL que habla DuckDB y sirve para consultarlo desde la terminal; [[cocoindex]] para el lado de pipelines.

**Licencia**: SaaS propietario (DuckDB upstream es MIT; los conectores de la org son MIT/Apache-2.0)
