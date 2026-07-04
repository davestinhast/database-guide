<div align="center">
<img src="https://avatars.githubusercontent.com/u/54801242?s=120" width="120"/>

# ClickHouse

![Rating](https://img.shields.io/badge/rating-★★★★★-blue?style=flat-square)
![License](https://img.shields.io/badge/license-Apache_2.0-brightgreen?style=flat-square)
![Type](https://img.shields.io/badge/type-OLAP_Columnar-orange?style=flat-square)
![Language](https://img.shields.io/badge/escrito_en-C%2B%2B-lightgrey?style=flat-square)

**La base de datos columnar open-source más rápida del mundo para analytics. Cloudflare procesa seis millones de eventos por segundo con esto. No es para OLTP, es para analizar millones de filas en milisegundos.**

</div>

---

## Quick stats

| Atributo | Valor |
|---|---|
| Tipo | OLAP, Columnar |
| ACID | Parcial (por partición, no transacciones multi-fila) |
| Licencia | Apache 2.0 (OSS real) |
| Lanzamiento | 2016 (open-source por Yandex) |
| DB-Engines rank | #25 (subiendo rápido) |
| Escrito en | C++ |
| Managed | ClickHouse Cloud, Altinity Cloud |
| Creador | Yandex → ClickHouse Inc. (2021) |

---

## Para qué sirve

Causa, ClickHouse está diseñado para un tipo muy específico de trabajo: analizar cantidades enormes de datos históricos rápidísimo. No es una base de datos para tu app web pe, es para el backend analítico que consume los datos de tu app web.

Sirve para:

- **Analytics de producto** — ¿cuántos usuarios hicieron clic en el botón azul entre el 3 y el 17 de marzo, divididos por país y dispositivo? ClickHouse responde eso en milisegundos sobre mil millones de filas.
- **Logs y eventos** — guardar y consultar logs de servidores, eventos de usuarios, telemetría. Cloudflare mete ahí seis millones de eventos por segundo.
- **Dashboards en tiempo real** — Grafana + ClickHouse es el combo estándar para dashboards de alto volumen.
- **Métricas de infraestructura** — CPU, RAM, latencias, errores, todo con timestamps y alta frecuencia.
- **Business intelligence** — reportes complejos con muchos GROUP BY, SUM, COUNT sobre tablas de cientos de millones de filas.
- **Datos de clickstream web** — cada visita de página, cada scroll, cada evento del usuario almacenado y analizable.
- **Análisis financiero** — backtesting, análisis de precios históricos, patrones en trades.

---

## Casos reales documentados

| Empresa | Uso | Escala |
|---|---|---|
| **Cloudflare** | Analítica de DNS, HTTP logs, DDoS | 6 millones eventos/seg |
| **ByteDance (TikTok)** | Analytics de contenido | Petabytes |
| **Uber** | Métricas de viajes, analytics | Cientos de millones de filas/día |
| **Yandex** | Yandex.Metrica (Google Analytics de Rusia) | 25 petabytes, 13 trillones de filas |
| **GitLab** | Product analytics, GitLab Insights | Producción |
| **Spotify** | Data pipelines internos | Petabytes |
| **eBay** | Search analytics | Miles de millones de filas |

---

## Por qué es tan rápido

**Almacenamiento columnar** es la clave pe. Las bases de datos relacionales normales guardan los datos fila por fila. ClickHouse los guarda columna por columna. Cuando haces `SELECT avg(precio) FROM ventas`, no necesita leer los nombres de productos, IDs de clientes, ni ningún otro campo, solo la columna `precio`. Menos I/O, mucho más rápido.

Además:

- Compresión agresiva por columna (LZ4 por defecto, ZSTD opcional). Una columna de enteros similares comprime 10x fácil.
- Ejecución vectorizada (SIMD), procesa múltiples valores en un solo ciclo de CPU.
- Paralelismo automático en todos los núcleos disponibles.
- MergeTree storage engine con particionado por fecha automático.

---

## Cuándo usarlo

- Tienes más de un millón de filas y necesitas analytics rápidas
- Los datos llegan en streams continuos (logs, eventos, métricas)
- Las queries son casi siempre SELECT con muchos filtros y agregaciones
- Necesitas dashboards en tiempo casi real sobre datos de producción
- Quieres reemplazar un data warehouse costoso (Snowflake, BigQuery) para casos de uso específicos

---

## Cuándo NO usarlo

- Tu app necesita UPDATE y DELETE frecuentes — ClickHouse los soporta pero son lentos, pe. No está diseñado para eso.
- Necesitas transacciones ACID multi-fila, para eso usa PostgreSQL.
- Consultas por clave primaria single-row (`SELECT * FROM users WHERE id = 123`), usa Redis o PostgreSQL.
- Tienes menos de un millón de filas, probablemente PostgreSQL alcanza y te evitas la complejidad.

---

## Quick stats de performance (documentados)

| Operación | Resultado | Hardware |
|---|---|---|
| Scan de 100M filas, suma simple | < 1 segundo | 8 vCPU / 32 GB |
| Ingesta | 1+ millón de filas/seg | por nodo |
| Compresión típica | 5x–10x | depende del dato |
| Query ad-hoc sobre 1 TB | segundos | cluster commodity |

Fuente: clickhouse.com/benchmark, Yandex whitepapers.

---

## Managed options

| Servicio | Free tier | Precio base |
|---|---|---|
| **ClickHouse Cloud** | $0 — 30 días trial con crédito | desde $150/mes aprox |
| **Altinity Cloud** | No | Enterprise |
| **Self-hosted** | Gratis (Apache 2.0) | Solo infra |

---

## Instalación mínima

```bash
# Docker (la forma más rápida pe)
docker run -d --name clickhouse-server \
  -p 8123:8123 -p 9000:9000 \
  clickhouse/clickhouse-server

# Insertar datos y hacer query
curl 'http://localhost:8123/' --data-binary \
  "CREATE TABLE eventos (ts DateTime, user_id UInt64, accion String) ENGINE = MergeTree() ORDER BY ts"
```

---

> [← Volver al README](../README.md)
