<div align="center">
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/firebase/firebase-plain.svg" width="120"/>

# Cloud Firestore

![Rating](https://img.shields.io/badge/rating-★★★★-blue?style=flat-square)
![License](https://img.shields.io/badge/license-Propietario_(Google)-red?style=flat-square)
![Type](https://img.shields.io/badge/type-Documento_NoSQL_Realtime-green?style=flat-square)
![Language](https://img.shields.io/badge/escrito_en-Java%2FC%2B%2B-lightgrey?style=flat-square)

**La base de datos de Firebase. Documentos JSON con sincronización en tiempo real al cliente, soporte offline, y SDK móvil de primera clase. El camino rápido para apps móviles y web que necesitan datos en vivo sin armar un backend.**

</div>

---

## Quick stats

| Atributo | Valor |
|---|---|
| Tipo | Documento NoSQL (BSON/JSON), Realtime |
| ACID | Sí — transacciones ACID desde 2019 |
| Licencia | Propietario (Google Cloud) |
| Lanzamiento | 2017 (reemplazó Firebase Realtime Database) |
| Free tier | 1 GB storage, 50K reads/día, 20K writes/día |
| Realtime sync | Sí — listeners en tiempo real al cliente |
| Offline support | Sí — cache local en el dispositivo |
| Creador | Google |

---

## Para qué sirve

Firestore pe es la opción cuando quieres que los datos de tu app se sincronicen en tiempo real a todos los clientes conectados sin armar tu propio WebSocket server ni nada de eso. El SDK de Firebase hace todo por debajo.

Sirve para:

- **Apps de chat y mensajería** — cada mensaje nuevo llega a todos los clientes en tiempo real sin polling. El listener de Firestore lo maneja automáticamente.
- **Apps colaborativas en tiempo real** — documentos que múltiples usuarios editan a la vez, pizarras colaborativas, tableros Kanban compartidos.
- **Apps móviles (iOS/Android)** — el SDK maneja cache offline, sincronización cuando vuelve la conexión, y conflictos automáticamente.
- **Juegos móviles** — estado de partida, leaderboards, inventario del jugador.
- **Apps de delivery y tracking** — actualización de posición del repartidor en tiempo real al cliente.
- **Notificaciones push con datos** — Firestore + Cloud Functions + FCM es el stack completo de Google para esto.
- **Prototipos rápidos** — sin backend propio, con auth incluida de Firebase Authentication, storage con Firebase Storage.

---

## La característica diferenciadora: listeners en tiempo real

```javascript
// En el cliente, escuchas cambios en tiempo real
import { onSnapshot, doc } from 'firebase/firestore';

const unsubscribe = onSnapshot(doc(db, "pedidos", pedidoId), (doc) => {
  // Esto se llama automáticamente cada vez que el documento cambia
  const data = doc.data();
  actualizarUI(data.estado, data.posicion);
});

// El usuario ve el estado del pedido actualizarse en vivo sin que 
// hagas un solo polling manual
```

Causa, esto que parece simple es bastante trabajo implementarlo tú solo. Firestore lo da listo pe.

---

## Modelo de datos: colecciones y documentos

```
/usuarios
  /user123
    nombre: "Carlos"
    email: "carlos@mail.com"
    /pedidos  (subcolección)
      /pedido-001
        producto: "Laptop"
        total: 1200
        estado: "enviado"
```

Los documentos son JSON sin schema fijo. Cada documento puede tener campos distintos. Las subcolecciones permiten organizar datos relacionados.

---

## Limitaciones que debes saber

Causa, Firestore tiene límites que no son obvios al principio:

- **1 escritura por documento por segundo** — si múltiples usuarios editan el mismo documento simultáneamente, hay contención. Para contadores de alta frecuencia usa Distributed Counters.
- **Queries limitadas** — no hay JOINs, no puedes filtrar por múltiples campos sin crear índices compuestos manualmente, no hay `OR` en queries.
- **Sin agregaciones nativas complejas** — no hay `SUM`, `AVG`, `GROUP BY` directo (existe Firestore Aggregation Queries pero es limitado).
- **Pricing puede sorprender** — el free tier de 50K reads/día suena bastante, pero en una app activa con listeners en tiempo real, cada cambio que llega al cliente cuenta como una lectura. Se gasta rápido.

---

## Cuándo usarlo

- App móvil que necesita sync en tiempo real y soporte offline
- Prototipo rápido sin backend propio
- Ya usas Firebase Authentication y Firebase Storage
- Necesitas que los cambios lleguen al cliente instantáneamente
- Equipo pequeño sin DevOps, quieren cero operaciones

---

## Cuándo NO usarlo

- Necesitas queries complejas tipo SQL con JOINs y filtros múltiples
- Tienes contadores de alta frecuencia (likes, views) — el límite de 1 escritura/seg por documento duele pe.
- Budget tight con alto volumen — los costos escalan más rápido que MongoDB Atlas o PostgreSQL.
- Datos que requieren análisis complejos — para BigQuery es mucho mejor.
- No quieres vendor lock-in con Google — migrar desde Firestore es tedioso.

---

## Firestore vs Firebase Realtime Database

Firestore es el reemplazo moderno de Firebase Realtime Database pe. Son productos distintos:

| | Firestore | Realtime Database |
|---|---|---|
| **Modelo** | Colecciones y documentos | JSON árbol único |
| **Queries** | Más poderosas | Muy limitadas |
| **Escalabilidad** | Multi-región | Single región |
| **Pricing** | Por operación | Por GB transferido |
| **Recomendado** | Sí, para nuevos proyectos | No, está en mantenimiento |

---

## Free tier detallado

```
Spark Plan (gratis, siempre):
  - 1 GB de storage
  - 50,000 lecturas por día
  - 20,000 escrituras por día
  - 20,000 deletes por día
  - 10 GB de egress por mes

Blaze Plan (pay-as-you-go):
  - Lectura: $0.06 por 100,000 docs
  - Escritura: $0.18 por 100,000 docs
  - Storage: $0.18 por GB/mes
```

---

> [← Volver al README](../README.md)
