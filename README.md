# AI Teamradar

Anonieme team self-assessment op vijf AI-maturity dimensies (Adoptie, Proces, Autonomie, Kwaliteit, Impact, schaal 1-5) met een live dashboard. Gebouwd voor de kick-off van het agentic-teams-traject bij PharmaPartners, september 2026.

Live: https://morgenacademy.github.io/teamradar/

## Hoe het werkt

- Eén bestand: `index.html`. Geen build, geen dependencies behalve supabase-js via CDN en Barlow via Google Fonts.
- Backend: Supabase-project "Companydashboard" (organisatie MorgenAcademy), tabel `pp_teamradar_responses`. Row Level Security: iedereen mag lezen, invullen en het eigen antwoord overschrijven, niemand mag wissen via de API.
- Eén rij per browser: de pagina bewaart een willekeurig id in localStorage en doet een upsert. Opnieuw versturen overschrijft, telt dus niet dubbel.
- Live updates via Supabase Realtime, met een poll elke 15 seconden als vangnet.
- Wissen kan alleen via de functie `pp_teamradar_wipe(p_secret)` met een wis-code die in een tabel zonder API-toegang staat. De code staat niet in deze repo.

## Weergaven (hash in de URL)

| Hash | Wat |
|---|---|
| `#invullen` | Formulier (standaard) |
| `#dashboard` | Live dashboard |
| `#dashboard-alles` | Dashboard, toont ook teams onder de drempel |
| `#dashboard-demo` | Dashboard met ingebouwde demo-data, zonder database |
| `#admin` | Alles wissen met wis-code |

De drempel (minimum aantal antwoorden voordat een team zichtbaar is, tegen herleidbaarheid) is de constante `MIN_N_DEFAULT` in `index.html`.

## Aanpassen en publiceren

Wijzig `index.html`, commit, push naar `main`. GitHub Pages bouwt binnen een minuut.

Nooit geheimen in deze repo zetten: hij is publiek. De Supabase-key in de pagina is de publishable key en hoort daar.
