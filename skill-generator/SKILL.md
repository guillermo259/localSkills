---
inclusion: manual
version: "1.0.0"
---

# Skill Generator — Steering para el Agente

## Propósito

Este steering le indica a el Agente cómo generar nuevas skills para el repositorio `localSkills`. Cuando el usuario lo invoque, el Agente sintetiza toda la conversación activa y produce una skill completa, lista para usar, sin hacer preguntas.

El output siempre es una carpeta con la siguiente estructura:

```
[NOMBRE_DEL_SKILL]/
├── scripts/          # Solo si aplica: scripts necesarios para entender o ejecutar el skill
├── SKILL.md          # Explicación detallada de qué hace el skill, cómo funciona y cómo usarlo
└── documentation.md  # Registro cronológico de cambios, decisiones y el por qué de cada una
```

---

## Contexto Técnico del Codebase

### Repositorio: localSkills
- **Propietario:** [@guillermo259](https://github.com/guillermo259)
- **Repo GitHub:** https://github.com/guillermo259/localSkills
- **Licencia:** CC BY 4.0

### Convenciones de los skills existentes

Todos los skills del proyecto siguen estas reglas que el Agente debe respetar al generar nuevos:

1. **Front-matter obligatorio** al inicio del archivo principal:
   ```yaml
   ---
   inclusion: manual
   version: "1.0.0"
   ---
   ```
2. **`inclusion: manual`** — los skills solo se activan cuando el usuario los referencia explícitamente en la conversación. Nunca se incluyen automáticamente.
3. **Idioma:** español, con términos técnicos en inglés cuando corresponda.
4. **Estructura por sección con `##`** — cada skill divide su contenido en secciones claras con encabezados de nivel 2.
5. **Instrucciones para el agente** — cada skill termina con una sección `## Instrucciones para el agente` que define exactamente cómo debe comportarse el Agente al ejecutar el skill.
6. **Organización en carpetas temáticas:** los skills se agrupan por área (`GITHUB/`, `SEO/`, etc.). el Agente debe sugerir la carpeta correcta o proponer una nueva si el skill no encaja en ninguna existente.

---

## Comportamiento de el Agente al ejecutar este steering

Cuando el usuario invoque este steering, el Agente debe:

### 1. Derivar el nombre del skill
- Analizar el tema central de la conversación activa.
- Generar un nombre descriptivo, conciso y en kebab-case (ej: `api-docs-generator`, `test-coverage-reporter`).
- El nombre de la carpeta raíz debe ser ese mismo slug.

### 2. Determinar la carpeta temática
- Revisar las categorías existentes (`GITHUB/`, `SEO/`, etc.).
- Asignar el skill a la categoría más apropiada.
- Si no existe una categoría adecuada, proponer una nueva con nombre en mayúsculas.

### 3. Generar `SKILL.md`
El archivo debe incluir obligatoriamente:
- **Front-matter** con `inclusion: manual` y `version: "1.0.0"`
- **Título** con `#` — nombre descriptivo del skill
- **Propósito** — qué problema resuelve, en 2-4 oraciones
- **Contexto técnico** — detalles del codebase relevantes para ejecutar el skill correctamente
- **Flujo de trabajo** — pasos numerados que el agente debe seguir
- **Reglas y restricciones** — qué debe y qué NO debe hacer el agente
- **Instrucciones para el agente** — comportamiento específico al activar el skill
- **Ejemplos de uso** — al menos un ejemplo concreto de cómo invocar el skill

### 4. Generar `documentation.md`
El archivo debe incluir:
- **Encabezado con fecha** (formato `YYYY-MM-DD`)
- **Historial cronológico** de decisiones tomadas durante la conversación
- **Por qué** de cada decisión de diseño (no solo el qué)
- **Versión inicial** claramente marcada como `[1.0.0]`
- **Sección de contexto** que explique de qué conversación surgió el skill

### 5. Generar `scripts/` (condicional)
- Solo si en la conversación se discutieron scripts concretos (bash, python, node, etc.) que sean parte del flujo del skill.
- Si no hay scripts, omitir completamente la carpeta.
- Cada script debe tener comentarios explicativos en la cabecera.

### 6. Entregar el contenido completo
- el Agente debe escribir el contenido real y completo de cada archivo.
- **Prohibido** dejar placeholders, instrucciones vacías o secciones sin completar.
- El skill debe estar listo para copiar y usar sin ediciones adicionales.

---

## Reglas de Calidad

- No hacer preguntas al usuario — sintetizar todo desde la conversación activa.
- Si la conversación es muy corta o el tema es ambiguo, hacer una única inferencia razonada y documentarla en `documentation.md`.
- El nivel de detalle en `SKILL.md` debe ser suficiente para que cualquier desarrollador que no estuvo en la conversación pueda entender y usar el skill.
- Mantener consistencia de estilo con los skills existentes del repositorio.
- Versionar siempre desde `1.0.0` en la primera entrega.

---

## Cómo usar este steering

En cualquier conversación donde hayas desarrollado una idea, solución o flujo de trabajo con el Agente, invoca este steering con:

```
#skill-generator — genera el skill para esta conversación
```

el Agente leerá toda la sesión, sintetizará el conocimiento acumulado y producirá los archivos listos para agregar al repositorio `localSkills`.
