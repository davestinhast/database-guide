<div align="center">
<img src="https://avatars.githubusercontent.com/u/125723492?s=120" width="120"/>

# Valkey

![Rating](https://img.shields.io/badge/rating-★★★★★-brightgreen?style=flat-square)
![License](https://img.shields.io/badge/license-BSD--3-brightgreen?style=flat-square)
![Type](https://img.shields.io/badge/type-In--Memory_Key--Value-red?style=flat-square)
![Language](https://img.shields.io/badge/escrito_en-C-lightgrey?style=flat-square)

**Fork de Redis 7.2.4 con licencia BSD-3 y gobernanza de la Linux Foundation. Es una alternativa compatible, pero la compatibilidad y el rendimiento deben validarse con cada workload.**

</div>

---

## Quick stats

| Atributo | Valor |
|---|---|
| Tipo | In-Memory Key-Value / Multi-model |
| ACID | Durabilidad configurable (AOF/RDB), no ACID clásico |
| Licencia | **BSD-3** (OSS real, sin restricciones) |
| Lanzamiento | Marzo 2024 (fork de Redis 7.2.4) |
| Respaldado por | Linux Foundation, Amazon, Google, Oracle, Snap, Ericsson |
| Compatibilidad | Drop-in con Redis (mismo protocolo, mismos comandos) |
| Último release estable | v8.1 (2025) |
| Creador | Fork comunitario desde Redis 7.2 |

---

## Para qué sirve

Exactamente lo mismo que Redis pe, porque es un fork compatible. La diferencia está en la licencia y la velocidad, no en los casos de uso.

Sirve para:

- **Caché** — el caso de uso principal. Guardar resultados de queries de base de datos, respuestas de API, fragmentos de HTML, para servirlos sin ir al disco. Sub-milisegundo siempre.
- **Sesiones de usuario** — guardar tokens de sesión, estado de autenticación, carrito de compras temporal. Con TTL nativo, las sesiones expiradas se eliminan solas.
- **Colas de mensajes** — con los tipos de dato List o Streams, Valkey/Redis es la queue de mensajes más simple disponible. Celery en Python la usa por defecto.
- **Rate limiting** — contar cuántas requests hizo un usuario en los últimos 60 segundos con operaciones atómicas `INCR` y `EXPIRE`.
- **Pub/Sub** — notificaciones en tiempo real entre servicios, aunque para producción seria Kafka o RabbitMQ son más robustos.
- **Leaderboards** — el tipo de dato Sorted Set es perfecto para rankings ordenados por puntuación.
- **Locks distribuidos** — el comando `SET key value NX EX seconds` implementa un mutex distribuido entre múltiples instancias de tu app.
- **Contadores en tiempo real** — visitas de página, clicks, likes, todo actualizable en tiempo real sin tocar la base de datos principal.

---

## Por qué existe Valkey — el drama de Redis 2024

En marzo de 2024, Redis Ltd. cambió la licencia de Redis de BSD-3 a SSPL + RSALv2. Ninguna de esas dos licencias estaba aprobada por la OSI, y varios proveedores impulsaron Valkey desde Redis 7.2.4. En mayo de 2025 Redis 8 añadió AGPLv3 como tercera opción, por lo que Redis volvió a ofrecer una licencia open source, aunque copyleft.

La comunidad respondió pe: en dos semanas, la Linux Foundation anunció Valkey con el respaldo de Amazon, Google, Oracle, Snap, y Ericsson. El fork partió desde Redis 7.2.4.

```
Redis 7.2.4 (BSD-3, última versión open-source)
    ↓ fork marzo 2024
Valkey 7.2.x → Valkey 8.0 (sept 2024) → Valkey 8.1 (2025)
```

Amazon Web Services dejó de actualizar ElastiCache con nuevas versiones de Redis y migró a Valkey. Google Cloud y otros proveedores hicieron lo mismo.

---

## Valkey vs Redis — diferencias reales

| | Valkey | Redis |
|---|---|---|
| **Licencia** | BSD-3 (permisiva) | AGPLv3, RSALv2 o SSPLv1 en Redis 8+ |
| **Rendimiento** | Depende del workload y configuración | Depende del workload y configuración |
| **Respaldo** | Linux Foundation | Redis Ltd. |
| **Managed AWS** | ElastiCache for Valkey | ElastiCache for Redis (legacy) |
| **Compatible** | Sí, drop-in | baseline |
| **Multi-threading** | Mejorado en v8 | disponible desde v6 |

Las cifras publicadas por proyectos y proveedores sirven como punto de partida,
no como garantía. Compara versiones equivalentes con la misma máquina,
persistencia, clientes, tamaño de valores y mezcla de comandos.

**Licencias verificadas:** 2026-07-07 · [Redis](https://redis.io/legal/licenses/) · [Valkey](https://github.com/valkey-io/valkey/blob/unstable/COPYING)

---

## Tipos de datos disponibles

```
String       → texto, enteros, flotantes. El tipo base.
List         → lista ordenada (deque). Push/pop desde ambos extremos.
Hash         → mapa de campos (como un objeto JSON pero directo en Valkey).
Set          → conjunto sin orden, sin duplicados.
Sorted Set   → conjunto con score, permite rankings y rangos.
Stream       → log de eventos append-only. Kafka simplificado.
Bitmap       → bits individuales para conteos ultracompactos.
HyperLogLog  → contador de únicos probabilístico (muy poca memoria).
Geospatial   → puntos GPS, radio search.
```

---

## Cuándo usarlo

- Necesitas caché en tu aplicación y no quieres pagar licencia
- Ya usabas Redis y quieres migrar a algo con licencia limpia
- Rate limiting, sesiones, contadores en tiempo real
- Queue de mensajes simple (Celery, sidekiq, resque)
- Cualquier cosa donde Redis era la respuesta antes de 2024

---

## Cuándo NO usarlo

- Tu base de datos principal — Valkey es in-memory, los datos pueden perderse si el proceso muere sin persistencia configurada pe.
- Datos que superen tu RAM disponible — si el dataset no cabe en memoria, usa otra opción.
- Queries complejas sobre datos relacionales — para eso PostgreSQL.

---

## Free tier / managed

| Servicio | Soporte Valkey | Free tier |
|---|---|---|
| **Upstash** | Valkey (anunciado 2024) | 256 MB, 500K commands/mes |
| **AWS ElastiCache** | Valkey nativo desde 2024 | No free tier (cargo por hora) |
| **Aiven** | Valkey disponible | 30 días trial |
| **Self-hosted** | Gratis (BSD-3) | Solo infra |

---

> [← Volver al README](../README.md)
