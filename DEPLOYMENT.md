# HCI Modules — Deployment Guide

## Files
- `index.html` — Landing page (alle 4 modules LIVE)
- `pmc.html` — Fase 1: PMC Creatie (goud accent)
- `gtm.html` — Fase 2: GTM Voorbereiding (blauw accent)
- `outreach.html` — Fase 3: Outreach & Engagement (groen accent)
- `sales.html` — Fase 4: Sales Executie (goud accent) ← NIEUW
- `chat.js` — Netlify serverless function (Claude API proxy)
- `netlify.toml` — Routing configuratie
- `package.json` — Dependencies (anthropic SDK)

## Deploy to Netlify
1. Push alle files naar GitHub repo
2. Connect repo in Netlify
3. Set environment variable: `ANTHROPIC_API_KEY`
4. Build command: (none needed)
5. Publish directory: `.` (root)

## Serverless Function
`chat.js` → deploy naar `netlify/functions/chat.js`
Route: `/api/chat` → proxied via netlify.toml

## NL/EN Toggle
Alle 4 modules + index.html hebben volledige NL/EN ondersteuning.
AI panel schakelt automatisch mee met de pagina taal.

## Modules Architectuur
Fase 1 PMC → Fase 2 GTM → Fase 3 Outreach → Fase 4 Sales
Elke module linkt door naar de volgende via journey rail.
