---
inclusion: manual
version: "1.0.0"
---

# Formato de Commits

Usa este formato para todos los mensajes de commit en el proyecto.

## Estructura

```
<tipo>(<alcance>): <descripción corta>

<cuerpo opcional>
```

## Tipos permitidos

| Tipo       | Cuándo usarlo                                      |
|------------|----------------------------------------------------|
| `feat`     | Nueva funcionalidad                                |
| `fix`      | Corrección de bug                                  |
| `docs`     | Cambios en documentación                           |
| `style`    | Formato, espacios, puntos y comas (no lógica)      |
| `refactor` | Reestructuración sin cambiar comportamiento        |
| `test`     | Agregar o corregir tests                           |
| `chore`    | Tareas de mantenimiento (deps, configs, scripts)   |
| `perf`     | Mejora de rendimiento                              |
| `ci`       | Cambios en CI/CD                                   |

## Reglas

1. La descripción corta va en minúsculas, sin punto final, máximo 50 caracteres.
2. El alcance (scope) es opcional y describe el área afectada (ej: `auth`, `api`, `ui`).
3. El cuerpo es opcional. Si se incluye, separar con una línea en blanco y explicar el **qué** y el **por qué**, no el cómo.
4. Si hay breaking changes, agregar `BREAKING CHANGE:` en el cuerpo.

## Ejemplos

```
feat(auth): agregar login con Google
```

```
fix(ui): corregir overflow en sidebar mobile
```

```
refactor(api): simplificar lógica de validación

Se eliminaron validaciones duplicadas que ya cubre el middleware
de autenticación.
```

```
chore: actualizar dependencias de desarrollo
```

## Instrucciones para el agente

- Al hacer un commit, sigue estrictamente este formato.
- Analiza los archivos modificados para elegir el tipo y alcance correctos.
- Escribe la descripción en español.
- Si hay múltiples cambios no relacionados, sugiere commits separados.
