---
name: atomic-design-ui
version: 1.0.0
description: >
  Reorganiza proyectos de UI/Frontend aplicando la Metodología Atomic Design de Brad Frost.
  Proporciona una estructura jerárquica (Átomos → Moléculas → Organismos → Templates → Páginas)
  para lograr consistencia visual, escalabilidad y armonía en el diseño y maquetación.
  Úsala cuando el usuario quiera reestructurar, estandarizar o escalar la UI de su proyecto.
---

# Atomic Design UI Skill

## ¿Cuándo usar esta skill?

- El usuario quiere **reorganizar** la estructura de UI de su proyecto.
- Necesita **armonía visual** y consistencia en estilos y componentes.
- Quiere aplicar **Atomic Design Methodology** (Brad Frost) a su frontend.
- Está construyendo un **Design System** o una **UI Library**.
- Necesita migrar código desordenado a una arquitectura de componentes escalable.

## Metodología Atomic Design

Atomic Design es una metodología para crear sistemas de diseño de forma jerárquica,
inspirada en la química. Se compone de 5 niveles:

```
┌─────────────────────────────────────────┐
│  PÁGINAS    (Pages)                     │  Instancias reales con contenido real
│  ─────────────────────────────────────  │
│  TEMPLATES  (Templates)                 │  Estructuras de página con placeholders
│  ─────────────────────────────────────  │
│  ORGANISMOS (Organisms)                 │  Secciones complejas de UI (header, footer, cards)
│  ─────────────────────────────────────  │
│  MOLÉCULAS  (Molecules)                 │  Grupos simples de átomos (input + label + button)
│  ─────────────────────────────────────  │
│  ÁTOMOS     (Atoms)                     │  Elementos indivisibles (botones, inputs, tipografía)
└─────────────────────────────────────────┘
```

### 1. Átomos (Atoms)

**Definición:** Los bloques de construcción más básicos. No pueden dividirse más sin dejar de ser funcionales.

**Ejemplos:**
- Colores, tipografía, espaciado (tokens de diseño)
- Botones, inputs, labels, iconos
- Enlaces, etiquetas, badges

**Reglas de oro:**
- Cada átomo debe ser **independiente** y **reutilizable**.
- Define **tokens de diseño** (colores, fuentes, spacing, border-radius, sombras) ANTES de crear componentes.
- Los átomos NO deben depender de contexto externo.

**Estructura de carpetas sugerida:**
```
src/
└── atoms/
    ├── Button/
    │   ├── Button.tsx
    │   ├── Button.module.css / Button.styles.ts
    │   ├── Button.stories.tsx
    │   └── index.ts
    ├── Input/
    ├── Label/
    ├── Icon/
    └── index.ts          # Barrel export
```

### 2. Moléculas (Molecules)

**Definición:** Grupos de átomos que funcionan juntos como una unidad simple.

**Ejemplos:**
- Campo de búsqueda (input + icono + botón)
- Campo de formulario (label + input + mensaje de error)
- Card simple (imagen + título)
- Navbar item (icono + texto)

**Reglas de oro:**
- Las moléculas combinan **2-3 átomos** como máximo.
- Deben ser **relativamente simples**; si crecen mucho, conviértelas en organismos.
- Mantén la lógica de presentación, NO lógica de negocio compleja.

**Estructura de carpetas sugerida:**
```
src/
└── molecules/
    ├── SearchField/
    ├── FormField/
    ├── NavItem/
    └── index.ts
```

### 3. Organismos (Organisms)

**Definición:** Secciones complejas de la interfaz compuestas por moléculas y/o átomos.

**Ejemplos:**
- Header / Navbar completo (logo + navegación + búsqueda + perfil)
- Footer (links + redes sociales + newsletter)
- Card de producto completa (imagen + título + precio + botón + rating)
- Sidebar (menú + filtros + acciones)
- Formulario completo (múltiples campos + botones)

**Reglas de oro:**
- Los organismos pueden contener **lógica de negocio** leve.
- Son **dependientes del contexto** (ej: un Header varía según la página).
- Pueden contener otros organismos en casos excepcionales.

**Estructura de carpetas sugerida:**
```
src/
└── organisms/
    ├── Header/
    ├── Footer/
    ├── ProductCard/
    ├── LoginForm/
    └── index.ts
```

### 4. Templates (Templates)

**Definición:** Estructuras de página que colocan organismos en un layout, usando placeholders.

**Ejemplos:**
- Layout de página de inicio
- Layout de página de producto
- Layout de dashboard
- Layout de autenticación

**Reglas de oro:**
- Los templates **NO contienen datos reales**, solo placeholders.
- Se enfocan en la **estructura y el layout** (grids, flexbox, áreas).
- Son la base para las páginas finales.

**Estructura de carpetas sugerida:**
```
src/
└── templates/
    ├── HomeTemplate/
    ├── ProductTemplate/
    ├── DashboardTemplate/
    └── index.ts
```

### 5. Páginas (Pages)

**Definición:** Instancias específicas de templates con contenido real y datos reales.

**Ejemplos:**
- Página de inicio con datos del CMS/API
- Página de producto "Nike Air Max"
- Dashboard del usuario autenticado

**Reglas de oro:**
- Las páginas **inyectan datos reales** en los templates.
- Aquí vive la **lógica de negocio**, fetching de datos, estado global.
- Son el punto de entrada de las rutas de la aplicación.

**Estructura de carpetas sugerida:**
```
src/
└── pages/
    ├── HomePage/
    ├── ProductPage/
    ├── DashboardPage/
    └── index.ts
```

---

## Flujo de trabajo para reorganizar un proyecto

Cuando el usuario solicite reorganizar su proyecto con Atomic Design, sigue este flujo paso a paso:

### Paso 1: Auditoría del proyecto actual
- Solicita al usuario que comparta la estructura actual de carpetas o componentes clave.
- Identifica qué componentes existen y cómo están organizados.
- Detecta duplicaciones, inconsistencias y dependencias circulares.

### Paso 2: Definición de tokens de diseño (Átomos fundamentales)
Antes de mover componentes, establece los tokens base:

```
tokens/
├── colors.ts         # Paleta de colores con nombres semánticos
├── typography.ts     # Familias, tamaños, pesos, line-heights
├── spacing.ts        # Escala de espaciado (4px, 8px, 16px, 24px...)
├── shadows.ts        # Elevaciones y sombras
├── borders.ts        # Radios y grosores de borde
└── breakpoints.ts    # Puntos de quiebre responsive
```

### Paso 3: Clasificación de componentes existentes
Clasifica cada componente en su nivel atómico:

| Componente actual | Clasificación | Justificación |
|-------------------|---------------|---------------|
| Button            | Átomo         | Indivisible, reutilizable |
| Input + Label     | Molécula      | Agrupa 2 átomos |
| Header            | Organismo     | Complejo, contexto específico |
| LoginPage         | Página        | Tiene datos y lógica real |

### Paso 4: Refactorización progresiva
1. **Empieza por los átomos:** Extrae tokens y componentes base.
2. **Construye moléculas:** Agrupa átomos en unidades funcionales.
3. **Ensambla organismos:** Usa moléculas y átomos para secciones.
4. **Crea templates:** Define layouts con placeholders.
5. **Conecta páginas:** Inyecta datos reales en los templates.

### Paso 5: Documentación y Storybook
- Crea stories para cada componente en su nivel correspondiente.
- Documenta props, variantes y casos de uso.
- Asegura que cada componente sea testeable de forma aislada.

---

## Reglas de dependencia (CRÍTICO)

```
┌────────────────────────────────────────────┐
│  REGLA DE ORO DE LAS DEPENDENCIAS          │
│                                            │
│  Un nivel SOLO puede depender de:          │
│  • SÍ MISMO (mismo nivel)                  │
│  • NIVELES INFERIORES (más atómicos)       │
│                                            │
│  NUNCA puede depender de niveles           │
│  SUPERIORES (más complejos).               │
│                                            │
│  Ejemplo: Un Organismo puede usar          │
│  Moléculas y Átomos, pero NUNCA            │
│  Templates ni Páginas.                     │
└────────────────────────────────────────────┘
```

**Dependencias permitidas:**
- Átomo → Átomo ✅ (ej: Button usa Icon)
- Molécula → Átomo ✅ (ej: SearchField usa Input + Button)
- Organismo → Molécula + Átomo ✅ (ej: Header usa NavItem + Logo)
- Template → Organismo + Molécula + Átomo ✅
- Página → Todo lo anterior ✅

**Dependencias PROHIBIDAS:**
- Átomo → Molécula ❌ (un botón no debe depender de un formulario)
- Molécula → Organismo ❌
- Organismo → Template ❌
- Template → Página ❌

---

## Estructura final recomendada del proyecto

```
project-root/
├── src/
│   ├── tokens/                 # Tokens de diseño (la base de todo)
│   │   ├── colors.ts
│   │   ├── typography.ts
│   │   ├── spacing.ts
│   │   └── index.ts
│   │
│   ├── atoms/                  # Componentes indivisibles
│   │   ├── Button/
│   │   ├── Input/
│   │   ├── Label/
│   │   ├── Icon/
│   │   ├── Badge/
│   │   ├── Avatar/
│   │   ├── Text/
│   │   ├── Heading/
│   │   └── index.ts
│   │
│   ├── molecules/              # Grupos simples de átomos
│   │   ├── SearchField/
│   │   ├── FormField/
│   │   ├── NavItem/
│   │   ├── CardHeader/
│   │   ├── BreadcrumbItem/
│   │   └── index.ts
│   │
│   ├── organisms/              # Secciones complejas
│   │   ├── Header/
│   │   ├── Footer/
│   │   ├── ProductCard/
│   │   ├── LoginForm/
│   │   ├── Sidebar/
│   │   ├── HeroSection/
│   │   └── index.ts
│   │
│   ├── templates/              # Layouts de página
│   │   ├── MainLayout/
│   │   ├── AuthLayout/
│   │   ├── DashboardLayout/
│   │   └── index.ts
│   │
│   ├── pages/                  # Instancias con datos reales
│   │   ├── HomePage/
│   │   ├── ProductPage/
│   │   ├── LoginPage/
│   │   ├── DashboardPage/
│   │   └── index.ts
│   │
│   ├── hooks/                  # Custom hooks (lógica reutilizable)
│   ├── utils/                  # Funciones utilitarias
│   ├── types/                  # Tipos TypeScript globales
│   ├── api/                    # Llamadas a API
│   └── styles/                 # Estilos globales (reset, fonts)
│
├── .storybook/                 # Configuración de Storybook
├── public/                     # Assets estáticos
└── ...config files
```

---

## Buenas prácticas adicionales

1. **Nomenclatura consistente:** Usa PascalCase para componentes, camelCase para archivos utilitarios.
2. **Barrel exports:** Cada carpeta debe tener un `index.ts` que exporte todo.
3. **Co-locación:** CSS/estilos deben vivir junto al componente (CSS Modules, Styled Components, etc.).
4. **Props drilling mínimo:** Usa contexto o state management solo en organismos/páginas.
5. **Atomic Design es flexible:** No seas dogmático. Si un componente no encaja perfectamente, elige el nivel más cercano.
6. **Mobile-first:** Los átomos deben ser responsivos por defecto.
7. **Accesibilidad:** Cada átomo debe cumplir con a11y (ARIA labels, focus states, etc.).

---

## Ejemplo de refactorización

### Antes (desorganizado):
```
src/
├── components/
│   ├── Button.tsx           # Usado en 15 lugares, 5 variantes diferentes
│   ├── Header.tsx           # Tiene lógica de búsqueda, auth, navegación
│   ├── LoginForm.tsx        # Mezcla UI con llamadas a API
│   ├── ProductCard.tsx      # Dependencia circular con ProductPage
│   └── ...
```

### Después (Atomic Design):
```
src/
├── tokens/
│   └── ...
├── atoms/
│   ├── Button/              # Variantes: primary, secondary, ghost, danger
│   ├── Input/
│   ├── Label/
│   └── Icon/
├── molecules/
│   ├── SearchField/         # Input + Icon + Button(ghost)
│   ├── FormField/           # Label + Input + mensaje error
│   └── CardHeader/          # Imagen + Título
├── organisms/
│   ├── Header/              # Logo(Átomo) + Nav(Moléculas) + Search(Molécula)
│   ├── LoginForm/           # FormFields(Moléculas) + Button(Átomo)
│   └── ProductCard/         # CardHeader(Molécula) + precio + botón
├── templates/
│   └── MainLayout/          # Header(Org) + Footer(Org) + slot
└── pages/
    ├── HomePage/            # MainLayout + ProductCards con datos reales
    └── LoginPage/           # AuthLayout + LoginForm + lógica API
```

---

## Prompts de activación sugeridos para el usuario

Cuando el usuario invoque esta skill, puede usar frases como:
- "Reorganiza mi proyecto con Atomic Design"
- "Aplica metodología Atomic Design a mi UI"
- "Quiero estructurar mi frontend con Atomic Design"
- "Necesito un Design System basado en Atomic Design"
- "Reestructura mis componentes con Atomic Design"

---

## Output esperado

Al aplicar esta skill, debes entregar:
1. **Análisis del estado actual** del proyecto.
2. **Mapa de clasificación** de componentes existentes.
3. **Estructura de carpetas propuesta** adaptada al stack tecnológico del usuario.
4. **Plan de migración paso a paso** (qué mover primero, qué después).
5. **Ejemplos de código** de componentes refactorizados (átomo, molécula, organismo).
6. **Recomendaciones de herramientas** (Storybook, CSS Modules, Tailwind, etc.).
"""
