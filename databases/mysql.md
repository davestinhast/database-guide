<div align="center">
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mysql/mysql-original.svg" width="120"/>

# MySQL

![Rating](https://img.shields.io/badge/rating-⭐⭐⭐-orange?style=flat-square)
![License](https://img.shields.io/badge/license-GPL_v2_%2F_Commercial-red?style=flat-square)
![Type](https://img.shields.io/badge/type-Relacional_ACID-blue?style=flat-square)
![Language](https://img.shields.io/badge/escrito_en-C%2B%2B-lightgrey?style=flat-square)

**El relacional más conocido del mundo — pero Oracle lo está matando lentamente. Todavía funciona, pero elige mejor.**

</div>

---

## ⚡ Quick stats

| Atributo | Valor |
|---|---|
| Tipo | Relacional (SQL) |
| ACID | ✅ Completo (InnoDB engine) |
| Licencia | GPL v2 (Community) / Comercial (Oracle) |
| Lanzamiento | 1995 |
| DB-Engines rank | #2 (bajando) |
| Admiration rate SO 2025 | **20.5%** (vs 46.5% de PostgreSQL) |
| Contributors activos | ~75 (desde 198 en 2006) |
| Propietario | Oracle Corporation |

---

## ✅ Cuándo usarlo

- Ya tienes MySQL en producción y migrar es costoso
- Stack LAMP / PHP donde MySQL es el default histórico
- Necesitas compatibilidad con herramientas antiguas (cPanel, etc.)
- WordPress, Drupal, Joomla (instalaciones existentes)
- Managed Cloud si usas MySQL Heatwave (AWS RDS, Google Cloud SQL)

## ❌ Cuándo NO usarlo

- Proyectos nuevos → usa **PostgreSQL** o **MariaDB** directamente
- Necesitas JSON avanzado o full-text search → PostgreSQL lo hace mejor
- Self-hosted open-source → **MariaDB** es drop-in replacement y más rápido
- Oracle priorizó la versión comercial; Community Edition está en declive

---

## 📊 Performance

```
Lectura simple (sysbench):     ~48,000 ops/seg
Escritura (InnoDB):            ~40,000 ops/seg
Latencia p50:                  ~3ms
Latencia p99:                  ~12ms
vs MariaDB:                    11–16% más lento (benchmarks 2024)
```

---

## ⚠️ Problemas documentados (2024–2025)

| Issue | Detalle |
|---|---|
| Bug crítico 9.0.0 | Crash al tener >8,000 tablas (Bug #36808732) |
| Layoffs Oracle | Developers de Community Edition fueron despedidos |
| Commit activity | Caída ~4x en 14 años de historia |
| Heatwave focus | Oracle prioriza versión comercial sobre Community |

**Fuentes**: [InfoQ dic 2025](https://www.infoq.com/news/2025/12/mysql-declining-development/) · [DoltHub 2024](https://www.dolthub.com/blog/2024-10-14-is-mysql-dying/)

---

## 💰 Precios managed

| Servicio | Free | Paid desde |
|---|---|---|
| **AWS RDS MySQL** | ❌ | ~$15/mes (db.t3.micro) |
| **Google Cloud SQL** | ❌ | ~$10/mes |
| **PlanetScale** | 🔴 Free tier eliminado abr 2024 | $5/mes |
| **Railway** | $5 crédito one-time | $5/mes |

---

## 🎥 Tutoriales

### 🇺🇸 English
[![MySQL Mosh](https://img.youtube.com/vi/7S_tz1z_5bA/mqdefault.jpg)](https://www.youtube.com/watch?v=7S_tz1z_5bA)
[![MySQL Crash](https://img.youtube.com/vi/9ylj9NR0Lcg/mqdefault.jpg)](https://www.youtube.com/watch?v=9ylj9NR0Lcg)

### 🇪🇸 Español
[![MySQL ES TodoCode](https://img.youtube.com/vi/wpdHPqONnqc/mqdefault.jpg)](https://www.youtube.com/watch?v=wpdHPqONnqc)
[![MySQL Fazt](https://img.youtube.com/vi/OqjnO5gPZoE/mqdefault.jpg)](https://www.youtube.com/watch?v=OqjnO5gPZoE)

### 🇨🇳 中文
[![MySQL ZH](https://img.youtube.com/vi/a9W7OpS4LfI/mqdefault.jpg)](https://www.bilibili.com/video/BV1iq4y1u7vj)

---

## 🔗 Links

- 📖 [Documentación oficial](https://dev.mysql.com/doc/)
- 🔀 [MariaDB — drop-in replacement recomendado](https://mariadb.org/)
- 🚀 [AWS RDS MySQL](https://aws.amazon.com/rds/mysql/)

---

> [← README](../README.md)
