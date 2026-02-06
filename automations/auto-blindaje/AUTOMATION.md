---
description: Sistema de Auto-Blindaje - Documentación automática de aprendizajes
---

# 🛡️ Auto-Blindaje Automation

## 🎯 Objetivo

Cada proyecto que inicies con Setup-Proyectos-Multiatlas automáticamente:
1. Documenta aprendizajes
2. Crea skills reutilizables
3. Alimenta el conocimiento global
4. Crece el sistema

---

## 🤖 Cómo Funciona

### Al Iniciar Proyecto

Antigravity automáticamente:
1. Lee `docs/auto-blindaje.md` (aprendizajes previos)
2. Aplica esos aprendizajes al nuevo proyecto
3. Evita errores ya documentados

**Ejemplo:**
```
Usuario: "Necesito enviar emails desde Railway"
Antigravity: "Según auto-blindaje.md, Railway bloquea SMTP.
             Recomiendo usar Resend (API HTTP)."
```

---

### Durante el Proyecto

Cuando encuentres algo reutilizable:

```bash
# 1. Antigravity te pregunta automáticamente
"¿Este patrón es reutilizable? (s/n)"

# 2. Si dices "sí"
"¿En qué categoría? (skill/automation/template)"

# 3. Antigravity crea el archivo automáticamente
# En: Setup-Proyectos-Multiatlas/skills/[nombre]/

# 4. Commit automático
git add Setup-Proyectos-Multiatlas/
git commit -m "feat: añadir skill [nombre] desde proyecto [X]"
```

---

### Al Final del Día

Antigravity ejecuta automáticamente:

```bash
# 1. Revisar cambios del día
git diff --name-only

# 2. Identificar patrones reutilizables
# - Nuevas funciones útiles
# - Componentes genéricos
# - Soluciones a problemas comunes

# 3. Preguntar si documentar
"Encontré estos patrones reutilizables:
 - canva.ts (integración Canva)
 - emailService.ts (envío emails)
 ¿Añadir a Setup-Proyectos-Multiatlas? (s/n)"

# 4. Actualizar auto-blindaje.md
echo "### $(date): [Aprendizaje]" >> docs/auto-blindaje.md

# 5. Commit y push
git push
```

---

## 📋 Comandos Disponibles

### `/extract-skill`
Extrae código actual como skill reutilizable.

**Uso:**
```
/extract-skill canva-integration
```

**Resultado:**
```
Setup-Proyectos-Multiatlas/
  └── skills/
      └── canva-integration/
          ├── SKILL.md
          ├── canva.ts
          └── README.md
```

---

### `/document-learning`
Documenta un aprendizaje en auto-blindaje.

**Uso:**
```
/document-learning "Railway bloquea SMTP"
```

**Resultado:**
```markdown
### 2026-02-06: Railway bloquea SMTP
- **Error:** Connection timeout en puertos 25, 465, 587
- **Fix:** Usar Resend (API HTTP)
- **Aplicar en:** Todos los proyectos en Railway
```

---

### `/sync-multiatlas`
Sincroniza aprendizajes con Setup-Proyectos-Multiatlas.

**Uso:**
```
/sync-multiatlas
```

**Resultado:**
```bash
✅ Aprendizajes documentados: 3
✅ Skills creadas: 2
✅ Commit y push completado
```

---

## 🔄 Workflow Automático

### 1. Inicio de Proyecto
```
Usuario: "Crear nuevo proyecto SaaS"
Antigravity:
  1. Lee auto-blindaje.md
  2. Aplica aprendizajes previos
  3. Configura proyecto con mejores prácticas
  4. Evita errores conocidos
```

### 2. Durante Desarrollo
```
Usuario: [Implementa algo]
Antigravity:
  1. Detecta patrón reutilizable
  2. Pregunta si extraer
  3. Crea skill automáticamente
  4. Commit a GitHub
```

### 3. Fin del Día
```
Antigravity (automático):
  1. Revisa cambios del día
  2. Identifica aprendizajes
  3. Actualiza auto-blindaje.md
  4. Sincroniza con GitHub
```

---

## 📊 Ejemplo Real

### Día 1: Proyecto Asiste Hogar
```
[Implementas Canva Connect]

Antigravity: "Detecté patrón reutilizable: Canva OAuth"
Usuario: "Sí, extraer"
Antigravity: 
  ✅ Creado: skills/canva-integration/
  ✅ Commit: "feat: añadir skill Canva desde Asiste Hogar"
  ✅ Push a GitHub
```

### Día 30: Proyecto Nuevo
```
Usuario: "Necesito integrar Canva"
Antigravity: "Encontré skill: canva-integration"
             "¿Usar este patrón? (s/n)"
Usuario: "Sí"
Antigravity: 
  ✅ Copiado: canva-integration → nuevo proyecto
  ✅ Configurado automáticamente
  ✅ Listo en 2 minutos
```

---

## 🎯 Beneficios

### Para Ti
- ✅ No repites errores
- ✅ No reinventas la rueda
- ✅ Cada proyecto es más rápido
- ✅ Conocimiento acumulado

### Para el Equipo
- ✅ Todos aprenden de todos
- ✅ Mejores prácticas compartidas
- ✅ Onboarding más rápido
- ✅ Calidad consistente

### Para Multiatlas
- ✅ Sistema que crece solo
- ✅ Ventaja competitiva
- ✅ Velocidad de desarrollo
- ✅ Menos bugs

---

## 🚀 Activación

### Automático
Antigravity detecta `Setup-Proyectos-Multiatlas/` y activa auto-blindaje.

### Manual
```bash
# En cualquier momento
/sync-multiatlas
```

---

## 📝 Configuración

### Frecuencia de Sync
```yaml
# Setup-Proyectos-Multiatlas/config.yml
auto_blindaje:
  sync_frequency: "daily"  # daily, weekly, manual
  auto_extract: true       # Preguntar automáticamente
  auto_commit: true        # Commit automático
```

---

## 🎓 Filosofía

> "La máquina que construye la máquina es más importante que el producto."
> - Elon Musk

**Setup-Proyectos-Multiatlas es la máquina.**  
**Cada proyecto la mejora.**  
**El sistema crece solo.**

---

**¿Activar auto-blindaje en Asiste Hogar ahora?**
