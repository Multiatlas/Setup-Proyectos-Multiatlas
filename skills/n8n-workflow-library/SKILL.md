---
name: n8n Workflow Library
description: Biblioteca curada de workflows n8n para automatizaciones SaaS. 2,053 templates organizados por categoría con instrucciones de importación. Fork desde Multiatlas/n8n-workflow-templates.
---

# 📦 Biblioteca de Workflows n8n para Multiatlas

## 🎯 Propósito

Colección curada de **2,053 workflows de n8n** organizados por categoría, con foco en los patrones más útiles para el ecosistema Multiatlas: Stripe, ActiveCampaign, Google Sheets, emails, leads, y automatizaciones IA.

**Repo fork:** [Multiatlas/n8n-workflow-templates](https://github.com/Multiatlas/n8n-workflow-templates)

## 🏗️ Instancia n8n de Multiatlas

| Campo | Valor |
|-------|-------|
| **URL** | `https://n8n.srv1193278.hstgr.cloud` |
| **Hosting** | Hostinger VPS (ID: 1193278) |
| **Acceso** | Panel admin → Workflows |

## 📂 Categorías de Workflows Disponibles

### Prioritarias para Multiatlas

| Categoría | Nodos | Uso en Multiatlas |
|-----------|-------|-------------------|
| **ecommerce** | Stripe, PayPal | Webhooks de pago, suscripciones, facturas |
| **email** | Gmail, SMTP, Mailjet | Nurturing leads, post-compra, recordatorios |
| **forms** | Typeform, Google Forms | Pipeline de leads desde formularios |
| **cloud_storage** | Google Sheets, Drive | Sincronizar datos de clientes y leads |
| **ai_ml** | OpenAI, Anthropic | Generación contenido, análisis datos |

### Secundarias (futuro)

| Categoría | Nodos | Potencial |
|-----------|-------|-----------|
| **messaging** | WhatsApp, Telegram | Atención al cliente automatizada |
| **social_media** | LinkedIn, Instagram | Marketing automatizado |
| **database** | PostgreSQL, Supabase | Sync multi-tenant |
| **analytics** | Google Analytics | Reporting automático |
| **calendar** | Cal.com, Calendly | Booking de reuniones |

## 🔧 Cómo Importar un Workflow a n8n

### Método 1: Manual (un workflow)
1. Ve al repo: `https://github.com/Multiatlas/n8n-workflow-templates/tree/main/workflows`
2. Encuentra el workflow `.json` que necesitas
3. Descarga el archivo (clic en "Raw" → Guardar como)
4. En n8n → **Menú (☰)** → **Import from File** → Selecciona el `.json`
5. **⚠️ IMPORTANTE:** Actualiza credenciales y URLs webhook antes de activar

### Método 2: Script automático (importar muchos)
```bash
# Clonar el repo
git clone https://github.com/Multiatlas/n8n-workflow-templates.git
cd n8n-workflow-templates

# Instalar dependencias
pip install -r requirements.txt

# Importar workflows a tu instancia n8n
python import_workflows.py
# (Configurar N8N_URL y N8N_API_KEY en el script)
```

### Método 3: Búsqueda con servidor local
```bash
# Levantar el buscador local (SQLite + FTS5)
python run.py

# Buscar por categoría en http://localhost:8000
# Ejemplo: workflows de Stripe
curl "http://localhost:8000/api/workflows?q=stripe+webhook"
curl "http://localhost:8000/api/workflows/category/ecommerce"
```

## 🎯 Workflows Curados para Casos de Uso Multiatlas

### 1. Lead Nurturing (Web 100€)
Buscar en el repo workflows que contengan:
- `Stripe` + `webhook` → Para capturar pagos
- `Google Sheets` + `form` → Para sincronizar leads
- `email` + `cron` + `reminder` → Para recordatorios automáticos
- `ActiveCampaign` + `tag` → Para segmentar contactos

### 2. SaaS Factory (Setup nuevo proyecto)
- `PostgreSQL` + `webhook` → Sync de datos multi-tenant
- `OpenAI` + `HTTP Request` → Generación automática de contenido
- `Slack`/`Telegram` → Notificaciones al equipo

### 3. Cron / Monitoring
- `schedule` + `HTTP Request` → Health checks de servicios
- `cron` + `email` → Alertas automáticas
- `webhook` + `error handler` → Monitoreo de errores

## ⚠️ Reglas de Seguridad al Importar

1. **NUNCA activar un workflow sin revisar** — Puede contener URLs/webhooks del autor original
2. **Siempre actualizar credenciales** — Los workflows vienen sin credenciales, hay que conectar las nuestras
3. **Revisar nodos HTTP Request** — Pueden apuntar a APIs externas no deseadas
4. **Usar el patrón de nombres en español** — Renombrar al importar siguiendo nuestra convención

## 📊 Estadísticas del Repo

- **Total workflows**: 2,053
- **Activos**: 215 (10.5%)
- **Nodos totales**: 29,445 (avg 14.3 por workflow)
- **Integraciones únicas**: 365 servicios
- **Por complejidad**: 35% bajo, 45% medio, 20% alto
- **Por trigger**: 40.5% complejo, 25.3% webhook, 23.2% manual, 11% programado

## 🔗 Patrones Comunes en n8n

| Patrón | Flujo | Ejemplo Multiatlas |
|--------|-------|-------------------|
| **Data Pipeline** | Trigger → Fetch → Transform → Store | Lead form → Validar → Google Sheets |
| **Integration Sync** | Cron → API → Compare → Update | Sync Stripe → Supabase cada hora |
| **Automation** | Webhook → Process → Condition → Action | Pago Stripe → Tag AC → Email |
| **Monitoring** | Schedule → Check → Alert | Health check Railway cada 5min |
