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

- **Total aprendizajes:** 3
- **Último actualizado:** 2026-02-06
- **Proyectos contribuyentes:** Asiste Hogar
- **Skills creadas:** 1 (spanish-naming-convention)

---

*Este archivo crece con cada proyecto. Cada error documentado hace el sistema más fuerte.*
