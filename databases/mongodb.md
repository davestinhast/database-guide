<div align="center">
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mongodb/mongodb-original.svg" width="120"/>

# MongoDB

![Rating](https://img.shields.io/badge/rating-⭐⭐⭐⭐-blue?style=flat-square)
![License](https://img.shields.io/badge/license-SSPL-red?style=flat-square)
![Type](https://img.shields.io/badge/type-Documento_NoSQL-green?style=flat-square)
![Language](https://img.shields.io/badge/escrito_en-C%2B%2B-lightgrey?style=flat-square)

**El NoSQL más popular del mundo. Documentos JSON, escalabilidad horizontal, y Atlas managed con free tier sólido.**

</div>

---

## ⚡ Quick stats

| Atributo | Valor |
|---|---|
| Tipo | Documento (NoSQL), JSON/BSON |
| ACID | ✅ Completo (desde v4.0, multi-document) |
| Licencia | SSPL (Server Side Public License — no OSS) |
| Lanzamiento | 2009 |
| DB-Engines rank | #5 |
| Managed | MongoDB Atlas (free tier disponible) |
| Creador | MongoDB Inc. |

---

## ✅ Cuándo usarlo

- Datos con estructura variable / semi-estructurada
- Catálogos de productos, perfiles de usuario, contenido CMS
- Prototipado rápido (schema flexible)
- Escala horizontal necesaria (sharding nativo)
- Stack MEAN/MERN (Node.js ecosystem)
- Real-time analytics con aggregation pipeline
- Geoespacial (GeoJSON nativo)

## ❌ Cuándo NO usarlo

- Datos con muchas relaciones complejas → PostgreSQL + JOINs
- Full-text search avanzado → Elasticsearch
- Time series → InfluxDB o TimescaleDB
- Cache → Redis
- Budget muy limitado y necesitas más control → PostgreSQL self-hosted

---

## 📊 Performance

```
Lectura simple (Altoros 2023):    ~58,290 ops/seg
Escritura (WiredTiger):           ~70,000 ops/seg
Latencia p50:                     ~3ms
Latencia p99:                     ~15ms (MongoDB Atlas)
Escalabilidad:                    Sharding horizontal nativo
```

**Fuente**: [Altoros MongoDB Comparative 2023](https://altoros.com/blog/benchmarking-mongodb-7-0/)

---

## 💰 Precios managed — MongoDB Atlas

| Plan | Storage | Límite | Precio |
|---|---|---|---|
| **M0 (Free)** | 512 MB | 100 ops/seg, 500 conexiones | Gratis, nunca expira |
| **M2** | 2 GB | Sin límite ops | $9/mes |
| **M5** | 5 GB | Sin límite ops | $25/mes |
| **M10** | 10 GB | Dedicated | $57/mes |
| **Serverless** | Pay-per-use | Por operación | $0.10/million RPUs |

> ⚠️ M0 tiene hardware compartido y caps duros de ops/seg — no apto para producción con carga variable.

---

## 🎥 Tutoriales

### 🇺🇸 English
[![MongoDB 100s](https://img.youtube.com/vi/-bt_y4Loofg/mqdefault.jpg)](https://www.youtube.com/watch?v=-bt_y4Loofg)
[![MongoDB fCC](https://img.youtube.com/vi/ExcRbA7fy5A/mqdefault.jpg)](https://www.youtube.com/watch?v=ExcRbA7fy5A)
[![MongoDB Amigoscode](https://img.youtube.com/vi/Www6cTUymCY/mqdefault.jpg)](https://www.youtube.com/watch?v=Www6cTUymCY)

### 🇪🇸 Español
[![MongoDB ES HolaMundo](https://img.youtube.com/vi/lWMemC6nBbQ/mqdefault.jpg)](https://www.youtube.com/watch?v=lWMemC6nBbQ)
[![MongoDB Fazt](https://img.youtube.com/vi/wWWNcqzSzs8/mqdefault.jpg)](https://www.youtube.com/watch?v=wWWNcqzSzs8)

### 🇨🇳 中文
[![MongoDB ZH](https://img.youtube.com/vi/gBlH1qvmBuc/mqdefault.jpg)](https://www.bilibili.com/video/BV18s411E78K)

---

## 🔗 Links

- 📖 [Documentación oficial](https://www.mongodb.com/docs/)
- 🎮 [MongoDB Atlas — Free tier](https://www.mongodb.com/cloud/atlas/register)
- 🧪 [MongoDB Playground online](https://mongoplayground.net/)
- 📚 [MongoDB University (cursos gratis)](https://learn.mongodb.com/)

---

> [← README](../README.md)
