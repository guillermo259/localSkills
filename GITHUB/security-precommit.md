---
inclusion: manual
version: "1.0.0"
---

# Security Pre-Commit Hook — Steering Guide

## Rol y contexto

Eres un **ingeniero de seguridad senior** especializado en análisis estático de código y hardening de pipelines CI/CD. Cuando el usuario te pida generar o mejorar un script de pre-commit de seguridad, sigue estrictamente las reglas de este documento.

---

## Objetivo del script

Generar un script Bash autocontenido (`security-check.sh`) que analice todo el proyecto antes del primer commit a GitHub y **bloquee el commit si detecta vulnerabilidades o problemas críticos**.

---

## Reglas de generación obligatorias

### 1. Estructura del script

El script debe tener estas secciones en orden:

```
1. Bloque de comentario con instrucciones de uso
2. Colores y constantes de UI (usando tput o códigos ANSI)
3. Arrays/variables configurables (patrones de secretos, archivos sensibles, reglas inseguras)
4. Funciones de utilidad (logging, detección de herramientas opcionales)
5. Funciones de check por categoría
6. Función de reporte final interactivo
7. Main: ejecuta todos los checks, acumula resultados, llama al reporte
```

### 2. Variables configurables al inicio (NUNCA hardcodeadas en la lógica)

```bash
# Patrones de secretos — array editable
SECRET_PATTERNS=(
  "sk_live_" "sk_test_" "pk_live_" "pk_test_"
  "AKIA[0-9A-Z]{16}" "ASIA[0-9A-Z]{16}"
  "-----BEGIN (RSA|EC|DSA|OPENSSH) PRIVATE KEY"
  "ghp_[a-zA-Z0-9]{36}" "ghs_[a-zA-Z0-9]{36}"
  "xox[baprs]-[0-9A-Za-z]"
  "AIza[0-9A-Za-z\\-_]{35}"
  "password\s*=\s*['\"][^'\"]{4,}"
  "api[_-]?key\s*=\s*['\"][^'\"]{8,}"
  "['\"]secret['\"]\\s*:\\s*['\"][^'\"]{8,}"
  "token\s*=\s*['\"][^'\"]{8,}"
  "[0-9a-f]{32,64}"  # hashes/tokens genéricos
)

# Archivos sensibles — array editable
SENSITIVE_FILES=(
  ".env" ".env.local" ".env.production" ".env.staging"
  "*.pem" "*.key" "*.p12" "*.pfx" "*.jks"
  "id_rsa" "id_ecdsa" "id_ed25519" "id_dsa"
  "*.sql" "*.dump" "*.bak"
  "config/secrets.yml" "config/database.yml"
  "terraform.tfvars" "*.tfstate"
  ".npmrc" ".pypirc" "*.kubeconfig"
)

# Reglas de configuración insegura — array editable
INSECURE_CONFIG_PATTERNS=(
  "DEBUG\s*=\s*True"
  "CORS.*\*"
  "AllowAllOrigins"
  "0\.0\.0\.0:[0-9]+"
  "ssl_verify\s*=\s*[Ff]alse"
  "verify=False"
  "NODE_ENV.*development"
  "APP_ENV.*dev"
)
```

### 3. Checks obligatorios

| Check | Herramienta primaria | Fallback |
|---|---|---|
| Secretos expuestos | `gitleaks` / `truffleHog` si disponibles | `grep -rE` con `SECRET_PATTERNS` |
| Archivos sensibles | find + lista `SENSITIVE_FILES` | — |
| Dependencias vulnerables | `npm audit` / `pip audit` / `bundler-audit` / `cargo audit` (autodetectado) | advertencia si no disponible |
| Configs inseguras | `grep -rE` con `INSECURE_CONFIG_PATTERNS` | — |
| `.gitignore` correcto | verificar que cada item de `SENSITIVE_FILES` aparezca en `.gitignore` | — |

### 4. Escaneo recursivo

- Desde `$PROJECT_ROOT` (por defecto `$(git rev-parse --show-toplevel)` o `$(pwd)`)
- Excluir siempre: `.git/`, `node_modules/`, `vendor/`, `.venv/`, `__pycache__/`, `dist/`, `build/`
- Para grep: usar `--include` y `--exclude-dir` apropiadamente

### 5. Output con colores

```bash
RED='\033[0;31m'      # crítico
YELLOW='\033[1;33m'   # advertencia
GREEN='\033[0;32m'    # limpio / ok
BLUE='\033[0;34m'     # informativo
BOLD='\033[1m'
RESET='\033[0m'
```

- Cada hallazgo muestra: `[CATEGORIA] archivo:línea → fragmento`
- Al inicio de cada sección: banner con nombre del check
- Al final: resumen por categoría con conteos

### 6. Reporte final interactivo (OBLIGATORIO si hay issues críticos)

```
╔══════════════════════════════════════════╗
║         SECURITY SCAN REPORT            ║
╚══════════════════════════════════════════╝
  Secretos expuestos:      X issues
  Archivos sensibles:      X issues
  Dependencias vulnerables: X issues
  Configs inseguras:       X issues
  .gitignore faltante:     X issues
  ─────────────────────────────────────
  TOTAL:                   X issues críticos

¿Cómo deseas proceder?
  [1] Abortar — no hacer commit (exit 1)
  [2] Continuar de todas formas (exit 0, con advertencia)
  [3] Ver reporte detallado completo
  [4] Salir sin hacer nada
```

- Opción 3 muestra el detalle completo y vuelve a preguntar
- Si no hay issues: sale con `exit 0` directo, sin preguntar
- Si `--ci` flag está presente: no preguntar, salir con `exit 1` automáticamente si hay issues

### 7. Flags de CLI obligatorios

```
--help        Muestra instrucciones de uso
--ci          Modo no-interactivo para pipelines CI/CD
--report-only No bloquea, solo muestra reporte (exit 0 siempre)
--fix-hints   Muestra sugerencias de corrección por cada issue
```

### 8. Detección de herramientas opcionales

```bash
check_optional_tools() {
  for tool in gitleaks truffleHog semgrep; do
    if command -v "$tool" &>/dev/null; then
      AVAILABLE_TOOLS+=("$tool")
      echo -e "${GREEN}[+] Herramienta opcional disponible: $tool${RESET}"
    fi
  done
}
```

Si `gitleaks` está disponible, usarlo como check primario de secretos y mostrar su output formateado. El grep manual actúa como fallback/complemento.

### 9. Requisitos de compatibilidad

- Shebang: `#!/usr/bin/env bash`
- Compatible con Bash 3.2+ (macOS default) y Bash 5.x (Linux)
- No usar `mapfile`/`readarray` sin verificar versión de Bash
- Usar `grep -E` (ERE) nunca `grep -P` (PCRE no disponible en macOS por defecto)
- Testear que `tput` esté disponible antes de usarlo para colores

---

## Instrucciones de uso (comentario al inicio del script)

```bash
# ============================================================
# security-check.sh — Pre-commit Security Scanner
# ============================================================
# USO:
#   chmod +x security-check.sh
#   ./security-check.sh            # Escaneo interactivo completo
#   ./security-check.sh --help     # Muestra esta ayuda
#   ./security-check.sh --ci       # Modo CI/CD no-interactivo
#   ./security-check.sh --report-only  # Solo reporte, sin bloquear
#   ./security-check.sh --fix-hints    # Incluye sugerencias de fix
#
# CONFIGURACIÓN:
#   Edita los arrays SECRET_PATTERNS, SENSITIVE_FILES e
#   INSECURE_CONFIG_PATTERNS al inicio del script para
#   adaptar los checks a tu proyecto.
#
# INTEGRACIÓN COMO PRE-COMMIT HOOK:
#   cp security-check.sh .git/hooks/pre-commit
#   chmod +x .git/hooks/pre-commit
# ============================================================
```

---

## Ejemplo de output esperado

```
══════════════════════════════════════
 🔍 CHECK 1/5: Secretos y credenciales
══════════════════════════════════════
[CRÍTICO] src/config.js:14 → apiKey = "sk_live_abc123..."
[CRÍTICO] .env:3 → AWS_SECRET=AKIAIOSFODNN7EXAMPLE

══════════════════════════════════════
 📁 CHECK 2/5: Archivos sensibles
══════════════════════════════════════
[CRÍTICO] .env → archivo sensible sin ignorar
[CRÍTICO] keys/server.pem → clave privada expuesta

══════════════════════════════════════
 📦 CHECK 3/5: Dependencias vulnerables
══════════════════════════════════════
[ADVERTENCIA] npm audit encontró 3 vulnerabilidades (1 crítica)

══════════════════════════════════════
 ⚙️  CHECK 4/5: Configuraciones inseguras
══════════════════════════════════════
[ADVERTENCIA] app/settings.py:8 → DEBUG = True

══════════════════════════════════════
 📋 CHECK 5/5: .gitignore
══════════════════════════════════════
[ADVERTENCIA] .env.production no está en .gitignore
[OK] .gitignore existe y cubre la mayoría de archivos sensibles
```

---

## Anti-patrones — NUNCA hacer esto

- ❌ Hardcodear patrones como strings en medio de funciones
- ❌ Usar `exit 1` sin mostrar qué causó el fallo
- ❌ Saltar el menú interactivo si hay issues críticos (salvo flag `--ci`)
- ❌ Requerir herramientas externas como dependencia obligatoria
- ❌ Usar `grep -P` (no compatible con macOS)
- ❌ Generar el script en múltiples archivos (debe ser autocontenido)
- ❌ Omitir el bloque de exclusión de directorios en escaneos recursivos
