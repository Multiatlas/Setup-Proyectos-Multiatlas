# 🏭 Setup Proyectos Multiatlas

> Configuración portable de skills, automations y metodología para desarrollo de proyectos SaaS

**Versión:** 1.0.0  
**Última actualización:** 2026-02-06

---

## 📋 ¿Qué es esto?

Este repositorio contiene toda la configuración necesaria para que cualquier agente de IA (Claude, Gemini, etc.) trabaje siguiendo la **metodología Multiatlas** para desarrollo de SaaS.

Incluye:
- ✅ **Skills globales** - Mejores prácticas de tecnologías (Supabase, Next.js, Resend, etc.)
- ✅ **Automations** - Flujos automatizados para tareas comunes
- ✅ **Templates** - Plantillas de proyectos base
- ✅ **Documentación** - Filosofía y metodología de trabajo

---

## 🚀 Instalación

### Prerrequisitos
- Git instalado
- Cuenta de GitHub
- Antigravity o Claude Code instalado

### Paso 1: Clonar el repositorio

```bash
# Navegar a la carpeta de configuración del agente
cd C:\Users\TU_USUARIO\.gemini

# Clonar este repo
git clone https://github.com/Multiatlas/Setup-Proyectos-Multiatlas.git
```

### Paso 2: Crear symlinks

**Windows (PowerShell como Administrador):**
```powershell
cd C:\Users\TU_USUARIO\.gemini

# Crear symlinks para que el agente use estos skills/automations
New-Item -ItemType SymbolicLink -Path "skills" -Target "Setup-Proyectos-Multiatlas\skills"
New-Item -ItemType SymbolicLink -Path "automations" -Target "Setup-Proyectos-Multiatlas\automations"
```

**Alternativa sin symlinks (copiar):**
```bash
# Si no tienes permisos de administrador
xcopy Setup-Proyectos-Multiatlas\skills skills\ /E /I
xcopy Setup-Proyectos-Multiatlas\automations automations\ /E /I
```

### Paso 3: Verificar instalación

Abre tu agente de IA y pregunta:
```
¿Qué skills tienes disponibles?
```

Deberías ver los skills de este repo listados.

---

## 🔄 Sincronización entre Ordenadores

### Actualizar (descargar cambios)

```bash
cd C:\Users\TU_USUARIO\.gemini\Setup-Proyectos-Multiatlas
git pull
```

### Subir cambios (si añadiste algo)

```bash
cd C:\Users\TU_USUARIO\.gemini\Setup-Proyectos-Multiatlas
git add .
git commit -m "Descripción de los cambios"
git push
```

---

## 📁 Estructura del Repositorio

```
Setup-Proyectos-Multiatlas/
├── skills/                    # Skills globales reutilizables
│   ├── supabase-best-practices/
│   ├── email-best-practices/
│   ├── nextjs-patterns/
│   ├── react-email/
│   └── multiatlas-methodology/  # Metodología Multiatlas
│
├── automations/               # Automatizaciones
│   ├── new-project-setup/
│   └── daily-sync/
│
├── templates/                 # Templates de proyecto
│   └── nextjs-supabase-base/
│
├── docs/                      # Documentación
│   ├── PHILOSOPHY.md
│   ├── GOLDEN_PATH.md
│   └── SECURITY.md
│
└── README.md                  # Este archivo
```

---

## 🎯 Uso

Una vez instalado, el agente automáticamente:
- ✅ Sigue las mejores prácticas definidas en los skills
- ✅ Usa las automations cuando sea apropiado
- ✅ Aplica la metodología Multiatlas en todos los proyectos

**No necesitas hacer nada especial**, el agente tiene acceso a todo.

---

## 👥 Colaboradores

Para añadir colaboradores al repo:

1. Ve a https://github.com/Multiatlas/Setup-Proyectos-Multiatlas/settings/access
2. Click en "Add people"
3. Invita por email o username de GitHub

Los colaboradores podrán:
- ✅ Clonar el repo
- ✅ Hacer pull de cambios
- ✅ Hacer push de mejoras

---

## 📚 Documentación Completa

Ver carpeta `docs/` para:
- **PHILOSOPHY.md** - Principios de desarrollo (Henry Ford, Elon Musk)
- **GOLDEN_PATH.md** - Stack tecnológico único
- **SECURITY.md** - Git Shield y mejores prácticas de seguridad

---

## 🔒 Seguridad

Este repo es **público** pero NO contiene:
- ❌ Credenciales
- ❌ API Keys
- ❌ Información sensible

Solo contiene:
- ✅ Metodología
- ✅ Mejores prácticas
- ✅ Templates de código

---

## 🆘 Soporte

**Problemas o dudas:**
- Email: platmultiatlas@gmail.com
- Issues: https://github.com/Multiatlas/Setup-Proyectos-Multiatlas/issues

---

## 📝 Licencia

Uso interno de Multiatlas © 2026
