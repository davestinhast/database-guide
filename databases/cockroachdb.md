<div align="center">
<img src="https://avatars.githubusercontent.com/u/12219835?s=120" width="120"/>

# CockroachDB

![Rating](https://img.shields.io/badge/rating-★★★★★-blue?style=flat-square)
![License](https://img.shields.io/badge/license-BSL_→_Apache_2.0_(3_años)-green?style=flat-square)
![Type](https://img.shields.io/badge/type-SQL_Distribuido_ACID-blue?style=flat-square)
![Language](https://img.shields.io/badge/escrito_en-Go-lightgrey?style=flat-square)

**PostgreSQL distribuido globalmente con ACID completo. Sin punto de falla. Escala horizontal sin perder transacciones. El free tier managed más generoso: 5 GB.**

</div>

---

##  Quick stats

| Atributo | Valor |
|---|---|
| Tipo | SQL Distribuido (NewSQL) |
| ACID |  Completo — distribuido, multi-región |
| Licencia | BSL 1.1 → Apache 2.0 (después de 3 años) |
| Lanzamiento | 2015 |
| DB-Engines rank | #30 |
| Compatible con | PostgreSQL wire protocol  |
| Sin SPOF |  Peer-to-peer, geo-distributed |
| Free tier | **5 GiB storage + 50M RU/mes** — nunca expira |

---

##  Cuándo usarlo

- Apps que necesitan distribución geográfica + ACID completo
- Multi-región sin sacrificar consistencia
- Baja latencia para usuarios globales (datos cerca de ellos)
- Proyectos que quieren PostgreSQL-compatible pero distribuido
- Compliance multi-región (GDPR: datos en EU, CCPA: en US)
- Apps críticas con 99.999% uptime requirement

##  Cuándo NO usarlo

- Proyecto single-node sin requisito multi-región → PostgreSQL directo
- Latencia ultra-baja in-process → SQLite
- Datos que NO necesitan distribución (overhead innecesario)
- Analytics pesado → herramienta OLAP dedicada

---

##  Performance — TPC-C (Strong Consistency ACID)

```
tpmC total:          1,680,000
Warehouses:          140,000
Efficiency:          95%
newOrder ops/seg:    28,074
payment ops/seg:     28,237
Escalabilidad:       Lineal con nodos añadidos
Versión tested:      v20.2
```

**Fuente**: [CockroachDB TPC-C benchmark](https://www.cockroachlabs.com/blog/cockroachdb-performance-20-2/)

> El throughput por nodo es menor que PostgreSQL single-node, pero en escala multi-región con ACID completo no hay rival open-source.

---

## ️ Arquitectura — distribución geo

```
                    ┌──────────────────────────────────┐
                    │         CockroachDB Cluster       │
                    │                                  │
   US-East          │   Node 1 ── Node 2 ── Node 3    │
   EU-West    ───→  │   Node 4 ── Node 5 ── Node 6    │
   Asia-Pac         │   Node 7 ── Node 8 ── Node 9    │
                    │                                  │
                    │  Raft consensus entre nodos      │
                    │  Datos replicados automáticamente │
                    │  Failover: < 1 segundo           │
                    └──────────────────────────────────┘
```

---

## Precios

| Plan | Storage | Request Units | Precio |
|---|---|---|---|
| **Free (Serverless)** | **5 GiB** | **50M RU/mes** | **Gratis, nunca expira** |
| **Serverless paid** | Pay-per-use | $1/million RU extra | $0 base + uso |
| **Dedicated (basic)** | 15 GiB | Sin límite | ~$0.20/hora |
| **Dedicated HA** | Custom | Sin límite | ~$0.60/hora+ |

> El free tier de 5 GiB es el más generoso en PostgreSQL-compatible — supera a Neon (512 MB) y Supabase (500 MB).

---

##  Compatibilidad PostgreSQL

```sql
-- CockroachDB entiende PostgreSQL wire protocol
-- Puedes usar libpq, psycopg2, node-postgres, etc.

-- Diferencias principales:
-- 1. SERIAL → secuencias distribuidas (no garantiza orden estricto)
-- 2. No hay LISTEN/NOTIFY
-- 3. Algunas extensiones PostgreSQL no disponibles
-- 4. Transacciones distribuidas son más lentas (network roundtrips)
```

---

##  Links

-  [Documentación oficial](https://www.cockroachlabs.com/docs/)
-  [CockroachDB Serverless — free tier](https://www.cockroachlabs.com/free-tier/)
-  [TPC-C benchmark details](https://www.cockroachlabs.com/blog/cockroachdb-performance-20-2/)
-  [Migración a CockroachDB](https://www.cockroachlabs.com/docs/molt/migrate-to-cockroachdb)

---

> [← README](../README.md)
