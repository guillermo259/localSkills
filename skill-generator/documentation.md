# Documentation — Skill Generator Steering

## Contexto de origen

Este steering surgió de una conversación donde el usuario necesitaba un mecanismo para capturar el conocimiento generado en sesiones de trabajo con el Agente y convertirlo en skills reutilizables para el repositorio `localSkills`. El problema central era que cada conversación producía soluciones valiosas que se perdían al cerrar la sesión, sin un proceso estandarizado para preservarlas.

---

## Historial de cambios

### [1.0.0] — 2026-07-28

#### Decisiones de diseño

**1. Nombre del steering: `skill-generator`**
- **Por qué:** El nombre describe exactamente su función — genera skills. Es corto, en kebab-case, consistente con las convenciones del repositorio y fácil de referenciar en chat con `#skill-generator`.

**2. `inclusion: manual` como modo de activación**
- **Por qué:** Seguir la convención establecida en todos los skills existentes del repositorio (`commit-format.md`, `readme-generator.md`, `seo-auditor.md`). Los skills de activación manual solo se cargan cuando el usuario los referencia explícitamente, evitando contaminación del contexto en conversaciones donde no son relevantes.

**3. Sin preguntas al usuario — síntesis automática de la conversación**
- **Por qué:** El requerimiento original fue explícito: "No me hagas preguntas — sintetiza todo lo que ya conoces de nuestra sesión." Hacer preguntas interrumpe el flujo y derrota el propósito del steering, que es capturar conocimiento acumulado de forma eficiente.

**4. Estructura de tres archivos: `SKILL.md` + `documentation.md` + `scripts/` (condicional)**
- **Por qué:** Separa responsabilidades claramente:
  - `SKILL.md` — el qué y el cómo (uso operativo)
  - `documentation.md` — el por qué (memoria de decisiones)
  - `scripts/` — solo cuando existen scripts concretos discutidos, para no crear carpetas vacías sin propósito
- Esta estructura fue definida por el usuario como requisito en la conversación original.

**5. Nombre de carpeta derivado del tema de la conversación**
- **Por qué:** Hace los skills autodescriptivos y fáciles de encontrar sin necesidad de abrir el archivo. Un nombre genérico como `skill-001` no aporta contexto.

**6. Organización en carpetas temáticas heredada del repositorio existente**
- **Por qué:** El repositorio ya tiene una estructura de carpetas por área (`GITHUB/`, `SEO/`). Respetar esa convención mantiene la coherencia del proyecto y facilita la navegación a medida que crece la colección de skills.

**7. Front-matter con `version: "1.0.0"` en todo skill nuevo**
- **Por qué:** Permite rastrear evoluciones futuras del skill. Empezar desde `1.0.0` sigue semantic versioning y es consistente con los skills existentes del repositorio.

**8. Nivel de detalle suficiente para desarrolladores que no estuvieron en la conversación**
- **Por qué:** Los skills son artefactos reutilizables que vivirán en el repositorio y serán usados en contextos futuros, potencialmente por otras personas. Un skill que solo tiene sentido si conoces la conversación original tiene vida útil muy corta.

---

## Notas de implementación

- El steering vive en `/skill-generator/SKILL.md` dentro del workspace del repositorio `localSkills`.
- Para que el Agente lo reconozca como steering manual, el archivo `SKILL.md` incluye el front-matter con `inclusion: manual`.
- No se generó carpeta `scripts/` para este steering porque no hubo scripts concretos en la conversación de origen — solo definición de estructura y comportamiento en Markdown.
