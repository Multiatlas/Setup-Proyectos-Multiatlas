# 🏭 Guía Maestra: Blueprint para Nuevos Proyectos SaaS

**Versión:** 2.0.0  
**Actualizado:** 2026-02-20  
**Basado en:** Aprendizajes reales de Asiste Hogar + ROI Master Calculator IA

---

## 🎯 Propósito

Este documento es el **blueprint definitivo** para levantar un proyecto SaaS desde cero. Contiene el stack validado en producción, los patrones que funcionan, y los errores que ya resolvimos para que NUNCA se repitan.

---

## ⚡ Golden Path (Stack Validado en Producción)

| Capa | Tecnología | Por Qué |
|------|------------|---------|
| Framework | Next.js 15+ (App Router) + React 19 + TypeScript | Full-stack en un solo lugar |
| Estilos | Tailwind CSS 3.4 + shadcn/ui | Utility-first, componentes listos |
| Backend | Supabase (Auth + PostgreSQL + RLS + Storage) | Sin servidor propio |
| Validación | Zod | Type-safe en runtime y compile-time |
| Estado | Zustand | Minimal, sin boilerplate |
| Email | Resend (o API REST del proveedor) | Ver auto-blindaje: Railway bloquea SMTP |
| Deploy | Railway | Precio competitivo, fácil configuración |
| AI (futuro) | Vercel AI SDK v5 + OpenRouter | Multi-modelo |

---

## 📋 Checklist de Setup (15 pasos)

### Fase 1: Infraestructura (30 min)
- [ ] Crear proyecto Next.js: `npx create-next-app@latest ./ --ts --app --tailwind`
- [ ] Instalar dependencias: `npm i @supabase/supabase-js @supabase/ssr zod zustand`
- [ ] Crear proyecto Supabase (región `eu-west-1` para España)
- [ ] Configurar `.env.local` con keys de Supabase
- [ ] Verificar `.env.local` en `.gitignore`

### Fase 2: Auth (1h)
- [ ] Implementar Supabase Auth (email/password)
- [ ] Crear tabla `profiles` con trigger `on_auth_user_created`
- [ ] Definir roles: `worker`, `client`, `admin`, `super_admin`
- [ ] Habilitar RLS en `profiles` con políticas por rol
- [ ] Crear middleware de protección de rutas

### Fase 3: Base de Datos (1h)
- [ ] Crear tablas con migraciones (`supabase db push` o MCP)
- [ ] ⚠️ **Siempre** habilitar RLS: `ALTER TABLE {tabla} ENABLE ROW LEVEL SECURITY;`
- [ ] ⚠️ **Siempre** crear políticas para SELECT, INSERT, UPDATE, DELETE
- [ ] Crear índices en todas las foreign keys
- [ ] Crear triggers `updated_at` donde sea necesario

### Fase 4: Deploy (30 min)
- [ ] Crear proyecto en Railway con nombre en español
- [ ] Configurar variables de entorno
- [ ] Verificar que el build pasa: `npm run build`
- [ ] Configurar dominio custom (si aplica)
- [ ] ⚠️ DNS tarda hasta 48h en propagar

---

## 🏗️ Arquitectura Feature-First

```
src/
├── app/                      # Next.js App Router
│   ├── (auth)/              # Login, signup, verificación
│   ├── (main)/              # Rutas principales
│   ├── admin/               # Panel admin
│   └── api/                 # API routes (server-side)
│
├── features/                 # Organizadas por funcionalidad
│   ├── auth/
│   │   ├── components/      # LoginForm, SignupForm
│   │   ├── hooks/           # useAuth
│   │   ├── services/        # authService.ts
│   │   └── types/           # User, Session
│   └── [feature]/           # Misma estructura
│
└── shared/                   # Código compartido
    ├── components/          # Button, Card, Modal
    ├── hooks/               # useDebounce, useMediaQuery
    ├── lib/                 # supabase.ts, api-response.ts
    ├── services/            # emailService.ts
    ├── templates/           # Templates HTML email/contratos
    └── types/               # Tipos compartidos
```

---

## 🔐 Seguridad Obligatoria

### Antes de cada deploy:
- [ ] RLS habilitado en **TODAS** las tablas (usar `get_advisors` de Supabase MCP)
- [ ] Passwords hasheados con `bcrypt` (nunca texto plano)
- [ ] `service_role` key solo en API routes del servidor, NUNCA en frontend
- [ ] `.env.local` en `.gitignore`
- [ ] Validación Zod en cliente Y servidor
- [ ] `npm audit` o `npx snyk test` para vulnerabilidades

### Auditoría de dependencias (Snyk):
```bash
npx snyk auth          # Una vez
npx snyk test          # Antes de cada deploy
npx snyk monitor       # Monitoreo continuo
```

---

## 📧 Patrones de Email

### En Railway/Vercel/Netlify (SMTP bloqueado):
- ✅ Usar **API REST HTTP** (Resend, Mailrelay API, SendGrid API)
- ❌ NO usar SMTP directo (puertos 25/465/587 bloqueados)

### Envío masivo:
- Añadir delay de **500ms** entre envíos para evitar rate limiting
- Implementar filtros (zona, servicio, aptitudes) antes de enviar

---

## 📄 Generación de Documentos (Contratos, Facturas)

### Patrón validado:
1. **Template HTML** con placeholders (`{{nombre}}`, `{{fecha}}`)
2. **Auto-relleno** desde datos de la BD (client + worker)
3. **Preview** en `<iframe>` para revisión en tiempo real
4. **Exportar** con `window.print()` (genera PDF nativo del navegador)

---

## 👥 Patrón de Roles (Multi-Admin)

```sql
-- 4 roles validados en producción
ALTER TABLE profiles ADD CONSTRAINT profiles_role_check
  CHECK (role IN ('worker', 'client', 'admin', 'super_admin'));

-- Para añadir un nuevo rol: DROP + re-ADD (nunca ALTER ADD)
ALTER TABLE profiles DROP CONSTRAINT profiles_role_check;
ALTER TABLE profiles ADD CONSTRAINT profiles_role_check
  CHECK (role IN ('worker', 'client', 'admin', 'super_admin', 'nuevo_rol'));
```

### Jerarquía:
- `super_admin` → Gestiona admins, acceso total
- `admin` → Gestiona usuarios y contenido
- `client` → Crea ofertas, revisa candidatos
- `worker` → Perfil, disponibilidad, muestra interés

---

## 📝 Reglas de Código

| Regla | Límite |
|-------|--------|
| Archivos | Máx 500 líneas |
| Funciones | Máx 50 líneas |
| Componentes | 1 responsabilidad, máx 300 líneas |
| TypeScript | Nunca `any`, usar `unknown` |
| Naming | Variables: camelCase, Componentes: PascalCase, Archivos: kebab-case |

---

## 🔗 Referencias

- **Auto-Blindaje:** `docs/auto-blindaje.md` (14 aprendizajes acumulados)
- **Skills:** `skills/` (patrones reutilizables)
- **SaaS Factory V3:** Referencia de la community

---

*Este blueprint se actualiza con cada proyecto. Úsalo como punto de partida, no como dogma.*
