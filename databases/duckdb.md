<div align="center">
<img src="https://duckdb.org/images/logo-dl/DuckDB_Logo.png" width="120"/>

# DuckDB

![Rating](https://img.shields.io/badge/rating-★★★★★-blue?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-brightgreen?style=flat-square)
![Type](https://img.shields.io/badge/type-OLAP_Embebida-orange?style=flat-square)
![Language](https://img.shields.io/badge/escrito_en-C%2B%2B-lightgrey?style=flat-square)

**"El SQLite de analytics." Cero configuración, cero servidor, un import de Python. Consulta archivos Parquet, CSV y JSON directamente sin cargarlos. El arma estándar del data science moderno desde 2024.**

</div>

---

## Quick stats

| Atributo | Valor |
|---|---|
| Tipo | OLAP, Embebida (in-process) |
| ACID | Sí (transacciones completas en proceso único) |
| Licencia | MIT (OSS real, sin restricciones) |
| Lanzamiento | 2019 (CWI, Amsterdam) |
| DB-Engines rank | #37 (creció más rápido en 2024-2025) |
| Sin servidor | Cero — corre en proceso |
| Managed | MotherDuck |
| Creador | DuckDB Labs / CWI |

---

## Para qué sirve

Pe, DuckDB es básicamente SQLite pero pensado para analytics en lugar de transacciones. Mismo concepto: no hay servidor, no hay configuración, es una librería que corre en tu proceso. Pero donde SQLite optimiza para lecturas y escrituras de filas individuales (OLTP), DuckDB optimiza para escanear millones de filas y agregar (OLAP).

Sirve para:

- **Data science y notebooks** — en Jupyter o cualquier entorno Python, es el motor analítico más rápido que puedes usar sin levantar infraestructura.
- **Consultar archivos directamente** — DuckDB puede abrir un Parquet, un CSV, o un JSON directamente con SQL, sin importarlo primero. Eso pe es enorme para pipelines de datos.
- **ETL liviano** — transformar y limpiar datos sin necesidad de un Spark o un dbt con servidor propio.
- **Análisis local de datos grandes** — hasta decenas de GB en una laptop, DuckDB los maneja sin problema.
- **Reemplazar pandas** — para operaciones analíticas, DuckDB es significativamente más rápido que pandas sobre los mismos datos.
- **Scripts de análisis ad-hoc** — tienes un CSV de 10 millones de filas y quieres hacer queries, DuckDB en Python en dos líneas.
- **Prototipado de pipelines** — antes de montar ClickHouse o BigQuery, validas la lógica analítica con DuckDB.

---

## Cómo se usa en Python (realmente así de simple)

```python
import duckdb

# Consultar un Parquet directamente sin cargar en memoria
duckdb.sql("SELECT mes, SUM(ventas) FROM 'datos.parquet' GROUP BY mes").show()

# O un CSV remoto (sí, remoto)
duckdb.sql("SELECT * FROM 'https://ejemplo.com/data.csv' LIMIT 100").df()

# Base de datos persistente
con = duckdb.connect("mi_base.db")
con.sql("CREATE TABLE usuarios AS SELECT * FROM 'usuarios.csv'")
con.sql("SELECT pais, COUNT(*) FROM usuarios GROUP BY pais").show()
```

Pe, eso es todo. No hay servidor que levantar, no hay config, no hay driver externo.

---

## Casos reales documentados

| Empresa / Proyecto | Uso |
|---|---|
| **MotherDuck** | Managed DuckDB en la nube, startup especializada |
| **Observable** | Notebooks con DuckDB-WASM (corre en el browser) |
| **dbt Labs** | Integración nativa, DuckDB como backend local |
| **Hugging Face** | Análisis de datasets del hub |
| **Data engineering community** | Reemplazando pandas + Spark para ETL local |

---

## DuckDB-WASM: corre en el browser

Pe esto es bastante loco: DuckDB tiene una versión compilada a WebAssembly que corre directo en el browser. Puedes hacer analytics SQL en el cliente sin servidor. Observable Framework lo usa como motor de análisis en sus dashboards.

---

## Cuándo usarlo

- Análisis de datos en Python, R, o cualquier entorno local
- Necesitas consultar Parquet, CSV, JSON con SQL sin overhead
- Quieres velocidad de ClickHouse para consultas locales sin montar clúster
- ETL scripts que no justifican infraestructura distribuida
- Prototipado rápido antes de escalar a un data warehouse real
- Notebooks de ciencia de datos donde pandas se queda corto

---

## Cuándo NO usarlo

- Necesitas acceso concurrente desde múltiples procesos — DuckDB es para un proceso a la vez, pe.
- Tu app web necesita una base de datos compartida entre servidores — usa PostgreSQL.
- Los datos superan la RAM + disco disponibles de una sola máquina — ahí ya es territorio de Spark o ClickHouse clúster.
- Necesitas actualizaciones transaccionales frecuentes de muchas filas con concurrencia alta.

---

## DuckDB vs ClickHouse

| | DuckDB | ClickHouse |
|---|---|---|
| **Modo** | Embebido (in-process) | Servidor (cliente-servidor) |
| **Setup** | `pip install duckdb` | Docker o instalación manual |
| **Escala** | Una máquina, decenas de GB | Clústeres, petabytes |
| **Ideal para** | Análisis local, scripts, notebooks | Producción, alto volumen, equipos |
| **Licencia** | MIT | Apache 2.0 |
| **Costo** | Gratis | Gratis (self-hosted) |

---

## Managed — MotherDuck

MotherDuck es el servicio managed de DuckDB. Combina DuckDB local con un motor en la nube, así que puedes hacer queries que procesan datos locales y datos en la nube al mismo tiempo en una sola query SQL. El free tier incluye 10 GB de storage.

---

> [← Volver al README](../README.md)
