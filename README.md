# 🐻 We Can Bearly Wait — Baby Shower Website

A beautiful, single-page baby shower invitation website for **Ronit Sutaria & Krishna Patel**, deployed via GitHub Pages with RSVP collection powered by Google Sheets.

**Event:** Saturday, August 2nd, 2025 · 9:30 AM – 2:00 PM
**Venue:** Lake Chateau Banquets, 1002 US-9, Woodbridge, NJ 07095
**Theme:** "We Can Bearly Wait" — Teddy Bear Baby Shower 🐻

---

## Features

- Warm, whimsical teddy bear theme with custom SVG illustrations
- Animated floating balloons, sparkles, and botanical accents
- Full invitation card with event details
- RSVP form that saves directly to Google Sheets (no server needed)
- Mobile-first responsive design
- Pure HTML/CSS/JS — no build tools, no dependencies, no frameworks
- Auto-deploys to GitHub Pages on every push

---

## 🚀 Deploy to GitHub Pages

### 1. Push to GitHub

```bash
git init
git add .
git commit -m "Initial baby shower website"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
git push -u origin main
```

### 2. Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** → **Pages** (left sidebar)
3. Under **Source**, select **GitHub Actions**
4. Click Save

### 3. Trigger Deployment

The site deploys automatically on every push to `main`. After your first push, GitHub Actions will build and deploy within ~1 minute.

Your site will be live at:
```
https://YOUR_USERNAME.github.io/YOUR_REPO_NAME/
```

### 4. Wire Up Google Sheets (RSVP)

Follow the step-by-step instructions in **[SETUP.md](./SETUP.md)** to connect the RSVP form to Google Sheets. This takes about 10 minutes and is free.

---

## File Structure

```
/
├── index.html              ← Entire website (HTML + CSS + JS, single file)
├── SETUP.md                ← Google Sheets RSVP setup guide
├── README.md               ← This file
└── .github/
    └── workflows/
        └── deploy.yml      ← GitHub Actions auto-deploy workflow
```

---

## Local Development

No build step needed — just open `index.html` in any browser:

```bash
# macOS / Linux
open index.html

# Windows
start index.html
```

Or serve with any static server:
```bash
npx serve .
# or
python -m http.server 8080
```

---

## Customization

All content is in `index.html`. Key areas to edit:

| What | Where to look |
|------|---------------|
| Party details | `#invitation` section, `.details-grid` |
| RSVP Google Script URL | `const GOOGLE_SCRIPT_URL = '...'` in `<script>` |
| Colors | `:root` CSS variables at the top of `<style>` |
| Copy / wording | Text nodes throughout `<body>` |

---

## Tech Stack

- **HTML5 / CSS3 / Vanilla JS** — zero dependencies
- **Google Fonts** — Playfair Display, Dancing Script, Nunito
- **Google Apps Script** — free serverless RSVP backend
- **Google Sheets** — free RSVP database
- **GitHub Actions** — free CI/CD deployment
- **GitHub Pages** — free hosting

---

*Made with love for our little cub 🍯*
