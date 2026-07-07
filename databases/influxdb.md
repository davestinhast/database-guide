<div align="center">
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/influxdb/influxdb-original.svg" width="120"/>

# InfluxDB

![Rating](https://img.shields.io/badge/rating-★★★★-blue?style=flat-square)
![License](https://img.shields.io/badge/license-MIT_%281.x%29_%2F_Proprietary_%282.x%2B%29-orange?style=flat-square)
![Type](https://img.shields.io/badge/type-Time_Series-teal?style=flat-square)
![Language](https://img.shields.io/badge/escrito_en-Go-lightgrey?style=flat-square)

**El #1 en bases de datos de series temporales. IoT, métricas, monitoreo, logs con timestamp. Si los datos tienen tiempo, InfluxDB es tu arma.**

</div>

---

##  Quick stats

| Atributo | Valor |
|---|---|
| Tipo | Time Series Database (TSDB) |
| ACID | Parcial (dentro de una serie temporal) |
| Licencia | MIT (v1.x OSS) / Propietario (v2.x+, Edge) |
| Lanzamiento | 2013 |
| DB-Engines rank | **#1 en Time Series** |
| Query language | InfluxQL (SQL-like), Flux (funcional) |
| Stack | TICK: Telegraf + InfluxDB + Chronograf + Kapacitor |
| Creador | InfluxData |

---

##  Cuándo usarlo

- Métricas de servidores y sistemas (CPU, RAM, I/O)
- IoT — sensores, telemetría, datos de dispositivos
- Monitoreo de aplicaciones y microservicios
- Datos financieros con timestamp (precios, trades)
- Analytics de eventos con alta frecuencia
- Dashboards en tiempo real (Grafana + InfluxDB = combo clásico)
- Redes eléctricas, plantas industriales (SCADA)

##  Cuándo NO usarlo

- Datos relacionales con JOINs → PostgreSQL
- Búsqueda full-text → Elasticsearch
- Datos de grafos → Neo4j
- Cache → Redis
- Series temporales simples en PostgreSQL (TimescaleDB puede ser suficiente)

---

##  Performance

```
Ingestión (InfluxDB OSS, NVMe):   ~300,000 puntos/seg
Ingestión (InfluxDB Cloud):        Escala horizontal
Queries de rango temporal:         <5ms en datos recientes (hot)
Compresión de datos:               ~90% vs almacenamiento raw
Retención:                         Configurable por bucket
```

---

##  Stack recomendado — TICK

```
Telegraf   → Agente de colección (700+ plugins: CPU, Docker, MQTT, SQL...)
InfluxDB   → Almacenamiento y query
Chronograf → UI de exploración (alternativa a Grafana)
Kapacitor  → Alertas y procesamiento de stream

Alternativa moderna: Telegraf → InfluxDB → Grafana (más popular)
```

---

##  InfluxQL básico

```sql
-- Últimas 24 horas de CPU de un host
SELECT mean("usage_user") AS "cpu_avg"
FROM "cpu"
WHERE "host" = 'server01'
  AND time > now() - 24h
GROUP BY time(1h)

-- Top 5 hosts por memoria usada
SELECT max("used_percent") FROM "mem"
WHERE time > now() - 1h
GROUP BY "host"
ORDER BY max DESC LIMIT 5
```

---

## Precios

| Servicio | Free | Paid desde |
|---|---|---|
| **InfluxDB OSS 1.x** |  Gratis (MIT) | — |
| **InfluxDB Cloud Serverless** | 5 días trial | $0 con límites + $0.008/MB escritura |
| **InfluxDB Clustered** |  | Enterprise (custom) |
| **Self-hosted v2.x** |  Gratis (para uso no-cloud) | — |

> [AVISO] InfluxDB 2.x+ cambió a licencia propietaria para el core. La versión 1.x sigue siendo MIT. Alternativa OSS: **VictoriaMetrics** (compatible Prometheus) o **TimescaleDB** (PostgreSQL-based).

---

## 🆚 Alternativas TSDB

| DB | Licencia | Fortaleza |
|---|---|---|
| **InfluxDB 1.x** | MIT  | Ecosistema maduro, TICK stack |
| **TimescaleDB** | Apache 2.0  | PostgreSQL extension — SQL completo |
| **VictoriaMetrics** | Apache 2.0  | Prometheus-compatible, muy rápido |
| **QuestDB** | Apache 2.0  | SQL nativo, alta velocidad ingestión |
| **Prometheus** | Apache 2.0  | Pull model, Kubernetes nativo |

---

##  Links

-  [Documentación oficial](https://docs.influxdata.com/)
-  [Grafana + InfluxDB — guía](https://grafana.com/docs/grafana/latest/datasources/influxdb/)
-  [Telegraf — agente de colección](https://www.influxdata.com/time-series-platform/telegraf/)
-  [TimescaleDB — alternativa PostgreSQL](https://www.timescale.com/)

---

> [← README](../README.md)
