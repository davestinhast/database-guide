<div align="center">
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/elasticsearch/elasticsearch-original.svg" width="120"/>

# Elasticsearch

![Rating](https://img.shields.io/badge/rating-★★★★-blue?style=flat-square)
![License](https://img.shields.io/badge/license-AGPL_v3_(2024)-green?style=flat-square)
![Type](https://img.shields.io/badge/type-Search_Engine_%2F_Analytics-yellow?style=flat-square)
![Language](https://img.shields.io/badge/escrito_en-Java-lightgrey?style=flat-square)

**El motor de búsqueda full-text más usado del mundo. Logs, analytics, autocompletado a escala. Revirtió a AGPL en 2024 tras el drama de licencias.**

</div>

---

##  Quick stats

| Atributo | Valor |
|---|---|
| Tipo | Search Engine + Documento (NoSQL) |
| ACID |  (eventual consistency, no transacciones) |
| Licencia | **AGPL v3** (revertido desde SSPL en 2024) |
| Lanzamiento | 2010 |
| DB-Engines rank | #8 |
| Stack | ELK / EFK (Elasticsearch + Logstash/Fluentd + Kibana) |
| Creador | Elastic NV |
| Casos de uso | Wikipedia, GitHub (búsqueda), Netflix, LinkedIn |

---

##  Historia de licencias (importante)

```
2010–2021:  Apache 2.0  (open source real)
2021:       SSPL  (bait-and-switch para atacar a AWS)
2021:       Amazon forkea → crea OpenSearch (Apache 2.0) 
2024:       Elastic revierte a AGPL  (parcialmente)
```

> El daño de confianza de 2021 permanece. **OpenSearch** tiene ahora comunidad propia y AWS lo prefiere. Ambas son opciones válidas.

---

##  Cuándo usarlo

- Full-text search avanzado (relevancia, fuzzy, multilenguaje)
- Logging y observabilidad (ELK stack — el estándar)
- Analytics en tiempo real sobre grandes volúmenes de datos
- Autocompletado y search-as-you-type
- E-commerce search (productos, filtros, facetas)
- SIEM / seguridad (Elastic Security)
- APM y trazas distribuidas (Elastic APM)

##  Cuándo NO usarlo

- Base de datos primaria con transacciones → PostgreSQL
- Cache → Redis
- Grafos → Neo4j
- Time series puro → InfluxDB o TimescaleDB
- Si la búsqueda que necesitas la hace PostgreSQL FTS (para <10M docs)

---

##  Performance

```
Indexación:              ~50,000–100,000 docs/seg (depende de tamaño)
Búsqueda simple:         <10ms (en índices calientes, NVMe)
Aggregations complejas:  50ms–2s (depende de dataset y shards)
Escalabilidad:           Horizontal (shards + réplicas)
```

---

## ️ ELK Stack — la combinación clásica

```
Logs → Logstash/Fluentd → Elasticsearch → Kibana (visualización)
APM  → Elastic Agent → Elasticsearch → Kibana APM
SIEM → Beats → Elasticsearch → Kibana Security
```

---

## 🆚 Elasticsearch vs OpenSearch (2025)

| Aspecto | Elasticsearch | OpenSearch |
|---|---|---|
| Licencia | AGPL v3 | Apache 2.0  |
| Managed gratis | Elastic Cloud Trial | AWS (no free tier) |
| Features avanzados | Más (ML, EQL, ESQL) | Menos |
| Respaldo | Elastic NV | Amazon Web Services |
| API compatibilidad | — | Compatible con ES 7.x |

---

## Precios managed

| Servicio | Free | Paid desde |
|---|---|---|
| **Elastic Cloud** | 14 días trial | $16/mes |
| **AWS OpenSearch** |  | ~$15/mes (t3.small) |
| **Bonsai** | 10K docs / 1 shard | $9.99/mes |
| **Self-hosted** |  Gratis (AGPL) | Solo infraestructura |

---

##  Tutoriales

### English
[![ES fCC](https://img.youtube.com/vi/ZP0NmfyfsoM/mqdefault.jpg)](https://www.youtube.com/watch?v=ZP0NmfyfsoM)

### 中文
[Elasticsearch 7 入门](https://www.bilibili.com/video/BV17a411B7ZV)

---

##  Links

-  [Documentación oficial](https://www.elastic.co/guide/index.html)
-  [OpenSearch docs (fork)](https://opensearch.org/docs/)
-  [Elastic Cloud trial](https://www.elastic.co/cloud)
-  [Kibana — visualización de datos](https://www.elastic.co/kibana)

---

> [← README](../README.md)
