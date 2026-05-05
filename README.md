# Orion Landing Page — evaluacionorion.org

High-converting dental campaign landing page for **Orión Odontología Integrativa IPS** (Armenia, Quindío, Colombia). Mobile-first, Typeform-style sliding survey, Colombian Spanish.

## Deploy to Vercel

1. Push repo to GitHub
2. vercel.com → **New Project** → Import repo
3. Framework: **Other**
4. Click **Deploy**

## Connect Domain on Namecheap

1. Vercel → **Settings → Domains** → add `evaluacionorion.org`
2. Copy A record + CNAME from Vercel
3. Namecheap → **Advanced DNS** → paste both
4. Wait 10–30 mins — SSL auto-issues

## GHL Webhook

```
https://services.leadconnectorhq.com/hooks/lVb1fZNupI3G31Dr2Kfh/webhook-trigger/53088fc1-0355-4f55-9ae2-2a85fe41360f
```

## Meta Pixel ID

`1344811954211995`

Events fired:
- `PageView` — every page load
- `ViewContent` — when user clicks the hero "Ver Si Califico" CTA (survey starts)
- `Lead` — when Q1 (intent) is answered (with intent value in COP)
- `CompleteRegistration` — when contact form submits successfully (value 40,000 COP)
- `Schedule` — when calendar appears
- `Purchase` — fires on `thank-you.html` load (value 40,000 COP)

## GHL Calendar

```
https://link.azevedogroup.com/widget/booking/pSbUG88su4sFlb3ASeeh
```

The calendar listens for the `appointment_booked` postMessage and redirects to `/thank-you.html` (which fires `Purchase`).

## GHL Custom Fields to Create (Contacts)

- `dental_intent`
- `dental_intent_priority`
- `dental_timeline`
- `dental_timeline_priority`
- `dental_concern`
- `dental_concern_priority`
- `lead_priority`
- `landing_page`
- `lead_timestamp`

## Replace Before Going Live

- [ ] `assets/dr-jovan-video.mp4` — Dr. Jovan video
- [ ] `assets/orion-clinic.jpg` — reception photo (already in repo)
- [ ] `assets/dr-jovan-patient.jpg` — doctor + patient photo (already in repo)

## WhatsApp Widget

Add the GHL chat script before `</body>` in **both** `index.html` and `thank-you.html` once WhatsApp is verified.

## File structure

```
.
├── index.html        # Single-file landing page (HTML + CSS + JS inline)
├── thank-you.html    # Confirmation page (fires Purchase event)
├── vercel.json       # Vercel deployment config
├── README.md         # This file
└── assets/
    ├── orion-clinic.jpg
    ├── dr-jovan-patient.jpg
    ├── dr-jovan-video.mp4         (placeholder until added)
    └── Logo-Orion-Odontologia-IPS-Armenia-Quindio.png
```

## Funnel flow

1. **Hero** — pitch + countdown + "Ver Si Califico →" CTA
2. **Survey** (Typeform-style sliding) — Q1 intent → (if revision: Q2B concern) → Q2A timeline
3. **Contact form** (revealed on survey complete) — name + WhatsApp + email
4. **Calendar** (revealed after webhook fires) — GHL embedded booking
5. **Trust + Proof** — value stack, testimonial, Google reviews, About, FAQ
6. **Final CTA** — scrolls back to survey

The cupos counter uses `localStorage` keyed by ISO week. Each unique session decrements (sessionStorage flag prevents refresh-counting). Floors at 1 — never shows 0.
