<div align="center">
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/postgresql/postgresql-original.svg" width="120"/>

# PostgreSQL

![Rating](https://img.shields.io/badge/rating-⭐⭐⭐⭐⭐-blue?style=flat-square)
![License](https://img.shields.io/badge/license-PostgreSQL_(OSS)-green?style=flat-square)
![Type](https://img.shields.io/badge/type-Relacional_ACID-blue?style=flat-square)
![Language](https://img.shields.io/badge/escrito_en-C-lightgrey?style=flat-square)

**La mejor base de datos relacional de propósito general. Gratis, open-source, y más poderosa que muchas enterprise.**

</div>

---

## ⚡ Quick stats

| Atributo | Valor |
|---|---|
| Tipo | Relacional (SQL), Multi-model |
| ACID | ✅ Completo |
| Licencia | PostgreSQL License (OSS, más permisiva que MIT) |
| Lanzamiento | 1996 |
| DB-Engines rank | #4 (subiendo) |
| Admiration rate SO 2025 | **46.5%** (el más alto de los relacionales) |
| Managed gratis | Neon, Supabase, Railway, CockroachDB |
| Creador | PostgreSQL Global Development Group |

---

## ✅ Cuándo usarlo

- App web de cualquier tamaño
- Datos con relaciones complejas (JOINs)
- Necesitas JSON + SQL en la misma query (`jsonb`)
- Full-text search sin Elasticsearch
- GIS / datos geoespaciales (PostGIS extension)
- Time series con TimescaleDB extension
- Cuando quieres una DB que te dure 10+ años

## ❌ Cuándo NO usarlo

- Necesitas >1M writes/seg (usa Cassandra/ScyllaDB)
- App embebida / mobile sin servidor (usa SQLite)
- Cache puro (usa Redis)
- Datos de grafos muy complejos (usa Neo4j)

---

## 📊 Performance

```
Lectura simple (tuned, NVMe):  ~69,000 TPS (OCI benchmark)
Escritura (WAL, MVCC):         ~30,000 ops/seg
Latencia p50:                  ~2ms
Latencia p99:                  ~10ms
Escalabilidad:                 Vertical + read replicas
```

---

## 💰 Precios managed

| Servicio | Free | Paid desde |
|---|---|---|
| **Neon** | 512 MB, 100 proyectos | ~$19/mes |
| **Supabase** | 500 MB, 2 proyectos | $25/mes |
| **Railway** | $5 crédito trial | $5/mes |
| **DigitalOcean** | ❌ | $15/mes |
| **Render** | ⚠️ 30 días (se borra) | $7/mes |

---

## 🎥 Tutoriales

### 🇺🇸 English
[![PostgreSQL 100s](https://img.youtube.com/vi/n2Fluyr3lbc/mqdefault.jpg)](https://www.youtube.com/watch?v=n2Fluyr3lbc)
[![PostgreSQL Full](https://img.youtube.com/vi/qw--VYLpxG4/mqdefault.jpg)](https://www.youtube.com/watch?v=qw--VYLpxG4)

### 🇪🇸 Español
[![PostgreSQL ES](https://img.youtube.com/vi/0Hf7WT9cKoA/mqdefault.jpg)](https://www.youtube.com/watch?v=0Hf7WT9cKoA)
[![PostgreSQL HolaMundo](https://img.youtube.com/vi/G_gmEEuuoMk/mqdefault.jpg)](https://www.youtube.com/watch?v=G_gmEEuuoMk)

### 🇨🇳 中文
[![PostgreSQL ZH](https://img.youtube.com/vi/eMIxuk0nzsQ/mqdefault.jpg)](https://www.bilibili.com/video/BV1TV4y147kY)

---

## 🔗 Links

- 📖 [Documentación oficial](https://www.postgresql.org/docs/)
- 🎮 [Ejercicios interactivos — pgexercises](https://pgexercises.com/)
- 🚀 [Supabase (managed + auth + storage)](https://supabase.com)
- 🌐 [Neon (serverless, free tier generoso)](https://neon.tech)

---

> [← README](../README.md)
