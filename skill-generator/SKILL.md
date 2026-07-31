---
inclusion: manual
version: "1.0.0"
---

# Skill Generator — Steering para el Agente

## Propósito

Este steering guía al Agente para crear y mantener SKILLs dentro del repositorio localSkills. Cuando se invoca, el Agente sintetiza la conversación activa y entrega un paquete listo para agregarse al repositorio: una carpeta con SKILL.md y, opcionalmente, scripts/, references/ y assets/ según corresponda.

El objetivo de esta versión es consolidar buenas prácticas, reducir la ambigüedad y garantizar que los skills generados sean compactos, reutilizables y listos para usarse sin ediciones manuales.

---

## Salida esperada

El agente debe producir una carpeta con la siguiente estructura (omitir carpetas vacías):

```
[NOMBRE_DEL_SKILL]/
├── scripts/          # Solo si aplica: scripts ejecutables necesarios para el flujo del skill
├── SKILL.md          # Documento principal: front-matter + instrucciones y reglas
└── references/       # Opcional: documentación detallada (solo si es necesaria)
```

---

## Convenciones y reglas obligatorias

1. Front-matter: Mantener las claves actuales `inclusion: manual` y `version: "1.0.0"` al inicio del archivo principal. No introducir otros campos automatizados que rompan la compatibilidad con herramientas existentes.
2. Idioma: Español. Usar términos técnicos en inglés cuando sean estándar.
3. Estructura: Usar secciones con encabezados de nivel 2 (##) para organizar el contenido.
4. Sección final `## Instrucciones para el agente`: Debe contener pasos accionables y reglas concretas para ejecutar el skill.
5. No dejar placeholders: el agente debe escribir contenido completo y funcional en todos los archivos generados.
6. Omitir carpetas vacías: si no hay scripts ni referencias, no crear esas carpetas.
7. Versionado: arrancar siempre desde `1.0.0` en la primera entrega.

---

## Flujo que debe seguir el Agente al generar un skill

1. Derivar nombre del skill
   - Analizar la conversación activa y generar un nombre descriptivo en kebab-case: `tema-subtema-accion` (ej.: `api-docs-generator`).
   - Confirmar que el slug no colisiona con skills existentes; si hay colisión, añadir sufijo numérico (`-v2`) o proponer alternativa.

2. Determinar carpeta temática
   - Revisar agrupaciones existentes (p. ej. `GITHUB/`, `SEO/`) y ubicar el skill en la carpeta más adecuada.
   - Si no existe una categoría adecuada, proponer una nueva con nombre en mayúsculas y justificar la elección en `documentation.md`.

3. Generar SKILL.md
   El archivo principal debe incluir, en este orden:
   - Front-matter (líneas iniciales tal como en la plantilla).
   - Título `# Nombre descriptivo` (en español).
   - Propósito breve (2–4 oraciones).
   - Contexto técnico relevante para implementar el skill en este repo.
   - Flujo de trabajo numerado con pasos claros.
   - Reglas y restricciones (qué hacer y qué evitar).
   - Instrucciones para el agente (pasos accionables, puntos de comprobación, inputs/outputs esperados).
   - Ejemplos de uso (al menos 1 ejemplo concreto de prompt que activaría el skill).

4. Generar documentation.md
   Debe contener:
   - Encabezado con fecha (`YYYY-MM-DD`).
   - Historial cronológico de decisiones (qué se decidió y cuándo).
   - Razonamiento: el "por qué" de cada decisión.
   - Origen: fragmento o resumen de la conversación que motivó el skill.
   - Versión inicial marcada como `[1.0.0]`.

5. Generar scripts/ (solo si aplica)
   - Añadir scripts reproducibles solo cuando forman parte del flujo (ej.: conversión, pruebas automáticas, empaquetado).
   - Cada script debe tener cabecera con descripción, inputs esperados y licencia/autor.

6. Entregar contenido completo
   - No deben quedar secciones vacías ni TODOs.
   - Los archivos deben ser listos para copiar y usar.

---

## Reglas de calidad y comprobaciones finales

- Si falta contexto en la conversación, realizar una única inferencia razonada y documentarla en `documentation.md`.
- Mantener consistencia de estilo con los skills existentes en el repositorio.
- Validar que ejemplos y comandos sean reproducibles localmente (mínimo revisión estática).
- Evitar duplicación: si un detalle es largo, moverlo a `references/` y referenciarlo desde SKILL.md.

---

## Plantilla mínima de SKILL.md que debe generar el Agente

```
---
inclusion: manual
version: "1.0.0"
---

# <nombre-del-skill>

## Propósito

<2-4 oraciones>

## Contexto técnico

<qué necesita saber el desarrollador/Agente sobre el repo o entorno>

## Flujo de trabajo

1. Paso uno
2. Paso dos

## Reglas y restricciones

- No hacer X
- Evitar Y

## Instrucciones para el agente

1. Acción concreta
2. Comprobar condición

## Ejemplo de uso

> "<prompt de usuario que activaría este skill>"
```

---

## Cómo invocar este steering

Usar el tag de steering en la conversación:

```
#skill-generator — genera el skill para esta conversación
```

El Agente leerá la sesión, sintetizará la información y producirá los archivos listos para commitear en `localSkills`.

---

## Instrucciones para el mantenedor del steering (nota interna)

- Mantener este archivo conciso: si el contenido de referencia crece, moverlo a `skill-generator/references/guidelines.md`.
- Cuando se actualicen convenciones (nombres, carpetas, front-matter), documentar el cambio en `documentation.md` con fecha y motivo.

---

## Ejemplo breve (caso real)

Supongamos una conversación donde se decide crear un generador de documentación OpenAPI para microservicios.

- Nombre propuesto: `openapi-docs-generator`
- Estructura:
  - `openapi-docs-generator/SKILL.md` (con propósito, contexto, flujo y ejemplos)
  - `openapi-docs-generator/scripts/generate_openapi.sh` (script opcional)
  - `openapi-docs-generator/references/README.md` (detalles de implementación)

Documentation.md debe registrar las decisiones y la razón para incluir el script.

---

## Cambio aplicado

He actualizado y consolidado este SKILL.md para que el Agente genere skills más completos y con menos ambigüedad. Si quieres, puedo:

- Añadir el archivo `skill-generator/references/guidelines.md` con la versión larga del material original.
- Crear una plantilla de script de ejemplo en `skill-generator/scripts/`.

Dime cuál de esas acciones quieres que haga a continuación.
