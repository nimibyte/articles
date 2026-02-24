<table>
  <tr>
    <td valign="middle"><img src="../../logo.png" alt="Nimibyte Academy" width="50" /></td>
    <td valign="middle"><h1>Mas Alla de Clean Architecture: un modelo pragmatico para escalar software real</h1></td>
  </tr>
</table>

Read in English: [`README.en.md`](./README.en.md)

## TL;DR

Si tu equipo necesita entregar rapido sin crear caos a largo plazo, este modelo te ayuda a tomar decisiones de arquitectura con impacto de cambio predecible.

Esta pensado para equipos que necesitan velocidad de entrega y mantenibilidad al mismo tiempo.

## Por que existe este modelo

Muchas conversaciones de arquitectura parten de un escenario ideal: alcance estable, tiempo de sobra y equipos hiper especializados. La mayoria de empresas no opera asi.

En la practica, casi siempre estamos en uno de estos contextos:

- Consultorias que entregan rapido con fechas muy exigentes.
- Startups que pivotan seguido y necesitan una arquitectura que absorba cambios.
- Productos maduros donde mantener y evolucionar pesa mas que reinventar.

En los tres casos, los problemas suelen repetirse:

- Muy simple: velocidad al inicio, caos despues.
- Muy rigido: pureza tecnica, baja velocidad de entrega.
- Muy complejo: onboarding lento y friccion constante.

Este modelo nace como punto medio: suficiente orden para escalar y suficiente simplicidad para adoptar.

## Para quien es este modelo

- Equipos que escalan de 3 a 30+ ingenieros.
- Productos con presion de releases semanales.
- Codebases donde onboarding y refactors empiezan a costar caro.

## Idea central

El modelo se apoya en tres reglas operativas:

- Contexto por Ruta: el path explica por que existe un archivo.
- Conciencia de Alcance: cada archivo tiene un impacto predecible.
- Escalabilidad Horizontal: crecer agregando piezas enfocadas, no inflando archivos nucleares.

Estas reglas reducen la fatiga de decisiones y hacen los cambios mas seguros.

## Tres capas logicas

![Modelo de arquitectura](./assets/graph.png)

Todo sistema orientado al negocio equilibra tres capas:

1. Capa de Negocio: reglas propias de la empresa y comportamiento del producto.
2. Capa de Implementacion: ejecucion ligada al stack (web, API, mobile).
3. Capa de Aplicacion: integraciones con bases de datos, cache, SDKs y terceros.

No se trata de dogma estricto. Se trata de mantener responsabilidades claras a medida que crece el codigo.

## Interfaces como contratos

Las interfaces marcan fronteras limpias entre capas:

- Interfaz de Producto: adapta salidas de negocio para APIs y clientes.
- Interfaz de Datos: traduce detalles de persistencia para la capa de negocio.
- Interfaz de UI: convierte informacion de dominio en modelos para vista.

En proyectos pequenos estas fronteras pueden ser livianas. En sistemas grandes, reforzarlas evita acoplamientos caros.

## Ejemplo practico de estructura (Next.js + DB + Redis)

Dentro de `/src`:

- `pages/`: rutas de implementacion con composicion controlada de negocio.
- `containers/`: comportamiento de UI, flujos de interaccion y wiring de casos de uso.
- `components/`: presentacion pura, reutilizable y sin logica de negocio.
- `providers/`: integraciones externas (SDKs, cache, APIs de terceros).
- `services/`: decisiones de negocio y orquestacion de dominio.
- `repositories/`: estrategias de lectura y escritura de datos.

Asi se separan responsabilidades del stack y del negocio sin perder velocidad.

## Matriz de adopcion

| Contexto | Prioridad | Como aplicar este modelo |
| --- | --- | --- |
| Consultoria | Velocidad con bajo retrabajo | Mantener convenciones de rutas estrictas e interfaces ligeras. |
| Startup | Pivotar rapido con deuda controlada | Empezar con limites minimos de capas y reforzar interfaces al estabilizar producto. |
| Producto maduro | Fiabilidad y mantenibilidad | Forzar contratos explicitos y ownership de alcance entre equipos. |

## Ejemplo de impacto de cambios

Solicitud: "Agregar alertas de vencimiento de trial en el dashboard de usuario".

Patron esperado de archivos:

- `services/subscription/...`: definir reglas de alerta.
- `repositories/subscription/...`: obtener datos de expiracion.
- `containers/dashboard/...`: decidir cuando y donde mostrar alertas.
- `components/alerts/...`: renderizar la UI de aviso.

Como el alcance de cada capa es explicito, puedes estimar efectos secundarios antes de codificar.

## Comparacion con enfoques comunes

| Enfoque | Velocidad inicial | Seguridad ante cambios | Carga cognitiva | Mejor escenario |
| --- | --- | --- | --- | --- |
| MVC / por capas | Alta | Media-Baja | Baja al inicio, mayor despues | Apps pequenas y proyectos cortos |
| Clean / Hexagonal | Media-Baja | Alta | Media-Alta | Sistemas con limites estrictos |
| Implementaciones cargadas de DDD | Media | Alta | Alta | Dominios complejos con equipos estables |
| Este modelo | Alta-Media | Alta-Media | Media | Equipos de producto que equilibran velocidad y escalabilidad |

## Cuando este modelo no es la mejor opcion

- Prototipos desechables sin horizonte de mantenimiento.
- Sistemas altamente regulados con requisitos formales muy estrictos.
- Equipos con arquitectura actual estable y metricas de entrega saludables.

## Conclusiones

Una buena arquitectura debe acelerar la entrega, no frenarla.

Este modelo apuesta por escalabilidad practica: rutas claras, alcance explicito y crecimiento modular. Permite iterar rapido sin esconder complejidad que luego bloquee la evolucion del producto.

## AI teaching pack (learn + apply + defend)

Usa estos prompts con cualquier asistente de IA para asimilar y exponer el modelo:

1. Explica este modelo a un perfil junior en 90 segundos usando una feature concreta.
2. Compara este modelo con Clean Architecture para una startup con pivots semanales.
3. Dado un bug en pricing de checkout, mapea archivos probables por capa y alcance de impacto.
4. Cuestiona este modelo: lista tres modos de fallo y como mitigarlos.
5. Simula una revision con CTO donde debo defender por que este modelo no es sobreingenieria.

## Rubrica rapida de evaluacion

Puntua cada respuesta de 0 a 5:

- Claridad: puede explicarlo de forma simple?
- Causalidad: explica por que importa cada regla?
- Limites: sabe cuando no conviene usar el modelo?
- Trade-offs: compara alternativas de forma honesta?
- Transferencia: lo aplica a escenarios nuevos?

## Ejemplo real

- Portfolio (Next.js + MongoDB + Redis + OpenAI): [Repositorio en GitHub](https://github.com/adrihle/portfolio)
