# 🛡️ Auto-Blindaje - Aprendizajes Continuos

## 🎯 Filosofía
> "Cada error es un impacto que refuerza nuestra estructura. 
> Blindamos el proceso para que la falla nunca se repita."

---

## 📚 Aprendizajes por Categoría

### Infraestructura

#### 2026-02-06: Railway bloquea puertos SMTP
- **Error:** Intentar usar SMTP directo en Railway
- **Síntoma:** Connection timeout en puertos 25, 465, 587
- **Fix:** Usar Resend (API HTTP) en vez de SMTP
- **Aplicar en:** Todos los proyectos en Railway, Heroku, Vercel, Netlify
- **Documentación:** `reporte_smtp_tests.md` (Asiste Hogar)
- **Proyecto:** Asiste Hogar

#### 2026-02-10: NO necesitas Resend — Usa la API REST de tu proveedor de email
- **Error:** Pensar que necesitas contratar Resend/SendGrid para enviar emails desde Railway
- **Síntoma:** Dependencia innecesaria de un servicio externo adicional (coste extra)
- **Fix:** Usar la API REST del proveedor que YA tienes (ej: Mailrelay `/api/v1/send_emails` vía HTTPS/443). Railway permite HTTPS perfectamente, solo bloquea puertos SMTP (25/465/587)
- **Aplicar en:** Todos los proyectos que ya usen Mailrelay, SendGrid, Mailgun u otro con API REST
- **Documentación:** `server.js` en ROI-MASTER-CALCULATOR-IA (función `sendROIEmail`)
- **Proyecto:** ROI Master Calculator IA
- **⚠️ Clave:** Estrategia doble → API REST (primario) + SMTP (fallback local)

---

### Mailrelay API

#### 2026-02-10: Filtro de búsqueda de suscriptores — usar q[email]
- **Error:** Buscar suscriptores con `?email=xxx` devuelve lista paginada genérica sin filtrar
- **Síntoma:** `ERROR CRITICO: Mailrelay dice que existe, pero no lo encontramos`
- **Fix:** Usar `?q%5Bemail%5D=xxx` (que es `q[email]=xxx` URL-encoded) para filtrar en servidor
- **Aplicar en:** Todos los proyectos con integración Mailrelay API v1
- **Documentación:** `server.js` función `addToMailrelay` en ROI-MASTER-CALCULATOR-IA  
- **Proyecto:** ROI Master Calculator IA

#### 2026-02-10: Campo correcto para grupos es group_ids (no groups)
- **Error:** Usar `groups: [9]` al crear/actualizar suscriptor
- **Síntoma:** Suscriptor se crea pero sin grupo asignado (silently ignored)
- **Fix:** Usar `group_ids: [9]` — la API acepta solo `group_ids` para asignar grupos
- **Aplicar en:** Todos los proyectos con Mailrelay
- **Documentación:** `server.js` función `addToMailrelay`
- **Proyecto:** ROI Master Calculator IA

---

### Naming y Organización

#### 2026-02-06: Nombres en inglés dificultan colaboración
- **Error:** Servicios con nombres técnicos en inglés
- **Síntoma:** Equipo sin inglés no entiende qué es cada cosa
- **Fix:** Skill `spanish-naming-convention`
- **Aplicar en:** Todos los proyectos
- **Documentación:** `skills/spanish-naming-convention/SKILL.md`
- **Proyecto:** Asiste Hogar

---

### DNS y Dominios

#### 2026-02-06: Propagación DNS tarda hasta 48h
- **Error:** Esperar que DNS funcione inmediatamente
- **Síntoma:** Domain not found después de configurar
- **Fix:** Usar herramientas de verificación (nslookup, whatsmydns.net)
- **Aplicar en:** Todos los proyectos con dominios custom
- **Documentación:** N/A
- **Proyecto:** Asiste Hogar

---

### Supabase / PostgreSQL

#### 2026-02-20: CHECK constraints — NO usar ALTER TABLE ADD, usar DROP + re-ADD
- **Error:** Intentar `ALTER TABLE profiles ADD CONSTRAINT` para añadir un nuevo valor al CHECK de roles
- **Síntoma:** Error SQL: constraint already exists
- **Fix:** Primero `ALTER TABLE profiles DROP CONSTRAINT profiles_role_check;` y luego `ALTER TABLE profiles ADD CONSTRAINT profiles_role_check CHECK (role IN ('worker', 'client', 'admin', 'super_admin'));`
- **Aplicar en:** Todos los proyectos con CHECK constraints en Supabase
- **Proyecto:** Asiste Hogar

#### 2026-02-20: service_role key obligatorio para operaciones admin (createUser)
- **Error:** Usar `anon` key para crear usuarios desde panel admin
- **Síntoma:** RLS bloquea la operación, error 403
- **Fix:** Crear cliente Supabase con `SUPABASE_SERVICE_ROLE_KEY` para operaciones admin (bypasa RLS)
- **Aplicar en:** Todos los proyectos con panel admin que cree/gestione usuarios
- **⚠️ Clave:** NUNCA exponer `service_role` en el frontend. Solo en API routes del servidor
- **Proyecto:** Asiste Hogar

---

### Seguridad

#### 2026-02-17: bcrypt obligatorio para hashing de passwords admin
- **Error:** Guardar passwords de admin en texto plano o con hash débil
- **Síntoma:** Vulnerabilidad crítica si la BD se compromete
- **Fix:** Usar `bcrypt.hash(password, 10)` para hashear y `bcrypt.compare()` para verificar
- **Aplicar en:** Todos los proyectos con autenticación custom (no Supabase Auth)
- **Proyecto:** Asiste Hogar

#### 2026-02-20: Integrar Snyk para auditoría de dependencias
- **Error:** No detectar vulnerabilidades en `node_modules` hasta producción
- **Síntoma:** Dependencias con CVEs conocidos pasan al deploy
- **Fix:** Integrar Snyk: `npx snyk auth` → `npx snyk test` → `npx snyk monitor`
- **Aplicar en:** Todos los proyectos Node.js / Python
- **Documentación:** `skills/snyk-security-audit/SKILL.md`
- **Proyecto:** Todos (mejora preventiva)

#### 2026-02-25: NUNCA hardcodear secrets en scripts de utilidades
- **Error:** 20+ scripts con DB passwords, access tokens y service role keys como strings literales
- **Síntoma:** Snyk detectó exposición de credenciales en historial de git
- **Fix:** Todos los scripts deben usar `dotenv.config({ path: '.env.local' })` + `process.env.VARIABLE`. Eliminar scripts obsoletos que ya no se usan
- **Aplicar en:** Cualquier script de utilidad (`scripts/*.mjs`, `scripts/*.js`)
- **Documentación:** `saas-factory/.claude/prompts/security-checklist.md` v2.0
- **Proyecto:** Asiste Hogar
- **⚠️ Clave:** Borrar el archivo de git NO borra el historial. El secreto sigue expuesto en `git log`

#### 2026-02-25: Supabase views exponen datos sensibles sin RLS
- **Error:** Views como `auth.users` y `pg_stat_statements` son accesibles vía API pública sin protección
- **Síntoma:** Supabase Security Advisor reporta "Unrevoked permissions for auth.users" y "Unrevoked permissions for pg_stat_statements"
- **Fix:** Ejecutar migración: `REVOKE ALL ON auth.users FROM anon, authenticated;` + `REVOKE USAGE ON SCHEMA auth FROM anon, authenticated;`
- **Aplicar en:** Toda migración que cree views, y como migración base en nuevos proyectos
- **Documentación:** `supabase/migrations/20260225_security_hardening.sql`
- **Proyecto:** Asiste Hogar

#### 2026-02-25: Rotar credenciales expuestas INMEDIATAMENTE — borrar NO es suficiente
- **Error:** Secretos expuestos en historial de git siguen siendo válidos incluso tras borrar el archivo
- **Síntoma:** Access tokens y DB passwords comprometidos pueden usarse para acceder a datos aunque el archivo ya no exista
- **Fix:** 1) Revocar la credencial antigua en el dashboard, 2) Generar nueva, 3) Actualizar `.env.local`, 4) Habilitar Leaked Password Protection en Supabase
- **Aplicar en:** Cualquier secreto que aparezca en `git log` o sea detectado por Snyk
- **Proyecto:** Asiste Hogar
- **⚠️ Clave:** Protocolo: Revocar → Rotar → Actualizar → Documentar

#### 2026-02-25: Auditoría periódica con múltiples herramientas
- **Error:** Vulnerabilidades en dependencias (jspdf 4.1.0) no detectadas hasta scan externo
- **Síntoma:** 3 CVEs High severity pasaron desapercibidos hasta correo de Snyk
- **Fix:** Ejecutar periódicamente: `npm audit` + Supabase `get_advisors(security)` + Snyk + `git grep` para buscar secrets hardcodeados
- **Aplicar en:** Todos los proyectos, especialmente tras `npm install` y migraciones
- **Proyecto:** Asiste Hogar

#### 2026-03-13: ⚠️ CRÍTICO — Stripe en modo TEST en producción tras pruebas E2E
- **Error:** Cambiar `stripe_mode` a "test" en la DB para pruebas E2E y NO restaurar a "live"
- **Síntoma:** Clientes reales no pueden pagar — tarjetas rechazadas por Stripe TEST
- **Fix:** 1) Cambiar `stripe_mode` a "live" en Integration table 2) Cambiar default del código de "test" a "live" 3) VERIFICAR con `GET /api/payments/public-key` que devuelve `pk_live_` y `mode: "live"`
- **Aplicar en:** Todos los proyectos con Stripe y flujo test/live
- **Documentación:** `.agent/skills/generation-web-learning/SKILL.md`
- **Proyecto:** VibeMultiatlas (GENERATION-WEB-guillermo)
- **⚠️ Clave:** PROTOCOLO POST-E2E: siempre ejecutar checklist: ✅ stripe_mode=live ✅ pk_live_ en public-key ✅ sk_live_ en create-intent

#### 2026-03-13: Nunca tener dos fuentes de verdad para templates de email
- **Error:** `sendCustomerEmail` leía templates HTML de la Integration table (DB) antes de usar los hardcodeados
- **Síntoma:** Emails con tema dark mode roto en Outlook porque la DB tenía templates viejos
- **Fix:** Eliminar lectura de templates de la DB. SIEMPRE usar `DEFAULT_TEMPLATES` en código. Una sola fuente de verdad
- **Aplicar en:** Cualquier sistema de email con templates configurables
- **Proyecto:** VibeMultiatlas (GENERATION-WEB-guillermo)

#### 2026-03-13: charset UTF-8 obligatorio en headers de email para idiomas con acentos
- **Error:** No incluir `charset=UTF-8` en headers de emails enviados via Resend/nodemailer
- **Síntoma:** Acentos españoles (é,á,ñ) aparecen como □ en Outlook
- **Fix:** Resend: `headers: { "Content-Type": "text/html; charset=UTF-8" }` / Nodemailer: `encoding: "utf-8"`
- **Aplicar en:** Todos los proyectos que envíen emails en español u otros idiomas con caracteres especiales
- **Proyecto:** VibeMultiatlas (GENERATION-WEB-guillermo)

---

### Desarrollo / DevX

#### 2026-02-09: Siempre `npm run dev`, nunca `next dev` directo
- **Error:** Ejecutar `next dev` directamente con puerto hardcodeado
- **Síntoma:** Conflictos de puerto si otro proceso ya usa 3000
- **Fix:** Configurar script en `package.json` con auto-detección de puerto libre (3000-3006)
- **Aplicar en:** Todos los proyectos Next.js
- **Proyecto:** Asiste Hogar

#### 2026-02-20: Bulk email — rate limiting 500ms entre envíos
- **Error:** Enviar emails masivos sin delay causa rate limiting del proveedor
- **Síntoma:** Resend devuelve 429 Too Many Requests después de ~10 emails rápidos
- **Fix:** Añadir `await new Promise(r => setTimeout(r, 500))` entre cada envío
- **Aplicar en:** Todos los proyectos con envío masivo de emails
- **Proyecto:** Asiste Hogar

---

### Contratos y Documentos

#### 2026-02-20: HTML templates + iframe para preview de contratos en tiempo real
- **Error:** Generar PDFs directamente sin previsualización
- **Síntoma:** Errores de formato solo detectados al descargar el PDF
- **Fix:** Generar HTML con template + placeholders, renderizar en `<iframe>` para preview, y usar `window.print()` para imprimir/descargar como PDF
- **Aplicar en:** Todos los proyectos con generación de documentos (contratos, facturas, presupuestos)
- **Proyecto:** Asiste Hogar

---

### Auth y Roles

#### 2026-02-20: Patrón super_admin para gestión de equipo
- **Error:** Admin único sin delegación ni control de acceso granular
- **Síntoma:** Un solo admin gestiona todo, sin audit trail ni control de permisos
- **Fix:** Implementar `super_admin` con CHECK constraint en `profiles.role`. Solo super_admin puede crear/eliminar otros admins. API protegida con verificación de rol
- **Aplicar en:** Todos los proyectos SaaS con múltiples administradores
- **Proyecto:** Asiste Hogar

---

## 🔄 Proceso de Documentación

Cuando encuentres un error:

1. **Arreglarlo** inmediatamente
2. **Documentarlo** aquí con formato:
   ```markdown
   #### YYYY-MM-DD: [Título corto]
   - **Error:** [Qué falló]
   - **Síntoma:** [Cómo se manifestó]
   - **Fix:** [Cómo se arregló]
   - **Aplicar en:** [Dónde más aplica]
   - **Documentación:** [Archivo de referencia]
   - **Proyecto:** [Nombre del proyecto]
   ```
3. **Crear skill** si es reutilizable
4. **Commit a GitHub** para compartir con equipo

---

## 📊 Estadísticas

- **Total aprendizajes:** 21
- **Último actualizado:** 2026-03-13
- **Proyectos contribuyentes:** Asiste Hogar, ROI Master Calculator IA, VibeMultiatlas
- **Skills creadas:** 3 (spanish-naming-convention, snyk-security-audit, generation-web-learning)

---

*Este archivo crece con cada proyecto. Cada error documentado hace el sistema más fuerte.*
