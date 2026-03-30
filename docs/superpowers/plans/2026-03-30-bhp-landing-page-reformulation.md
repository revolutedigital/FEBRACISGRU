# BHP Landing Page Reformulation — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Complete rewrite of the BHP landing page with new copy, design, and sections while preserving form integrations and video.

**Architecture:** Single HTML file (`bhp/index.html`) with all CSS in `<style>` and JS in `<script>`. No build tools, no external dependencies beyond Google Fonts. Images served from `bhp/img/`.

**Tech Stack:** HTML5, CSS3 (custom properties, grid, flexbox), vanilla JavaScript, Google Fonts (Montserrat), inline SVG icons.

**Spec:** `docs/superpowers/specs/2026-03-30-bhp-landing-page-reformulation-design.md`

---

## File Structure

| File | Action | Responsibility |
|------|--------|----------------|
| `bhp/index.html` | Rewrite | Entire landing page (HTML + CSS + JS) |
| `bhp/img/` | Create dir | Image assets copied from `bhp/reformulation/Imagens/` |

---

## Task 1: Setup — Copy images and create HTML skeleton

**Files:**
- Create: `bhp/img/` (copy images from `bhp/reformulation/Imagens/`)
- Create: `bhp/index.html` (skeleton with `<head>`, CSS variables, base styles)

- [ ] **Step 1: Copy image assets to `bhp/img/`**

```bash
mkdir -p bhp/img
cp bhp/reformulation/Imagens/*.webp bhp/img/
```

- [ ] **Step 2: Write HTML skeleton with `<head>`, meta tags, Google Fonts, GTM, Schema.org, CSS reset, variables, typography, and layout base styles**

Create `bhp/index.html` with:
- `<!DOCTYPE html>`, `<html lang="pt-BR">`
- `<head>`: charset, viewport, title, meta description, OG tags, Twitter card, favicon, Google Fonts (Montserrat 400/500/700/800 with print/onload swap), Schema.org JSON-LD (Event type with dates 2026-06-24 to 2026-06-26), GTM via Stape proxy
- `<style>`: CSS reset, `:root` variables (full color palette from spec), `html`/`body` base, `.container` (max-width 1200px), `.section` (padding 80-100px desktop, 60px mobile), typography classes, `.btn-primary` (gold gradient CTA with pulse animation), `.reveal` (fade-in-up animation), scroll progress bar styles
- `<body>`: GTM noscript, skip link, empty sections as comments (placeholders for each section), empty `<script>` block
- Responsive breakpoints: mobile-first with `@media (min-width: 768px)` and `@media (min-width: 1024px)`

Key CSS to include:
- Top alert bar styles (fixed, red gradient, z-index 10003)
- Hero video background styles (absolute, object-fit cover, overlay)
- Card base styles (bg-card, border-subtle, border-radius 12px, hover translateY)
- CTA button styles (gradient-gold, dark text, border-radius 8px, pulse @keyframes)
- Section alternating backgrounds (odd: bg-primary, even: bg-secondary)
- Scroll progress bar (fixed top, 3px height, gold, z-index 10002)
- `.reveal` animation (opacity 0, translateY 30px -> visible state)

- [ ] **Step 3: Verify skeleton opens in browser with correct fonts loading and dark background**

Open `bhp/index.html` in browser. Confirm:
- Dark background (#0B1A2E) renders
- Montserrat font loads (check Network tab)
- No console errors
- Scroll progress bar visible at top

- [ ] **Step 4: Commit**

```bash
git add bhp/img/ bhp/index.html
git commit -m "BHP reformulation: setup skeleton with CSS, fonts, and image assets"
```

---

## Task 2: Top Alert Bar + Hero Section

**Files:**
- Modify: `bhp/index.html`

- [ ] **Step 1: Add Top Alert Bar HTML**

Fixed bar at top with text: "Vagas Limitadas — 24 a 26 de Junho 2026 — Guarulhos, SP"
Red gradient background, uppercase, small font, z-index 10003.
Add `padding-top` to `<body>` to offset the fixed bar height.

- [ ] **Step 2: Add Hero section HTML**

Structure:
```
<section class="hero" id="hero">
  <div class="hero-video-bg">
    <video muted loop playsinline preload="none">
      <source src="/bhp/bhp-video.mp4" type="video/mp4">
    </video>
    <div class="video-overlay"></div>
  </div>
  <div class="container hero-content">
    - Badge (small bordered pill)
    - H1: two lines (line 2 in red)
    - Paragraph
    - Benefits list (4 items with inline SVG check icons)
    - Scarcity alert (SVG alert-triangle icon + text)
    - CTA button (.btn-primary.open-form-popup)
    - Microcopy
    - 4 stat cards in flex row (number + label)
    - Date badge
  </div>
</section>
```

- [ ] **Step 3: Add Hero CSS**

- Hero: min-height 100vh (desktop), auto (mobile), position relative
- Video bg: absolute, full cover, z-index 0, with dark overlay
- Hero content: relative, z-index 1, centered text, padding-top for alert bar
- Badge: inline-block, border 1px solid gold-primary, border-radius 100px, uppercase, small font
- H1: Montserrat 800, 48-56px desktop, 32-36px mobile, line-height 1.05
- `.text-red`: color var(--red-accent)
- Benefits list: text-align left, max-width centered, SVG icons 20px inline
- Scarcity alert: background bg-highlight with subtle border, border-radius 12px, padding
- Stat cards: flex row, gap 16px, each card with bg-card, border-subtle, border-radius 12px, number in gold-primary font-weight 800 size 2rem, label small muted text
- Date badge: inline-block, gold border, small text
- Mobile: stat cards wrap 2x2, H1 smaller

- [ ] **Step 4: Verify hero renders correctly on desktop and mobile (browser dev tools)**

Check: video background loads, copy is readable, stats display in row, CTA button has gold gradient, responsive at 375px width.

- [ ] **Step 5: Commit**

```bash
git add bhp/index.html
git commit -m "BHP: add top alert bar and hero section with video background"
```

---

## Task 3: Video YouTube Section + Dores Section

**Files:**
- Modify: `bhp/index.html`

- [ ] **Step 1: Add Video YouTube section HTML + CSS**

- Section with bg-secondary
- H2 with bold "A sua pode ser a proxima." part
- Paragraph
- YouTube placeholder: 16:9 responsive container (padding-bottom 56.25%), dark bg, centered play SVG icon + "Video em breve" text
- CTA + microcopy

CSS for video placeholder:
```css
.video-placeholder {
  position: relative;
  padding-bottom: 56.25%;
  background: var(--bg-card);
  border-radius: 16px;
  border: 1px solid var(--border-subtle);
  overflow: hidden;
}
.video-placeholder-content {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
```

- [ ] **Step 2: Add Dores section HTML + CSS**

- Section with bg-primary
- H2 with "pelo menos" bolded
- 5 pain cards, each with:
  - `border-left: 3px solid var(--red-accent)`
  - SVG icon (different per card: clock, trending-down, user-minus, help-circle, message-circle)
  - Title (h3, bold) — the spec title sentence for each card
  - Body paragraph — the spec body text for each card (spec provides both title and body separately)
  - `.reveal` class with staggered delays
  - Note: The spec's PROMPT file (bhp/reformulation/PROMPT_CLAUDE_CODE_BHP_GUARULHOS.md) has full title + body text for each of the 5 cards. Use that as the source of truth for exact copy.

Pain card CSS:
```css
.pain-card {
  background: var(--bg-card);
  border: 1px solid rgba(255,255,255,0.08);
  border-left: 3px solid var(--red-accent);
  border-radius: 0 16px 16px 0;
  padding: 28px 32px;
  margin-bottom: 20px;
}
```

- Transition block: different background (bg-highlight), larger text, centered, with emphasis styling
- CTA

- [ ] **Step 3: Verify both sections render, pain cards stack properly on mobile**

- [ ] **Step 4: Commit**

```bash
git add bhp/index.html
git commit -m "BHP: add video YouTube placeholder and dores sections"
```

---

## Task 4: O Que E o BHP + 3 Pilares Sections

**Files:**
- Modify: `bhp/index.html`

- [ ] **Step 1: Add "O Que E o BHP" section HTML + CSS**

- Section with bg-secondary
- H2: two lines, line 2 in gold (`.text-gold { color: var(--gold-primary); }`)
- Main paragraph (description of BHP)
- Subtitle
- 4 differentials with gold SVG check-circle icons
- Closing paragraph
- Image: `<img src="/bhp/img/newton-e-paulo.webp" alt="Newton e Paulo Vieira" loading="lazy">` with max-width, border-radius 16px, margin centered

- [ ] **Step 2: Add 3 Pilares section HTML + CSS**

- Section with bg-primary
- H2
- 3 cards in CSS grid (1fr 1fr 1fr desktop, 1fr mobile):
  - Each card: bg-card, border-subtle, border-radius 20px, padding 32px
  - SVG icon at top (compass, dollar-sign, users)
  - Title (gold)
  - Problem paragraph with `color: var(--red-accent)` and SVG x-circle icon
  - Solution paragraph with `color: var(--green-accent)` and SVG check-circle icon
  - Hover: translateY(-6px), border-color gold
- CTA

```css
.pilares-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}
@media (max-width: 768px) {
  .pilares-grid { grid-template-columns: 1fr; }
}
```

- [ ] **Step 3: Verify layout, image loads, pilares cards display correctly**

- [ ] **Step 4: Commit**

```bash
git add bhp/index.html
git commit -m "BHP: add 'o que e o BHP' and 3 pilares sections"
```

---

## Task 5: Conteudo Programatico + Ferramentas Sections

**Files:**
- Modify: `bhp/index.html`

- [ ] **Step 1: Add Conteudo Programatico section HTML + CSS**

- Section with bg-secondary
- H2
- 3 columns in CSS grid (3 desktop, 2 mobile, 1 small mobile):
  - Each column: title in gold, 4 bullet items with small SVG chevron-right icons
- CTA

```css
.conteudo-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 32px;
}
@media (max-width: 768px) {
  .conteudo-grid { grid-template-columns: repeat(2, 1fr); }
}
@media (max-width: 480px) {
  .conteudo-grid { grid-template-columns: 1fr; }
}
```

Full topic list from spec:
- Column 1 (Estrategia e Visao): Mentalidade Empreendedora, Analise de Cenarios, Posicionamento de Mercado, Estrategias para Escalar
- Column 2 (Vendas e Resultado): Lideranca Comercial e Pipeline, Tecnicas de Negociacao, Planejamento Financeiro, Cultura de Vendas
- Column 3 (Gestao e Lideranca): Recrutamento Estrategico, Lideranca por Processo, Feedback que Gera Retencao, Inteligencia Relacional

- [ ] **Step 2: Add Ferramentas section HTML + CSS**

- Section with bg-primary
- H2: two lines (line 2 gold)
- Paragraph
- 4 tool cards in CSS grid (2x2 desktop, 1 column mobile):
  - Each card: bg-card, border with gold-primary 15% opacity, border-radius 20px
  - Large number in gold (font-size 3rem, font-weight 800)
  - Title (h3)
  - "Resolve:" tag in italic, red-accent color
  - Description paragraph
  - Hover: translateY(-6px), brighter border

Full content from spec for each card (Identificacao de Rotina, Matriz de Decisao, Aplicativo Gerencial, Matriz de Feedback).

- CTA

- [ ] **Step 3: Verify grids render on desktop and mobile**

- [ ] **Step 4: Commit**

```bash
git add bhp/index.html
git commit -m "BHP: add conteudo programatico and ferramentas sections"
```

---

## Task 6: Numeros + Personalizado + Escola Febracis Sections

**Files:**
- Modify: `bhp/index.html`

- [ ] **Step 1: Add Numeros section HTML + CSS**

- Section with bg-secondary
- H2 with "Sao numeros." bolded
- 5 stat items in flex grid (3+2 desktop, 2+2+1 mobile):
  - Each: large number (gold, font-size 2.5rem, font-weight 800) + label below
  - `.count-up` data attribute for animation (data-target value)
- Company logos image: `<img src="/bhp/img/empresas-que-tiveram-acesso-a-metodologia-febracis-img-desktop-1.webp" alt="Empresas parceiras" loading="lazy">` with max-width 100%, margin-top
- Closing quote: italic, centered, text-light color, max-width 700px

- [ ] **Step 2: Add Personalizado section HTML + CSS**

- Section with bg-primary
- H2: two lines (line 2 gold)
- Paragraph
- 4 feature items with SVG icons (heart, tool/wrench, users, tag/gift):
  - Each: flex row, icon left (40px circle with gold border), text right
  - Title bold + description

- [ ] **Step 3: Add Escola Febracis section HTML + CSS**

- Section with bg-secondary
- H2
- Paragraph (institutional description from spec)
- Logo: `<img src="/bhp/img/logo-febracis-dourado-1.webp" alt="Febracis" loading="lazy">` centered, max-width 300px
- CTA

- [ ] **Step 4: Verify all three sections, especially company logos image renders**

- [ ] **Step 5: Commit**

```bash
git add bhp/index.html
git commit -m "BHP: add numeros, personalizado, and escola febracis sections"
```

---

## Task 7: Depoimentos + Para Quem Sections

**Files:**
- Modify: `bhp/index.html`

- [ ] **Step 1: Add Depoimentos section HTML + CSS**

- Section with bg-primary
- H2
- Grid of 3 placeholder testimonial cards (1fr 1fr 1fr desktop, 1fr mobile):
  - Each card: bg-card, border-subtle, border-radius 16px, padding 32px
  - Circular photo placeholder: 64px circle, bg-highlight, centered SVG user icon
  - Name: "Nome do Empresario" (bold)
  - Company: "Empresa X" (text-muted)
  - Quote: placeholder text in italics, text-light
- CTA

- [ ] **Step 2: Add Para Quem section HTML + CSS**

- Section with bg-secondary
- H2
- Two-column layout (side by side desktop, stacked mobile):
  - Left card (green): bg-card with green-accent 15% border, border-radius 24px
    - H3 in green: "O BHP e para voce se:"
    - 5 items, each with SVG check icon in green + text
  - Right card (red): bg-card with red-accent 15% border, border-radius 24px
    - H3 in red: "O BHP nao e para voce se:"
    - 5 items, each with SVG x icon in red + text
- Text below: CIS recommendation paragraph

Full copy for all 10 items from spec.

- [ ] **Step 3: Verify cards display, responsive behavior correct**

- [ ] **Step 4: Commit**

```bash
git add bhp/index.html
git commit -m "BHP: add depoimentos and para quem sections"
```

---

## Task 8: FAQ + Formulario Final Inline + Footer

**Files:**
- Modify: `bhp/index.html`

- [ ] **Step 1: Add FAQ section HTML + CSS**

- Section with bg-primary
- H2: "Perguntas Frequentes"
- 6 accordion items:
  - Each: `.faq-item` with question button (flex, justify-between, SVG chevron-down that rotates on active) and answer div (max-height 0, overflow hidden, transition)
  - `.faq-item.active .faq-answer`: max-height 500px (or auto with JS)
  - Border-bottom separator between items

Full Q&A content from spec (6 items with complete answers).

CSS:
```css
.faq-item { border-bottom: 1px solid rgba(255,255,255,0.08); }
.faq-question {
  width: 100%; background: none; border: none; color: var(--text-white);
  padding: 24px 0; font-size: 1.1rem; font-weight: 700; cursor: pointer;
  display: flex; justify-content: space-between; align-items: center;
}
.faq-question svg { transition: transform 0.3s; }
.faq-item.active .faq-question svg { transform: rotate(180deg); }
.faq-answer {
  max-height: 0; overflow: hidden; transition: max-height 0.4s ease;
  color: var(--text-light); line-height: 1.7; padding: 0 0;
}
.faq-item.active .faq-answer { max-height: 300px; padding-bottom: 24px; }
```

- [ ] **Step 2: Add Formulario Final inline section HTML + CSS**

- Section with bg-secondary, id="formFinal"
- H2: two lines (line 2 gold)
- Paragraph
- Date badge
- Inline form card (bg-card, border-subtle, border-radius 24px, padding 40px, max-width 600px centered):
  - `<form id="leadFormInline">`
  - Hidden fields: utm_source_inline, utm_medium_inline, utm_campaign_inline, treinamento=BHP
  - All 7 fields with same options as popup but unique IDs (`*Inline` suffix)
  - Redirect message div (`id="formRedirectMsgInline"`)
  - Submit button
  - Microcopy

Form field CSS (shared between popup and inline — reuse same classes):
```css
.form-group { margin-bottom: 16px; }
.form-group input, .form-group select {
  width: 100%; padding: 14px 16px;
  background: rgba(255,255,255,0.05);
  border: 1px solid rgba(255,255,255,0.1);
  border-radius: 12px; color: var(--text-white);
  font-family: 'Montserrat', sans-serif; font-size: 1rem;
}
.form-group input:focus, .form-group select:focus {
  outline: none; border-color: var(--gold-primary);
  box-shadow: 0 0 0 3px rgba(212,168,67,0.15);
}
```

- [ ] **Step 3: Add Footer HTML + CSS**

- `<footer>` with bg darker than primary, border-top subtle, padding 40px
- Logo: `/Logo-CIS-GLOBAL-2023Presencial.png` (existing)
- Text: Febracis Guarulhos info + copyright + Facebook disclaimer
- Centered, text-muted, small font

- [ ] **Step 4: Verify FAQ accordion looks correct (will wire JS in next task), form layout renders, footer displays**

- [ ] **Step 5: Commit**

```bash
git add bhp/index.html
git commit -m "BHP: add FAQ, inline form, and footer sections"
```

---

## Task 9: Sticky CTA + Form Popup

**Files:**
- Modify: `bhp/index.html`

- [ ] **Step 1: Add Sticky CTA HTML + CSS**

- Fixed bottom bar, hidden by default (transform translateY 100%), shown when `.visible` (translateY 0)
- Gold gradient background, high z-index (10001), box-shadow
- Button: `.btn-primary.open-form-popup` with text "Solicitar Minha Vaga no BHP" + arrow SVG
- Microcopy: "Vagas limitadas | Junho 2026"
- Glassmorphism/shadow to stand out from content

CSS:
```css
.sticky-cta {
  position: fixed; bottom: 0; left: 0; right: 0; z-index: 10001;
  background: var(--gradient-gold);
  padding: 12px 24px; text-align: center;
  transform: translateY(100%);
  transition: transform 0.4s cubic-bezier(0.16, 1, 0.3, 1);
  box-shadow: 0 -4px 30px rgba(0,0,0,0.3);
}
.sticky-cta.visible { transform: translateY(0); }
```

- [ ] **Step 2: Add Form Popup HTML + CSS**

- Overlay: fixed, inset 0, bg rgba(0,0,0,0.7), z-index 10004, flex center, hidden by default (opacity 0, pointer-events none), `.active` shows it
- Card: bg-card, border gold subtle, border-radius 24px, max-width 500px, padding 40px
- Close button (X) top-right
- H3: "Solicite sua vaga no BHP"
- Subtitle
- Form `id="leadForm"` with:
  - Hidden fields: utm_source, utm_medium, utm_campaign, treinamento=BHP
  - 7 fields (same as inline but with popup IDs: name, whatsapp, email, empresa, cargo, faturamentoSelect, funcionarios)
  - Redirect message div `id="formRedirectMsg"`
  - Submit button
  - Microcopy
- Scale animation on show (scale 0.8 -> 1)

- [ ] **Step 3: Verify popup and sticky bar HTML renders (JS wiring in next task)**

- [ ] **Step 4: Commit**

```bash
git add bhp/index.html
git commit -m "BHP: add sticky CTA bar and form popup overlay"
```

---

## Task 10: JavaScript — All Interactive Behavior

**Files:**
- Modify: `bhp/index.html` (the `<script>` block at bottom)

- [ ] **Step 1: Add hero video lazy loading**

```javascript
(function() {
  'use strict';

  // Hero video lazy load
  var heroVideo = document.querySelector('#heroVideoBg video');
  var heroVideoBg = document.getElementById('heroVideoBg');
  if (heroVideo && heroVideoBg) {
    function showVideo() { heroVideoBg.classList.add('playing'); }
    heroVideo.addEventListener('playing', showVideo);
    function lazyLoadVideo() {
      heroVideo.preload = 'auto';
      heroVideo.load();
      heroVideo.play().catch(function() { showVideo(); });
    }
    if (document.readyState === 'complete') {
      setTimeout(lazyLoadVideo, 100);
    } else {
      window.addEventListener('load', function() { setTimeout(lazyLoadVideo, 100); });
    }
  }
```

- [ ] **Step 2: Add scroll progress bar + reveal animations**

```javascript
  // Scroll progress
  var scrollProgress = document.getElementById('scrollProgress');
  window.addEventListener('scroll', function() {
    var docHeight = document.documentElement.scrollHeight - window.innerHeight;
    var pct = docHeight > 0 ? (window.scrollY / docHeight) * 100 : 0;
    if (scrollProgress) scrollProgress.style.width = pct + '%';
  }, { passive: true });

  // Reveal on scroll
  var revealElements = document.querySelectorAll('.reveal');
  var revealObserver = new IntersectionObserver(function(entries) {
    entries.forEach(function(entry) {
      if (entry.isIntersecting) entry.target.classList.add('visible');
    });
  }, { threshold: 0.1, rootMargin: '0px 0px -50px 0px' });
  revealElements.forEach(function(el) { revealObserver.observe(el); });
```

- [ ] **Step 3: Add sticky CTA show/hide**

```javascript
  // Sticky CTA
  var stickyCta = document.getElementById('stickyCta');
  var heroSection = document.querySelector('.hero');
  var floatObserver = new IntersectionObserver(function(entries) {
    entries.forEach(function(entry) {
      if (stickyCta) {
        stickyCta.classList.toggle('visible', !entry.isIntersecting);
      }
    });
  }, { threshold: 0 });
  if (heroSection) floatObserver.observe(heroSection);
```

- [ ] **Step 4: Add FAQ accordion**

```javascript
  // FAQ accordion
  window.toggleFaq = function(button) {
    var item = button.parentElement;
    var isActive = item.classList.contains('active');
    document.querySelectorAll('.faq-item').forEach(function(faq) {
      faq.classList.remove('active');
      faq.querySelector('.faq-question').setAttribute('aria-expanded', 'false');
    });
    if (!isActive) {
      item.classList.add('active');
      button.setAttribute('aria-expanded', 'true');
    }
  };
```

- [ ] **Step 5: Add UTM capture**

```javascript
  // UTM capture
  var params = new URLSearchParams(window.location.search);
  ['utm_source', 'utm_medium', 'utm_campaign'].forEach(function(key) {
    // Popup form
    var el = document.getElementById(key);
    if (el && params.get(key)) el.value = params.get(key);
    // Inline form
    var elInline = document.getElementById(key + '_inline');
    if (elInline && params.get(key)) elInline.value = params.get(key);
  });
```

- [ ] **Step 6: Add form popup open/close logic**

```javascript
  // Form popup
  var formPopup = document.getElementById('formPopup');
  var formPopupClose = document.getElementById('formPopupClose');

  function openFormPopup() {
    if (formPopup) {
      formPopup.classList.add('active');
      document.body.style.overflow = 'hidden';
      var firstInput = formPopup.querySelector('input[name="name"]');
      if (firstInput) setTimeout(function() { firstInput.focus(); }, 400);
    }
  }
  function closeFormPopup() {
    if (formPopup) {
      formPopup.classList.remove('active');
      document.body.style.overflow = '';
    }
  }

  document.querySelectorAll('.open-form-popup').forEach(function(btn) {
    btn.addEventListener('click', openFormPopup);
  });
  if (formPopupClose) formPopupClose.addEventListener('click', closeFormPopup);
  if (formPopup) {
    formPopup.addEventListener('click', function(e) {
      if (e.target === formPopup) closeFormPopup();
    });
  }
  document.addEventListener('keydown', function(e) {
    if (e.key === 'Escape' && formPopup && formPopup.classList.contains('active')) closeFormPopup();
  });
```

- [ ] **Step 7: Add form submission handler (both popup and inline)**

```javascript
  // Form submission helper
  function setupForm(formId, endpoint) {
    var form = document.getElementById(formId);
    if (!form) return;
    form.addEventListener('submit', function(e) {
      e.preventDefault();
      var formData = new FormData(form);
      fetch(endpoint, { method: 'POST', body: formData });
      form.innerHTML = '<div style="text-align:center;padding:24px"><p style="font-size:1.3rem;font-weight:700;color:var(--gold-primary);margin-bottom:12px">Inscri\u00e7\u00e3o recebida!</p><p style="color:var(--text-light)">Nossa equipe entrar\u00e1 em contato em breve.</p></div>';
    });
  }

  var webhookUrl = 'https://hook.us2.make.com/2izbvm95o1e4njleuw7hpzccaanfirt6';
  setupForm('leadForm', webhookUrl);
  setupForm('leadFormInline', webhookUrl);
```

- [ ] **Step 8: Add faturamento redirect logic (both forms)**

```javascript
  // Faturamento redirect logic
  // Both popup and inline forms use .form-submit for submit button
  // and .funcionarios-group wrapper around the funcionarios select
  function setupFaturamentoRedirect(selectId, msgId) {
    var select = document.getElementById(selectId);
    var msg = document.getElementById(msgId);
    if (!select) return;
    select.addEventListener('change', function() {
      var form = select.closest('form');
      var submitBtn = form.querySelector('.form-submit');
      var funcGroup = form.querySelector('.funcionarios-group');
      if (this.value === 'Abaixo-R$200mil') {
        if (msg) msg.classList.add('active');
        if (submitBtn) submitBtn.style.display = 'none';
        if (funcGroup) funcGroup.style.display = 'none';
      } else {
        if (msg) msg.classList.remove('active');
        if (submitBtn) submitBtn.style.display = '';
        if (funcGroup) funcGroup.style.display = '';
      }
    });
  }

  setupFaturamentoRedirect('faturamentoSelect', 'formRedirectMsg');
  setupFaturamentoRedirect('faturamentoSelectInline', 'formRedirectMsgInline');

  // Note: In both forms, wrap the funcionarios field in a div.funcionarios-group
  // so the redirect logic can hide it when faturamento < R$200k.
```

- [ ] **Step 9: Add count-up animation for stats**

```javascript
  // Count-up animation
  var countElements = document.querySelectorAll('[data-count-target]');
  var countObserver = new IntersectionObserver(function(entries) {
    entries.forEach(function(entry) {
      if (entry.isIntersecting && !entry.target.dataset.counted) {
        entry.target.dataset.counted = 'true';
        var target = parseInt(entry.target.dataset.countTarget);
        var duration = 2000;
        var start = 0;
        var startTime = null;
        function animate(currentTime) {
          if (!startTime) startTime = currentTime;
          var progress = Math.min((currentTime - startTime) / duration, 1);
          var eased = 1 - Math.pow(1 - progress, 3);
          entry.target.textContent = Math.floor(eased * target).toLocaleString('pt-BR');
          if (progress < 1) requestAnimationFrame(animate);
          else entry.target.textContent = target.toLocaleString('pt-BR');
        }
        requestAnimationFrame(animate);
      }
    });
  }, { threshold: 0.3 });
  countElements.forEach(function(el) { countObserver.observe(el); });

})();
```

- [ ] **Step 10: Verify all interactive features work**

Test checklist:
- Scroll progress bar tracks scroll position
- Sections fade in on scroll
- Sticky CTA appears after scrolling past hero
- FAQ items expand/collapse (one at a time)
- CTA buttons open popup form
- Popup closes on X, overlay click, Escape
- Popup form submits and shows success message
- Inline form submits and shows success message
- Faturamento "Abaixo R$200k" shows redirect message in both forms
- Count-up animation triggers on stats scroll
- Video plays in hero background

- [ ] **Step 11: Commit**

```bash
git add bhp/index.html
git commit -m "BHP: add all JavaScript - forms, animations, popup, FAQ, sticky CTA"
```

---

## Task 11: Final Polish — Responsive, Accessibility, and Cleanup

**Files:**
- Modify: `bhp/index.html`

- [ ] **Step 1: Test and fix responsive layout at key breakpoints**

Test at: 375px (iPhone SE), 390px (iPhone 14), 768px (iPad), 1024px (laptop), 1440px (desktop).

Common fixes needed:
- Hero stat cards: 2x2 grid on mobile
- Pilares cards: stack on mobile
- Conteudo grid: 2 columns tablet, 1 column mobile
- Ferramentas grid: 1 column mobile
- Para Quem: stack columns on mobile
- Form popup: full-width on mobile with less padding
- Font sizes: reduce H1/H2 on mobile per spec
- Section padding: reduce to 60px on mobile
- Sticky CTA: full width, appropriate padding

- [ ] **Step 2: Accessibility pass**

- Verify all `aria-label` attributes on form fields
- Verify `aria-expanded` on FAQ buttons
- Verify `role="dialog"` and `aria-modal` on popup
- Verify skip link works
- Verify tab order is logical
- Add `aria-hidden="true"` to decorative SVGs
- Ensure color contrast meets WCAG AA (gold on dark should be fine)

- [ ] **Step 3: Add prefers-reduced-motion media query**

```css
@media (prefers-reduced-motion: reduce) {
  .reveal { opacity: 1; transform: none; }
  .sticky-cta { transition: none; }
  .btn-primary { animation: none; }
}
```

- [ ] **Step 4: Final visual review — open page and scroll through entirely**

Verify:
- All sections render with correct copy from spec
- Alternating backgrounds work (primary/secondary)
- All CTAs have correct text per CTA journey map
- All images load correctly from `/bhp/img/`
- No horizontal scroll on mobile
- No console errors

- [ ] **Step 5: Commit**

```bash
git add bhp/index.html
git commit -m "BHP: responsive fixes, accessibility pass, and final polish"
```
