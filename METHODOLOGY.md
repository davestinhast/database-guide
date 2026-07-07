# Metodología editorial

Esta guía combina datos verificables con recomendaciones editoriales. Para que
el lector pueda distinguirlos, toda contribución debe seguir estas reglas.

## Jerarquía de fuentes

1. Documentación, precios, notas de versión y repositorios oficiales.
2. Estándares o benchmarks reproducibles con configuración publicada.
3. Estudios independientes que expliquen hardware, dataset y metodología.
4. Publicaciones de proveedores, identificadas explícitamente como tales.

Una cifra sin enlace y sin contexto no se considera verificada. Los agregadores,
blogs y videos pueden aportar contexto, pero no deben ser la única fuente de una
afirmación sobre licencias, precios, límites o rendimiento.

## Datos que envejecen

Precios, free tiers, versiones, licencias y límites deben incluir una fecha de
verificación en formato `AAAA-MM-DD`. Una fecha en el título, como “2025/2026”,
no reemplaza la fecha del dato.

Cuando un proveedor cambie una condición:

- se conserva el contexto histórico si ayuda a entender la decisión;
- se describe primero el estado vigente;
- se enlaza el anuncio o la documentación oficial;
- se evita presentar una predicción como un hecho.

## Benchmarks

Los resultados solo son comparables cuando comparten, como mínimo:

- versión del producto;
- hardware y topología;
- dataset y tamaño de datos;
- configuración y durabilidad;
- concurrencia, duración y herramienta de carga;
- métrica y percentil reportado.

No se construyen rankings mezclando resultados de equipos, clusters o workloads
distintos. Un benchmark del proveedor se etiqueta como `vendor benchmark`; sirve
como referencia, no como comparación independiente.

## Opinión editorial

Las recomendaciones deben declarar el caso de uso y sus tradeoffs. Se permiten
opiniones firmes y lenguaje informal, pero no insultos, garantías absolutas ni
afirmaciones como “gana en todo”. En particular:

- “mejor” exige criterios visibles;
- “más rápido” exige un benchmark comparable;
- “muerto” se reserva para productos retirados oficialmente;
- una licencia copyleft no se describe como propietaria.

## Correcciones

Una corrección factual debe explicar qué cambió, aportar la fuente y actualizar
las páginas duplicadas. Si hay duda, abre un issue con la etiqueta
`fact-check` antes de modificar un ranking.
