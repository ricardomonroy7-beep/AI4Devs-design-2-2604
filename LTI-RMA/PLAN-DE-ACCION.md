# PLAN DE ACCIÓN — Entrega Módulo 5 (AI4Devs) · LTI-RMA

> **Contexto compartido.** Este archivo + `99PROGRESS.md` viven en `WORK/` y son la
> única fuente de verdad de orquestación. Cualquier agente (Opus, Sonnet, Haiku,
> Cursor) que retome el trabajo LEE ESTOS DOS ARCHIVOS PRIMERO, mira la bitácora para
> saber qué tarea sigue, ejecuta UNA tarea atómica, y actualiza el 99PROGRESS al cerrar.
> **Autor:** RMA (Ricardo Monroy Alvarez) · **Fecha:** Jun 2026 · **Modo:** CONSERVATIVE, baby steps.

---

## 0 · Resumen de la actividad (qué hay que entregar)

Actividad del Módulo 5: **Creación del Backlog de Producto LTI**. A partir del PRD ya
existente (`LTI-RMA.md`), actuando como **Product Manager + Business Analyst**, producir:

1. **User Stories** (mínimo 2; aquí: 3) con plantilla común, criterios **INVEST** y
   **acceptance criteria en formato BDD Gherkin** (Given/When/Then).
2. **Backlog de producto** priorizado con **una metodología concreta** → aquí:
   **tabla multifactor** (Impacto·Urgencia·Complejidad·Riesgos/Dependencias).
3. **Experimentación de prompts**: probar varios prompts para generar el backlog,
   indicar cuál dio mejores resultados y por qué (va en `prompts.md`).
4. **Tickets de trabajo** de **UNA** User Story (la más fácil de empezar),
   aterrizados técnicamente.
5. *(Extra — NO se hará)* Estimación de esfuerzo. **Descartado por decisión de RMA.**

**Entregables finales (los únicos 2 archivos que importan al repo):**
- `UserStories-iniciales.md` — en **inglés**, con **resumen ejecutivo en español** al inicio.
- `prompts.md` — en **español**.

Ubicación destino en repo: `AI4Devs-design-2/LTI-iniciales/`. El fork, la branch,
OpenSpec y specboot **ya están cargados** por RMA. La carpeta `WORK/` y su contenido
**no se entrega**; es andamiaje de proceso.

---

## 1 · Decisiones bloqueadas (no re-cuestionar)

| Tema | Decisión |
|---|---|
| Iniciales | **RMA** en todo. `GUIA.md` (que decía RGD) está mal, ignorar esa parte. |
| Alcance US | **3 User Stories** (mínimo coherente: da señal real al backlog priorizado). |
| US para tickets | **US-1 — Recruiter crea y publica un JobPosting** (la más fácil de empezar: CRUD + validación, sin dependencias de candidato). |
| Priorización | **Tabla multifactor** del Módulo 5. |
| Estimación de esfuerzo | **NO se hace.** |
| Idioma entrega | `UserStories-iniciales.md` en inglés + resumen en español. `prompts.md` en español. |
| Idioma técnico | Code/entidades/tickets siempre en inglés (igual que el PRD). |
| Prioridad | **Calidad de entrega CON rapidez.** Es hora límite: el objetivo es ENTREGAR ya. |

---

## 2 · Stack y contenido ya presente (no inventar)

**Stack del producto** (del PRD `LTI-RMA.md` §1.5, §4, §5): Express + Prisma +
PostgreSQL · React CRA + Bootstrap · arquitectura modular monolith (Clean Arch / DDD),
pipeline asíncrono BullMQ + Redis, vectores en pgvector. *Esta actividad es de
documentación, no de código*: el stack solo se usa para aterrizar técnicamente los tickets.

**Material reutilizable del PRD (base de oro, ya hecho):**
- Lean Canvas (§2) · 3 Use Cases con diagramas Mermaid (§3): UC-1 publicar/recibir
  solicitudes, UC-2 screening IA explicable, UC-3 colaboración/evaluación.
- Modelo de datos (§4): 13 entidades + 3 tablas de unión, ER en Mermaid, tipos Prisma.
  Entidades clave: `Company, User, Candidate, JobPosting, PipelineStage, Application,
  Resume, Interview, Evaluation, MatchResult, Skill, Notification, AuditLog`.
- HLD (§5) y C4 (§6) del Screening Engine.

**Las 3 User Stories de esta entrega (derivadas del PRD):**
- **US-1** — *Recruiter creates and publishes a JobPosting.* (Épica UC-1) → **fácil de empezar → TICKETS.**
- **US-2** — *Candidate applies to a JobPosting and uploads a Resume.* (Épica UC-1)
- **US-3** — *AI produces an explainable MatchResult for an Application.* (Épica UC-2, diferenciador)

---

## 3 · Metodología a aplicar (de la teoría M4/M5)

- **Plantilla US común** + **INVEST** (Independent, Negotiable, Valuable, Estimable, Small, Testable).
- **Acceptance Criteria en BDD Gherkin** (Given/When/Then), varios escenarios por US (happy path + edge + error).
- **Backlog Agile**: Épicas → User Stories → Tickets (jerarquía Product Roadmap del M5).
- **Modelado de datos**: subset de entidades tocadas por las US + diagrama Mermaid (`erDiagram`).
- **Priorización**: tabla multifactor (columnas: Impacto en Usuario/Valor de Negocio ·
  Urgencia · Complejidad/Esfuerzo · Riesgos/Dependencias) → ranking + racional.
- **Plantilla de Ticket de trabajo** (M5, completa): Título claro · Descripción detallada ·
  Criterios de Aceptación · Prioridad · *(Estimación — omitida)* · Asignación · Etiquetas/Tags ·
  Comentarios/Notas · Enlaces/Referencias · Historial de Cambios.

---

## 4 · Orquestación multi-agente y ruteo por costo

| Tier | Herramienta | Para qué (regla de ruteo) |
|---|---|---|
| **Orquestador** | **Este chat — Opus 4.8 adaptativo** | Plan, orden general, arquitectura de US y tickets, revisión final senior. Asistente principal. |
| **Arquitectura** | **Claude Code — Opus** | Tareas de criterio/arquitectura; delega tareas mecánicas a subagentes Haiku. |
| **Media complejidad** | **Claude Code — Sonnet** | Extracción de modelo de datos, redacción de `prompts.md`, ensamblado del .md. |
| **Mecánico (subagentes)** | **Haiku** (delegados por CC-Opus/Sonnet) | Verificar checklist INVEST, lint de sintaxis Mermaid, chequeo de consistencia de nombres, formateo markdown. |
| **Fallback** | **Cursor** | SOLO si se acaban los tokens de sesión y quedan tareas atómicas pendientes. Lee `WORK/` y retoma desde el 99PROGRESS. |

> **Camino rápido recomendado (por la hora límite):** el orquestador (este chat, Opus)
> puede ejecutar **Fases A→F completas aquí mismo** y entregar `UserStories-iniciales.md`
> + `prompts.md` terminados; RMA solo hace commit/PR (Fase G). El ruteo multi-agente de
> arriba queda documentado para el fallback con Cursor o para repartir si se prefiere.

---

## 5 · Tareas atómicas (qué hace el usuario / qué hace la IA / output)

> Gate por fase: al cerrar una fase, RMA responde `ok` / `ajustes: <x>` / `no` antes de cruzar a la siguiente.
> Cada tarea produce su salida en un borrador de trabajo (`WORK/draft-*.md`) que luego se ensambla.

### Fase 0 — Setup *(IA: Opus, este chat — HECHO en este turno)*
- **T-00** · Crear `WORK/PLAN-DE-ACCION.md` + `WORK/99PROGRESS.md`. → Salida: estos 2 archivos.
  - *Usuario:* nada. *IA:* genera plan y bitácora.

### Fase A — User Stories *(IA: Opus)*
- **T-A1** · Redactar las 3 US con plantilla común + INVEST + AC en Gherkin. → `WORK/draft-userstories.md`.
- **T-A2** · *(Haiku)* Verificar cada US contra checklist INVEST y marcar ✔/✖ por criterio. → sección "INVEST evaluation".

### Fase B — Modelo de datos (slice) *(IA: Sonnet)*
- **T-B1** · Extraer del PRD las entidades tocadas por las 3 US + diagrama Mermaid `erDiagram` reducido. → `WORK/draft-datamodel.md`.

### Fase C — Backlog + priorización *(IA: Opus)*
- **T-C1** · Armar backlog (Épicas → US) con contexto Agile. → `WORK/draft-backlog.md`.
- **T-C2** · Tabla multifactor + ranking priorizado + racional. → mismo archivo.

### Fase D — Tickets de US-1 *(IA: Opus — tarea senior)*
- **T-D1** · Descomponer US-1 en tickets de trabajo con plantilla completa M5 (sin estimación). → `WORK/draft-tickets.md`.
- **T-D2** · Aterrizar técnicamente cada ticket contra el stack (Prisma schema, endpoints Express, validación Zod, UI React CRA). → mismo archivo.

### Fase E — prompts.md *(IA: Sonnet)*
- **T-E1** · Documentar (en español) ≥3 variantes de prompt usadas para generar el backlog, comparar, elegir la mejor y escribir conclusiones del porqué. → `prompts.md`.

### Fase F — Ensamblado + QA *(IA: Sonnet ensambla, Opus revisa)*
- **T-F1** · Ensamblar `UserStories-iniciales.md`: resumen ejecutivo ES + cuerpo EN, TOC, US, modelo de datos, backlog+tabla, tickets. Verificar render Mermaid y consistencia de nombres con el PRD. → `UserStories-iniciales.md`.
- **T-F2** · *(Opus)* Revisión final contra el checklist de la actividad y completitud INVEST/plantilla. → visto bueno.

### Fase G — Handoff / commit *(Usuario + opcional CC)*
- **T-G1** · Colocar los 2 archivos en `LTI-iniciales/`, commit por fase, push a la branch, abrir PR con el prompt DRASTIC en la descripción.
  - *Usuario:* commit/push/PR (GitHub Desktop). *IA (opcional CC):* puede generar mensajes de commit y descripción de PR.

---

## 6 · Mapa de archivos

```
WORK/
├── PLAN-DE-ACCION.md      ← este archivo (no se entrega)
├── 99PROGRESS.md          ← bitácora viva (no se entrega)
├── draft-userstories.md   ← borrador Fase A
├── draft-datamodel.md     ← borrador Fase B
├── draft-backlog.md       ← borrador Fase C
└── draft-tickets.md       ← borrador Fase D

ENTREGA (van a AI4Devs-design-2/LTI-iniciales/):
├── UserStories-iniciales.md   ← inglés + resumen ES   [ENTREGABLE]
└── prompts.md                 ← español               [ENTREGABLE]
```

## 7 · Definition of Done (entrega)

- [ ] 3 User Stories con plantilla común, INVEST y AC en Gherkin.
- [ ] Backlog con épicas + tabla multifactor priorizada + racional.
- [ ] Tickets de US-1 con plantilla completa M5 (sin estimación), aterrizados al stack.
- [ ] `UserStories-iniciales.md` en inglés con resumen ejecutivo en español; Mermaid válido.
- [ ] `prompts.md` en español con ≥3 prompts, comparación, mejor prompt y conclusiones.
- [ ] Nombres de entidades/actores consistentes con `LTI-RMA.md`.
- [ ] Todo bajo iniciales RMA.
