<div align="center">
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mariadb/mariadb-original.svg" width="120"/>

# MariaDB

![Rating](https://img.shields.io/badge/rating-⭐⭐⭐⭐-blue?style=flat-square)
![License](https://img.shields.io/badge/license-GPL_v2-brightgreen?style=flat-square)
![Type](https://img.shields.io/badge/type-Relacional_ACID-blue?style=flat-square)
![Language](https://img.shields.io/badge/escrito_en-C%2B%2B-lightgrey?style=flat-square)

**El fork de MySQL que escapó de Oracle. Drop-in replacement, 11–16% más rápido, licencia real. Si usas MySQL self-hosted, deberías estar usando esto.**

</div>

---

## ⚡ Quick stats

| Atributo | Valor |
|---|---|
| Tipo | Relacional (SQL) |
| ACID | ✅ Completo |
| Licencia | GPL v2 ✅ (sin dobles licencias Oracle) |
| Lanzamiento | 2009 (fork de MySQL 5.1) |
| DB-Engines rank | #12 |
| Compatibilidad | Drop-in replacement para MySQL |
| Admiration rate SO 2025 | ~36% |
| Creador | Monty Widenius (creador original de MySQL) |

---

## ✅ Cuándo usarlo

- Proyectos nuevos que habrían usado MySQL self-hosted
- Migración desde MySQL sin cambiar código ni queries
- WordPress, Drupal, Joomla en servidores propios
- Stack LAMP con mayor rendimiento que MySQL
- Cuando quieres MySQL features sin depender de Oracle
- Sistemas embebidos (mejor soporte que MySQL)
- Columnstore storage engine para analytics (incluido)

## ❌ Cuándo NO usarlo

- Proyectos nuevos con escala considerable → PostgreSQL directamente
- JSON avanzado, extensions del ecosistema → PostgreSQL gana
- Managed cloud con vendor lock-in → PostgreSQL tiene más opciones

---

## 📊 Performance vs MySQL

```
Lecturas simples:          11–16% más rápido que MySQL (benchmarks 2024)
Escrituras concurrentes:   ~40,000–45,000 ops/seg
Latencia p50:              ~2.5ms
Latencia p99:              ~10ms
InnoDB:                    Compartido, mismo rendimiento base
Aria engine:               Reemplaza MyISAM, más rápido
```

---

## 🔧 Features que MySQL Community no tiene

| Feature | MariaDB | MySQL Community |
|---|---|---|
| Columnstore engine | ✅ Incluido | ❌ |
| Flashback | ✅ | ❌ |
| Dynamic columns | ✅ | ❌ |
| Temporal tables | ✅ Mejorado | Básico |
| Parallel query execution | ✅ | Limitado |
| Roles más completos | ✅ | Básico |

---

## 🔄 Migración MySQL → MariaDB

```bash
# En la mayoría de casos: solo reemplaza el binario
# El protocolo, archivos de datos y queries son compatibles

# Verificar compatibilidad
mysql_upgrade -u root -p

# Los dumps de MySQL funcionan directo en MariaDB
mysqldump -u root -p mydb > backup.sql
mysql -u root -p mydb < backup.sql   # en MariaDB
```

---

## 💰 Precios managed

| Servicio | Free | Paid desde |
|---|---|---|
| **Self-hosted** | ✅ Gratis (GPL v2) | — |
| **AWS RDS MariaDB** | ❌ | ~$13/mes (db.t3.micro) |
| **DigitalOcean Managed** | ❌ | $15/mes |
| **Railway** | $5 crédito | $5/mes + usage |
| **PlanetScale** (compatible) | 🔴 Free eliminado | $5/mes |

---

## 🎥 Tutoriales

### 🇺🇸 English
[![MariaDB fCC](https://img.youtube.com/vi/_AMj02sANpI/mqdefault.jpg)](https://www.youtube.com/watch?v=_AMj02sANpI)

### 🇪🇸 Español
🔗 Los tutoriales de MySQL aplican directamente — misma sintaxis
[![MySQL ES TodoCode](https://img.youtube.com/vi/wpdHPqONnqc/mqdefault.jpg)](https://www.youtube.com/watch?v=wpdHPqONnqc)

### 🇨🇳 中文
🔗 Los cursos de MySQL de 尚硅谷 y 黑马程序员 aplican directamente

---

## 🔗 Links

- 📖 [Documentación oficial](https://mariadb.com/kb/en/)
- 🔄 [Migración MySQL → MariaDB](https://mariadb.com/kb/en/moving-from-mysql-to-mariadb/)
- 📊 [MariaDB vs MySQL benchmarks](https://mariadb.com/resources/blog/mariadb-vs-mysql/)

---

> [← README](../README.md)
