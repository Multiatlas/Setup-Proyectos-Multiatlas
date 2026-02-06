# 📧 Email para Guillermo y Desi

**Asunto:** 🏭 Setup Proyectos Multiatlas - Configuración de Agente IA

---

Hola Guillermo y Desi,

Os escribo para compartir el nuevo **Setup Proyectos Multiatlas**, un repositorio que contiene toda la configuración necesaria para que vuestros agentes de IA (Claude, Gemini, etc.) trabajen siguiendo nuestra metodología de desarrollo.

## 🎯 ¿Qué es esto?

Es un repositorio de GitHub que incluye:
- ✅ **Skills globales** - Mejores prácticas de Supabase, Next.js, Resend, etc.
- ✅ **Metodología Multiatlas** - Principios de desarrollo, arquitectura, seguridad
- ✅ **Automations** - Flujos automatizados para tareas comunes
- ✅ **Templates** - Plantillas de proyectos base

## 🚀 ¿Cómo lo instalo?

### Opción 1: Si usáis Antigravity o Claude Code

**Paso 1: Clonar el repositorio**
```bash
# Abrir PowerShell y ejecutar:
cd C:\Users\VUESTRO_USUARIO\.gemini
git clone https://github.com/Multiatlas/Setup-Proyectos-Multiatlas.git
```

**Paso 2: Crear symlinks (requiere PowerShell como Administrador)**
```powershell
cd C:\Users\VUESTRO_USUARIO\.gemini

New-Item -ItemType SymbolicLink -Path "skills" -Target "Setup-Proyectos-Multiatlas\skills"
New-Item -ItemType SymbolicLink -Path "automations" -Target "Setup-Proyectos-Multiatlas\automations"
```

**Paso 3: Verificar**
Abrid vuestro agente y preguntadle:
```
¿Qué skills tienes disponibles?
```

Debería listar los skills de Multiatlas.

---

### Opción 2: Si NO tenéis permisos de administrador

```bash
cd C:\Users\VUESTRO_USUARIO\.gemini
git clone https://github.com/Multiatlas/Setup-Proyectos-Multiatlas.git

# Copiar en vez de symlink
xcopy Setup-Proyectos-Multiatlas\skills skills\ /E /I
xcopy Setup-Proyectos-Multiatlas\automations automations\ /E /I
```

---

## 🔄 ¿Cómo sincronizo cambios?

### Descargar actualizaciones (cuando yo o alguien añada algo)

```bash
cd C:\Users\VUESTRO_USUARIO\.gemini\Setup-Proyectos-Multiatlas
git pull
```

### Subir vuestras mejoras (si añadís skills o automations)

```bash
cd C:\Users\VUESTRO_USUARIO\.gemini\Setup-Proyectos-Multiatlas
git add .
git commit -m "Descripción de lo que añadisteis"
git push
```

**Nota:** Necesitáis ser colaboradores del repo para hacer push. Si queréis contribuir, decidme vuestros usuarios de GitHub y os añado.

---

## 📚 ¿Qué contiene?

### 1. **Skill: Metodología Multiatlas**
Define cómo trabajamos:
- Golden Path (Next.js + Supabase + Resend + Tailwind)
- Arquitectura Feature-First
- Git Shield (seguridad)
- Reglas de código
- Auto-Blindaje (aprender de errores)

### 2. **Skills de Tecnologías** (próximamente)
- Supabase Best Practices
- Email Best Practices (Resend)
- Next.js Patterns
- React Email

### 3. **Automations** (próximamente)
- New Project Setup
- Daily Sync

---

## ❓ Preguntas Frecuentes

**P: ¿Tengo que hacer esto en cada ordenador?**
R: Sí, cada ordenador necesita clonar el repo. Pero una vez hecho, se sincroniza con `git pull`.

**P: ¿Puedo modificar los skills?**
R: Sí! Si sois colaboradores, podéis hacer cambios y subirlos. Si no, podéis hacer fork del repo.

**P: ¿Esto afecta a mis proyectos actuales?**
R: No. Solo añade capacidades al agente. Vuestros proyectos siguen igual.

**P: ¿Funciona con mi cuenta de Google/Claude?**
R: Sí, funciona con cualquier agente que use la carpeta `.gemini` o `.claude`.

---

## 🆘 ¿Necesitáis ayuda?

Si tenéis problemas con la instalación, escribidme y os echo una mano.

**Repositorio:** https://github.com/Multiatlas/Setup-Proyectos-Multiatlas

Saludos,
**Plat**
platmultiatlas@gmail.com

---

## 📎 Anexo: Comandos Rápidos

```bash
# Instalar (primera vez)
cd C:\Users\VUESTRO_USUARIO\.gemini
git clone https://github.com/Multiatlas/Setup-Proyectos-Multiatlas.git

# Actualizar (cuando haya cambios)
cd C:\Users\VUESTRO_USUARIO\.gemini\Setup-Proyectos-Multiatlas
git pull

# Subir cambios (si añadisteis algo)
cd C:\Users\VUESTRO_USUARIO\.gemini\Setup-Proyectos-Multiatlas
git add .
git commit -m "Vuestro mensaje"
git push
```
