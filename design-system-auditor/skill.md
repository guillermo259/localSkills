---
name: design-system-auditor
description: >
  Auditoria de la implementacion de Design Tokens, consistencia visual y uso del Sistema de Diseno (Design System).
  Escanea hojas de estilo (Tailwind, CSS Modules, Styled Components) y arboles de componentes para identificar
  valores hardcodeados, duplicacion de estilos y desviaciones del sistema de diseno atomico del proyecto.
  Mantiene la coherencia visual del producto y evita el crecimiento descontrolado de CSS.
---

# Design System Auditor — Integracion de Sistemas de Diseno y Reutilizacion

## Proposito

Este skill permite auditar la implementacion de Design Tokens, la consistencia visual y el uso correcto del Sistema de Diseno en proyectos frontend. Su objetivo es:

- **Mantener la coherencia visual** del producto en toda la base de codigo.
- **Evitar la duplicacion de estilos** y el crecimiento descontrolado de CSS.
- **Prohibir valores hardcodeados** de color, espaciado o tipografia.
- **Validar que los componentes** utilicen variables CSS o Design Tokens estandarizados.
- **Asegurar que los componentes de UI** provengan de la libreria atomica del proyecto.

---

## Metodologia de Auditoria

### 1. Escaneo de Hojas de Estilo

Revisar archivos de estilo en busca de desviaciones del sistema de diseno:

| Tecnologia | Patrones a escanear |
|---|---|
| **Tailwind CSS** | Clases arbitrarias: `bg-[#1a1a1a]`, `text-[14px]`, `p-[20px]`, `w-[100px]` |
| **CSS Modules** | Declaraciones con valores literales: `color: #ff0000`, `margin: 16px`, `font-size: 14px` |
| **Styled Components** | Propiedades con valores fijos: `color: #ff0000`, `padding: ${20}px` |
| **CSS Global / SASS** | Variables no tokenizadas, selectores anidados profundos, `!important` excesivo |

#### Patrones de deteccion (regex / heuristics)

```
# Tailwind arbitrario
\b(bg|text|border|shadow|ring|from|to|via|stroke|fill)-\[.*?\]

# Valores hex/rgb/hsl hardcodeados en CSS
#([0-9a-fA-F]{3,8})|rgb\(|rgba\(|hsl\(|hsla\(

# Espaciado / tipografia hardcodeado (px, rem sin token)
:\s*\d+(px|rem|em)\s*;?\s*(?!.*var\(--)

# Font-family arbitrario
font-family:\s*[^var(][^;]+;
```

### 2. Escaneo de Arboles de Componentes

Analizar la estructura de componentes para detectar:

- **Importacion de componentes base**: Se importan desde la libreria atomica o se re-crean inline?
- **Composicion atomica**: Se usan `Button`, `Input`, `Card`, `Text`, `Heading` del design system?
- **Props de estilo prohibidas**: `style={{ color: 'red' }}`, `className="custom-red"`
- **Anidamiento de componentes**: Componentes que deberian ser atomicos pero contienen markup crudo

### 3. Validacion de Design Tokens

Verificar que los valores usados correspondan a tokens definidos:

| Categoria | Ejemplos de Tokens Validos | Ejemplos Prohibidos |
|---|---|---|
| **Colores** | `var(--color-primary-500)`, `theme.colors.blue.600`, `bg-primary` | `#1a1a1a`, `rgb(255,0,0)`, `red` |
| **Espaciado** | `var(--space-4)`, `theme.spacing(4)`, `p-4`, `gap-2` | `16px`, `1rem`, `20px` |
| **Tipografia** | `var(--font-body)`, `text-sm`, `font-heading` | `14px`, `Arial`, `1.2rem` |
| **Bordes / Sombras** | `var(--radius-md)`, `shadow-lg`, `border-default` | `4px`, `0 2px 4px rgba(0,0,0,0.1)` |
| **Z-Index** | `var(--z-dropdown)`, `z-modal` | `z-index: 9999`, `z-[999]` |

---

## Criterios del Agente (Checklist de Auditoria)

### PROHIBIDO (debe reportarse como error critico)

- [ ] **Valores de color hardcodeados**: cualquier hex, rgb, hsl, o nombre de color CSS literal (`red`, `blue`) fuera de la definicion de tokens.
- [ ] **Espaciado arbitrario**: valores de `margin`, `padding`, `gap`, `width`, `height` que no provengan del scale de tokens.
- [ ] **Tipografia arbitraria**: `font-size`, `font-family`, `line-height`, `letter-spacing` con valores literales.
- [ ] **Shadows / borders / radius hardcodeados**: cualquier valor de sombra, borde o radio que no use token.
- [ ] **Tailwind arbitrary values**: cualquier clase con sintaxis `[...]` que no este en la safelist aprobada.
- [ ] **Componentes re-creados**: crear un `<button>` nativo cuando existe `<Button>` del design system.
- [ ] **Props `style` inline**: uso de `style={{ ... }}` con valores de estilo en componentes JSX.
- [ ] `!important` en CSS: salvo excepciones documentadas de utilidad.

### REQUERIDO (debe validarse)

- [ ] **Uso de variables CSS / CSS custom properties**: todos los valores semanticos deben usar `var(--token)`.
- [ ] **Uso de Design Tokens del proyecto**: colores, espaciado, tipografia via el sistema de tokens (Style Dictionary, Tailwind theme, etc.).
- [ ] **Componentes atomicos**: los elementos de UI deben importarse de la libreria de componentes del proyecto.
- [ ] **Consistencia tematica**: soporte correcto de dark/light mode via tokens semanticos.
- [ ] **Documentacion de excepciones**: cualquier desviacion debe estar documentada con un comentario `/* design-system-exempt: razon */`.

### ADVERTENCIA (debe reportarse como warning)

- [ ] **Duplicacion de reglas CSS**: selectores con propiedades identicas o muy similares.
- [ ] **Selectores anidados profundos**: mas de 3 niveles de anidamiento en CSS/SASS.
- [ ] **Clases no utilizadas**: reglas CSS que no se aplican a ningun componente.
- [ ] **Sobrescritura de tokens**: redefinir una variable CSS del design system en scope local.

---

## Formatos de Reporte

### Reporte por Archivo

```markdown
## src/components/UserCard.tsx

| Linea | Severidad | Problema | Token Sugerido |
|-------|-----------|----------|----------------|
| 24 | Error | `color: #333333` hardcodeado | `var(--color-text-primary)` |
| 31 | Error | `<button>` nativo en lugar de `<Button>` | Importar `Button` de `@/ui` |
| 45 | Warning | `margin-bottom: 12px` | `var(--space-3)` o `mb-3` |
| 52 | Error | `className="shadow-[0_2px_8px_rgba(0,0,0,0.15)]"` | `shadow-card` |
```

### Reporte Consolidado (Resumen Ejecutivo)

```markdown
# Design System Audit Report

**Proyecto:** [nombre]
**Fecha:** [fecha]
**Scope:** [archivos analizados]

## Metricas
- Errores criticos: [N]
- Advertencias: [N]
- Archivos conformes: [N]/[Total]
- Cobertura de tokens: [X]%

## Hallazgos principales
1. [Descripcion del hallazgo mas critico]
2. [Segundo hallazgo]

## Recomendaciones
1. [Accion concreta]
2. [Accion concreta]
```

---

## Flujo de Trabajo del Agente

1. **Solicitar contexto**: Preguntar al usuario por la estructura del proyecto, ubicacion de tokens, y libreria de componentes.
2. **Identificar tecnologias**: Detectar si usa Tailwind, CSS Modules, Styled Components, SASS, etc.
3. **Cargar tokens de referencia**: Leer el archivo de tokens (tokens.json, theme.ts, variables.css, etc.).
4. **Escaneo selectivo**: Analizar archivos relevantes (no node_modules, no build).
5. **Clasificar hallazgos**: Separar en errores criticos, warnings e info.
6. **Sugerir fixes**: Proporcionar el codigo corregido usando tokens validos.
7. **Generar reporte**: Entregar el reporte en formato markdown con metricas.

---

## Ejemplos de Fixes

### Antes (Hardcodeado)
```tsx
// UserBadge.tsx
export const UserBadge = () => (
  <div style={{ backgroundColor: '#f3f4f6', padding: '16px', borderRadius: '8px' }}>
    <span style={{ fontSize: '14px', color: '#1f2937' }}>Usuario</span>
  </div>
);
```

### Despues (Con Design Tokens)
```tsx
// UserBadge.tsx
import { Box, Text } from '@/ui';

export const UserBadge = () => (
  <Box bg="surface.secondary" p="4" rounded="md">
    <Text size="sm" color="text.primary">Usuario</Text>
  </Box>
);
```

### Antes (Tailwind Arbitrario)
```html
<div class="bg-[#f3f4f6] p-[16px] rounded-[8px]">
  <span class="text-[14px] text-[#1f2937]">Usuario</span>
</div>
```

### Despues (Tailwind Tokens)
```html
<div class="bg-gray-100 p-4 rounded-lg">
  <span class="text-sm text-gray-800">Usuario</span>
</div>
```

---

## Integracion con CI/CD (Recomendado)

El agente puede sugerir integrar estas reglas como:

- **Stylelint** con plugins como `stylelint-declaration-strict-value`, `stylelint-no-unsupported-browser-features`.
- **ESLint** con reglas custom para detectar `style` props y imports no atomicos.
- **Pre-commit hooks** con `lint-staged` para bloquear commits con valores hardcodeados.
- **Visual Regression Testing** con Chromatic o Percy para detectar cambios visuales no intencionales.

---

## Notas para el Agente

- Siempre preguntar primero: "Cual es la fuente de verdad de tus Design Tokens?" (archivo, URL, o documentacion).
- Si el proyecto no tiene tokens definidos, el primer paso es proponer la creacion de un token system antes de auditar.
- No ser dogmatico: algunos valores de diseno grafico (gradients complejos, imagenes, SVGs) pueden requerir excepciones documentadas.
- Priorizar la **reutilizacion de componentes** sobre la reutilizacion de estilos: un componente atomico mal usado es preferible a un div estilizado desde cero.
