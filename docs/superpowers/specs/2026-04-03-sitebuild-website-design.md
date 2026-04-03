# sitebuild.app — Website Design Spec
**Date:** 2026-04-03  
**Status:** Approved

---

## Overview

Marketing website for sitebuild.app — a yearly website building and management service. Primary goal: drive iOS app downloads. Secondary: allow users to reach out via email if they prefer not to use the app.

**Service details:**
- $129/year (discounted from $249)
- Custom website built and delivered within 48 hours
- Includes: build, hosting management, small edits
- 1 revision included after delivery
- Domain add-on: +$20

---

## Tech Stack

- **Pure HTML/CSS/JS** — no build tools, no framework
- **Deployment:** Cloudflare Pages via GitHub
- **Form handling:** Deferred (web order form will be synced with iOS app later)
- **Font:** Inter (Google Fonts)

---

## Pages

| File | Purpose |
|------|---------|
| `index.html` | Main landing page |
| `terms.html` | Terms of Use |
| `privacy.html` | Privacy Policy |
| `sitemap.xml` | XML sitemap |
| `robots.txt` | Search crawler rules |
| `style.css` | Shared styles |

---

## Landing Page Sections (index.html)

### 1. Navigation
- Logo (left)
- "Get the App" button (right, primary color)
- Minimal, sticky on scroll

### 2. Hero
- Bold headline (e.g. "Your website, live in 48 hours.")
- Subheadline highlighting the value: professional build + ongoing management, $129/year
- Primary CTA: App Store badge (links to iOS app — placeholder until app is live)
- Secondary CTA: "Continue on Browser" — opens `mailto:hello@sitebuild.app`
- Clean, full-width layout with visual weight on the headline

### 3. How It Works
- 3-step visual flow:
  1. **Order** — fill out your details in the app
  2. **We Build** — your site is ready within 48 hours
  3. **Go Live** — your site is published and managed for you

### 4. What's Included
- Icon list:
  - Custom website design & build
  - Hosting management
  - Small edits as needed
  - 1 revision after delivery
  - Domain registration available (+$20)

### 5. Pricing
- Single pricing card
- ~~$249/year~~ → **$129/year**
- Bullet list of inclusions
- CTA button: "Get the App"

### 6. Sample Websites
- Placeholder section: "Coming soon — see what we've built"
- Will be populated with real examples after launch

### 7. FAQ
Suggested questions:
1. What's included in the $129/year plan?
2. How does the 48-hour delivery work?
3. What if I need changes after delivery?
4. Do I need to provide a domain?
5. What happens when my year ends?

### 8. Footer
- Copyright line
- Links: Terms of Use · Privacy Policy
- Email: hello@sitebuild.app

---

## Visual Design

- **Background:** Deep navy (#0A0F1E)
- **Text:** White / light grey
- **Accent:** Electric blue (#4F8EF7)
- **Font:** Inter (400, 600, 700)
- **Style:** Clean, premium SaaS — trustworthy and modern
- **Note:** Exact palette may be adjusted after seeing rendered output

---

## Legal Pages

### Terms of Use (terms.html)
Covers: service description, payment terms, revision policy, domain add-on policy, cancellation/refund policy, limitation of liability.

### Privacy Policy (privacy.html)
Covers: data collected (name, email, business info, uploaded files), how it's used (to deliver the service), no third-party selling, contact for data requests.

---

## SEO & Crawl Files

### sitemap.xml
Lists: index.html, terms.html, privacy.html

### robots.txt
```
User-agent: *
Allow: /
Sitemap: https://sitebuild.app/sitemap.xml
```

---

## Out of Scope (Deferred)

- **Web order form** — will be built later, synced with iOS app form fields
- **Sample websites gallery** — placeholder only at launch
- **iOS app** — App Store link is a placeholder until app is submitted

---

## Deployment

1. Create GitHub repo: `itsdsd/sitebuild-app`
2. Connect to Cloudflare Pages
3. Build command: none (static)
4. Output directory: `/` (root)
