<div align="center">
<img src="https://avatars.githubusercontent.com/u/43250847?s=120" width="120"/>

# Meilisearch

![Rating](https://img.shields.io/badge/rating-★★★★★-blue?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-brightgreen?style=flat-square)
![Type](https://img.shields.io/badge/type-Search_Engine-yellow?style=flat-square)
![Language](https://img.shields.io/badge/escrito_en-Rust-lightgrey?style=flat-square)

**Búsqueda full-text instantánea con tolerancia a errores tipográficos. Escrito en Rust, resultados en menos de 50ms, configuración en minutos. La alternativa seria a Elasticsearch cuando no necesitas la complejidad del ELK stack.**

</div>

---

## Quick stats

| Atributo | Valor |
|---|---|
| Tipo | Motor de búsqueda (Search Engine) |
| ACID | No aplica (search engine, no base de datos transaccional) |
| Licencia | MIT (OSS real) |
| Lanzamiento | 2018 |
| Escrito en | Rust |
| Latencia p50 | <50ms en datasets de millones de documentos |
| Managed | Meilisearch Cloud |
| Creador | Meilisearch SAS (Francia) |

---

## Para qué sirve

Meilisearch pe es un motor de búsqueda, no una base de datos de propósito general. Lo instalas al lado de tu base de datos principal y le envías los documentos que quieres que sean buscables. Cuando el usuario escribe en la barra de búsqueda de tu app, consultas Meilisearch en lugar de hacer un `LIKE '%query%'` en PostgreSQL que es lentísimo.

Sirve para:

- **Barra de búsqueda de productos** — e-commerce, marketplace. El usuario escribe "lapiz azul" y Meilisearch encuentra "lápiz azul" (tolera el error de tilde), "bolígrafo azul", etc. ordenados por relevancia.
- **Búsqueda de contenido** — blogs, documentación, wikis internas. Indexas todos los artículos y el usuario encuentra lo que busca en tiempo real.
- **Autocompletado (search-as-you-type)** — respuestas en <50ms por cada tecla que presiona el usuario.
- **Búsqueda de usuarios/contactos** — en apps SaaS, directorio de empleados, contactos de messaging.
- **Catálogos** — listados de propiedades, empleos, autos. Con faceting puedes filtrar por categoría al mismo tiempo que buscas texto.
- **Búsqueda con filtros** — "encuentra laptops bajo $1000 de la marca Dell" combina full-text con filtros estructurados.
- **Aplicaciones multilenguaje** — Meilisearch soporta CJK (chino, japonés, coreano), árabe, y más out of the box.

---

## Tolerancia a typos — la diferencia que importa

Causa, el feature diferenciador de Meilisearch es la tolerancia a errores. Un `LIKE` en SQL es exacto, no perdona nada. Elasticsearch es bueno pero la configuración es compleja. Meilisearch lo hace bien desde el primer día.

```
Query: "procersador"    → encuentra "procesador" ✓
Query: "javascrpt"      → encuentra "javascript" ✓
Query: "poscgresql"     → encuentra "postgresql" ✓
Query: "bazed datos"    → encuentra "bases de datos" ✓
```

El algoritmo de tolerancia usa distancia de Levenshtein configurable: para palabras de 1-4 caracteres, 0 errores; de 5-8, 1 error; de 9+, 2 errores. Todo configurable.

---

## Meilisearch vs Elasticsearch

| | Meilisearch | Elasticsearch |
|---|---|---|
| **Setup** | Binario único, 30 segundos | Clúster Java, memoria, config |
| **Curva de aprendizaje** | Baja | Alta |
| **Latencia** | <50ms | 50-200ms (configurable) |
| **Escalabilidad** | Media (millones de docs) | Alta (billones de docs, clústeres) |
| **Licencia** | MIT | AGPL v3 |
| **Uso de memoria** | Moderado | Alto (JVM) |
| **Ideal para** | Apps medianas, startups | Logs, analytics, escala enterprise |
| **Typo tolerance** | Excelente out-of-the-box | Requiere config |

---

## Indexado en 5 minutos

```bash
# Levantar con Docker
docker run -p 7700:7700 getmeili/meilisearch

# Agregar documentos (HTTP o SDK)
curl -X POST 'http://localhost:7700/indexes/productos/documents' \
  -H 'Content-Type: application/json' \
  --data '[
    {"id": 1, "nombre": "Laptop ASUS ROG", "precio": 1200, "categoria": "electrónica"},
    {"id": 2, "nombre": "Teclado mecánico", "precio": 85, "categoria": "periféricos"}
  ]'

# Buscar
curl 'http://localhost:7700/indexes/productos/search?q=lapto+mecanico'
```

Pe, eso es todo el setup básico. Los documentos quedan indexados y buscables en segundos.

---

## SDKs disponibles

JavaScript, Python, PHP, Ruby, Go, Rust, Swift, Java, .NET — hay cliente oficial para casi todo.

---

## Cuándo usarlo

- Necesitas búsqueda en tu app y `LIKE '%query%'` ya no alcanza
- Quieres Elasticsearch pero sin la complejidad operacional
- Autocompletado instantáneo en la UI
- Dataset de hasta decenas de millones de documentos
- Multilenguaje con caracteres no latinos

---

## Cuándo NO usarlo

- Logs a escala de petabytes — Elasticsearch con ELK stack está diseñado para eso.
- Analytics pesadas sobre los datos — Meilisearch no reemplaza una base de datos analítica.
- Necesitas actualizar documentos parcialmente con alta frecuencia — el re-indexado tiene costo.
- Buscas una base de datos principal — Meilisearch es complementario, no reemplaza tu DB.

---

## Free tier managed

```
Meilisearch Cloud:
  - Gratis: 100,000 documentos, 10,000 searches/mes
  - Build: $30/mes — 1M documentos, 100K searches/mes
  - Pro:   $300/mes — 10M documentos, 1M searches/mes
```

Para proyectos propios self-hosted: gratis, MIT, sin límites.

---

> [← Volver al README](../README.md)
