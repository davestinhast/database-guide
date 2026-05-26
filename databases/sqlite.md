<div align="center">
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/sqlite/sqlite-original.svg" width="120"/>

# SQLite

![Rating](https://img.shields.io/badge/rating-★★★★★-blue?style=flat-square)
![License](https://img.shields.io/badge/license-Public_Domain-brightgreen?style=flat-square)
![Type](https://img.shields.io/badge/type-Embebida_ACID-blue?style=flat-square)
![Language](https://img.shields.io/badge/escrito_en-C-lightgrey?style=flat-square)

**La base de datos más deployada del mundo. Está en tu teléfono, en tu browser, en tu avión. Sin servidor, sin configuración, un solo archivo.**

</div>

---

##  Quick stats

| Atributo | Valor |
|---|---|
| Tipo | Embebida (SQL), in-process |
| ACID |  Completo |
| Licencia | Public Domain (sin restricciones absolutas) |
| Lanzamiento | 2000 |
| DB-Engines rank | #9 |
| Deployments estimados | 1,000,000,000+ (teléfonos, browsers, sistemas) |
| Creador | D. Richard Hipp |
| Sin servidor |  Cero configuración, un archivo `.db` |

---

##  Cuándo usarlo

- Apps móviles (iOS, Android — es el default)
- Apps de escritorio (Electron, Qt, WPF)
- Proyectos personales y prototipos
- Archivos de configuración que necesitan queries
- Edge computing y dispositivos IoT
- Testing / CI (en memoria, velocísimo)
- Herramienta CLI con datos persistentes
- Turso (libSQL fork) para SQLite edge con múltiples regiones

##  Cuándo NO usarlo

- Múltiples escritores concurrentes (WAL ayuda pero tiene límites)
- App web con >1K escrituras/seg concurrentes
- Datos distribuidos en varios servidores
- Necesitas roles/permisos granulares de usuario

---

##  Performance

```
Lectura (WAL mode, in-process):  ~100,000 reads/seg
Latencia p50:                    10–20 µs (microsegundos, sin red)
Latencia p99:                    <100 µs
Escritura (WAL, NORMAL sync):    ~35,000 inserts/seg
Escritura (WAL, OFF sync):       ~1,000,000+ inserts/seg (sin durabilidad)
Modo WAL:                        Lecturas y escrituras concurrentes 
```

> La latencia en microsegundos lo hace inigualable para cualquier app in-process. No hay overhead de red.

---

##  Modos importantes

| Modo | Comportamiento |
|---|---|
| **WAL** (Write-Ahead Log) | Lecturas no bloquean escrituras → recomendado para todo |
| **Journal (DELETE)** | Default, más lento, bloqueos más agresivos |
| **In-Memory** (`:memory:`) | Ultra rápido, datos volátiles — perfecto para tests |
| **Shared Cache** | Múltiples conexiones comparten cache — uso avanzado |

```sql
PRAGMA journal_mode=WAL;   -- activa WAL mode
PRAGMA synchronous=NORMAL; -- balance durabilidad/velocidad
PRAGMA cache_size=10000;   -- cache pages en memoria
```

---

##  Variantes modernas

| Proyecto | Descripción |
|---|---|
| **Turso** (libSQL) | SQLite en el edge, múltiples regiones, 5 GB gratis |
| **Litestream** | Replicación continua de SQLite a S3/GCS |
| **LiteFS** | SQLite distribuido (Fly.io) |
| **cr-sqlite** | CRDTs para SQLite — sync sin conflictos |
| **Cloudflare D1** | SQLite serverless en el edge (Workers) |

---

## Precios

| Servicio | Free | Paid desde |
|---|---|---|
| **SQLite self-hosted** |  Gratis total (Public Domain) | — |
| **Turso** (libSQL) | 5 GB, 500M rows read/mes | $4.99/mes |
| **Cloudflare D1** | 5 GB, 25M reads/día | $0.001/million reads |
| **Litestream** |  OSS gratis + costo S3 | ~$0.023/GB en S3 |

---

##  Tutoriales

### English
[![SQLite 100s](https://img.youtube.com/vi/byHcYRpMgI4/mqdefault.jpg)](https://www.youtube.com/watch?v=byHcYRpMgI4)
[![SQLite fCC](https://img.youtube.com/vi/HQp4JhMoHw4/mqdefault.jpg)](https://www.youtube.com/watch?v=HQp4JhMoHw4)

### Español
[![SQLite ES](https://img.youtube.com/vi/ANT5tQm2gUQ/mqdefault.jpg)](https://www.youtube.com/watch?v=ANT5tQm2gUQ)

### 中文
 [SQLite 官方文档 (中文译版)](https://www.sqlite.net.cn/) · [Turso 中文文档](https://docs.turso.tech/)

---

##  Links

-  [Documentación oficial](https://www.sqlite.org/docs.html)
-  [SQLite vs PostgreSQL vs MySQL — comparativa](https://www.sqlite.org/whentouse.html)
-  [Turso — SQLite en el edge (gratis)](https://turso.tech/)
-  [Litestream — replicación a S3](https://litestream.io/)

---

> [← README](../README.md)
