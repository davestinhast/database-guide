<div align="center">
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/dynamodb/dynamodb-original.svg" width="120"/>

# Amazon DynamoDB

![Rating](https://img.shields.io/badge/rating-★★★★-blue?style=flat-square)
![License](https://img.shields.io/badge/license-Propietario_(AWS)-red?style=flat-square)
![Type](https://img.shields.io/badge/type-Key--Value_%2F_Documento_Managed-orange?style=flat-square)
![Language](https://img.shields.io/badge/escrito_en-Java%2FC%2B%2B-lightgrey?style=flat-square)

**La base de datos serverless más usada de AWS. Latencia de un dígito de milisegundo a cualquier escala. Sin clúster que manejar, sin nodos, sin configuración. Amazon la usa internamente para Alexa, Prime Video, y el carrito de compras de amazon.com.**

</div>

---

## Quick stats

| Atributo | Valor |
|---|---|
| Tipo | Key-Value + Documento (NoSQL) |
| ACID | Sí — transacciones multi-ítem desde 2018 |
| Licencia | Propietario (AWS) |
| Lanzamiento | 2012 (servicio AWS) |
| DB-Engines rank | #18 |
| Free tier permanente | 25 GB + 25 WCU + 25 RCU (nunca expira) |
| Latencia garantizada | Single-digit millisecond (p99) |
| Sin servidor | Completamente managed, cero operaciones |

---

## Para qué sirve

DynamoDB resuelve pe un problema específico: necesitas una base de datos que escale automáticamente de cero a millones de requests por segundo sin que tengas que pensar en clústeres, réplicas, o configuración. Es la definición de serverless para bases de datos.

Sirve para:

- **Perfiles de usuario** — guardar y recuperar perfil por user_id en milisegundos. El acceso por clave primaria es instantáneo sin importar cuántos usuarios tengas.
- **Carritos de compra e-commerce** — Amazon usa DynamoDB para su propio carrito. El modelo de datos de sesión encaja perfecto.
- **Datos de sesión y tokens** — TTL nativo elimina sesiones expiradas automáticamente, pe, sin cron jobs.
- **Leaderboards y ranking** — con el tipo de dato SortedSet y los Global Secondary Indexes puedes hacer rankings eficientes.
- **Configuraciones por usuario** — preferencias, settings, flags de features por usuario.
- **Gaming** — estado de juego, inventarios, progreso del jugador. King (Candy Crush) lo usa.
- **Notificaciones y mensajería** — DynamoDB Streams actúa como un event bus, cada cambio genera un evento.
- **Catálogos de productos** — atributos variables por tipo de producto (electrónica tiene voltaje, ropa tiene talla) encajan bien en el modelo flexible.

---

## Casos reales documentados

| Empresa | Uso | Escala |
|---|---|---|
| **Amazon** | Carrito de compras, recomendaciones | Millones de requests/seg durante Prime Day |
| **Netflix** | Metadatos de contenido, preferencias | Petabytes |
| **Lyft** | Datos de viajes en tiempo real | Alto throughput |
| **Airbnb** | Inventario de listados | Millones de propiedades |
| **Samsung** | IoT, datos de dispositivos | Miles de millones de registros |
| **Capital One** | Datos bancarios, transacciones | Regulado, alta disponibilidad |
| **Twitch** | Chat, métricas de streams | Millones de usuarios concurrentes |

---

## El modelo de datos — la parte difícil

Causa, DynamoDB tiene una curva de aprendizaje particular. No funciona como una base de datos relacional y si intentas usarla como una, te vas a frustrar pe.

El concepto clave es **single-table design**: en lugar de muchas tablas con JOINs, guardas diferentes tipos de entidades en la misma tabla usando prefijos en las claves.

```
Tabla: MiApp
PK (Partition Key)     | SK (Sort Key)         | Datos
-----------------------|-----------------------|-------------------
USER#123               | PROFILE               | {nombre, email, ...}
USER#123               | ORDER#2025-001        | {productos, total}
USER#123               | ORDER#2025-002        | {productos, total}
PRODUCT#ABC            | METADATA              | {nombre, precio}
PRODUCT#ABC            | REVIEW#user123        | {estrella, texto}
```

Una sola tabla, múltiples tipos de entidad. Esto maximiza la eficiencia pero requiere diseñar el modelo de acceso antes de diseñar los datos. Es el opuesto de cómo piensas en SQL.

---

## Precios — cuándo se pone caro

DynamoDB tiene dos modos de pricing:

**On-demand** (recomendado para tráfico variable):
- Escritura: $1.25 por millón de WCU
- Lectura: $0.25 por millón de RCU
- Storage: $0.25 por GB/mes

**Provisioned capacity** (para tráfico predecible, más barato):
- Escritura: $0.00065 por WCU/hora
- Lectura: $0.00013 por RCU/hora

Pe, el free tier es generoso para proyectos chicos: 25 GB storage + 25 WCU + 25 RCU por siempre. Pero a escala de millones de requests diarios, los costos suben bastante. Muchas startups han tenido sorpresas con la factura de DynamoDB.

---

## Cuándo usarlo

- Ya estás en AWS y quieres cero operaciones de DB
- El patrón de acceso es principalmente por clave primaria (get por ID)
- Necesitas escala automática sin configurar nada
- TTL nativo para datos que expiran (sesiones, tokens, caché)
- DynamoDB Streams para trigger de Lambda en cada cambio
- Workloads variables: muy bajo en la noche, pico en el día

---

## Cuándo NO usarlo

- Necesitas queries ad-hoc complejas — DynamoDB no tiene JOINs ni filtros arbitrarios eficientes pe.
- Tu equipo viene de SQL y no tiene tiempo para aprender single-table design.
- El proyecto está en GCP o Azure — hay mejores opciones nativas ahí.
- Budget limitado con alto volumen de escrituras — puede salir caro comparado con PostgreSQL self-hosted.
- Necesitas analytics — DynamoDB no es para GROUP BY ni aggregations pesadas.

---

## Alternativa open-source: ScyllaDB Alternator

ScyllaDB tiene un modo compatible con la API de DynamoDB llamado Alternator. Si quieres el modelo de datos de DynamoDB sin el lock-in de AWS, es una opción. Aunque ten en cuenta el cambio de licencia de ScyllaDB en 2024.

---

> [← Volver al README](../README.md)
