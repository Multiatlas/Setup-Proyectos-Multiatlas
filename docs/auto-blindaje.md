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

- **Total aprendizajes:** 6
- **Último actualizado:** 2026-02-10
- **Proyectos contribuyentes:** Asiste Hogar, ROI Master Calculator IA
- **Skills creadas:** 1 (spanish-naming-convention)

---

*Este archivo crece con cada proyecto. Cada error documentado hace el sistema más fuerte.*
