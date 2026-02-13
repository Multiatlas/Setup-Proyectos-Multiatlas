# GUIA MAESTRA: PRP GLOBAL (Template SaaS Factory)
Fecha: 2026-02-13
Version: 1.0.0 (Template Generico)

---

## Proposito
Este documento es el "Cerebro del Proyecto". Ha sido disenado para que cualquier IA o desarrollador pueda levantar una aplicacion SaaS similar a "Asiste Hogar" en one-shot, entendiendo no solo el codigo, sino la logica  de negocio, arquitectura y aprendizajes criticos.

## Golden Path (Stack Tecnologico)
- Framework: Next.js 14+ (App Router)
- - Backend/DB: Supabase (Auth + RLS + POSTGRES)
  - - Estilos: Tailwind CSS + Shadcn/UI
    - - Integraciones: Resend (SMTP/API), Google Maps (Autocomplete), Canva (OAuth).
     
      - ## APRENDIZAJES CRITICOS (FUNDAMENTALES)
     
      - ### 1. Distincion Empresa vs Particular
      - En un SaaS de gestion de servicios, existen dos tipos de clientes con flujos DIFERENTES:
      - - Empresa (Persona Juridica): Hoteles, residencias. Requiere CIF y Responsable.
        - - Particular (Persona Fisica): Hogares. Requiere NIF y Direccion de Servicio.
         
          - ### 2. Railway SMTP Fix
          - Para evitar bloqueos de puertos, usar la API de Resend o un relay SMTP robusto configurado en Railway.
         
          - ---



          ---

          ## Arquitectura Feature-First
          Organizar carpetas por dominio (ofertas, clientes, trabajadores) en lugar de tipo de archivo  (components, hooks).

          ---
          *Este documento es el blueprint para la proxima gran SaaS de Multiatlas.*
          
