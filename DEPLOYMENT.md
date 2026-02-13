# HCI Modules — Deployment Guide

## Project Structuur

```
hci-modules/
├── netlify.toml          ← Netlify configuratie + redirects
├── package.json          ← Dependencies (Anthropic SDK)
├── public/
│   ├── index.html        ← Landing page / module hub
│   ├── pmc.html          ← PMC Creatie Module + AI
│   ├── gtm.html          ← GTM Voorbereiding Module + AI
│   └── outreach.html     ← Outreach & Engagement Module + AI
└── netlify/
    └── functions/
        └── chat.js       ← Claude API proxy (server-side, veilig)
```

## Deployment Stappen

### 1. GitHub Repository Aanmaken

```bash
# In terminal:
cd hci-modules
git init
git add .
git commit -m "HCI Modules: PMC + GTM + Outreach met AI assistant"
git remote add origin https://github.com/JOUW-USERNAME/hci-modules.git
git push -u origin main
```

### 2. Netlify Koppelen

1. Ga naar [app.netlify.com](https://app.netlify.com)
2. Klik **"Add new site"** → **"Import an existing project"**
3. Kies **GitHub** → selecteer `hci-modules` repository
4. Build settings worden automatisch herkend via `netlify.toml`
5. Klik **Deploy site**

### 3. Claude API Key Instellen

1. In Netlify dashboard → **Site settings** → **Environment variables**
2. Klik **Add a variable**
3. Key: `ANTHROPIC_API_KEY`
4. Value: je Claude API key (van [console.anthropic.com](https://console.anthropic.com))
5. Klik **Save**
6. **Redeploy** de site (Deploys → Trigger deploy)

### 4. Custom Domein (optioneel)

1. Netlify → **Domain settings** → **Add custom domain**
2. Voer in: `app.hes-consultancy-international.com`
3. Voeg CNAME record toe bij je DNS provider:
   - Type: `CNAME`
   - Name: `app`
   - Value: `jouw-site-naam.netlify.app`
4. SSL wordt automatisch ingesteld door Netlify

## URLs na Deployment

| URL | Pagina |
|-----|--------|
| `/` | Landing page met module overzicht |
| `/pmc` | PMC Creatie Module (Fase 1) |
| `/gtm` | GTM Voorbereiding Module (Fase 2) |
| `/outreach` | Outreach & Engagement Module (Fase 3) |
| `/api/chat` | Claude API endpoint (intern) |

## Toekomstige Modules

- `/sales` — Sales Executie (Fase 4)

## Kosten

| Component | Kosten |
|-----------|--------|
| Netlify hosting | Gratis (free tier) |
| GitHub repository | Gratis |
| Claude API (Sonnet) | ~$3/1M input tokens, ~$15/1M output tokens |
| Geschat gebruik | €5-20/maand bij normaal gebruik |

## Technische Details

- **Frontend:** Standalone HTML, geen build stap nodig
- **Backend:** Netlify Functions (serverless Node.js)
- **AI Model:** Claude Sonnet 4 (claude-sonnet-4-20250514)
- **Security:** API key alleen server-side, nooit in frontend code
- **Rate limiting:** Netlify heeft ingebouwde rate limiting; extra custom limiting mogelijk in chat.js
