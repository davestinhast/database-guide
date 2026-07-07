# Guía de bases de datos

Este repositorio reúne comparativas y notas prácticas sobre bases de datos. No
pretende encontrar una ganadora universal. La elección depende del tipo de
datos, las consultas, el volumen, las garantías de consistencia y la capacidad
del equipo para operar el sistema.

La información que cambia con frecuencia, como precios, licencias y versiones,
debe incluir una fuente y una fecha de revisión. Los criterios están explicados
en la [metodología editorial](./METHODOLOGY.md).

## Contenido

| Documento | Descripción |
|---|---|
| [Benchmarks](./BENCHMARKS.md) | Cómo diseñar y leer pruebas comparables |
| [Precios](./PRICING.md) | Planes gratuitos y costes de servicios administrados |
| [Recursos](./RESOURCES.md) | Documentación y material de aprendizaje |
| [Tier list](./TIERLIST.md) | Clasificación editorial con criterios explícitos |
| [Productos retirados y cambios de licencia](./WORST.md) | Riesgos históricos y comerciales |
| [Metodología](./METHODOLOGY.md) | Reglas sobre fuentes, vigencia y opinión |

## Por dónde empezar

Para una aplicación transaccional convencional, PostgreSQL suele ser un punto
de partida sensato. Tiene buenas garantías de consistencia, un ecosistema amplio
y extensiones para documentos JSON, datos geográficos, series temporales y
búsqueda vectorial.

Eso no lo convierte en la respuesta para todo. SQLite encaja mejor en programas
locales y aplicaciones móviles. ClickHouse y DuckDB están diseñados para
análisis. Valkey y Redis resuelven caché y estructuras en memoria. Cassandra y
ScyllaDB abordan cargas distribuidas que exigen muchas escrituras. Elegir uno de
estos sistemas sin necesitar sus ventajas suele añadir coste operativo.

Antes de decidir, conviene responder cinco preguntas:

1. ¿Qué operaciones hará la aplicación con mayor frecuencia?
2. ¿Qué datos no se pueden perder o duplicar?
3. ¿Cuántas escrituras y lecturas debe soportar el sistema hoy?
4. ¿Se necesita operar en varias regiones?
5. ¿Quién mantendrá copias de seguridad, actualizaciones y observabilidad?

## Elección por tipo de carga

| Necesidad | Opciones que conviene evaluar | Observación |
|---|---|---|
| Aplicación web transaccional | PostgreSQL, MySQL, MariaDB | Prioriza integridad, índices y facilidad de operación |
| Datos locales o integrados en una aplicación | SQLite | No requiere un servidor separado |
| Documentos con estructura variable | MongoDB, Firestore | Diseña las consultas antes de elegir el modelo |
| Caché, sesiones y contadores | Valkey, Redis | No sustituyen automáticamente a la base principal |
| Escrituras distribuidas a gran escala | Cassandra, ScyllaDB | El modelo se diseña alrededor de las consultas |
| Análisis sobre grandes volúmenes | ClickHouse | Adecuado para agregaciones, no para OLTP convencional |
| Análisis local de archivos | DuckDB | Consulta Parquet, CSV y otros formatos desde el proceso |
| Series temporales | TimescaleDB, InfluxDB | La elección depende de si se necesita SQL y datos relacionales |
| Búsqueda de texto | Meilisearch, Elasticsearch | Meilisearch simplifica casos pequeños; Elasticsearch ofrece mayor alcance operativo |
| Relaciones y recorridos complejos | Neo4j | Útil cuando el grafo es parte central del problema |
| SQL distribuido entre regiones | CockroachDB | Aporta consistencia fuerte con mayor complejidad y latencia |
| Servicios administrados en AWS | DynamoDB | Funciona bien cuando las claves de acceso se conocen de antemano |
| Búsqueda por similitud | pgvector, Qdrant, Weaviate, Pinecone | Empieza con pgvector si los datos ya viven en PostgreSQL |

## Relacional o no relacional

Un sistema relacional es apropiado cuando existen relaciones claras entre los
datos, se necesitan transacciones o las consultas pueden cambiar con el tiempo.
Las restricciones y claves foráneas evitan estados inválidos antes de que lleguen
a la aplicación.

Un sistema no relacional puede ser mejor cuando el patrón de acceso está bien
definido y el modelo especializado aporta una ventaja concreta. Esa ventaja
puede ser distribución, sincronización en tiempo real, búsqueda, almacenamiento
en memoria o flexibilidad documental. Elegir NoSQL solo para evitar diseñar un
esquema suele trasladar el problema al código.

| Situación | Orientación inicial |
|---|---|
| Pedidos, pagos, inventario y relaciones entre entidades | Relacional |
| Consultas variadas y reportes no previstos | Relacional |
| Catálogos con atributos muy distintos por documento | Documental |
| Acceso casi exclusivo mediante una clave conocida | Clave valor o wide column |
| Sincronización directa con clientes móviles | Firestore u otro servicio en tiempo real |
| Recorridos de varios niveles entre entidades | Grafo |

## Familias principales

### OLTP

Los sistemas de procesamiento transaccional atienden muchas operaciones cortas:
crear un pedido, actualizar un saldo o consultar un usuario. PostgreSQL, MySQL,
MariaDB y SQL Server pertenecen a este grupo. MongoDB también puede cubrir
ciertas cargas transaccionales, aunque usa un modelo documental.

### OLAP

Los sistemas analíticos recorren muchas filas para calcular agregaciones. Suelen
usar almacenamiento por columnas y aceptar que una consulta tarde segundos en
lugar de milisegundos. ClickHouse trabaja como servidor analítico; DuckDB lleva
ese enfoque a un proceso local.

### Datos distribuidos

Cassandra y ScyllaDB distribuyen datos entre nodos y favorecen la disponibilidad
y el volumen sostenido de escrituras. CockroachDB conserva SQL y transacciones
fuertes en una arquitectura distribuida. Son soluciones distintas y ninguna
debería adoptarse únicamente por una expectativa vaga de crecimiento.

### Sistemas especializados

TimescaleDB e InfluxDB se centran en series temporales. Neo4j modela grafos.
Elasticsearch y Meilisearch crean índices de búsqueda. Valkey y Redis mantienen
estructuras en memoria. Estas herramientas suelen complementar a una base de
datos principal en lugar de reemplazarla.

## Búsqueda vectorial

Una búsqueda vectorial compara representaciones numéricas de texto, imágenes u
otros datos. Se utiliza en recuperación semántica y en sistemas RAG.

Si la aplicación ya usa PostgreSQL, pgvector evita incorporar otro servicio y
suele ser suficiente para comenzar. Qdrant y Weaviate ofrecen motores dedicados
con filtros y funciones especializadas. Pinecone proporciona una opción
administrada. Chroma resulta cómoda para prototipos locales. La decisión debe
considerar el tamaño del índice, la frecuencia de actualización, los filtros y
la latencia requerida.

Ejemplo mínimo con pgvector:

```sql
CREATE EXTENSION vector;

CREATE TABLE documentos (
  id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  contenido text NOT NULL,
  embedding vector(1536)
);

SELECT contenido
FROM documentos
ORDER BY embedding <=> $1
LIMIT 5;
```

## Fichas disponibles

| Categoría | Bases de datos |
|---|---|
| Relacionales | [PostgreSQL](./databases/postgresql.md), [MySQL](./databases/mysql.md), [MariaDB](./databases/mariadb.md), [SQLite](./databases/sqlite.md), [SQL Server](./databases/sqlserver.md) |
| Documentales | [MongoDB](./databases/mongodb.md), [Firestore](./databases/firestore.md) |
| Clave valor | [Redis](./databases/redis.md), [Valkey](./databases/valkey.md), [DynamoDB](./databases/dynamodb.md) |
| Wide column | [Cassandra](./databases/cassandra.md), [ScyllaDB](./databases/scylladb.md) |
| SQL distribuido | [CockroachDB](./databases/cockroachdb.md) |
| Grafos | [Neo4j](./databases/neo4j.md) |
| Búsqueda | [Elasticsearch](./databases/elasticsearch.md), [Meilisearch](./databases/meilisearch.md) |
| Series temporales | [InfluxDB](./databases/influxdb.md), [TimescaleDB](./databases/timescaledb.md) |
| Analíticas | [ClickHouse](./databases/clickhouse.md), [DuckDB](./databases/duckdb.md) |

## Sobre benchmarks y precios

Un resultado de rendimiento solo es útil si especifica versión, hardware,
dataset, configuración, concurrencia y garantías de durabilidad. La página de
[benchmarks](./BENCHMARKS.md) explica cómo comparar productos sin mezclar pruebas
incompatibles.

Los precios y planes gratuitos cambian con frecuencia. La tabla de
[precios](./PRICING.md) sirve como referencia fechada, no como cotización. Antes
de contratar un servicio, confirma las condiciones en la documentación del
proveedor.

## Contribuciones

Las correcciones y nuevas fichas son bienvenidas. Lee la
[guía de contribución](./CONTRIBUTING.md) y adjunta fuentes primarias cuando el
cambio afecte versiones, licencias, límites o precios.

El contenido se publica bajo [CC BY 4.0](./LICENSE). Los nombres, logotipos y
marcas pertenecen a sus respectivos propietarios.
