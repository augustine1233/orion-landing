# Orion Landing Page — evaluacionorion.org

High-converting dental campaign landing page for **Orión Clínica Odontológica IPS** (Armenia, Quindío, Colombia). Static HTML/CSS/JS — deploy-ready for Vercel.

## Deploy to Vercel

1. Push repo to GitHub
2. vercel.com → **New Project** → Import repo
3. Framework preset: **Other**
4. Click **Deploy**

## Connect evaluacionorion.org on Namecheap

1. Vercel → Project → **Settings → Domains** → Add `evaluacionorion.org`
2. Vercel gives you an A record + CNAME
3. Namecheap → **Advanced DNS** → paste both records
4. Wait 10–30 mins — SSL auto-issues

## Add WhatsApp Chat Widget (when ready)

Paste the GHL chat widget script before `</body>` in **both** `index.html` and `thank-you.html`.

## Create these GHL Custom Fields (Contacts)

- `dental_intent` / `dental_intent_priority`
- `dental_timeline` / `dental_timeline_priority`
- `dental_concern` / `dental_concern_priority`
- `lead_priority` / `landing_page` / `lead_timestamp`

## Replace before going live

- [ ] `assets/dr-jovan-video.mp4` — Dr. Jovan video
- [ ] `assets/orion-clinic.jpeg` — reception photo
- [ ] `assets/dr-jovan-patient.jpeg` — doctor + patient photo
- [ ] Real testimonial if not using Mauricio Lopez

> The page currently uses styled placeholder divs in the hero (video block) and About section (Dr. Jovan photo). Each placeholder shows the file path it expects — just drop the asset into `/assets/` and swap the placeholder div for the real `<video>` / `<img>` element.

## Meta Pixel ID

`1344811954211995`

Events fired:
- `PageView` — on every page load
- `Lead` — when an intent card is selected (with COP value: implantes 4M, diseno_sonrisa 3M, ortodoncia 2.5M, blanqueamiento 800K, revision_general 200K)
- `InitiateCheckout` — when any CTA button is clicked
- `CompleteRegistration` + `Schedule` — on successful form submit (value 40,000 COP)
- `Purchase` — on `thank-you.html` load (value 40,000 COP)

## GHL Webhook

```
https://services.leadconnectorhq.com/hooks/lVb1fZNupI3G31Dr2Kfh/webhook-trigger/53088fc1-0355-4f55-9ae2-2a85fe41360f
```

Sends `firstName`, `lastName`, `name`, `email`, `phone`, `source`, `tags` (comma string), all dental intent/timeline/concern fields + a `customFields` array — so any GHL field-name shape works.

## GHL Calendar Embed

```
https://link.azevedogroup.com/widget/booking/pSbUG88su4sFlb3ASeeh
```

The calendar listens for the `appointment_booked` postMessage and redirects to `/thank-you.html`, firing the `Purchase` Pixel event.

## File structure

```
.
├── index.html        # Single-file landing page (HTML + CSS + JS inline)
├── thank-you.html    # Confirmation page (fires Purchase event)
├── vercel.json       # Vercel deployment config
├── README.md         # This file
└── assets/
    ├── orion-clinic.jpeg        # Hero poster (placeholder until added)
    ├── dr-jovan-patient.jpeg    # About section (placeholder until added)
    └── dr-jovan-video.mp4      # Hero video (placeholder until added)
```

## Tech notes

- Plain HTML/CSS/JS. No frameworks, no build step.
- Google Fonts: Poppins + Open Sans (`display=swap`).
- Mobile-first, responsive down to 360px.
- Cupos counter uses `localStorage` keyed per ISO week (Colombia UTC-5), `sessionStorage` to avoid double-counting refreshes, floors at 1.
- FAQ accordion, smooth scroll, and step navigation are all vanilla JS.
- `prefers-reduced-motion` disables animations.
