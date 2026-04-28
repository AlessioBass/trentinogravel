# Trentino Gravel — Pioneer Edition

Single-page landing for the **Trentino Gravel — Pioneer Edition** event (Rovereto, 26 September 2026), organised by [Bike Adventure Series](https://www.bikeadventureseries.com) / Tuscany Trail.

Goal: collect emails for the waiting list before registration opens.

## Files

| File | Purpose |
|------|---------|
| `index.html` | Landing page (HTML + inline CSS + inline JS, mobile-first) |
| `content.json` | Tutti i testi IT/EN gestiti da Pages CMS |
| `.pages.yml` | Schema Pages CMS |
| `_worker.js` | Cloudflare Worker: proxy POST /api/waitlist → Brevo |
| `wrangler.jsonc` | Configurazione deploy Cloudflare Workers |
| `privacy.html` | Privacy policy |
| `photos/` | Foto del sito (gestite via Pages CMS) |
| `extracted/` | Brand assets (loghi SVG/PNG, favicon) |
| `archive/` | Snapshot vecchie versioni |

## Local preview

```bash
cd trentinogravelweb
python3 -m http.server 8765
open http://localhost:8765
```

> Il form waitlist non funziona in locale (richiede il Worker CF). Per testarlo usa il deploy di preview.

## Modifica contenuti (Pages CMS)

Tutti i testi bilingui (IT/EN) sono in `content.json`. Per modificarli senza toccare il codice:

1. Vai su **[app.pagescms.org](https://app.pagescms.org)** e accedi con GitHub
2. Apri il repository `vietts/trentinogravel`
3. Seleziona **Contenuto Sito** → modifica qualsiasi testo o foto
4. Salva → Pages CMS committa su GitHub → Cloudflare rideploya automaticamente

Le modifiche sono live in ~30 secondi.

## Deploy (Cloudflare Workers)

Il sito è deployato su Cloudflare Workers con Assets. Il deploy parte automaticamente ad ogni push su `main`.

**Env var richieste nel CF dashboard** (Settings → Environment variables):

| Variable | Dove trovarla |
|---|---|
| `BREVO_API_KEY` | Brevo → Settings → API Keys |
| `BREVO_LIST_ID` | ID numerico lista "Trentino Gravel Pioneer" in Brevo |

## Stack

- **HTML/CSS/JS**, zero build step
- **Fonts**: Bebas Neue · Barlow Condensed · DM Sans · DM Mono (Google Fonts)
- **Photos**: `photos/` (committate in git, servite da CF Assets)
- **i18n**: vanilla JS toggle IT/EN via `data-i18n-it` / `data-i18n-en`
- **Form**: POST a `/api/waitlist` (CF Worker) → Brevo REST API

## Design system (tokens)

```css
--blue:       #2C5E2E  /* forest green */
--blue-deep:  #1A3C1C
--blue-light: #3D7A40
--orange:     #C25832  /* terracotta */
--cream:      #F2EEAE
--offwhite:   #F5EDE0
--ink:        #0A150A
```

## Roadmap

- [ ] OG image (`extracted/og-image.jpg`) per anteprime social (1200×630)
- [ ] Sostituire foto placeholder con lo shooting reale Trentino
- [ ] Aggiornare loghi partner (APT Trentino, Comune di Rovereto, brand bike)
- [ ] Privacy policy definitiva in `privacy.html`
- [ ] Video teaser nella sezione `.film-player`

## Usare Claude Code su questo progetto

```bash
git clone https://github.com/vietts/trentinogravel.git
cd trentinogravel
claude
```

### Esempi di prompt utili

```
cambia il colore del bottone CTA in #D46840
aggiungi una nuova FAQ: domanda "..." risposta "..."
il form non mostra il messaggio di errore, controllalo
fai il commit e pusha su GitHub
```

## License

Private — © 2026 Bike Adventure Series
