---
inclusion: manual
version: "1.0.0"
---

# Release & Versionado

Instrucciones para lanzar una nueva versión de la aplicación Taskiando.

## Proceso de Release

Cuando el usuario indique que quiere lanzar una nueva versión, sigue estos pasos en orden:

### 1. Solicitar información al usuario

- **Número de versión**: Preguntar cuál es la nueva versión (ej: `1.0.0`, `1.1.0`, `0.2.0`).
- **Resumen de cambios**: Pedir un listado breve de los cambios incluidos en esta versión (features, fixes, mejoras, etc.).

### 2. Actualizar `package.json`

- Cambiar el campo `"version"` al nuevo número de versión proporcionado.

### 3. Actualizar `README.md`

- Asegurarse de que el README refleje el estado actual del proyecto (nombre, descripción, instrucciones).
- Al **final del archivo** agregar (o actualizar) la sección de Changelog con la nueva entrada.
- Para saber cuales son los cambios debes revisar los ultimos commits que hayan hecho en Git. primero debes revisar el ultimo que tienes en el README.md y revisas los cambios que se tengan de ahi en adelante.

### 4. Formato del Changelog

El changelog se agrega al final del `README.md` con el siguiente formato:

```markdown
---

## Changelog

### [X.Y.Z] - YYYY-MM-DD

#### Agregado
- Descripción del feature nuevo

#### Corregido
- Descripción del bug fix

#### Cambiado
- Descripción del cambio

#### Eliminado
- Descripción de lo removido
```

**Reglas del Changelog:**
- Las versiones se ordenan de la más reciente (arriba) a la más antigua (abajo).
- Solo incluir las categorías que apliquen (Agregado, Corregido, Cambiado, Eliminado).
- Usar la fecha actual del release.
- Si ya existe una sección `## Changelog`, agregar la nueva versión justo debajo del título `## Changelog`.
- Si no existe la sección, crearla al final del README con un separador `---` antes.

### 5. Confirmar cambios

- Mostrar al usuario un resumen de los cambios realizados en `package.json` y `README.md` antes de finalizar.
