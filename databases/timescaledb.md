<div align="center">
<img src="https://avatars.githubusercontent.com/u/8914246?s=120" width="120"/>

# TimescaleDB

![Rating](https://img.shields.io/badge/rating-★★★★★-blue?style=flat-square)
![License](https://img.shields.io/badge/license-Apache_2.0_%2F_TSL-green?style=flat-square)
![Type](https://img.shields.io/badge/type-Time_Series_sobre_PostgreSQL-teal?style=flat-square)
![Language](https://img.shields.io/badge/escrito_en-C-lightgrey?style=flat-square)

**PostgreSQL con superpoderes para series temporales. Es una extensión, no un fork, así que tienes SQL completo, JOINs, y toda la potencia de Postgres más hypertables con particionado automático por tiempo. La alternativa seria a InfluxDB que no te obliga a aprender otro lenguaje.**

</div>

---

## Quick stats

| Atributo | Valor |
|---|---|
| Tipo | Time Series Database (TSDB), extensión de PostgreSQL |
| ACID | Sí — hereda ACID completo de PostgreSQL |
| Licencia | Apache 2.0 (core) / Timescale License (features avanzados) |
| Lanzamiento | 2017 |
| DB-Engines rank | #2 en Time Series (detrás de InfluxDB) |
| Velocidad vs PostgreSQL | 10x–100x más rápido en queries de tiempo |
| Managed | Timescale Cloud (free tier disponible) |
| Creador | Timescale Inc. |

---

## Para qué sirve

Causa, TimescaleDB existe porque PostgreSQL no está optimizado para el patrón típico de series temporales: insertar millones de filas ordenadas por timestamp y luego consultarlas por rango de tiempo. Vanilla PostgreSQL puede hacerlo pero se pone lento conforme los datos crecen.

TimescaleDB agrega el concepto de **hypertable**: una tabla que se ve y se comporta exactamente igual que una tabla de PostgreSQL, pero por debajo se parte automáticamente en chunks por tiempo. Así, una query `WHERE tiempo > '2025-01-01'` no toca los chunks de 2024, 2023, etc. Solo lee lo relevante.

Sirve para:

- **Monitoreo de infraestructura** — CPU, RAM, latencias, errores, todo con timestamp. Grafana + TimescaleDB es el stack estándar para DevOps/SRE que quiere PostgreSQL.
- **IoT y telemetría** — sensores industriales, flotas de vehículos, dispositivos con datos continuos de medición.
- **Datos financieros** — precios históricos de acciones, tipo de cambio, orderbooks. El hecho de que sea ACID es importante acá pe.
- **Analytics de aplicaciones** — eventos de usuarios, pageviews, conversion funnels todos con timestamp.
- **Redes eléctricas y SCADA** — plantas industriales que necesitan registrar lecturas de sensores cada segundo.
- **Datos climáticos** — temperatura, presión, humedad con timestamps, consultas de promedios horarios o diarios.
- **Logs estructurados** — alternativa a ELK cuando ya tienes PostgreSQL y no quieres otra infraestructura.

---

## La ventaja real sobre InfluxDB

InfluxDB tiene su propio lenguaje de query (InfluxQL o Flux) que hay que aprenderse. TimescaleDB usa SQL estándar pe. Si ya sabes PostgreSQL, ya sabes TimescaleDB. Además, puedes hacer JOINs entre tus métricas y tus tablas de negocio en la misma query, algo imposible en InfluxDB.

```sql
-- Esto funciona en TimescaleDB: JOIN entre métricas y datos de negocio
SELECT s.nombre_servidor, avg(m.cpu_uso) as cpu_promedio
FROM metricas m
JOIN servidores s ON m.servidor_id = s.id
WHERE m.tiempo > NOW() - INTERVAL '1 hour'
GROUP BY s.nombre_servidor
ORDER BY cpu_promedio DESC;
```

Causa, eso en InfluxDB es imposible de hacer directo.

---

## Funciones especiales para tiempo

TimescaleDB agrega funciones SQL que no existen en vanilla PostgreSQL:

```sql
-- Agrupar por intervalos de tiempo automáticamente
SELECT time_bucket('5 minutes', tiempo) AS bucket,
       avg(temperatura) as temp_promedio
FROM sensores
WHERE tiempo > NOW() - INTERVAL '24 hours'
GROUP BY bucket
ORDER BY bucket;

-- Interpolación de datos faltantes
SELECT time_bucket_gapfill('1 hour', tiempo),
       locf(avg(temperatura)) -- Last observation carried forward
FROM sensores
GROUP BY 1;
```

---

## Casos reales documentados

| Empresa | Uso |
|---|---|
| **Ingestor (Grafana Labs)** | Backend de métricas |
| **Omni Analytics** | Analytics de producto |
| **Billions of rows** de IoT companies | Telemetría industrial |
| **Financial services** | Datos de mercado históricos |

---

## Cuándo usarlo

- Ya usas PostgreSQL y quieres agregar capacidades de time series sin migrar nada
- Necesitas JOINs entre datos temporales y datos relacionales
- Tienes datos de sensores, métricas, o cualquier dato con timestamp continuo
- Quieres ACID completo en tus series temporales (InfluxDB no lo tiene completo)
- Stack de monitoreo con Grafana, no quieres aprender InfluxQL/Flux

---

## Cuándo NO usarlo

- Volúmenes de escritura extremos (millones de inserts/seg distribuidos) — para eso Cassandra o InfluxDB clúster son mejores opciones.
- Solo necesitas caché con expiración — Redis tiene TTL nativo, esto es overkill.
- Ya tienes InfluxDB en producción y funcionando bien — no justifica migración.

---

## Free tier managed

```
Timescale Cloud:
  - 30 días gratis sin tarjeta de crédito
  - 10 GB storage incluidos en el trial
  - Después: desde $26/mes (0.5 CPU, 2 GB RAM, 10 GB)
```

---

## InfluxDB vs TimescaleDB

| | InfluxDB | TimescaleDB |
|---|---|---|
| **Lenguaje** | InfluxQL / Flux | SQL estándar |
| **JOINs** | No | Sí (PostgreSQL completo) |
| **ACID** | Parcial | Completo |
| **Curva de aprendizaje** | Nueva sintaxis | SQL que ya sabes |
| **Velocidad pura TSDB** | Ligeramente mejor | Muy buena |
| **Licencia** | MIT (v1.x) / Propietario (v2.x+) | Apache 2.0 / TSL |
| **Mejor para** | TSDB puro, ecosistema TICK | TSDB + relacional en uno |

---

> [← Volver al README](../README.md)
