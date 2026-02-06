---
description: Convención de nombres en español para servicios externos
---

# Skill: Nombres en Español para Servicios

## 🎯 Objetivo

Asegurar que TODOS los nombres en servicios externos (Railway, Supabase, Resend, etc.) estén en español para que cualquier persona sin conocimientos de inglés pueda identificar qué es cada cosa.

---

## 📋 Regla General

**Si es visible en un dashboard o interfaz externa → ESPAÑOL**  
**Si es código interno o estándar técnico → Inglés (cuando sea necesario)**

---

## 🚂 Railway

### Nombres de Servicios
```
❌ asiste-hogar-app
✅ app-principal

❌ function-bun
✅ funciones-bun

❌ worker-queue
✅ cola-trabajos
```

### Entornos
```
❌ production
✅ produccion

❌ staging
✅ pruebas

❌ development
✅ desarrollo
```

### Variables de Entorno
- Nombre: Puede ser inglés (estándar técnico)
- **Descripción: SIEMPRE en español**

```yaml
SMTP_HOST:
  descripcion: "Servidor de correo saliente"
  
DATABASE_URL:
  descripcion: "URL de conexión a base de datos"
```

---

## 🗄️ Supabase

### Nombre del Proyecto
```
❌ asiste-hogar-production
✅ Asiste Hogar - Producción
```

### Tablas
```
❌ workers
✅ trabajadores

❌ companies
✅ empresas

❌ job_offers
✅ ofertas_trabajo

❌ applications
✅ postulaciones
```

**Nota:** Usa `snake_case` en español: `ofertas_trabajo`, no `ofertasTrabajo`

### Políticas RLS
```
❌ Users can view own data
✅ Usuarios pueden ver sus propios datos

❌ Companies can update workers
✅ Empresas pueden actualizar trabajadores
```

### Funciones de Base de Datos
```
❌ get_worker_by_id
✅ obtener_trabajador_por_id

❌ create_job_offer
✅ crear_oferta_trabajo
```

---

## 📧 Resend

### API Keys
```
❌ Production API Key
✅ Clave API Producción

❌ Test Key
✅ Clave Pruebas
```

### Dominios
- Mantener dominio real: `asistehogar.net` ✅

---

## 🎨 Canva

### Templates
```
❌ Certificate Template
✅ Plantilla Certificado

❌ Worker Badge
✅ Credencial Trabajador
```

---

## 💾 GitHub

### Repositorio
- Puede ser inglés si es público/compartido
- Español si es privado del cliente

### Branches
```
❌ feature/new-login
✅ funcionalidad/nuevo-login

❌ fix/email-bug
✅ correccion/error-email
```

**Excepciones:**
- `main` → Mantener (estándar)
- `develop` → Mantener (estándar)

---

## 🔧 Código Fuente

### ❌ NO Cambiar a Español

1. **Rutas de API**
   ```typescript
   // ✅ Correcto (estándar web)
   /api/workers
   /api/job-offers
   ```

2. **Nombres de funciones/variables**
   ```typescript
   // ✅ Correcto (estándar código)
   function getWorkerById(id: string) {}
   const jobOffers = [];
   ```

3. **Tipos TypeScript**
   ```typescript
   // ✅ Correcto
   interface Worker {}
   type JobOffer = {};
   ```

### ✅ SÍ Cambiar a Español

1. **Comentarios**
   ```typescript
   // ✅ Correcto
   // Obtiene el trabajador por ID
   function getWorkerById(id: string) {}
   ```

2. **Mensajes de error**
   ```typescript
   // ✅ Correcto
   throw new Error('Trabajador no encontrado');
   ```

3. **Logs**
   ```typescript
   // ✅ Correcto
   console.log('Iniciando proceso de notificaciones...');
   ```

4. **Documentación**
   ```markdown
   # ✅ Correcto
   ## Cómo crear un trabajador
   ```

---

## 🤖 Automatización

### Al crear nuevos recursos

1. **Railway:**
   ```bash
   # Antes de crear servicio, pensar nombre en español
   Servicio: "procesador-emails"
   Entorno: "produccion"
   ```

2. **Supabase:**
   ```sql
   -- Crear tabla con nombre español
   CREATE TABLE trabajadores (
     id UUID PRIMARY KEY,
     nombre TEXT NOT NULL
   );
   
   -- Política con descripción español
   CREATE POLICY "Usuarios ven sus datos"
   ON trabajadores FOR SELECT
   USING (auth.uid() = user_id);
   ```

3. **Variables de Entorno:**
   ```bash
   # Añadir descripción en español
   SMTP_HOST="mail.example.com"
   # Descripción: "Servidor de correo saliente"
   ```

---

## ✅ Checklist de Verificación

Antes de dar por terminado un proyecto:

- [ ] Railway: Servicios renombrados
- [ ] Railway: Entornos en español
- [ ] Railway: Variables con descripción
- [ ] Supabase: Tablas en español
- [ ] Supabase: Políticas RLS en español
- [ ] Resend: API Keys descriptivas
- [ ] Canva: Templates con nombres claros
- [ ] Código: Comentarios en español
- [ ] Código: Mensajes de error en español
- [ ] Documentación: Todo en español

---

## 🚨 Excepciones Permitidas

**Mantener en inglés cuando:**

1. Es un estándar técnico universal
   - `main`, `develop` (branches)
   - `/api/...` (rutas)
   - Nombres de funciones/variables

2. Es requerido por la herramienta
   - Algunos campos de configuración
   - Nombres de archivos del framework

3. Es código compartido públicamente
   - Librerías open source
   - Ejemplos para comunidad

**En caso de duda:** Español. Es mejor ser descriptivo que técnico.

---

## 📝 Ejemplos Completos

### Railway Service

```yaml
Nombre: app-principal
Entorno: produccion
Variables:
  SMTP_HOST:
    valor: "mail.asistehogar.net"
    descripcion: "Servidor de correo para notificaciones"
  DATABASE_URL:
    valor: "postgresql://..."
    descripcion: "Conexión a base de datos principal"
```

### Supabase Table

```sql
CREATE TABLE ofertas_trabajo (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  titulo TEXT NOT NULL,
  descripcion TEXT,
  empresa_id UUID REFERENCES empresas(id),
  created_at TIMESTAMPTZ DEFAULT NOW()
);

CREATE POLICY "Empresas ven sus ofertas"
ON ofertas_trabajo FOR SELECT
USING (empresa_id = auth.uid());
```

### Resend API Key

```
Nombre: Clave API Producción - Asiste Hogar
Descripción: Usada para envío de emails desde app principal
```

---

## 🎓 Filosofía

> "Si tu abuela no entiende qué hace, el nombre está mal."

El objetivo es que **cualquier persona** pueda:
1. Identificar qué es cada servicio
2. Entender qué hace cada componente
3. Solucionar problemas básicos sin ayuda técnica

**Prioridad:** Claridad > Brevedad > Tecnicismos
