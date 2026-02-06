---
name: Multiatlas SaaS Methodology
description: Metodología completa para desarrollo de aplicaciones SaaS production-ready siguiendo los principios de Multiatlas
---

# 🏭 Metodología Multiatlas para Desarrollo SaaS

## 🎯 Filosofía

### Principio Henry Ford
> *"Pueden tener el coche del color que quieran, siempre que sea negro."*

**Un solo stack perfeccionado (Golden Path).**
- NO dar opciones técnicas innecesarias al cliente
- Ejecutar el stack probado y optimizado
- Velocidad > Flexibilidad en decisiones técnicas

### Principio Elon Musk
> *"La máquina que construye la máquina es más importante que el producto."*

**El proceso > El producto.**
- Los comandos y sistemas que construyen el SaaS son más valiosos que el SaaS mismo
- Optimizar el proceso de desarrollo constantemente
- Eliminar fricción en cada iteración

> *"Si no estás fallando, no estás innovando lo suficiente."*

**Auto-Blindaje: Cada error refuerza el proceso.**
```
Error ocurre → Se arregla → Se DOCUMENTA → NUNCA ocurre de nuevo
```

---

## 🛠️ Golden Path (Stack Único)

| Capa | Tecnología | Por Qué |
|------|------------|---------|
| **Framework** | Next.js 16 + React 19 + TypeScript | Full-stack, Turbopack 70x más rápido |
| **Estilos** | Tailwind CSS 3.4 + shadcn/ui | Utility-first, componentes profesionales |
| **Backend** | Supabase (PostgreSQL + Auth + Storage) | Todo-en-uno, sin servidor propio |
| **Email** | Resend (prod) + SMTP (dev) | Deliverability garantizada |
| **Validación** | Zod | Type-safe runtime + compile-time |
| **Estado** | Zustand | Minimal, sin boilerplate |
| **Testing** | Playwright | E2E visual |
| **Deploy** | Railway (backend) + Vercel (frontend) | Auto-deploy, escalable |

**NO se dan opciones.** Este es el stack. Punto.

---

## 🏗️ Arquitectura Feature-First

> **¿Por qué?** Colocalización para IA. Todo el contexto de una feature en un solo lugar.

```
src/
├── app/                      # Next.js App Router
│   ├── (auth)/              # Rutas de autenticación
│   ├── (main)/              # Rutas principales
│   └── layout.tsx
│
├── features/                 # Organizadas por funcionalidad
│   ├── auth/
│   │   ├── components/      # LoginForm, SignupForm
│   │   ├── hooks/           # useAuth
│   │   ├── services/        # authService.ts
│   │   ├── types/           # User, Session
│   │   └── store/           # authStore.ts
│   │
│   └── [feature]/           # Misma estructura
│
└── shared/                   # Código reutilizable
    ├── components/          # Button, Card, etc.
    ├── hooks/               # useDebounce, etc.
    ├── lib/                 # supabase.ts, etc.
    └── types/               # Tipos compartidos
```

**Regla de oro:** Si necesitas saltar entre 3+ carpetas para entender una feature, la arquitectura está mal.

---

## 🔒 Git Shield (Seguridad Obligatoria)

### Checklist Pre-Commit (SIEMPRE)

```markdown
- [ ] `.env.local` está en `.gitignore`
- [ ] `.mcp.json` está en `.gitignore`
- [ ] `.env.example` existe (sin valores reales)
- [ ] No hay API keys en código
- [ ] No hay credenciales hardcodeadas
- [ ] RLS habilitado en tablas nuevas
```

### Convención de Nombres en Servicios Externos

**SIEMPRE usar nombres descriptivos en español:**
```
✅ Asiste Hogar - Producción
✅ Asiste Hogar - API Key Resend
✅ Asiste Hogar - Service Account Drive

❌ My App
❌ Test
❌ API Key 1
```

**Razón:** Facilita identificación cuando tienes múltiples clientes.

---

## 📏 Reglas de Código

### Límites Estrictos
- **Archivos:** Máximo 500 líneas
- **Funciones:** Máximo 50 líneas
- **Componentes:** Una responsabilidad clara

### Naming Conventions
```typescript
// Variables y funciones
const userName = 'Juan';
function calculateTotal() {}

// Componentes
function LoginForm() {}

// Constantes
const MAX_RETRIES = 3;

// Archivos y carpetas
login-form.tsx
user-service.ts
```

### TypeScript Estricto
```typescript
// ✅ SIEMPRE type hints
function calculateTotal(items: Item[], tax: number): number {
  return items.reduce((sum, item) => sum + item.price, 0) * (1 + tax);
}

// ❌ NUNCA usar 'any'
function process(data: any) {} // ❌

// ✅ Usar 'unknown' si es necesario
function process(data: unknown) {
  if (typeof data === 'string') {
    // ...
  }
}
```

### Patrón de Componente
```typescript
interface Props {
  children: React.ReactNode;
  variant?: 'primary' | 'secondary';
  onClick: () => void;
}

export function Button({ 
  children, 
  variant = 'primary', 
  onClick 
}: Props) {
  return (
    <button 
      onClick={onClick} 
      className={`btn btn-${variant}`}
    >
      {children}
    </button>
  );
}
```

---

## 🔄 Proceso de Desarrollo (Bucle Agéntico)

### 1. **Delimitar**
- Dividir en FASES (no subtareas)
- Cada fase debe ser completable en una sesión
- Máximo 5 fases por feature

### 2. **Mapear**
- Explorar contexto REAL antes de cada fase
- Leer archivos existentes
- Verificar estructura actual
- NO asumir nada

### 3. **Ejecutar**
- Usar MCPs cuando sea posible (Supabase, Next.js, Playwright)
- Crear subtareas según juicio
- Validar cada paso

### 4. **Auto-Blindaje**
- Documentar errores encontrados
- Actualizar PRP o documentación
- Añadir a checklist si aplica

### 5. **Transicionar**
- Verificar fase completada
- Actualizar contexto
- Pasar a siguiente fase

---

## 🧪 Testing (Patrón AAA)

```typescript
test('should calculate total with tax', () => {
  // Arrange
  const items = [{ price: 100 }, { price: 200 }];
  const taxRate = 0.1;

  // Act
  const result = calculateTotal(items, taxRate);

  // Assert
  expect(result).toBe(330);
});
```

---

## 📋 PRPs (Product Requirements Proposals)

Para features complejas, SIEMPRE generar un PRP:

```markdown
# PRP-XXX: [Nombre de la Feature]

## Contexto
[Por qué necesitamos esto]

## Objetivo
[Qué queremos lograr]

## Alcance
[Qué incluye y qué NO incluye]

## Especificaciones Técnicas
[Detalles de implementación]

## Fases de Implementación
1. Fase 1: [Descripción]
2. Fase 2: [Descripción]
...

## Criterios de Aceptación
- [ ] Criterio 1
- [ ] Criterio 2
...
```

---

## ❌ Anti-Patrones (NO HACER)

### Código
- ❌ Usar `any` en TypeScript
- ❌ Commits sin verificar build
- ❌ Omitir manejo de errores
- ❌ Hardcodear configuraciones
- ❌ Componentes de 500+ líneas

### Seguridad
- ❌ Exponer secrets en código
- ❌ Loggear información sensible
- ❌ Saltarse validación de entrada
- ❌ Tablas sin RLS en Supabase

### Arquitectura
- ❌ Dependencias circulares
- ❌ Mezclar responsabilidades
- ❌ Estado global innecesario
- ❌ Sobre-engineerear la primera versión

---

## 🚀 Comandos Estándar

```bash
# Development
npm run dev          # Servidor (auto-detecta puerto 3000-3006)
npm run build        # Build producción
npm run typecheck    # Verificar tipos
npm run lint         # ESLint

# Git
npm run commit       # Conventional Commits

# Testing
npm run test         # Tests unitarios
npm run test:e2e     # Tests E2E
```

---

## 📊 Auto-Blindaje Activo

### Formato de Aprendizaje

```markdown
### [YYYY-MM-DD]: [Título corto]
- **Error**: [Qué falló]
- **Fix**: [Cómo se arregló]
- **Aplicar en**: [Dónde más aplica]
- **Prevención**: [Cómo evitarlo en futuro]
```

### Dónde Documentar

| Tipo de Error | Dónde Documentar |
|---------------|------------------|
| Específico de feature | PRP de esa feature |
| Aplica a múltiples features | `.claude/prompts/*.md` |
| Crítico para TODO | `GEMINI.md` o `CLAUDE.md` |

---

## 🎯 Principios SOLID

- **S**ingle Responsibility: Un componente, una responsabilidad
- **O**pen/Closed: Abierto a extensión, cerrado a modificación
- **L**iskov Substitution: Subtipos deben ser intercambiables
- **I**nterface Segregation: Interfaces específicas, no genéricas
- **D**ependency Inversion: Depender de abstracciones, no de implementaciones

---

## 💡 Mejores Prácticas

### 1. **KISS** (Keep It Simple, Stupid)
Prefiere soluciones simples sobre complejas.

### 2. **YAGNI** (You Aren't Gonna Need It)
Implementa solo lo necesario ahora, no lo que "podrías necesitar".

### 3. **DRY** (Don't Repeat Yourself)
Evita duplicación de código.

### 4. **Fail Fast**
Detecta errores lo antes posible.

### 5. **Progressive Enhancement**
Funcionalidad básica primero, mejoras después.

---

*Esta metodología es un documento vivo. Se actualiza con cada proyecto.*
