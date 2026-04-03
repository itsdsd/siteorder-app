# sitebuild.app Website Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a production-ready static marketing website for sitebuild.app — a yearly website-building and management service — deployed to Cloudflare Pages via GitHub.

**Architecture:** Pure HTML/CSS/JS — no build tools, no framework. All pages share one `style.css`. Navigation and footer are duplicated across pages (no server-side includes needed for 3 pages). JS is minimal: sticky nav on scroll + FAQ accordion.

**Tech Stack:** HTML5, CSS3 (custom properties), vanilla JS, Inter font (Google Fonts), Cloudflare Pages, GitHub

---

## File Map

| File | Responsibility |
|------|---------------|
| `index.html` | Landing page — all marketing sections |
| `terms.html` | Terms of Use legal page |
| `privacy.html` | Privacy Policy legal page |
| `style.css` | All shared styles — CSS variables, reset, components |
| `sitemap.xml` | XML sitemap for SEO |
| `robots.txt` | Crawler rules |

---

## Task 1: Base CSS + HTML shell

**Files:**
- Create: `style.css`
- Create: `index.html` (shell only, content added in later tasks)

- [ ] **Step 1: Create `style.css`**

```css
/* ============================================================
   SITEBUILD.APP — Global Styles
   ============================================================ */

@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');

/* --- Variables --- */
:root {
  --bg:           #0A0F1E;
  --bg-card:      #111827;
  --bg-card-2:    #161f30;
  --text:         #FFFFFF;
  --text-muted:   #8B9CB0;
  --accent:       #4F8EF7;
  --accent-hover: #3a7ae8;
  --border:       rgba(255, 255, 255, 0.08);
  --radius:       12px;
  --radius-sm:    8px;
  --max-width:    1100px;
  --nav-height:   64px;
}

/* --- Reset --- */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; }
body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  background: var(--bg);
  color: var(--text);
  line-height: 1.6;
  -webkit-font-smoothing: antialiased;
}
img { display: block; max-width: 100%; }
a { color: inherit; text-decoration: none; }
ul { list-style: none; }

/* --- Layout --- */
.container {
  max-width: var(--max-width);
  margin: 0 auto;
  padding: 0 24px;
}
section { padding: 96px 0; }

/* --- Typography --- */
h1 { font-size: clamp(2.5rem, 6vw, 4rem); font-weight: 800; line-height: 1.1; letter-spacing: -0.02em; }
h2 { font-size: clamp(1.8rem, 4vw, 2.5rem); font-weight: 700; line-height: 1.2; letter-spacing: -0.01em; }
h3 { font-size: 1.2rem; font-weight: 600; }
p  { color: var(--text-muted); font-size: 1.05rem; }

/* --- Buttons --- */
.btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 14px 28px;
  border-radius: var(--radius-sm);
  font-family: inherit;
  font-size: 0.95rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s ease;
  border: none;
  text-decoration: none;
}
.btn-primary {
  background: var(--accent);
  color: #fff;
}
.btn-primary:hover {
  background: var(--accent-hover);
  transform: translateY(-1px);
  box-shadow: 0 8px 24px rgba(79, 142, 247, 0.35);
}
.btn-ghost {
  background: transparent;
  color: var(--text-muted);
  border: 1px solid var(--border);
}
.btn-ghost:hover {
  border-color: var(--accent);
  color: var(--text);
}

/* --- Section headings utility --- */
.section-label {
  display: inline-block;
  font-size: 0.8rem;
  font-weight: 600;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 16px;
}
.section-heading {
  margin-bottom: 16px;
}
.section-sub {
  font-size: 1.1rem;
  max-width: 580px;
  margin-bottom: 56px;
}
.centered { text-align: center; }
.centered .section-sub { margin-left: auto; margin-right: auto; }

/* --- Divider --- */
.divider {
  border: none;
  border-top: 1px solid var(--border);
  margin: 0;
}

/* ============================================================
   NAVIGATION
   ============================================================ */
.nav {
  position: sticky;
  top: 0;
  z-index: 100;
  height: var(--nav-height);
  display: flex;
  align-items: center;
  background: rgba(10, 15, 30, 0.85);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border-bottom: 1px solid transparent;
  transition: border-color 0.3s ease;
}
.nav.scrolled { border-bottom-color: var(--border); }
.nav .container {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.nav-logo {
  font-size: 1.1rem;
  font-weight: 700;
  color: var(--text);
  letter-spacing: -0.02em;
}
.nav-logo span { color: var(--accent); }

/* ============================================================
   HERO
   ============================================================ */
.hero {
  padding: 120px 0 96px;
  text-align: center;
  position: relative;
  overflow: hidden;
}
.hero::before {
  content: '';
  position: absolute;
  top: -200px;
  left: 50%;
  transform: translateX(-50%);
  width: 800px;
  height: 600px;
  background: radial-gradient(ellipse at center, rgba(79, 142, 247, 0.12) 0%, transparent 70%);
  pointer-events: none;
}
.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: rgba(79, 142, 247, 0.1);
  border: 1px solid rgba(79, 142, 247, 0.25);
  border-radius: 100px;
  padding: 6px 16px;
  font-size: 0.85rem;
  font-weight: 500;
  color: var(--accent);
  margin-bottom: 32px;
}
.hero h1 { margin-bottom: 20px; }
.hero-sub {
  font-size: 1.2rem;
  max-width: 520px;
  margin: 0 auto 48px;
  color: var(--text-muted);
}
.hero-ctas {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 16px;
  flex-wrap: wrap;
}
.appstore-btn {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  background: var(--text);
  color: var(--bg);
  padding: 12px 22px;
  border-radius: var(--radius-sm);
  font-weight: 600;
  font-size: 0.95rem;
  transition: all 0.2s ease;
}
.appstore-btn:hover {
  background: #e5e5e5;
  transform: translateY(-1px);
}
.appstore-btn svg { flex-shrink: 0; }
.browser-link {
  font-size: 0.9rem;
  color: var(--text-muted);
  text-decoration: underline;
  text-underline-offset: 3px;
  transition: color 0.2s;
}
.browser-link:hover { color: var(--text); }

/* ============================================================
   HOW IT WORKS
   ============================================================ */
.steps {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
  position: relative;
}
.steps::before {
  content: '';
  position: absolute;
  top: 28px;
  left: calc(16.66% + 12px);
  right: calc(16.66% + 12px);
  height: 1px;
  background: linear-gradient(to right, transparent, var(--border), transparent);
}
.step {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 32px 28px;
  position: relative;
}
.step-number {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: rgba(79, 142, 247, 0.12);
  border: 1px solid rgba(79, 142, 247, 0.3);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.85rem;
  font-weight: 700;
  color: var(--accent);
  margin-bottom: 20px;
}
.step h3 { margin-bottom: 8px; }
.step p { font-size: 0.95rem; }

/* ============================================================
   WHAT'S INCLUDED
   ============================================================ */
.included-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 16px;
}
.included-item {
  display: flex;
  align-items: flex-start;
  gap: 16px;
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 24px;
  transition: border-color 0.2s;
}
.included-item:hover { border-color: rgba(79, 142, 247, 0.3); }
.included-icon {
  width: 40px;
  height: 40px;
  border-radius: var(--radius-sm);
  background: rgba(79, 142, 247, 0.1);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  color: var(--accent);
}
.included-item h3 { margin-bottom: 4px; font-size: 1rem; }
.included-item p { font-size: 0.9rem; }

/* ============================================================
   PRICING
   ============================================================ */
.pricing-section { background: var(--bg-card-2); }
.pricing-card {
  max-width: 480px;
  margin: 0 auto;
  background: var(--bg-card);
  border: 1px solid rgba(79, 142, 247, 0.3);
  border-radius: 16px;
  padding: 48px 40px;
  text-align: center;
  box-shadow: 0 0 60px rgba(79, 142, 247, 0.08);
}
.pricing-badge {
  display: inline-block;
  background: rgba(79, 142, 247, 0.15);
  border: 1px solid rgba(79, 142, 247, 0.3);
  border-radius: 100px;
  padding: 4px 14px;
  font-size: 0.78rem;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 24px;
}
.pricing-old {
  font-size: 1.1rem;
  color: var(--text-muted);
  text-decoration: line-through;
  margin-bottom: 4px;
}
.pricing-price {
  font-size: 3.5rem;
  font-weight: 800;
  color: var(--text);
  letter-spacing: -0.03em;
  line-height: 1;
  margin-bottom: 4px;
}
.pricing-period {
  font-size: 0.9rem;
  color: var(--text-muted);
  margin-bottom: 32px;
}
.pricing-features {
  text-align: left;
  margin-bottom: 36px;
}
.pricing-feature {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 10px 0;
  border-bottom: 1px solid var(--border);
  font-size: 0.95rem;
}
.pricing-feature:last-child { border-bottom: none; }
.check-icon {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: rgba(79, 142, 247, 0.15);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  color: var(--accent);
}
.pricing-card .btn { width: 100%; justify-content: center; }

/* ============================================================
   SAMPLE WEBSITES (placeholder)
   ============================================================ */
.samples-placeholder {
  border: 1px dashed var(--border);
  border-radius: var(--radius);
  padding: 64px;
  text-align: center;
  color: var(--text-muted);
}
.samples-placeholder p { font-size: 1rem; }

/* ============================================================
   FAQ
   ============================================================ */
.faq-list { max-width: 720px; margin: 0 auto; }
.faq-item {
  border-bottom: 1px solid var(--border);
}
.faq-question {
  width: 100%;
  background: none;
  border: none;
  color: var(--text);
  font-family: inherit;
  font-size: 1rem;
  font-weight: 600;
  text-align: left;
  padding: 24px 0;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 16px;
  transition: color 0.2s;
}
.faq-question:hover { color: var(--accent); }
.faq-icon {
  flex-shrink: 0;
  width: 20px;
  height: 20px;
  position: relative;
  transition: transform 0.3s ease;
}
.faq-icon::before,
.faq-icon::after {
  content: '';
  position: absolute;
  background: currentColor;
  border-radius: 2px;
}
.faq-icon::before { width: 12px; height: 2px; top: 9px; left: 4px; }
.faq-icon::after  { width: 2px; height: 12px; top: 4px; left: 9px; transition: transform 0.3s ease; }
.faq-item.open .faq-icon::after { transform: rotate(90deg); }
.faq-answer {
  overflow: hidden;
  max-height: 0;
  transition: max-height 0.3s ease;
}
.faq-answer p {
  padding-bottom: 24px;
  font-size: 0.95rem;
  line-height: 1.7;
}

/* ============================================================
   FOOTER
   ============================================================ */
.footer {
  background: var(--bg-card);
  border-top: 1px solid var(--border);
  padding: 40px 0;
}
.footer-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 16px;
}
.footer-copy { font-size: 0.85rem; color: var(--text-muted); }
.footer-links { display: flex; align-items: center; gap: 24px; }
.footer-links a {
  font-size: 0.85rem;
  color: var(--text-muted);
  transition: color 0.2s;
}
.footer-links a:hover { color: var(--text); }

/* ============================================================
   LEGAL PAGES
   ============================================================ */
.legal-page { padding: 80px 0; }
.legal-page h1 { font-size: 2rem; margin-bottom: 8px; }
.legal-page .legal-date { color: var(--text-muted); font-size: 0.9rem; margin-bottom: 48px; }
.legal-content h2 { font-size: 1.2rem; margin-top: 40px; margin-bottom: 12px; }
.legal-content p { margin-bottom: 16px; line-height: 1.75; }
.legal-content ul { padding-left: 20px; margin-bottom: 16px; }
.legal-content ul li { color: var(--text-muted); margin-bottom: 8px; font-size: 1.05rem; list-style: disc; }
.legal-content a { color: var(--accent); text-decoration: underline; }

/* ============================================================
   RESPONSIVE
   ============================================================ */
@media (max-width: 768px) {
  section { padding: 64px 0; }
  .steps { grid-template-columns: 1fr; }
  .steps::before { display: none; }
  .included-grid { grid-template-columns: 1fr; }
  .pricing-card { padding: 36px 24px; }
  .footer-inner { flex-direction: column; align-items: flex-start; }
  .samples-placeholder { padding: 40px 24px; }
}
```

- [ ] **Step 2: Create `index.html` shell**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>sitebuild.app — Your Website, Live in 48 Hours</title>
  <meta name="description" content="Professional website design, hosting, and management for $129/year. Order from your iPhone and go live in 48 hours.">
  <link rel="canonical" href="https://sitebuild.app/">
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <!-- NAV -->
  <!-- HERO -->
  <!-- HOW IT WORKS -->
  <!-- WHAT'S INCLUDED -->
  <!-- PRICING -->
  <!-- SAMPLE WEBSITES -->
  <!-- FAQ -->
  <!-- FOOTER -->

  <script src="main.js"></script>
</body>
</html>
```

- [ ] **Step 3: Create `main.js`**

```js
// Sticky nav border on scroll
const nav = document.querySelector('.nav');
window.addEventListener('scroll', () => {
  nav.classList.toggle('scrolled', window.scrollY > 8);
});

// FAQ accordion
document.querySelectorAll('.faq-question').forEach(btn => {
  btn.addEventListener('click', () => {
    const item = btn.closest('.faq-item');
    const answer = item.querySelector('.faq-answer');
    const isOpen = item.classList.contains('open');

    // Close all
    document.querySelectorAll('.faq-item').forEach(i => {
      i.classList.remove('open');
      i.querySelector('.faq-answer').style.maxHeight = null;
    });

    // Open clicked (if it was closed)
    if (!isOpen) {
      item.classList.add('open');
      answer.style.maxHeight = answer.scrollHeight + 'px';
    }
  });
});
```

- [ ] **Step 4: Open `index.html` in browser and verify styles load (Inter font, navy background, no errors in console)**

- [ ] **Step 5: Commit**

```bash
git add style.css index.html main.js
git commit -m "feat: base CSS, HTML shell, and JS scaffold"
```

---

## Task 2: Navigation + Hero section

**Files:**
- Modify: `index.html` (fill in NAV and HERO comments)

- [ ] **Step 1: Replace `<!-- NAV -->` in index.html**

```html
  <!-- NAV -->
  <nav class="nav">
    <div class="container">
      <a href="/" class="nav-logo">sitebuild<span>.app</span></a>
      <a href="#" class="btn btn-primary" id="nav-cta">Get the App</a>
    </div>
  </nav>
```

- [ ] **Step 2: Replace `<!-- HERO -->` in index.html**

```html
  <!-- HERO -->
  <section class="hero">
    <div class="container">
      <div class="hero-badge">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><polyline points="20 6 9 17 4 12"/></svg>
        Limited-time offer — save $120/year
      </div>
      <h1>Your website,<br>live in 48 hours.</h1>
      <p class="hero-sub">We design, build, and manage your website for $129/year. No tech skills needed — just tell us what you need.</p>
      <div class="hero-ctas">
        <a href="#" class="appstore-btn" id="appstore-link">
          <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M18.71 19.5c-.83 1.24-1.71 2.45-3.05 2.47-1.34.03-1.77-.79-3.29-.79-1.53 0-2 .77-3.27.82-1.31.05-2.3-1.32-3.14-2.53C4.25 17 2.94 12.45 4.7 9.39c.87-1.52 2.43-2.48 4.12-2.51 1.28-.02 2.5.87 3.29.87.78 0 2.26-1.07 3.8-.91.65.03 2.47.26 3.64 1.98-.09.06-2.17 1.28-2.15 3.81.03 3.02 2.65 4.03 2.68 4.04-.03.07-.42 1.44-1.38 2.83M13 3.5c.73-.83 1.94-1.46 2.94-1.5.13 1.17-.34 2.35-1.04 3.19-.69.85-1.83 1.51-2.95 1.42-.15-1.15.41-2.35 1.05-3.11z"/></svg>
          Download on the App Store
        </a>
        <a href="mailto:hello@sitebuild.app" class="browser-link">Continue on Browser →</a>
      </div>
    </div>
  </section>
```

- [ ] **Step 3: Verify in browser — hero renders with glow, badge, headline, two CTAs correctly stacked**

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add navigation and hero section"
```

---

## Task 3: How It Works + What's Included sections

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Replace `<!-- HOW IT WORKS -->` in index.html**

```html
  <!-- HOW IT WORKS -->
  <hr class="divider">
  <section id="how-it-works">
    <div class="container">
      <div class="centered">
        <span class="section-label">Simple process</span>
        <h2 class="section-heading">How it works</h2>
        <p class="section-sub">Three steps from idea to a live, managed website.</p>
      </div>
      <div class="steps">
        <div class="step">
          <div class="step-number">1</div>
          <h3>Place your order</h3>
          <p>Download the app, fill in your details — what you do, your style, your content. Upload your logo and images.</p>
        </div>
        <div class="step">
          <div class="step-number">2</div>
          <h3>We build it in 48hrs</h3>
          <p>Our team gets to work immediately. You'll receive a preview link within 48 hours, ready to review.</p>
        </div>
        <div class="step">
          <div class="step-number">3</div>
          <h3>Your site goes live</h3>
          <p>Approve the preview, we publish it. Your site is live and we handle hosting and small updates year-round.</p>
        </div>
      </div>
    </div>
  </section>
```

- [ ] **Step 2: Replace `<!-- WHAT'S INCLUDED -->` in index.html**

```html
  <!-- WHAT'S INCLUDED -->
  <hr class="divider">
  <section id="included">
    <div class="container">
      <span class="section-label">Everything you need</span>
      <h2 class="section-heading">What's included</h2>
      <p class="section-sub">One flat price. No hidden fees. Everything to get you online and keep you there.</p>
      <div class="included-grid">
        <div class="included-item">
          <div class="included-icon">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="18" height="18" rx="2"/><path d="M3 9h18M9 21V9"/></svg>
          </div>
          <div>
            <h3>Custom website design &amp; build</h3>
            <p>A unique, professionally designed site built to match your brand — not a template.</p>
          </div>
        </div>
        <div class="included-item">
          <div class="included-icon">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>
          </div>
          <div>
            <h3>Hosting management</h3>
            <p>We handle the server, security, and uptime. Your site just works, all year long.</p>
          </div>
        </div>
        <div class="included-item">
          <div class="included-icon">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"/><path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"/></svg>
          </div>
          <div>
            <h3>Small edits included</h3>
            <p>Need to update your hours, swap a photo, or tweak your copy? Just ask — we'll handle it.</p>
          </div>
        </div>
        <div class="included-item">
          <div class="included-icon">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="1 4 1 10 7 10"/><path d="M3.51 15a9 9 0 1 0 .49-4.5"/></svg>
          </div>
          <div>
            <h3>1 revision after delivery</h3>
            <p>Not quite right? One full round of revisions is included. We'll get it perfect.</p>
          </div>
        </div>
        <div class="included-item">
          <div class="included-icon">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><line x1="2" y1="12" x2="22" y2="12"/><path d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"/></svg>
          </div>
          <div>
            <h3>Domain registration (+$20)</h3>
            <p>Need a domain? We'll register and connect it for a one-time $20 add-on.</p>
          </div>
        </div>
        <div class="included-item">
          <div class="included-icon">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07A19.5 19.5 0 0 1 4.69 12a19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 3.6 1.2h3a2 2 0 0 1 2 1.72c.127.96.361 1.903.7 2.81a2 2 0 0 1-.45 2.11L7.91 8.81a16 16 0 0 0 6.29 6.29l.96-.96a2 2 0 0 1 2.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0 1 22 16.92z"/></svg>
          </div>
          <div>
            <h3>48-hour delivery guarantee</h3>
            <p>We commit to delivering your preview within 48 hours of your order — no exceptions.</p>
          </div>
        </div>
      </div>
    </div>
  </section>
```

- [ ] **Step 3: Verify in browser — 3-step cards render with numbered circles and connector line; 6 included items in 2-column grid**

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add how it works and what's included sections"
```

---

## Task 4: Pricing + Sample Websites placeholder

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Replace `<!-- PRICING -->` in index.html**

```html
  <!-- PRICING -->
  <section class="pricing-section" id="pricing">
    <div class="container centered">
      <span class="section-label">Pricing</span>
      <h2 class="section-heading">Simple, flat pricing</h2>
      <p class="section-sub">One plan. Everything included. Cancel anytime.</p>
      <div class="pricing-card">
        <div class="pricing-badge">Limited Offer</div>
        <p class="pricing-old">$249/year</p>
        <div class="pricing-price">$129</div>
        <p class="pricing-period">per year &nbsp;·&nbsp; renews annually</p>
        <ul class="pricing-features">
          <li class="pricing-feature">
            <span class="check-icon"><svg width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3"><polyline points="20 6 9 17 4 12"/></svg></span>
            Custom website design &amp; build
          </li>
          <li class="pricing-feature">
            <span class="check-icon"><svg width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3"><polyline points="20 6 9 17 4 12"/></svg></span>
            Hosting management included
          </li>
          <li class="pricing-feature">
            <span class="check-icon"><svg width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3"><polyline points="20 6 9 17 4 12"/></svg></span>
            Small edits throughout the year
          </li>
          <li class="pricing-feature">
            <span class="check-icon"><svg width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3"><polyline points="20 6 9 17 4 12"/></svg></span>
            1 revision after delivery
          </li>
          <li class="pricing-feature">
            <span class="check-icon"><svg width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3"><polyline points="20 6 9 17 4 12"/></svg></span>
            48-hour delivery guarantee
          </li>
          <li class="pricing-feature">
            <span class="check-icon"><svg width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3"><polyline points="20 6 9 17 4 12"/></svg></span>
            Domain registration add-on (+$20)
          </li>
        </ul>
        <a href="#" class="btn btn-primary" id="pricing-cta">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M18.71 19.5c-.83 1.24-1.71 2.45-3.05 2.47-1.34.03-1.77-.79-3.29-.79-1.53 0-2 .77-3.27.82-1.31.05-2.3-1.32-3.14-2.53C4.25 17 2.94 12.45 4.7 9.39c.87-1.52 2.43-2.48 4.12-2.51 1.28-.02 2.5.87 3.29.87.78 0 2.26-1.07 3.8-.91.65.03 2.47.26 3.64 1.98-.09.06-2.17 1.28-2.15 3.81.03 3.02 2.65 4.03 2.68 4.04-.03.07-.42 1.44-1.38 2.83M13 3.5c.73-.83 1.94-1.46 2.94-1.5.13 1.17-.34 2.35-1.04 3.19-.69.85-1.83 1.51-2.95 1.42-.15-1.15.41-2.35 1.05-3.11z"/></svg>
          Get the App
        </a>
      </div>
    </div>
  </section>
```

- [ ] **Step 2: Replace `<!-- SAMPLE WEBSITES -->` in index.html**

```html
  <!-- SAMPLE WEBSITES -->
  <hr class="divider">
  <section id="samples">
    <div class="container">
      <div class="centered">
        <span class="section-label">Portfolio</span>
        <h2 class="section-heading">See what we build</h2>
        <p class="section-sub">Real websites, built and delivered for our customers.</p>
      </div>
      <div class="samples-placeholder">
        <p>Sample websites coming soon</p>
      </div>
    </div>
  </section>
```

- [ ] **Step 3: Verify in browser — pricing card renders centered with strikethrough old price, feature list with check icons, and blue CTA button**

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add pricing card and sample websites placeholder"
```

---

## Task 5: FAQ + Footer

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Replace `<!-- FAQ -->` in index.html**

```html
  <!-- FAQ -->
  <hr class="divider">
  <section id="faq">
    <div class="container">
      <div class="centered">
        <span class="section-label">Questions</span>
        <h2 class="section-heading">Frequently asked</h2>
      </div>
      <div class="faq-list">

        <div class="faq-item">
          <button class="faq-question">
            What's included in the $129/year plan?
            <span class="faq-icon"></span>
          </button>
          <div class="faq-answer">
            <p>Everything you need to get online: a custom-designed and built website, hosting management, small edits throughout the year, and one full revision after delivery. Domain registration is available as an add-on for $20.</p>
          </div>
        </div>

        <div class="faq-item">
          <button class="faq-question">
            How does the 48-hour delivery work?
            <span class="faq-icon"></span>
          </button>
          <div class="faq-answer">
            <p>Once you submit your order through the app, our team starts building immediately. You'll receive a preview link within 48 hours. Review it, request your revision if needed, then we publish it live.</p>
          </div>
        </div>

        <div class="faq-item">
          <button class="faq-question">
            What if I need changes after delivery?
            <span class="faq-icon"></span>
          </button>
          <div class="faq-answer">
            <p>Every order includes one revision round after delivery — just let us know what to change and we'll update it within 48 hours. For ongoing small edits (text updates, image swaps, etc.), those are included in your yearly plan. Large redesigns are scoped separately.</p>
          </div>
        </div>

        <div class="faq-item">
          <button class="faq-question">
            Do I need to provide a domain?
            <span class="faq-icon"></span>
          </button>
          <div class="faq-answer">
            <p>If you already have a domain, we'll connect your site to it. If you need one, we can register it for a one-time add-on of $20. Just select the domain option when placing your order.</p>
          </div>
        </div>

        <div class="faq-item">
          <button class="faq-question">
            What happens when my year ends?
            <span class="faq-icon"></span>
          </button>
          <div class="faq-answer">
            <p>Your plan renews automatically each year at the standard rate. You can cancel at any time — your site will remain live until the end of your paid period. We'll always notify you before any renewal.</p>
          </div>
        </div>

      </div>
    </div>
  </section>
```

- [ ] **Step 2: Replace `<!-- FOOTER -->` in index.html**

```html
  <!-- FOOTER -->
  <footer class="footer">
    <div class="container">
      <div class="footer-inner">
        <p class="footer-copy">&copy; 2026 sitebuild.app · All rights reserved</p>
        <div class="footer-links">
          <a href="terms.html">Terms of Use</a>
          <a href="privacy.html">Privacy Policy</a>
          <a href="mailto:hello@sitebuild.app">hello@sitebuild.app</a>
        </div>
      </div>
    </div>
  </footer>
```

- [ ] **Step 3: Verify in browser — FAQ accordion opens/closes correctly, footer links are visible**

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add FAQ accordion and footer"
```

---

## Task 6: Terms of Use page

**Files:**
- Create: `terms.html`

- [ ] **Step 1: Create `terms.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Terms of Use — sitebuild.app</title>
  <meta name="robots" content="noindex">
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <nav class="nav">
    <div class="container">
      <a href="/" class="nav-logo">sitebuild<span>.app</span></a>
      <a href="/#pricing" class="btn btn-primary">Get the App</a>
    </div>
  </nav>

  <main class="legal-page">
    <div class="container">
      <h1>Terms of Use</h1>
      <p class="legal-date">Last updated: April 3, 2026</p>

      <div class="legal-content">
        <p>By placing an order through sitebuild.app or our iOS application, you agree to the following terms. Please read them carefully before purchasing.</p>

        <h2>1. Service Description</h2>
        <p>sitebuild.app provides a website design, build, and management service. Upon placing an order, we will design and deliver a custom website within 48 hours. Your subscription includes hosting management and the ability to request small edits throughout your subscription period.</p>

        <h2>2. Payment &amp; Subscription</h2>
        <p>The service is billed annually at $129/year. Subscriptions renew automatically at the end of each billing period unless cancelled. The current promotional price is not guaranteed to apply to renewals — you will be notified of any price changes before renewal.</p>
        <p>Payments are processed through Apple In-App Purchase (iOS app). All billing is subject to Apple's payment terms.</p>

        <h2>3. Domain Add-On</h2>
        <p>Domain registration is an optional one-time add-on for $20. This covers the registration of a single domain for one year. Domain renewals are the responsibility of the customer after the first year unless otherwise agreed.</p>

        <h2>4. Delivery</h2>
        <p>We commit to delivering a preview of your website within 48 hours of order submission. This timeline assumes you have provided all required information at the time of ordering. Delays caused by incomplete information or delayed responses from the customer may extend the delivery window.</p>

        <h2>5. Revisions</h2>
        <p>Each order includes one revision round after the initial delivery. A revision is defined as a set of feedback items submitted within 48 hours of receiving your preview. We will implement reasonable revision requests within 48 hours. Additional revision rounds beyond the included one may be subject to additional charges.</p>

        <h2>6. Ongoing Edits</h2>
        <p>Small edits (text updates, image replacements, minor layout adjustments) are included throughout your subscription period. We reserve the right to determine what constitutes a "small edit." Substantial redesigns or new page builds are outside the scope of included edits.</p>

        <h2>7. Cancellation &amp; Refunds</h2>
        <p>You may cancel your subscription at any time. Cancellation takes effect at the end of the current billing period. We do not offer refunds for partial subscription periods. If your website has not been delivered within 72 hours of order submission (excluding delays caused by missing information from you), you may request a full refund by contacting us at <a href="mailto:hello@sitebuild.app">hello@sitebuild.app</a>.</p>

        <h2>8. Intellectual Property</h2>
        <p>Upon full payment, you own the content and design of your delivered website. sitebuild.app retains the right to display completed work in our portfolio unless you request otherwise in writing.</p>

        <h2>9. Limitation of Liability</h2>
        <p>sitebuild.app is not liable for any indirect, incidental, or consequential damages arising from use of our service. Our total liability is limited to the amount paid by you in the current subscription period.</p>

        <h2>10. Changes to These Terms</h2>
        <p>We may update these terms at any time. Continued use of the service after changes constitutes acceptance of the updated terms. We will notify active subscribers of material changes.</p>

        <h2>11. Contact</h2>
        <p>For questions about these terms, contact us at <a href="mailto:hello@sitebuild.app">hello@sitebuild.app</a>.</p>
      </div>
    </div>
  </main>

  <footer class="footer">
    <div class="container">
      <div class="footer-inner">
        <p class="footer-copy">&copy; 2026 sitebuild.app · All rights reserved</p>
        <div class="footer-links">
          <a href="terms.html">Terms of Use</a>
          <a href="privacy.html">Privacy Policy</a>
          <a href="mailto:hello@sitebuild.app">hello@sitebuild.app</a>
        </div>
      </div>
    </div>
  </footer>

</body>
</html>
```

- [ ] **Step 2: Open `terms.html` in browser — verify nav, readable legal content, footer**

- [ ] **Step 3: Commit**

```bash
git add terms.html
git commit -m "feat: add terms of use page"
```

---

## Task 7: Privacy Policy page

**Files:**
- Create: `privacy.html`

- [ ] **Step 1: Create `privacy.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Privacy Policy — sitebuild.app</title>
  <meta name="robots" content="noindex">
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <nav class="nav">
    <div class="container">
      <a href="/" class="nav-logo">sitebuild<span>.app</span></a>
      <a href="/#pricing" class="btn btn-primary">Get the App</a>
    </div>
  </nav>

  <main class="legal-page">
    <div class="container">
      <h1>Privacy Policy</h1>
      <p class="legal-date">Last updated: April 3, 2026</p>

      <div class="legal-content">
        <p>This Privacy Policy explains how sitebuild.app ("we", "us", "our") collects, uses, and protects your personal information when you use our website or iOS application.</p>

        <h2>1. Information We Collect</h2>
        <p>When you place an order or contact us, we may collect:</p>
        <ul>
          <li>Your name and email address</li>
          <li>Your business name and website requirements</li>
          <li>Images, logos, and other files you upload as part of your order</li>
          <li>Payment information (processed by Apple — we do not store card details)</li>
          <li>Communications between you and our team</li>
        </ul>

        <h2>2. How We Use Your Information</h2>
        <p>We use your information solely to:</p>
        <ul>
          <li>Build and deliver your website</li>
          <li>Communicate with you about your order and revisions</li>
          <li>Manage your hosting and ongoing edits</li>
          <li>Send service-related notifications (e.g. renewal reminders)</li>
        </ul>
        <p>We do not sell, rent, or share your personal information with third parties for marketing purposes.</p>

        <h2>3. File Storage</h2>
        <p>Files you upload (logos, images, content) are stored securely and used only to build and maintain your website. We retain these files for the duration of your subscription plus 30 days after cancellation, after which they are deleted.</p>

        <h2>4. Third-Party Services</h2>
        <p>We use the following third-party services:</p>
        <ul>
          <li><strong>Apple In-App Purchase</strong> — payment processing. Subject to Apple's Privacy Policy.</li>
          <li><strong>Cloudflare</strong> — hosting and CDN for delivered websites.</li>
          <li><strong>Firebase</strong> — order management and file storage within our iOS app.</li>
        </ul>

        <h2>5. Data Security</h2>
        <p>We take reasonable technical and organisational measures to protect your information. However, no method of transmission over the internet is 100% secure.</p>

        <h2>6. Your Rights</h2>
        <p>You may request to access, correct, or delete your personal data at any time by emailing <a href="mailto:hello@sitebuild.app">hello@sitebuild.app</a>. We will respond within 14 days.</p>

        <h2>7. Cookies</h2>
        <p>Our marketing website (sitebuild.app) does not use tracking cookies or analytics at this time.</p>

        <h2>8. Children's Privacy</h2>
        <p>Our service is not directed at children under 13. We do not knowingly collect personal information from children.</p>

        <h2>9. Changes to This Policy</h2>
        <p>We may update this policy from time to time. We will notify active users of material changes by email. Continued use of the service constitutes acceptance of the updated policy.</p>

        <h2>10. Contact</h2>
        <p>For privacy-related questions or requests, contact us at <a href="mailto:hello@sitebuild.app">hello@sitebuild.app</a>.</p>
      </div>
    </div>
  </main>

  <footer class="footer">
    <div class="container">
      <div class="footer-inner">
        <p class="footer-copy">&copy; 2026 sitebuild.app · All rights reserved</p>
        <div class="footer-links">
          <a href="terms.html">Terms of Use</a>
          <a href="privacy.html">Privacy Policy</a>
          <a href="mailto:hello@sitebuild.app">hello@sitebuild.app</a>
        </div>
      </div>
    </div>
  </footer>

</body>
</html>
```

- [ ] **Step 2: Open `privacy.html` in browser — verify it matches the terms page style**

- [ ] **Step 3: Commit**

```bash
git add privacy.html
git commit -m "feat: add privacy policy page"
```

---

## Task 8: sitemap.xml + robots.txt

**Files:**
- Create: `sitemap.xml`
- Create: `robots.txt`

- [ ] **Step 1: Create `sitemap.xml`**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://sitebuild.app/</loc>
    <changefreq>monthly</changefreq>
    <priority>1.0</priority>
  </url>
  <url>
    <loc>https://sitebuild.app/terms.html</loc>
    <changefreq>yearly</changefreq>
    <priority>0.3</priority>
  </url>
  <url>
    <loc>https://sitebuild.app/privacy.html</loc>
    <changefreq>yearly</changefreq>
    <priority>0.3</priority>
  </url>
</urlset>
```

- [ ] **Step 2: Create `robots.txt`**

```
User-agent: *
Allow: /
Disallow:

Sitemap: https://sitebuild.app/sitemap.xml
```

- [ ] **Step 3: Commit**

```bash
git add sitemap.xml robots.txt
git commit -m "feat: add sitemap.xml and robots.txt"
```

---

## Task 9: GitHub repo + Cloudflare Pages

**Files:** None — deployment configuration only.

- [ ] **Step 1: Create GitHub repo**

```bash
cd "/Users/dsd/Documents/Claude Folder/sitebuild-app"
gh repo create itsdsd/sitebuild-app --public --source=. --remote=origin --push
```

Expected output: repo URL printed, all commits pushed.

- [ ] **Step 2: Connect to Cloudflare Pages**

1. Go to Cloudflare Dashboard → Workers & Pages → Create application → Pages
2. Connect to Git → select `itsdsd/sitebuild-app`
3. Settings:
   - **Framework preset:** None
   - **Build command:** *(leave empty)*
   - **Build output directory:** `/`
4. Click "Save and Deploy"
5. Wait for deployment to complete — note the `*.pages.dev` preview URL

- [ ] **Step 3: Add custom domain**

1. In Cloudflare Pages → your project → Custom domains
2. Add `sitebuild.app`
3. Follow DNS instructions (add CNAME record pointing to Pages)
4. Wait for SSL to provision (usually under 5 minutes)

- [ ] **Step 4: Verify live site**

Open `https://sitebuild.app` — verify:
- All sections render correctly
- FAQ accordion works
- "Continue on Browser" link opens mail client to hello@sitebuild.app
- Footer links go to terms.html and privacy.html
- Mobile layout at 375px width looks correct

- [ ] **Step 5: Final commit (update any placeholder App Store link if available)**

```bash
git add -A
git commit -m "chore: final pre-launch check"
git push
```
