<div align="center">
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/neo4j/neo4j-original.svg" width="120"/>

# Neo4j

![Rating](https://img.shields.io/badge/rating-⭐⭐⭐⭐-blue?style=flat-square)
![License](https://img.shields.io/badge/license-GPL_v3_%2F_Commercial-green?style=flat-square)
![Type](https://img.shields.io/badge/type-Grafos_ACID-purple?style=flat-square)
![Language](https://img.shields.io/badge/escrito_en-Java-lightgrey?style=flat-square)

**La base de datos de grafos más popular del mundo. Relaciones como ciudadanos de primera clase. Cypher como lenguaje nativo. Nada mejor para redes complejas.**

</div>

---

## ⚡ Quick stats

| Atributo | Valor |
|---|---|
| Tipo | Grafos (Property Graph) |
| ACID | ✅ Completo |
| Licencia | GPL v3 (Community) / Comercial (Enterprise) |
| Lanzamiento | 2007 |
| DB-Engines rank | #23 (líder absoluto en grafos) |
| Lenguaje query | Cypher (declarativo, intuitivo) |
| Casos de uso | LinkedIn, eBay, NASA, UBS |
| Managed | Neo4j AuraDB (free tier) |

---

## ✅ Cuándo usarlo

- Redes sociales (amigos-de-amigos, recomendaciones)
- Detección de fraude (patrones en transacciones)
- Knowledge graphs y ontologías
- Sistemas de recomendación (e-commerce, content)
- Análisis de dependencias (microservicios, supply chain)
- Grafos de acceso / permisos / roles
- Rutas y navegación (pathfinding)
- Compliance y trazabilidad regulatoria

## ❌ Cuándo NO usarlo

- Datos principalmente tabulares con pocas relaciones → SQL
- Alta carga de escrituras simples → Cassandra/ScyllaDB
- Full-text search → Elasticsearch
- Cache → Redis
- Datos de series temporales → InfluxDB
- Cuando el grafo es simple y un JOIN SQL lo resuelve

---

## 📊 Performance

```
Traversal profundo (6+ hops):    Seconds (vs minutos en SQL)
Pattern matching:                Nativo y eficiente con índices
Latencia queries simples:        <5ms
Límite nodos (Community):        Sin límite técnico
Escalabilidad:                   Vertical (Community) / Clustering (Enterprise)
```

> La ventaja de Neo4j no es throughput bruto — es la capacidad de traversar grafos complejos en tiempo real donde SQL requeriría JOINs exponenciales.

---

## 🗺️ Cypher — el lenguaje

```cypher
-- Encontrar amigos de amigos que comparten intereses
MATCH (me:User {name: "Alice"})-[:FRIENDS_WITH*2]->(fof:User)
WHERE NOT (me)-[:FRIENDS_WITH]->(fof)
  AND (fof)-[:INTERESTED_IN]->(:Topic {name: "GraphDB"})
RETURN fof.name, count(*) AS commonFriends
ORDER BY commonFriends DESC
LIMIT 10

-- Detección de fraude — ciclos sospechosos
MATCH path = (a:Account)-[:TRANSFER*3..6]->(a)
WHERE all(r IN relationships(path) WHERE r.amount > 10000)
RETURN path LIMIT 25
```

---

## 💰 Precios

| Servicio | Free | Paid desde |
|---|---|---|
| **Neo4j AuraDB Free** | 200K nodos / 400K relaciones | Gratis, nunca expira |
| **AuraDB Professional** | — | $65/mes |
| **AuraDB Enterprise** | — | Custom |
| **Self-hosted Community** | ✅ Gratis (GPL v3) | — |
| **Self-hosted Enterprise** | — | Custom (licencia) |

---

## 🎥 Tutoriales

### 🇺🇸 English
[![Neo4j 100s](https://img.youtube.com/vi/T6L9EoBy8Zk/mqdefault.jpg)](https://www.youtube.com/watch?v=T6L9EoBy8Zk)
[![Neo4j Full](https://img.youtube.com/vi/8jNPelugC2s/mqdefault.jpg)](https://www.youtube.com/watch?v=8jNPelugC2s)

### 🇪🇸 Español
🔗 [Canal Neo4j en Español](https://www.youtube.com/@neo4j/search?query=español)

### 🇨🇳 中文
🔗 [Neo4j 中文社区](https://neo4j.com.cn/)

---

## 🔗 Links

- 📖 [Documentación oficial](https://neo4j.com/docs/)
- 🎮 [Neo4j Sandbox — prueba gratis online](https://sandbox.neo4j.com/)
- 🚀 [AuraDB — managed free tier](https://neo4j.com/cloud/platform/aura-graph-database/)
- 📚 [GraphAcademy — cursos gratis](https://graphacademy.neo4j.com/)

---

> [← README](../README.md)
