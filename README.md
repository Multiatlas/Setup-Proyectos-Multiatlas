# 🏭 Setup-Proyectos-Multiatlas

> Sistema de conocimiento compartido que crece automáticamente con cada proyecto

**Versión:** 1.0.0  
**Última actualización:** 2026-02-07

---

## 🎯 ¿Qué es esto?

Un repositorio de **aprendizajes, skills y mejores prácticas** que se alimenta automáticamente de cada proyecto que haces. Piensa en ello como un "cerebro colectivo" del equipo.

---

## 🚀 Inicio Rápido

### 1. Clonar el Repositorio

```bash
git clone https://github.com/Multiatlas/Setup-Proyectos-Multiatlas.git
cd Setup-Proyectos-Multiatlas
```

### 2. Leer la Documentación

- **[VISION.md](VISION.md)** - Qué es y por qué existe (10 min)
- **[docs/auto-blindaje.md](docs/auto-blindaje.md)** - Aprendizajes del equipo (5 min)
- **[skills/](skills/)** - Patrones reutilizables

### 3. Solicitar Acceso de Colaborador

**Para poder contribuir (hacer push), necesitas ser colaborador invitado.**

Contacta al admin del repo:
```
Hola, quiero contribuir a Setup-Proyectos-Multiatlas.
¿Puedes añadirme como colaborador?
Mi usuario de GitHub: [tu_username]
```

Una vez invitado, podrás hacer `git push`.

---

## 📋 Uso Diario

### Al Inicio del Día

```bash
cd Setup-Proyectos-Multiatlas
git pull  # Obtener últimos aprendizajes del equipo
```

### Durante el Proyecto

1. **Lee `docs/auto-blindaje.md`** antes de empezar
2. Aplica los aprendizajes documentados
3. Evita errores que otros ya resolvieron

### Al Final del Día (5 min)

```bash
# 1. ¿Encontraste un error?
echo "### 2026-02-07: Railway bloquea SMTP" >> docs/auto-blindaje.md
echo "- **Error:** Connection timeout" >> docs/auto-blindaje.md
echo "- **Fix:** Usar Resend (API HTTP)" >> docs/auto-blindaje.md

# 2. ¿Creaste algo reutilizable?
cp src/lib/canva.ts skills/canva-integration/

# 3. Commit y push
git add .
git commit -m "docs: añadir aprendizaje Railway SMTP"
git push
```

**Nota:** Necesitas ser colaborador invitado para hacer `git push`.

---

## 📁 Estructura del Repositorio

```
Setup-Proyectos-Multiatlas/
├── README.md              # Este archivo
├── VISION.md              # Visión y filosofía (lectura obligatoria)
│
├── skills/                # Patrones reutilizables
│   ├── spanish-naming-convention/
│   ├── email-best-practices/
│   ├── supabase-agent-skills/
│   └── ...
│
├── automations/           # Procesos automatizables
│   └── auto-blindaje/
│
├── docs/                  # Documentación
│   └── auto-blindaje.md   # Aprendizajes acumulados
│
└── templates/             # Plantillas reutilizables
```

---

## 🎯 Filosofía

### Auto-Blindaje

> "Cada error es un impacto que refuerza nuestra estructura. Blindamos el proceso para que la falla nunca se repita."

**Proceso:**
```
Error ocurre → Se arregla → Se DOCUMENTA → NUNCA ocurre de nuevo
```

### Crecimiento Orgánico

No es un proyecto que se "termina". Crece naturalmente con cada proyecto:
- Hoy: 3 aprendizajes, 7 skills
- En 6 meses: 50+ aprendizajes, 20+ skills
- En 1 año: 100+ aprendizajes, 50+ skills

---

## 👥 Roles y Permisos

### Visitante (Cualquiera)
- ✅ Ver código
- ✅ Clonar repo
- ❌ No puede hacer push

### Colaborador (Invitado)
- ✅ Ver código
- ✅ Clonar repo
- ✅ Hacer push
- ✅ Contribuir aprendizajes

### Admin
- ✅ Todo lo anterior
- ✅ Invitar colaboradores
- ✅ Cambiar configuración

---

## 🔐 Seguridad

**Este repositorio NO contiene:**
- ❌ Credenciales (API keys, passwords)
- ❌ Código de clientes
- ❌ Información sensible

**Solo contiene:**
- ✅ Documentación
- ✅ Patrones genéricos
- ✅ Mejores prácticas
- ✅ Aprendizajes

---

## 🤝 Contribuir

### Opción 1: Colaborador Invitado (Recomendado)

1. Solicitar acceso al admin
2. Aceptar invitación de GitHub
3. Hacer cambios y push directo

### Opción 2: Pull Request (Sin Invitación)

1. Hacer fork del repo
2. Hacer cambios en tu fork
3. Abrir Pull Request
4. Esperar aprobación del admin

---

## 📊 Métricas

**Estado actual:**
- Aprendizajes documentados: 3
- Skills creadas: 7
- Automations: 1
- Proyectos contribuyentes: 1 (Asiste Hogar)

**Objetivo 6 meses:**
- Aprendizajes: 50+
- Skills: 20+
- Automations: 5+
- Proyectos: 10+

---

## 📞 Contacto

**Admin del repo:** [Tu nombre]  
**Email:** [Tu email]  
**GitHub:** [@Multiatlas](https://github.com/Multiatlas)

---

## 📜 Licencia

Privado - Solo para equipo Multiatlas y colaboradores invitados.

---

**Lee [VISION.md](VISION.md) para entender el propósito completo del sistema.**
