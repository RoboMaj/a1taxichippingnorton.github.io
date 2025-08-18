# A1 Taxi Chipping Norton – Website

A simple, fast, single‑page website for A1 Taxi Chipping Norton. It highlights services, reviews, booking, and contact details, optimized for mobile with Tailwind CSS.

Live site: https://a1taxichippingnorton.co.uk

## What’s inside

- Static HTML (no build tools required)
- Tailwind CSS (CDN), Google Fonts (Inter), Font Awesome icons (CDN)
- Google Maps embed
- Customer reviews via Elfsight widget
- Booking form posting to a Google Apps Script endpoint
- Quick CTAs for Call and WhatsApp

### Repository layout

- `index.html` – The entire site (sections: Hero, About, Services, Reviews, Booking, Contact, Footer)
- `CNAME` – Configures the custom domain for GitHub Pages

## Local development

- Open `index.html` directly in a browser, or
- Use a simple static server (e.g., VS Code Live Server) for auto‑reload
- No dependencies, builds, or frameworks required

## Customization guide

Most edits happen in `index.html`.

- Branding and hero image
  - Title and meta description: `<title>` and `<meta name="description">` in the `<head>`
  - Hero background image URL in the “Hero Section”: inline `background-image`
- Colors and fonts
  - Tailwind classes throughout; font is Google Fonts "Inter" (head `<link>`)
- Contact details
  - Phone: search for `+447528133960` and update the `tel:` links and WhatsApp link (`https://wa.me/447528133960`)
  - Email: `a1taxichippingnorton@gmail.com`
  - Address appears in the Contact section
- Reviews (Elfsight)
  - Replace the `div` with class `elfsight-app-...` ID with your own app ID from Elfsight
- Map
  - Update the Google Maps `<iframe>` `src` to your preferred location
- SEO
  - `<title>`, `<meta name="description">`, and the Google site verification meta tag (if you manage Search Console)
- Footer year/company name in the Footer section

## Booking form – how it works

The form posts to a Google Apps Script Web App (action URL set in the `form` tag). The JavaScript expects a JSON response:

```json
{ "result": "success" }
```

If you’re using Google Apps Script, deploy a Web App that returns JSON. Minimal example:

```javascript
function doPost(e) {
  // Access form fields via e.parameter.name, e.parameter.phone, etc.
  // TODO: forward to email/Sheet/Drive as needed
  return ContentService
    .createTextOutput(JSON.stringify({ result: 'success' }))
    .setMimeType(ContentService.MimeType.JSON);
}
```

Alternatively, you can switch to a service like Formspree by updating the `action` URL and following their docs.

Tip: Ensure your Web App is deployed with access set to “Anyone” (or appropriate) and returns proper CORS/JSON headers.

## Deployment (GitHub Pages + custom domain)

- This repo is set up for GitHub Pages (root) with a custom domain (`CNAME` file)
- Steps (summary):
  1. In GitHub, enable Pages for the `main` branch, root
  2. Add your custom domain in Pages settings (already present in `CNAME`)
  3. Configure your DNS to point the domain to GitHub Pages per GitHub’s docs
  4. Wait for DNS and SSL to provision; enforce HTTPS in Pages settings

## Third‑party services

- Tailwind CSS CDN: utility classes, responsive layout
- Font Awesome CDN: icons
- Google Fonts (Inter): typography
- Elfsight: Google Reviews widget (requires your own Elfsight app configuration)
- Google Maps: embedded map
- Google Apps Script: form handling endpoint

## Troubleshooting

- Form doesn’t submit
  - Confirm the `form action` URL is correct and the Web App is deployed and publicly accessible
  - Ensure the Web App returns JSON with `{ result: 'success' }` (or handle errors in the front‑end script)
- Reviews not showing
  - Ensure the Elfsight script loads and the app ID is valid; some ad blockers may block widgets
- Styles/icons missing
  - Check CDN availability for Tailwind and Font Awesome
- Custom domain not working
  - Verify DNS setup and that GitHub Pages is enabled with the same domain; allow time for propagation

## License

No license specified. If you intend to open‑source this, add a LICENSE file.

## Credits

- Tailwind CSS, Font Awesome, Google Fonts
- Google Apps Script and Google Maps
- Elfsight (reviews)
