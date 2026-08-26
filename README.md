# Labourites Website

Plain HTML/CSS/JS site deployed on Vercel. No build step.

---

## How to Add a New Event

### Step 1 — Copy the template

Copy `_event-template.html` into the `events/` folder and name it after the event slug:

```
events/your-event-slug-here.html
```

The slug should be lowercase, words separated by hyphens, no special characters.
Example: `events/labourites-partners-with-xyz.html`

### Step 2 — Fill in the placeholders

Open the new file and replace every `PLACEHOLDER_*` value:

| Placeholder | What to put |
|---|---|
| `PLACEHOLDER_TITLE` | Full event title |
| `PLACEHOLDER_SLUG` | The slug you chose (e.g. `labourites-partners-with-xyz`) |
| `PLACEHOLDER_META_DESCRIPTION` | 1–2 sentence summary for Google (under 160 chars) |
| `PLACEHOLDER_CATEGORY` | `EVENT` or `PARTNERSHIP` |
| `PLACEHOLDER_DATE` | e.g. `15 August 2026` |
| `PLACEHOLDER_COVER_IMAGE_URL` | Full URL or path to the cover image |
| `PLACEHOLDER_SHORT_DESCRIPTION` | 1–2 sentence lead paragraph |
| `PLACEHOLDER_PARAGRAPH_*` | Body paragraphs (add or remove as needed) |
| `PLACEHOLDER_GALLERY_IMAGE_*` | Gallery image URLs (delete the gallery block if no images) |

For a **Partnership** post, change the category span to:
```html
<span class="upd-detail-category cat-partnership"><i class="fas fa-tag"></i> PARTNERSHIP</span>
```

### Step 3 — Add the event card to the listing page

Open `events-updates.html` and add a new `<article class="upd-card">` block **at the top** of the `.updates-grid` div (newest first). Copy an existing card and update the image, href, badge, date, title, description, and read-more link.

### Step 4 — Update the homepage (if it's one of the 3 latest)

Open `index.html`, find the `home-events` section, and replace the oldest card with the new one.

### Step 5 — Add images to git

If images are stored locally in `assets/images/events/`, stage them:

```bash
git add assets/images/events/your-new-image.jpg
```

### Step 6 — Commit and push

```bash
git add events/your-event-slug-here.html events-updates.html index.html
git commit -m "Add event: Your Event Title Here"
git push
```

Vercel deploys automatically on every push.

---

## Project Structure

```
/
├── index.html              # Homepage
├── about.html
├── gallery.html
├── events-updates.html     # Events listing (static cards)
├── update-details.html     # Redirects old ?slug= URLs to /events/
├── events/                 # Individual event pages (one file per event)
├── assets/
│   └── images/
│       └── events/         # Store event images here
├── js/                     # Admin JS (Supabase-based, managed separately)
├── admin/                  # Admin panel (managed separately)
├── style.css
├── script.js
├── vercel.json
├── robots.txt
├── sitemap.xml
└── _event-template.html    # Template for new events (gitignored)
```

---

## Contact Form

Submissions go to a Google Apps Script endpoint that:
- Writes a row to the Labourites Leads Google Sheet
- Sends an email notification to info.labourites@gmail.com
