<div align="center">
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/redis/redis-original.svg" width="120"/>

# Redis / Valkey

![Rating Redis](https://img.shields.io/badge/Redis-★★★★-red?style=flat-square)
![Rating Valkey](https://img.shields.io/badge/Valkey-★★★★★-brightgreen?style=flat-square)
![Type](https://img.shields.io/badge/type-In--Memory_Key--Value-red?style=flat-square)
![Language](https://img.shields.io/badge/escrito_en-C-lightgrey?style=flat-square)

**Dos proyectos compatibles con historias de licencia y gobernanza distintas. Valkey conserva BSD-3; Redis 8 ofrece AGPLv3 además de RSALv2 y SSPLv1.**

</div>

---

##  Quick stats

| Atributo | Redis | Valkey |
|---|---|---|
| Tipo | In-Memory Key-Value / Multi-model | In-Memory Key-Value |
| ACID |  (AOF/RDB durability, no ACID completo) |  mismo modelo |
| Licencia | **AGPLv3, RSALv2 o SSPLv1** (Redis 8+) | **BSD-3** |
| Lanzamiento | 2009 | 2024 (fork de Redis 7.2) |
| DB-Engines rank | #6 | N/A (nuevo) |
| Respaldo | Redis Inc. | Linux Foundation, Amazon, Google, Oracle |
| Managed gratis | Upstash (256 MB) | — |

---

## Historia de licencias

```
Redis <= 7.2: BSD-3
Redis 7.4–7.8: RSALv2 o SSPLv1 (source-available)
Redis >= 8: AGPLv3, RSALv2 o SSPLv1
Valkey: BSD-3 bajo gobernanza de Linux Foundation
```

El cambio de 2024 motivó la creación de Valkey. En mayo de 2025 Redis añadió
AGPLv3, una licencia open source aprobada por la OSI, para Redis 8 y posteriores.
Llamar “propietario” a todo Redis actual ya no es correcto.

**Verificado:** 2026-07-07 · [Licencias oficiales de Redis](https://redis.io/legal/licenses/) · [Licencia de Valkey](https://github.com/valkey-io/valkey/blob/unstable/COPYING)

---

## Rendimiento

Redis y Valkey pueden superar cientos de miles de operaciones por segundo con
pipelining, pero una cifra aislada no permite declarar un ganador. El resultado
depende de la versión, CPU, red, tamaño de valores, persistencia, número de
clientes y distribución de comandos.

Para decidir entre ambos, ejecuta `memtier_benchmark` o `redis-benchmark` con tu
configuración de durabilidad y tu mezcla real de comandos. No compares un
resultado de Redis en un portátil con uno de Valkey en AWS Graviton.

Referencias: [benchmark oficial de Redis](https://redis.io/docs/latest/operate/oss_and_stack/management/optimization/benchmarks/) y [herramienta de benchmarking de Valkey](https://valkey.io/topics/benchmark/).

---

##  Cuándo usarlo

- Cache de sesiones y datos de usuario
- Rate limiting / throttling
- Pub/Sub y message queues
- Leaderboards y contadores en tiempo real
- Almacenamiento de tokens JWT / OAuth
- Job queues (con BullMQ, Sidekiq, Celery)
- Datos que necesitan TTL automático

##  Cuándo NO usarlo

- Datos primarios persistentes → PostgreSQL
- Datos relacionales → cualquier SQL
- Búsqueda full-text → Elasticsearch
- Time series → InfluxDB

---

## Precios managed

| Servicio | Free | Paid desde | Nota |
|---|---|---|---|
| **Upstash** | 256 MB, 500K cmds/mes | $10/mes (fixed) | Serverless, por comando |
| **Redis Cloud** | 30 MB (muy limitado) | $5/mes | Managed by Redis Inc. |
| **AWS ElastiCache** |  | ~$15/mes | Redis OSS + managed |
| **Railway** | $5 crédito | $5/mes + usage | Cualquier version |

>  Para proyectos pequeños: **Upstash** free tier es el mejor de la categoría.

---

## ¿Cuál usar?

```
Licencia permisiva y gobernanza comunitaria → Valkey (BSD-3)
Features integradas de Redis 8 y soporte Redis → Redis 8 (AGPLv3 disponible)
Managed cloud                              → compara SLA, precio y compatibilidad
Migración desde Redis 7.2                  → prueba compatibilidad antes de cambiar
```

---

##  Tutoriales

### English
[![Redis 100s](https://img.youtube.com/vi/G1rOthIU-uo/mqdefault.jpg)](https://www.youtube.com/watch?v=G1rOthIU-uo)
[![Redis Crash](https://img.youtube.com/vi/jgpVdJB2sKQ/mqdefault.jpg)](https://www.youtube.com/watch?v=jgpVdJB2sKQ)
[![Redis Hussein](https://img.youtube.com/vi/sVCZo5B8ghE/mqdefault.jpg)](https://www.youtube.com/watch?v=sVCZo5B8ghE)

### 中文
[Redis 7 入门到实战](https://www.bilibili.com/video/BV1Rv41177Af)

---

##  Links

-  [Documentación Redis](https://redis.io/docs/)
-  [Documentación Valkey](https://valkey.io/docs/)
-  [Licencias Redis por versión](https://redis.io/legal/licenses/)
-  [Upstash — Redis serverless gratis](https://upstash.com/)

---

> [← README](../README.md)
