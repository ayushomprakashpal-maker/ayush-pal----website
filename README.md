# ⚡ Apex Sports Arena Website

A responsive, multi-page website for **Apex Sports Arena**, a sports facility offering futsal, box cricket, badminton, and basketball/pickleball courts. Built with plain HTML, CSS, and a little JavaScript, so there is no build step and no dependencies to install.

## Pages

| File | Page | Purpose |
|------|------|---------|
| `index.html` | Home | Hero section with a promo tag, call-to-action, and highlights of the arena's main features |
| `about.html` | About Us | Arena story, vision, and standards (tournament ready, safety and hygiene, 24/7 availability) |
| `services.html` | Courts & Pricing | Cards for each court with descriptions and hourly rates |
| `gallery.html` | Gallery | Photo grid of the facility with captions |
| `contact.html` | Book a Slot | Booking and enquiry form that submits to Google Sheets |
| `style.css` | Stylesheet | Shared styling for all pages |

## Features

- **Dark, neon-accented design** with glassmorphism cards and a sticky blurred header
- **Responsive layout** using CSS Grid (`auto-fit` / `minmax`) and `clamp()` for fluid headings
- **Hover effects** on cards, buttons, nav links, and gallery images
- **Booking form** with name, phone, court selection, date/time picker, and special requests
- **Success and error messages** shown after form submission
- **Google Fonts**: Plus Jakarta Sans and Space Grotesk

## Courts & Pricing

| Court | Rate |
|-------|------|
| 5-a-Side Futsal Turf | $40 / hour |
| Box Cricket Arena | $35 / hour |
| Indoor Badminton Court | $20 / hour |
| Pro Basketball / Pickleball | $30 / hour |

## Project Structure

```
.
├── index.html
├── about.html
├── services.html
├── gallery.html
├── contact.html
└── style.css
```

## Getting Started

1. Download or clone all the files into one folder.
2. Open `index.html` in any modern browser.

No server is needed. Internet access is required to load the Google Fonts and the Unsplash images.

## Setting Up the Booking Form

The form on `contact.html` sends bookings to a **Google Apps Script Web App**, which can save them to a Google Sheet.

1. Create a new Google Sheet with headers matching the form fields: `name`, `phone`, `sport`, `slotDate`, `notes`.
2. Open **Extensions → Apps Script** and add a `doPost(e)` function that appends `e.parameter` values to the sheet.
3. Click **Deploy → New deployment → Web app**. Set *Execute as* to **Me** and *Who has access* to **Anyone**.
4. Copy the Web App URL.
5. In `contact.html`, replace the placeholder:

   ```js
   const SCRIPT_URL = "YOUR_GOOGLE_APPS_SCRIPT_WEB_APP_URL_HERE";
   ```

Until the URL is set, submitting the form shows an alert reminding you to add it.

### Example Apps Script

```js
function doPost(e) {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  const p = e.parameter;
  sheet.appendRow([new Date(), p.name, p.phone, p.sport, p.slotDate, p.notes]);
  return ContentService.createTextOutput("OK");
}
```

## Customization

- **Colors:** edit the CSS variables in `:root` at the top of `style.css` (`--neon-orange`, `--neon-green`, `--neon-cyan`, `--bg-dark`, and so on).
- **Prices and courts:** edit the cards in `services.html`, and update the court options in the `<select>` in `contact.html`.
- **Images:** replace the Unsplash URLs with your own photos, ideally stored in an `images/` folder.
- **Branding:** change the logo text (`⚡ APEX ARENA`) in the `<nav>` of each page.

## Known Notes

- The navigation is duplicated in every HTML file, so any menu change must be made in all five pages.
- Nav labels on the home page ("About", "Courts & Deals", "Vibe Check", "Book Slot") differ from the other pages ("About Us", "Courts & Pricing", "Gallery", "Book a Slot"). Pick one set for consistency.
- The form uses `fetch` without `mode: 'no-cors'` handling, so depending on your Apps Script setup, the browser may report a CORS error even when the data is saved. If that happens, add `mode: 'no-cors'` to the `fetch` options.
- The success message shows for any completed request, without checking the server's response.
- The About page says "24/7 availability" while the home page highlights midnight and late-night play, so confirm your actual opening hours and keep them consistent.
- The placeholder phone format in the form (`+1 555-0199`) is US style, so adjust it for your region.

## Tech Stack

- HTML5
- CSS3 (Grid, Flexbox, custom properties, `backdrop-filter`)
- Vanilla JavaScript
- Google Apps Script (for form submissions)

## License

© 2026 Apex Sports Arena. All rights reserved.
