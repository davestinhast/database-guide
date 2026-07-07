# Benchmarks — cómo comparar sin engañarse

> Última revisión metodológica: 2026-07-07. Los resultados de productos
> distintos no forman un ranking si no comparten hardware, dataset,
> configuración y workload.

## Resumen

No existe un número de “operaciones por segundo” que permita ordenar SQLite,
PostgreSQL, Redis, Cassandra y ClickHouse en una sola gráfica. Cada producto
resuelve cargas diferentes y los resultados publicados usan configuraciones
incompatibles.

Esta página conserva referencias útiles, pero separa tres preguntas:

1. ¿Qué producto encaja con el patrón de acceso?
2. ¿Qué configuración cumple la durabilidad y consistencia necesarias?
3. ¿Qué rendimiento obtiene esa configuración en un entorno comparable?

## Requisitos mínimos de un resultado

Antes de citar una cifra, documenta:

| Campo | Ejemplo |
|---|---|
| Producto y versión | PostgreSQL 18.1 |
| Hardware | 8 vCPU, 32 GiB RAM, NVMe |
| Topología | 1 nodo, misma zona |
| Dataset | 100 GiB, no cabe completamente en RAM |
| Durabilidad | `fsync=on`, réplica síncrona desactivada |
| Workload | 70% lectura, 30% escritura, valores de 1 KiB |
| Concurrencia | 64 clientes durante 20 minutos |
| Herramienta | `pgbench`, YCSB, `memtier_benchmark`, etc. |
| Métricas | throughput, p50, p95, p99 y errores |
| Fuente | script, configuración y resultado bruto |

Sin estos datos, el número es una anécdota y debe etiquetarse como tal.

## Qué herramienta usar

| Familia | Herramienta inicial | Qué evitar |
|---|---|---|
| PostgreSQL | `pgbench` | Comparar TPC-B-like con un GET por clave |
| MySQL/MariaDB | `sysbench` | Omitir motor, aislamiento o durabilidad |
| Redis/Valkey | `memtier_benchmark` | Mezclar pipelining y requests individuales |
| Cassandra/ScyllaDB | `cassandra-stress` o YCSB | Comparar clusters con distinto número de nodos |
| MongoDB | `mongoreplay` o YCSB | Ignorar índices y write concern |
| SQLite | benchmark dentro de la aplicación | Comparar acceso in-process con una DB por red |
| OLAP | TPC-H/TPC-DS adaptado | Mezclar tiempos de carga con tiempos de consulta |

## Referencias publicadas

Estas fuentes ayudan a diseñar pruebas; sus cifras no son directamente
comparables entre sí.

| Producto | Referencia | Clasificación | Limitación principal |
|---|---|---|---|
| Redis | [Benchmarks oficiales](https://redis.io/docs/latest/operate/oss_and_stack/management/optimization/benchmarks/) | Vendor | El pipelining cambia radicalmente el throughput |
| Valkey | [Herramienta de benchmarking](https://valkey.io/topics/benchmark/) | Proyecto | Debe ejecutarse con la misma versión y hardware del candidato |
| ScyllaDB | [Benchmarks publicados](https://www.scylladb.com/product/benchmarks/) | Vendor | Promocionales; revisar topología y configuración |
| CockroachDB | [TPC-C 20.2](https://www.cockroachlabs.com/blog/cockroachdb-performance-20-2/) | Vendor, histórico | No representa versiones ni hardware actuales |
| MongoDB | [Comparativa de Altoros](https://altoros.com/blog/benchmarking-mongodb-7-0/) | Tercero | Requiere revisar dataset y configuración completa |

## Redis frente a Valkey

Ambos comparten protocolo y gran parte de su historia, pero las versiones
actuales ya divergen. Para una comparación defendible:

1. usa la misma máquina y kernel;
2. fija afinidad de CPU y límites de memoria;
3. prueba sin persistencia, con RDB y con AOF por separado;
4. usa igual número de clientes, conexiones y pipeline;
5. repite GET, SET y la mezcla real de comandos;
6. reporta throughput junto con p50, p95 y p99;
7. publica configuración y resultados brutos.

Una prueba con Redis en un portátil y Valkey en AWS Graviton no demuestra una
ventaja del motor. Tampoco se puede extrapolar un resultado de SET a Streams,
Lua, Pub/Sub o módulos.

## Cassandra frente a ScyllaDB

La arquitectura C++/shard-per-core de ScyllaDB y la JVM de Cassandra producen
perfiles operativos distintos. Aun así, frases como “10x más rápido” solo tienen
sentido con igual factor de replicación, consistencia, compaction, dataset,
número de nodos y percentil de latencia.

Los benchmarks del proveedor deben marcarse como `vendor benchmark`. Para una
decisión real importa el costo total del cluster que mantiene el SLA, no el pico
de inserts de una configuración promocional.

## Plantilla de resultado reproducible

```text
Fecha:
Producto y versión:
Commit o imagen:
Hardware y sistema operativo:
Topología:
Dataset:
Configuración de durabilidad/consistencia:
Herramienta y comando:
Warm-up y duración:
Clientes y concurrencia:
Throughput:
Latencia p50/p95/p99:
Errores:
Enlace a datos brutos:
```

Consulta también la [metodología editorial](./METHODOLOGY.md).

---

> [← README](./README.md) · [Precios →](./PRICING.md)
