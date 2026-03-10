---
name: snyk-security-audit
description: Auditoría de seguridad de dependencias con Snyk para proyectos Node.js y Python
---

# 🔒 Snyk Security Audit

## ¿Qué es Snyk?

Herramienta gratuita para detectar vulnerabilidades en dependencias de tu proyecto. Escanea `package.json` / `requirements.txt` y reporta CVEs conocidos con fixes sugeridos.

---

## Instalación y Setup

### 1. Autenticación (una vez)

```bash
npx snyk auth
```

Esto abre el navegador para vincular tu cuenta gratuita de Snyk.

### 2. Escanear vulnerabilidades

```bash
# Node.js
npx snyk test

# Python
npx snyk test --file=requirements.txt
```

### 3. Monitoreo continuo

```bash
npx snyk monitor
```

Snyk monitorizará tu proyecto y te avisará por email si aparecen nuevas vulnerabilidades.

---

## Integración CI/CD (GitHub Actions)

```yaml
# .github/workflows/security.yml
name: Security Audit

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
  schedule:
    - cron: '0 9 * * 1'  # Lunes a las 9:00

jobs:
  snyk:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
      - run: npm ci
      - uses: snyk/actions/node@master
        env:
          SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
        with:
          args: --severity-threshold=high
```

### Configurar el secret:
1. Ve a [app.snyk.io](https://app.snyk.io) → Settings → API Token
2. Copia el token
3. En GitHub → Settings → Secrets → `SNYK_TOKEN`

---

## Cuándo usar

| Momento | Comando | Frecuencia |
|---------|---------|------------|
| Antes de cada deploy | `npx snyk test` | Cada vez |
| Después de `npm install` | `npx snyk test` | Cada vez |
| Monitoreo en background | `npx snyk monitor` | Semanal |
| CI/CD automático | GitHub Action | Cada push/PR + semanal |

---

## Alternativas

| Herramienta | Ventaja | Desventaja |
|-------------|---------|------------|
| `npm audit` | Ya incluido en npm | Menos detallado |
| `npx snyk test` | Más completo, fix sugeridos | Requiere cuenta gratuita |
| Dependabot (GitHub) | Automático en GitHub | Solo PRs, no bloquea deploy |

**Recomendación:** Usar Snyk + Dependabot en paralelo para máxima cobertura.

---

## Coste

- **Free tier:** 200 tests/mes (más que suficiente para equipos pequeños)
- **Team:** $25/dev/mes (para empresas con CI/CD intensivo)

---

*Skill creado: 2026-02-20 — Proyecto: Multiatlas (preventivo)*
