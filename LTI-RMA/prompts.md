# prompts.md — LTI · Módulo 5 (RMA)

> Bitácora de prompts usados para generar las User Stories, el Backlog priorizado y los
> Tickets de trabajo a partir del PRD `LTI-RMA.md`. Asistente principal: **Claude (Opus 4.8)**.
> Se experimentó con varias formulaciones para generar el backlog; abajo se comparan y se
> indica cuál dio el mejor resultado y por qué.

---

## 1 · Contexto previo

Punto de partida: el PRD `LTI-RMA.md` (documento de diseño del Módulo 4) ya contenía Lean
Canvas, tres casos de uso con diagramas, modelo de datos de 13 entidades y arquitectura
C4. El objetivo de esta entrega era **derivar** de ese PRD los artefactos de Product
Management, sin reinventar el dominio.

---

## 2 · Prompts usados (en orden)

### Prompt 0 — Encuadre de rol, plan de acción y restricciones (setup)

```
ERES UN PRODUCT MANAGER, BUSINESS ANALYST, SOFTWARE DEVELOPER SENIOR, ARQUITECTO DE SISTEMAS SENIOR.
VAMOS A REALIZAR LA ACTIVIDAD DEL MODULO 4 DE AI4DEVS. ESTE CHAT ES PARA ORGANIZAR EL TRABAJO A REALIZAR.

SOLICITUDES:
    CREA EL PLAN GENERAL DE ACCION PARA COMPLETAR LA ACTIVIDAD DE LIDR, DEBE INCLUIR LOS PASOS A SEGUIR
    DE PARTE DEL USUARIO, LAS ACTIVIDADES REALIZADAS POR LA IA/AGENTE Y LOS OUTPUTS ESPERADOS HASTA EL
    .MD FINAL A SUBIR.
    NO NECESARIAMENTE SE VA A REALIZAR TODO EN UN SOLO CHAT O AGENTE, SE PUEDES USAR VARIOS Y MULTIPLES
    HERRAMIENTAS, YA SEA ORQUESTANDO O HACIENDO "MANUALMENTE", TU DECIDE LO QUE ME CONVENGA.

CONSTRAINTS:
    IDENTIFICA EL STACK Y EL CONTENIDO YA PRESENTE EN EL PROYECTO.
    ORGANIZA TAREAS ATOMICAS (PEQUEÑAS PARA QUE LAS PUEDA REALIZAR LA IA CORRECTAMENTE) DENTRO DE CADA
    SECCION A TRABAJAR.
    REALIZAME LAS PREGUNTAS NECESARIAS SI TE FALTA INFORMACION O CONTEXTO ANTES DE CREAR EL PLAN DE
    TRABAJO, NO SUPONGAS NADA.
    LEE LA TEORIA DEL MODULO 5 EN CONTEXTO COMPARTIDO PARA ESTAR AL TANTO.
    CADA PROCESO DE LOS ENTREGABLES, DEBE INVESTIGARSE PARA TENER CONTEXTO ACTUALIZADO Y PROFESIONAL.
    SE DEBE TRABAJAR EN UNA CARPETA WORK/ CON UN 99PROGRESS CHECKLIST Y ESTE PLAN DE ACCION.

PROCEDIMENTO QUE SE APRENDIO EN LA TEORIA DEL MODULO DEL MASTER PARA LA ACTIVIDAD Y SE DESEA APLICAR:

    TRABAJAR A PARTIR DE PRD LTI-RMA EXISTENTE
    HISTORIAS DE USUARIO A PARTIR DE CRITERIOS INVEST, Y FORMATO BDD CON ACCEPTANCE CRITERIA.
    BACKLOG DE PRODUCTO CON CONTEXTO AGILE
    MODELADO DE DATOS
        ENTIDADES EN MODELOS DE DATOS
        DIAGRAMAS MERMAID
    PRIORIZACION DEL BACKLOG DE PRODUCTO
        ESTIMACION DE PRIORIZACION
    TICKETS DE TRABAJO CON TITULO CLARO, DESCRIPCION DETALLADA, CRITERIOS DE ACEPTACION, PRIORIDAD,
    ESTIMACION DE ESFUERZO, ASIGNACION, ETIQUETAS O TAGS, COMENTARIOS Y NOTAS, ENLACES,
    HISTORIAL DE CAMBIOS.

SOLICITUD DIRECTA DE LA ACTIVIDAD:
    GENERAR USER STORIES
    ARMAR BACKLOG DE PRODUCTO
    GENERAR TICKETS DE TRABAJO DE USER STORY
```

**Respuestas de RMA al Prompt 0:**

```
Me parece bien usar hibrido con la carpeta works, que el agente tenga el contexto pero la entrega solo
es el .md y el prompts.md. No olvides las iniciales son RMA.
Usaré este chat con opus 4.8 adaptativo para el plan de accion y orden general (asistente principal).
Usaré Claude Code con opus para correr las tareas de arquitectura, y las tareas secundarias que el
mismo agente delegue a subagentes haiku (segun las instrucciones en el plan de accion).
Usaré Claude Code con sonnet para correr tareas de media complejidad.
Esto será así para ser mas eficientes en tokens.
Cursor lo usaré solo si se me acaban los tokens de sesion y me faltaron tareas atomicas por realizar.
Al usar varios agentes, ventanas, será importante trabajar con este sistema de contexto compartido.
El plan generado se agregará a la carpeta para referencia de todos.
Idiomas de entregables:
    prompts.md en español
    entrega en inglés con resumen en español

PROCUREMOS CALIDAD DE ENTREGA PERO RAPIDEZ PORQUE YA ES HORA LIMITE. AL MENOS PARA ESTE MODULO,
SOLO QUIERO ENTREGAR.

solo hacer las user stories minimas para la entrega.
realiza los tickets de la user story mas facil de empezar.
usar tabla multifactor para priorizacion backlog.
no se hara la estimacion de esfuerzo.
ya se tiene todo en la carpeta de design2, desde el fork con nueva branch, hasta openspec y specboot
cargados, mas los archivos anexos.
todo es con RMA, GUIA.MD ESTA MAL.
```

### Prompt A — Backlog directo (variante "todo de una")

```
Con base en el PRD adjunto, genera el backlog de producto completo: todas las
épicas, todas las user stories que se te ocurran, priorizadas, con criterios de
aceptación y tickets. Hazlo en un solo paso.
```

### Prompt B — Backlog por roles + INVEST (variante estructurada)

```
A partir de los tres casos de uso del PRD (UC-1, UC-2, UC-3), genera EXACTAMENTE
3 user stories, una por cada capacidad más valiosa. Para cada una:
- Escríbela en formato "Como <rol>, quiero <capacidad>, para <valor de negocio>".
- Añade criterios de aceptación en BDD (Given/When/Then) con al menos un happy
  path, un caso límite y un caso de error.
- Evalúala contra INVEST, criterio por criterio, marcando ✔/◐/✖ y justificando.
Usa los nombres de actores y entidades idénticos al PRD.
```

### Prompt C — Priorización con tabla multifactor (variante de método explícito)

```
Toma las 3 user stories y arma el backlog como jerarquía Épica → User Story.
Priorízalas con una TABLA MULTIFACTOR de cuatro columnas: Impacto en Usuario y
Valor de Negocio, Urgencia, Complejidad y Esfuerzo, Riesgos y Dependencias.
Califica cada una como Bajo/Medio/Alto. Como todas tienen alto valor de negocio,
NO uses el valor para desempatar: ordena por la combinación de urgencia,
complejidad y dependencias, y explica el racional del orden resultante.
```

### Prompt D — Tickets aterrizados al stack (variante de descomposición técnica)

```
Toma la user story más fácil de empezar (la de menor complejidad y sin
dependencias) y descomponla en tickets de trabajo. Usa la plantilla del Módulo 5:
título, descripción, criterios de aceptación, prioridad, asignación, etiquetas,
comentarios, enlaces e historial de cambios. NO incluyas estimación de esfuerzo.
Aterriza cada ticket técnicamente contra el stack del PRD (Express, Prisma,
PostgreSQL, React CRA, Bootstrap, validación con Zod): nombra endpoints, modelos
de Prisma y componentes de React concretos.
```

---

## 3 · Comparación de resultados

| Prompt | Enfoque | Resultado | Veredicto |
|---|---|---|---|
| **A** | "Todo de una" | Generó muchas historias genéricas, mezcló niveles (épica/historia/tarea), criterios de aceptación vagos y sin método de priorización. | ❌ Disperso, poco accionable. |
| **B** | 3 US ancladas a UC + INVEST | Historias enfocadas, trazables al PRD, con BDD y autoevaluación INVEST que reveló que US-3 era demasiado grande. | ✔ Sólido para las US. |
| **C** | Tabla multifactor con regla de desempate | Backlog ordenado con racional claro (dependencias y riesgo, no solo valor). | ✔ Mejor priorización. |
| **D** | Tickets descompuestos + stack | Tickets concretos con endpoints, modelos Prisma y componentes reales; plantilla completa. | ✔ Mejor aterrizaje técnico. |

---

## 4 · Mejor prompt y por qué

El mejor resultado **no vino de un único prompt**, sino de la **secuencia B → C → D
encadenada** (cada uno tomando como entrada la salida del anterior). Si hay que elegir
**uno solo**, el más efectivo fue el **Prompt B**, porque fue el que cambió la calidad de
todo lo que siguió.

**Por qué el Prompt B fue el más efectivo:**

1. **Ancló las historias al PRD** ("una por cada capacidad más valiosa de UC-1/2/3"), lo
   que evitó inventar dominio y garantizó trazabilidad de nombres.
2. **Fijó el número (exactamente 3)**, evitando la dispersión del Prompt A.
3. **Exigió BDD con tres tipos de escenario** (happy/límite/error), lo que produjo
   criterios de aceptación verificables, no decorativos.
4. **Forzó la autoevaluación INVEST criterio por criterio**, lo que hizo que el propio
   modelo detectara que US-3 violaba el criterio *Small* — un hallazgo de calidad que un
   prompt genérico nunca habría producido.

La lección general: **los prompts que imponen una estructura de salida y un método
explícito (INVEST, BDD, tabla multifactor) producen artefactos accionables; los prompts
abiertos ("genera el backlog completo") producen texto plausible pero inútil para
planificar.** Acotar el alcance y nombrar el método importa más que pedir "más".

---

## 5 · Prompt consolidado (DRASTIC) — para la descripción del PR

> *Nota de transparencia: este prompt consolidado se redactó con asistencia de IA y fue
> revisado y ajustado por RMA antes de su uso.*

```
[Direction] Actúa como Product Manager, Business Analyst y arquitecto senior.
[Results] Produce dos entregables: UserStories-iniciales.md (inglés + resumen en
español) y prompts.md (español).
[Audience] Equipo de producto del máster AI4Devs; revisor técnico.
[Structure] (1) 3 user stories ancladas a los UC del PRD, con plantilla común,
INVEST y criterios BDD (happy/límite/error); (2) slice del modelo de datos con
diagrama Mermaid; (3) backlog Épica→US priorizado con tabla multifactor
(Impacto·Urgencia·Complejidad·Riesgos/Dependencias) y racional; (4) tickets de la
US más fácil de empezar, con la plantilla del Módulo 5 y aterrizados al stack
(Express/Prisma/PostgreSQL/React CRA/Bootstrap/Zod), sin estimación de esfuerzo.
[Tone] Profesional, conciso, trazable.
[Identity] Reutiliza actores y entidades EXACTAMENTE como en el PRD LTI-RMA.md.
[Context] Parte del PRD existente; no reinventes el dominio; nombres en inglés
para artefactos técnicos.
```

---

## 6 · Conclusiones

- **Reutilizar el PRD como fuente de verdad** fue lo que más subió la calidad: las
  historias y tickets son trazables y consistentes porque heredan actores y entidades ya
  validados en el Módulo 4.
- **El método explícito gana al volumen.** Pedir 3 historias bien hechas con INVEST + BDD
  superó por mucho a pedir "todas las historias posibles".
- **La priorización mejora cuando se prohíbe el desempate fácil.** Forzar a no usar el
  valor de negocio como criterio (porque todas lo tienen alto) obligó a razonar por
  dependencias y riesgo, que es como se prioriza en la práctica.
- **El encadenamiento de prompts** (cada salida alimenta el siguiente) produjo mejor
  resultado que cualquier prompt monolítico.
