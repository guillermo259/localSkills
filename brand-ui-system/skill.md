---
name: brand-ui-system
description: Sistema de diseño y librería de componentes multi-framework (React, Astro, Next.js). Usa este skill para generar, mantener y escalar componentes UI con armonía de marca, tokens de diseño consistentes y la misma línea visual en todos los proyectos. Inspirado en sistemas como Untitled UI pero adaptado a tu marca personal.
---

# Brand UI System

Sistema de componentes UI tokenizado para React, Astro y Next.js. Todos los componentes comparten la misma base visual; solo los tokens de color y tipografía cambian entre marcas.

## Filosofía

- **Una sola línea, mil marcas**: La estructura, espaciado, bordes, sombras y comportamiento son idénticos. Solo cambian los valores de los tokens de diseño.
- **Tokens primero**: Nunca hardcodees colores, tamaños de fuente, espaciado o radios en los componentes. Todo se resuelve vía CSS variables o props de tema.
- **Estilos intercambiables**: Sombras y bordes se definen como "familias" que puedes cambiar con una sola clase CSS.
- **Framework-agnostic patterns**: Los componentes usan la misma API mental sin importar si están en React, Astro o Next.js.

## Tokens de Diseño Obligatorios

Cada proyecto debe definir estos tokens en `:root` o en su config de tema. Los componentes del sistema siempre referencian estas variables.

### Colores
```css
:root {
  /* Brand */
  --color-brand-50: #...;
  --color-brand-100: #...;
  --color-brand-200: #...;
  --color-brand-300: #...;
  --color-brand-400: #...;
  --color-brand-500: #...;
  --color-brand-600: #...;
  --color-brand-700: #...;
  --color-brand-800: #...;
  --color-brand-900: #...;
  --color-brand-950: #...;

  /* Neutral (siempre escala de grises) */
  --color-gray-50: #...;
  --color-gray-100: #...;
  --color-gray-200: #...;
  --color-gray-300: #...;
  --color-gray-400: #...;
  --color-gray-500: #...;
  --color-gray-600: #...;
  --color-gray-700: #...;
  --color-gray-800: #...;
  --color-gray-900: #...;
  --color-gray-950: #...;

  /* Semánticos */
  --color-text-primary: var(--color-gray-900);
  --color-text-secondary: var(--color-gray-500);
  --color-text-tertiary: var(--color-gray-400);
  --color-text-inverse: #ffffff;
  --color-text-brand: var(--color-brand-600);

  --color-bg-primary: #ffffff;
  --color-bg-secondary: var(--color-gray-50);
  --color-bg-tertiary: var(--color-gray-100);
  --color-bg-inverse: var(--color-gray-900);

  --color-border-primary: var(--color-gray-200);
  --color-border-secondary: var(--color-gray-100);
  --color-border-brand: var(--color-brand-500);

  /* Estados */
  --color-error-50: #FEF2F2;
  --color-error-100: #FEE2E2;
  --color-error-200: #FECACA;
  --color-error-300: #FCA5A5;
  --color-error-400: #F87171;
  --color-error-500: #EF4444;
  --color-error-600: #DC2626;
  --color-error-700: #B91C1C;
  --color-error-800: #991B1B;
  --color-error-900: #7F1D1D;
  --color-error-950: #450A0A;

  --color-warning-50: #FFFBEB;
  --color-warning-100: #FEF3C7;
  --color-warning-200: #FDE68A;
  --color-warning-300: #FCD34D;
  --color-warning-400: #FBBF24;
  --color-warning-500: #F59E0B;
  --color-warning-600: #D97706;
  --color-warning-700: #B45309;
  --color-warning-800: #92400E;
  --color-warning-900: #78350F;
  --color-warning-950: #451A03;

  --color-success-50: #F0FDF4;
  --color-success-100: #DCFCE7;
  --color-success-200: #BBF7D0;
  --color-success-300: #86EFAC;
  --color-success-400: #4ADE80;
  --color-success-500: #22C55E;
  --color-success-600: #16A34A;
  --color-success-700: #15803D;
  --color-success-800: #166534;
  --color-success-900: #14532D;
  --color-success-950: #052E16;
}
```

### Tipografía
```css
:root {
  --font-family-sans: 'Inter', system-ui, sans-serif;
  --font-family-mono: 'JetBrains Mono', monospace;

  --font-size-xs: 0.75rem;   /* 12px */
  --font-size-sm: 0.875rem;  /* 14px */
  --font-size-md: 1rem;      /* 16px */
  --font-size-lg: 1.125rem;  /* 18px */
  --font-size-xl: 1.25rem;   /* 20px */
  --font-size-2xl: 1.5rem;   /* 24px */
  --font-size-3xl: 1.875rem; /* 30px */
  --font-size-4xl: 2.25rem;  /* 36px */

  --font-weight-regular: 400;
  --font-weight-medium: 500;
  --font-weight-semibold: 600;
  --font-weight-bold: 700;

  --line-height-tight: 1.25;
  --line-height-normal: 1.5;
  --line-height-relaxed: 1.75;

  --letter-spacing-tight: -0.025em;
  --letter-spacing-normal: 0;
  --letter-spacing-wide: 0.025em;
}
```

### Espaciado
```css
:root {
  --space-0: 0;
  --space-1: 0.25rem;  /* 4px */
  --space-2: 0.5rem;   /* 8px */
  --space-3: 0.75rem;  /* 12px */
  --space-4: 1rem;     /* 16px */
  --space-5: 1.25rem;  /* 20px */
  --space-6: 1.5rem;   /* 24px */
  --space-8: 2rem;     /* 32px */
  --space-10: 2.5rem;  /* 40px */
  --space-12: 3rem;    /* 48px */
  --space-16: 4rem;    /* 64px */
  --space-20: 5rem;    /* 80px */
  --space-24: 6rem;    /* 96px */
}
```

## 🎨 Familias de Estilo Intercambiables

Este es el sistema clave. En lugar de tener un solo set de sombras y bordes, defines **familias completas** que se activan con una clase en el `<html>` o en cualquier contenedor.

### Familias de Sombra

```css
/* === FAMILIA: SOFT (default, difusa y elegante) === */
:root,
.shadow-soft {
  --shadow-xs: 0 1px 2px 0 rgb(0 0 0 / 0.04);
  --shadow-sm: 0 1px 3px 0 rgb(0 0 0 / 0.06), 0 1px 2px -1px rgb(0 0 0 / 0.06);
  --shadow-md: 0 4px 6px -1px rgb(0 0 0 / 0.06), 0 2px 4px -2px rgb(0 0 0 / 0.06);
  --shadow-lg: 0 10px 15px -3px rgb(0 0 0 / 0.06), 0 4px 6px -4px rgb(0 0 0 / 0.06);
  --shadow-xl: 0 20px 25px -5px rgb(0 0 0 / 0.06), 0 8px 10px -6px rgb(0 0 0 / 0.06);
  --shadow-2xl: 0 25px 50px -12px rgb(0 0 0 / 0.12);
  --shadow-inner: inset 0 2px 4px 0 rgb(0 0 0 / 0.04);
}

/* === FAMILIA: SHARP (nítida, profesional, corporativa) === */
.shadow-sharp {
  --shadow-xs: 0 1px 1px 0 rgb(0 0 0 / 0.10);
  --shadow-sm: 0 2px 2px 0 rgb(0 0 0 / 0.10);
  --shadow-md: 0 4px 4px 0 rgb(0 0 0 / 0.10);
  --shadow-lg: 0 8px 8px 0 rgb(0 0 0 / 0.10);
  --shadow-xl: 0 16px 16px 0 rgb(0 0 0 / 0.10);
  --shadow-2xl: 0 32px 32px 0 rgb(0 0 0 / 0.15);
  --shadow-inner: inset 0 1px 2px 0 rgb(0 0 0 / 0.08);
}

/* === FAMILIA: GLOW (moderna, luminosa, SaaS) === */
.shadow-glow {
  --shadow-xs: 0 0 2px 0 rgb(var(--color-brand-rgb) / 0.15);
  --shadow-sm: 0 0 4px 0 rgb(var(--color-brand-rgb) / 0.15), 0 1px 2px -1px rgb(0 0 0 / 0.05);
  --shadow-md: 0 0 8px 0 rgb(var(--color-brand-rgb) / 0.15), 0 4px 6px -1px rgb(0 0 0 / 0.05);
  --shadow-lg: 0 0 16px 0 rgb(var(--color-brand-rgb) / 0.15), 0 10px 15px -3px rgb(0 0 0 / 0.05);
  --shadow-xl: 0 0 24px 0 rgb(var(--color-brand-rgb) / 0.20), 0 20px 25px -5px rgb(0 0 0 / 0.05);
  --shadow-2xl: 0 0 48px 0 rgb(var(--color-brand-rgb) / 0.25);
  --shadow-inner: inset 0 0 4px 0 rgb(var(--color-brand-rgb) / 0.10);
}

/* === FAMILIA: DEPTH (realista, 3D sutil) === */
.shadow-depth {
  --shadow-xs: 0 1px 1px 0 rgb(0 0 0 / 0.08), 0 1px 0 0 rgb(0 0 0 / 0.04);
  --shadow-sm: 0 2px 3px 0 rgb(0 0 0 / 0.08), 0 1px 0 0 rgb(0 0 0 / 0.04);
  --shadow-md: 0 4px 6px 0 rgb(0 0 0 / 0.08), 0 2px 0 0 rgb(0 0 0 / 0.04);
  --shadow-lg: 0 8px 12px 0 rgb(0 0 0 / 0.08), 0 4px 0 0 rgb(0 0 0 / 0.04);
  --shadow-xl: 0 16px 24px 0 rgb(0 0 0 / 0.08), 0 8px 0 0 rgb(0 0 0 / 0.04);
  --shadow-2xl: 0 24px 48px 0 rgb(0 0 0 / 0.12), 0 12px 0 0 rgb(0 0 0 / 0.04);
  --shadow-inner: inset 0 2px 4px 0 rgb(0 0 0 / 0.06);
}

/* === FAMILIA: GLASS (para fondos glassmorphism) === */
.shadow-glass {
  --shadow-xs: 0 1px 2px 0 rgb(0 0 0 / 0.03);
  --shadow-sm: 0 2px 4px 0 rgb(0 0 0 / 0.03);
  --shadow-md: 0 4px 8px 0 rgb(0 0 0 / 0.03);
  --shadow-lg: 0 8px 16px 0 rgb(0 0 0 / 0.03);
  --shadow-xl: 0 16px 32px 0 rgb(0 0 0 / 0.03);
  --shadow-2xl: 0 32px 64px 0 rgb(0 0 0 / 0.05);
  --shadow-inner: inset 0 1px 1px 0 rgb(255 255 255 / 0.10);
}
```

### Familias de Borde (Radio)

```css
/* === FAMILIA: ROUNDED (default, moderna, amigable) === */
:root,
.radius-rounded {
  --radius-none: 0;
  --radius-xs: 0.125rem;   /* 2px */
  --radius-sm: 0.25rem;    /* 4px */
  --radius-md: 0.375rem;   /* 6px */
  --radius-lg: 0.5rem;     /* 8px */
  --radius-xl: 0.75rem;    /* 12px */
  --radius-2xl: 1rem;      /* 16px */
  --radius-3xl: 1.5rem;    /* 24px */
  --radius-full: 9999px;
}

/* === FAMILIA: SHARP (corporativa, editorial, seria) === */
.radius-sharp {
  --radius-none: 0;
  --radius-xs: 0;
  --radius-sm: 0;
  --radius-md: 0;
  --radius-lg: 0;
  --radius-xl: 0;
  --radius-2xl: 0;
  --radius-3xl: 0;
  --radius-full: 9999px; /* Avatares y badges siguen redondos */
}

/* === FAMILIA: PILL (suave, orgánica, amigable) === */
.radius-pill {
  --radius-none: 0;
  --radius-xs: 0.25rem;
  --radius-sm: 0.5rem;
  --radius-md: 0.75rem;
  --radius-lg: 1rem;
  --radius-xl: 1.25rem;
  --radius-2xl: 1.5rem;
  --radius-3xl: 2rem;
  --radius-full: 9999px;
}

/* === FAMILIA: BRUTALIST (llamativa, contraste fuerte) === */
.radius-brutalist {
  --radius-none: 0;
  --radius-xs: 0;
  --radius-sm: 0;
  --radius-md: 0;
  --radius-lg: 0;
  --radius-xl: 0;
  --radius-2xl: 0;
  --radius-3xl: 0;
  --radius-full: 0; /* Todo cuadrado, incluso avatares */
}

/* === FAMILIA: BUBBLE (juguetona, redondeada extrema) === */
.radius-bubble {
  --radius-none: 0.5rem;
  --radius-xs: 0.5rem;
  --radius-sm: 0.75rem;
  --radius-md: 1rem;
  --radius-lg: 1.25rem;
  --radius-xl: 1.5rem;
  --radius-2xl: 2rem;
  --radius-3xl: 2.5rem;
  --radius-full: 9999px;
}
```

### Familias de Borde (Grosor y Estilo)

```css
/* === FAMILIA: SUBTLE (default, bordes finos) === */
:root,
.border-subtle {
  --border-width-thin: 1px;
  --border-width-medium: 1px;
  --border-width-thick: 2px;
  --border-style: solid;
  --border-color-default: var(--color-gray-200);
  --border-color-hover: var(--color-gray-300);
  --border-color-focus: var(--color-brand-500);
}

/* === FAMILIA: BOLD (bordes gruesos, estilo neobrutalismo suave) === */
.border-bold {
  --border-width-thin: 2px;
  --border-width-medium: 2px;
  --border-width-thick: 3px;
  --border-style: solid;
  --border-color-default: var(--color-gray-900);
  --border-color-hover: var(--color-gray-900);
  --border-color-focus: var(--color-brand-600);
}

/* === FAMILIA: HAIRLINE (minimalista, bordes casi invisibles) === */
.border-hairline {
  --border-width-thin: 0.5px;
  --border-width-medium: 0.5px;
  --border-width-thick: 1px;
  --border-style: solid;
  --border-color-default: var(--color-gray-100);
  --border-color-hover: var(--color-gray-200);
  --border-color-focus: var(--color-brand-400);
}
```

## Cómo usar las familias

### En HTML/CSS puro
```html
<!-- Activa todo el sitio con sombras nítidas y bordes cuadrados -->
<html class="shadow-sharp radius-sharp border-bold">
  <body>
    <!-- Un card con sombra y radio del sistema activo -->
    <div class="card" style="box-shadow: var(--shadow-md); border-radius: var(--radius-lg);">
      Contenido
    </div>

    <!-- Este card ignora la familia global y usa otra sombra -->
    <div class="card shadow-glow" style="box-shadow: var(--shadow-lg);">
      Contenido con glow
    </div>
  </body>
</html>
```

### En React / Next.js
```tsx
// Aplica la familia en el layout raíz
export default function RootLayout({ children }) {
  return (
    <html className="shadow-glow radius-pill border-subtle">
      <body>{children}</body>
    </html>
  );
}

// Los componentes usan las variables, nunca valores fijos
function Card({ children, shadow = 'md' }) {
  return (
    <div style={{ 
      boxShadow: `var(--shadow-${shadow})`,
      borderRadius: 'var(--radius-lg)',
      border: 'var(--border-width-thin) var(--border-style) var(--border-color-default)'
    }}>
      {children}
    </div>
  );
}
```

### En Astro
```astro
---
// layouts/Layout.astro
const { shadowFamily = 'soft', radiusFamily = 'rounded', borderFamily = 'subtle' } = Astro.props;
---
<html class={`shadow-${shadowFamily} radius-${radiusFamily} border-${borderFamily}`}>
  <slot />
</html>
```

## Combinaciones recomendadas

| Estilo | Sombra | Radio | Borde | Vibe |
|--------|--------|-------|-------|------|
| **Corporate** | `shadow-sharp` | `radius-sharp` | `border-subtle` | Serio, banca, enterprise |
| **SaaS Modern** | `shadow-soft` | `radius-rounded` | `border-subtle` | Limpio, profesional |
| **Startup Friendly** | `shadow-glow` | `radius-pill` | `border-subtle` | Cálido, acogedor |
| **Brutalist** | `shadow-sharp` | `radius-brutalist` | `border-bold` | Atrevido, memorable |
| **Minimal** | `shadow-glass` | `radius-rounded` | `border-hairline` | Elegante, editorial |
| **Playful** | `shadow-depth` | `radius-bubble` | `border-subtle` | Divertido, app |

## Estructura de Componentes

### Principios
1. **Single source of truth**: Cada componente existe en una carpeta con su implementación por framework.
2. **API consistente**: Mismos nombres de props, mismos comportamientos, mismos estados.
3. **Composición sobre configuración**: Prefiere slots/children sobre props booleanas masivas.
4. **Accesibilidad primero**: Todos los componentes deben ser usables con teclado y lectores de pantalla.

### Convención de nombres
- Componentes: PascalCase (`Button`, `TextInput`, `ModalDialog`)
- Props de tamaño: `size="sm" | "md" | "lg"`
- Props de variante: `variant="primary" | "secondary" | "tertiary" | "ghost"`
- Props de estado: `isDisabled`, `isLoading`, `isError`
- Props de layout: `width="full" | "auto"`, `align="start" | "center" | "end"`

## Componentes Base (siempre presentes)

### 1. Button
```
Props:
- variant: "primary" | "secondary" | "tertiary" | "ghost" | "danger"
- size: "sm" | "md" | "lg"
- isDisabled: boolean
- isLoading: boolean
- leftIcon: ReactNode / slot
- rightIcon: ReactNode / slot
- onClick: () => void
- type: "button" | "submit" | "reset"
- width: "auto" | "full"
```

### 2. TextInput
```
Props:
- label: string
- placeholder: string
- helperText: string
- errorText: string
- isDisabled: boolean
- isRequired: boolean
- size: "sm" | "md" | "lg"
- state: "default" | "error" | "success"
- leftIcon: ReactNode / slot
- rightIcon: ReactNode / slot
- type: "text" | "email" | "password" | "number" | "url" | "tel"
```

### 3. Card
```
Props:
- padding: "none" | "sm" | "md" | "lg" | "xl"
- shadow: "none" | "xs" | "sm" | "md" | "lg" | "xl" | "2xl"
- border: boolean
- hover: boolean
- width: "auto" | "full"
```

### 4. Badge
```
Props:
- variant: "primary" | "secondary" | "outline" | "ghost"
- size: "sm" | "md" | "lg"
- color: "brand" | "gray" | "error" | "warning" | "success"
```

### 5. Avatar
```
Props:
- src: string
- alt: string
- size: "xs" | "sm" | "md" | "lg" | "xl" | "2xl"
- fallback: string (iniciales)
- shape: "circle" | "square"
- status: "online" | "offline" | "away" | "busy" | none
```

### 6. Modal / Dialog
```
Props:
- isOpen: boolean
- onClose: () => void
- title: string
- description: string
- size: "sm" | "md" | "lg" | "xl" | "full"
- closeOnOverlayClick: boolean
- closeOnEsc: boolean
- footer: ReactNode / slot
```

### 7. Dropdown / Select
```
Props:
- options: Array<{ label, value, icon?, disabled? }>
- placeholder: string
- isSearchable: boolean
- isMulti: boolean
- isDisabled: boolean
- size: "sm" | "md" | "lg"
```

### 8. Tabs
```
Props:
- tabs: Array<{ id, label, icon?, badge?, disabled? }>
- activeTab: string
- onChange: (id) => void
- variant: "line" | "enclosed" | "soft" | "pills"
- size: "sm" | "md" | "lg"
- orientation: "horizontal" | "vertical"
```

### 9. Toast / Notification
```
Props:
- title: string
- description: string
- variant: "info" | "success" | "warning" | "error"
- duration: number (ms)
- isClosable: boolean
- position: "top-right" | "top-left" | "bottom-right" | "bottom-left" | "top-center" | "bottom-center"
```

### 10. Tooltip
```
Props:
- content: string | ReactNode
- placement: "top" | "bottom" | "left" | "right"
- delay: number (ms)
- trigger: "hover" | "focus" | "click"
```

## Implementación por Framework

### React (con Tailwind CSS)
```tsx
// components/Button/Button.tsx
import { forwardRef } from 'react';
import { cn } from '@/lib/utils';

export interface ButtonProps extends React.ButtonHTMLAttributes<HTMLButtonElement> {
  variant?: 'primary' | 'secondary' | 'tertiary' | 'ghost' | 'danger';
  size?: 'sm' | 'md' | 'lg';
  isLoading?: boolean;
  leftIcon?: React.ReactNode;
  rightIcon?: React.ReactNode;
  width?: 'auto' | 'full';
}

const variantStyles = {
  primary: 'bg-[var(--color-brand-600)] text-white hover:bg-[var(--color-brand-700)] active:bg-[var(--color-brand-800)]',
  secondary: 'bg-[var(--color-gray-100)] text-[var(--color-text-primary)] hover:bg-[var(--color-gray-200)] border-[length:var(--border-width-thin)] [border-style:var(--border-style)] border-[var(--border-color-default)]',
  tertiary: 'bg-transparent text-[var(--color-brand-600)] hover:bg-[var(--color-brand-50)]',
  ghost: 'bg-transparent text-[var(--color-text-secondary)] hover:bg-[var(--color-gray-100)] hover:text-[var(--color-text-primary)]',
  danger: 'bg-[var(--color-error-500)] text-white hover:opacity-90',
};

const sizeStyles = {
  sm: 'h-8 px-3 text-sm',
  md: 'h-10 px-4 text-sm',
  lg: 'h-12 px-5 text-base',
};

export const Button = forwardRef<HTMLButtonElement, ButtonProps>(
  ({ variant = 'primary', size = 'md', isLoading, leftIcon, rightIcon, width = 'auto', className, children, disabled, ...props }, ref) => {
    return (
      <button
        ref={ref}
        disabled={disabled || isLoading}
        className={cn(
          'inline-flex items-center justify-center gap-2 rounded-[var(--radius-md)] font-medium transition-colors focus:outline-none focus:ring-2 focus:ring-[var(--color-brand-500)] focus:ring-offset-2 disabled:opacity-50 disabled:cursor-not-allowed',
          variantStyles[variant],
          sizeStyles[size],
          width === 'full' && 'w-full',
          className
        )}
        {...props}
      >
        {isLoading && <LoadingSpinner size={size} />}
        {!isLoading && leftIcon}
        {children}
        {!isLoading && rightIcon}
      </button>
    );
  }
);
Button.displayName = 'Button';
```

### Astro (con Tailwind CSS)
```astro
---
// components/Button/Button.astro
export interface Props {
  variant?: 'primary' | 'secondary' | 'tertiary' | 'ghost' | 'danger';
  size?: 'sm' | 'md' | 'lg';
  isLoading?: boolean;
  width?: 'auto' | 'full';
  type?: 'button' | 'submit' | 'reset';
  disabled?: boolean;
  class?: string;
}

const { 
  variant = 'primary', 
  size = 'md', 
  isLoading = false, 
  width = 'auto',
  type = 'button',
  disabled = false,
  class: className = ''
} = Astro.props;

const variantClasses = {
  primary: 'bg-[var(--color-brand-600)] text-white hover:bg-[var(--color-brand-700)]',
  secondary: 'bg-[var(--color-gray-100)] text-[var(--color-text-primary)] hover:bg-[var(--color-gray-200)] border-[length:var(--border-width-thin)] [border-style:var(--border-style)] border-[var(--border-color-default)]',
  tertiary: 'bg-transparent text-[var(--color-brand-600)] hover:bg-[var(--color-brand-50)]',
  ghost: 'bg-transparent text-[var(--color-text-secondary)] hover:bg-[var(--color-gray-100)]',
  danger: 'bg-[var(--color-error-500)] text-white hover:opacity-90',
};

const sizeClasses = {
  sm: 'h-8 px-3 text-sm',
  md: 'h-10 px-4 text-sm',
  lg: 'h-12 px-5 text-base',
};
---

<button
  type={type}
  disabled={disabled || isLoading}
  class:list={[
    'inline-flex items-center justify-center gap-2 rounded-[var(--radius-md)] font-medium transition-colors focus:outline-none focus:ring-2 focus:ring-[var(--color-brand-500)] disabled:opacity-50 disabled:cursor-not-allowed',
    variantClasses[variant],
    sizeClasses[size],
    width === 'full' && 'w-full',
    className
  ]}
>
  {isLoading && <span class="animate-spin">↻</span>}
  <slot />
</button>
```

### Next.js (App Router compatible)
Usa la misma estructura que React pero con:
- `'use client'` cuando sea necesario (interactividad)
- Server Components para componentes puramente presentacionales
- CSS Modules o Tailwind para estilos

## Dark Mode

Todos los componentes deben soportar dark mode vía `data-theme="dark"` o clase `.dark`:

```css
.dark {
  --color-text-primary: var(--color-gray-50);
  --color-text-secondary: var(--color-gray-400);
  --color-bg-primary: var(--color-gray-950);
  --color-bg-secondary: var(--color-gray-900);
  --color-bg-tertiary: var(--color-gray-800);
  --color-border-primary: var(--color-gray-800);
  --color-border-secondary: var(--color-gray-900);
}
```

## Checklist para nuevos componentes

Antes de considerar un componente "listo":
- [ ] Implementado en React
- [ ] Implementado en Astro (si aplica)
- [ ] Todos los tokens usan CSS variables, nunca valores hardcodeados
- [ ] Soporta dark mode
- [ ] Estados: default, hover, active, focus, disabled, loading
- [ ] Accesible: roles, aria-labels, keyboard navigation
- [ ] Documentado: props, ejemplos, casos de uso
- [ ] Responsive: funciona en mobile, tablet, desktop

## Adaptación a nueva marca

Para crear una nueva instancia del sistema con otra marca:

1. Copia la estructura de tokens
2. Cambia solo estos valores:
   - `--color-brand-*`: tu paleta de marca
   - `--font-family-sans`: tu tipografía
   - `--radius-*`: tu estilo de bordes (más cuadrado o más redondeado)
3. Todo lo demás (grises, espaciado, sombras) puede mantenerse igual para consistencia
4. Los componentes no necesitan cambios

## Comandos sugeridos (package.json)

```json
{
  "scripts": {
    "dev": "storybook dev -p 6006",
    "build": "storybook build",
    "lint": "eslint components --ext .ts,.tsx,.astro",
    "typecheck": "tsc --noEmit",
    "test": "vitest run",
    "test:ui": "vitest --ui"
  }
}
```
