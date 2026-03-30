# BHP Landing Page Reformulation — Design Spec

**Date:** 2026-03-30
**Status:** Approved
**File:** `bhp/index.html`

---

## Overview

Complete rewrite of the BHP (Business High Performance) landing page at `bhp/index.html`. Replace all copy and redesign the visual layout while preserving the existing form integration (Make/webhook), MP4 hero video, and core JavaScript functionality.

---

## Key Decisions

| Decision | Choice |
|----------|--------|
| Approach | Full rewrite of `index.html` |
| Hero layout | Full-width centered copy, CTA opens popup |
| Form | Popup (preserved from current) + inline form at page bottom |
| Video | MP4 background on hero + separate YouTube embed section (placeholder) |
| Testimonials | Placeholder cards (structure ready for future content) |
| Company logos | Use `reformulation/Imagens/empresas-que-tiveram-acesso-a-metodologia-febracis-img-desktop-1.webp` |
| Photo | Use `reformulation/Imagens/newton-e-paulo.webp` |
| Event date | 24 a 26 de junho de 2026 |
| Icons | SVG icons (Lucide-style), no emojis anywhere on the page |
| Typography | Montserrat (800/700 for headlines, 400/500 for body) via Google Fonts |

---

## Color Palette (new tokens — replaces current Inter/Playfair + old variable names)

> **Note:** The current page uses `Inter` + `Playfair Display` fonts and color variables like `--gold: #EBA818`. This rewrite introduces **Montserrat** typography and a **new color token naming scheme**. These are intentional changes, not preserved values.

```css
:root {
  /* Backgrounds */
  --bg-primary: #0B1A2E;
  --bg-secondary: #0F2240;
  --bg-hero: #1A1A1A;
  --bg-card: #112240;
  --bg-highlight: #162D50;

  /* Accent / CTA */
  --gold-primary: #D4A843;
  --gold-hover: #E8BC4F;
  --gold-light: #F0D078;
  --gold-dark: #B8912E;

  /* Text */
  --text-white: #FFFFFF;
  --text-light: #C8D6E5;
  --text-muted: #7B8FA3;
  --text-dark: #0B1A2E;

  /* Functional */
  --red-accent: #E74C3C;
  --green-accent: #2ECC71;
  --border-subtle: rgba(212, 168, 67, 0.2);
  --overlay-dark: rgba(11, 26, 46, 0.85);

  /* Gradients */
  --gradient-hero: linear-gradient(135deg, #0B1A2E 0%, #162D50 100%);
  --gradient-gold: linear-gradient(135deg, #D4A843 0%, #E8BC4F 100%);
  --gradient-card: linear-gradient(180deg, #112240 0%, #0B1A2E 100%);
}
```

---

## Typography

- **Headlines (H1, H2):** Montserrat 800/700, bold, impactful
- **Body:** Montserrat 400/500
- **H1 Hero:** 48-56px desktop, 32-36px mobile
- **H2 sections:** 36-42px desktop, 28-32px mobile
- **Body text:** 18px desktop, 16px mobile. Line-height: 1.7
- **Highlight words:** `--gold-primary`
- **Pain/urgency words:** `--red-accent`

---

## Layout Principles

- Dark background dominant (`--bg-primary`), sections alternate between `--bg-primary` and `--bg-secondary`
- Cards: `--bg-card` + subtle gold border (`--border-subtle`) + border-radius 12px
- CTAs: gold gradient (`--gradient-gold`) with dark text (`--text-dark`), border-radius 8px, generous padding, hover with scale + shadow
- Section padding: 80-100px vertical desktop, 60px mobile
- Max-width: 1200px, centered
- Responsive: mobile-first

---

## Effects

- Sections with `fade-in-up` on viewport entry (IntersectionObserver)
- Cards with subtle hover: `transform: translateY(-4px)` + box-shadow
- CTAs with subtle pulse every 3s
- Stats with count-up animation on viewport entry
- Sticky CTA fixed at bottom on mobile and desktop

---

## Page Structure (16 sections + 2 overlays)

### 1. Top Alert Bar (fixed)
- Fixed at top, red gradient background
- Text: "Vagas Limitadas — 24 a 26 de Junho 2026 — Guarulhos, SP"
- Small font, uppercase, high z-index

### 2. HERO
- **Background:** MP4 video (`/bhp/bhp-video.mp4`) with dark overlay, lazy loaded
- **Badge:** "Febracis Guarulhos | Imersao Presencial para Empresarios" — small bordered badge
- **H1 (two lines):**
  - Line 1: "Voce construiu uma empresa de R$200 mil/mes..."
  - Line 2 (red): "pra virar refem dela?"
- **Paragraph:** "Em 33 horas, voce vai sair com o metodo que separa empresarios que trabalham no negocio dos que fazem o negocio trabalhar pra eles."
- **Benefits list (4 items with check SVG icons):**
  - Descobrir exatamente onde estao os gargalos que travam seu lucro
  - Montar um sistema de gestao que roda sem voce no operacional
  - Implementar 4 ferramentas de gestao ja na segunda-feira seguinte
  - Criar previsibilidade real de vendas e caixa — sem achismo
- **Scarcity alert:** SVG alert icon + "Vagas limitadas e mediante aprovacao. O BHP nao e para todo mundo — e para quem ja fatura alto e quer o proximo nivel."
- **CTA button (gold):** "SOLICITAR MINHA VAGA NO BHP" -> opens popup
- **Microcopy:** "Turma presencial em Guarulhos | Aprovacao em ate 48h"
- **4 stat cards in row:**
  - 33h — de imersao (nao e cursinho de fim de semana)
  - 9 — areas de negocio cobertas em profundidade
  - 4 — ferramentas praticas para aplicar na segunda
  - +30 mil — empresarios ja formados pelo metodo (Note: Section 9 uses "+45 mil empresarios impactados" — different metric: "formados" = completed BHP specifically, "impactados" = broader Febracis reach)
- **Date badge:** "Proxima Turma: 24 a 26 de Junho 2026 | Guarulhos, SP | Presencial"

### 3. VIDEO (YouTube)
- **Background:** `--bg-secondary`
- **H2:** "33 horas que mudaram a historia de +30 mil empresas. A sua pode ser a proxima."
- **Paragraph:** "Assista e veja o que acontece quando um empresario para de apagar incendio e comeca a liderar com metodo."
- **YouTube embed:** Placeholder — responsive 16:9 container with dark background, play icon SVG centered, and text "Video em breve". When a real YouTube URL is provided, replace with standard iframe embed.
- **CTA:** "QUERO O MESMO RESULTADO" -> opens popup
- **Microcopy:** "Vagas limitadas | Aprovacao em ate 48h"

### 4. DORES (Pain Points)
- **Background:** `--bg-primary`
- **H2:** "Se sua empresa fatura R$200 mil+ por mes, voce provavelmente vive pelo menos um desses cenarios:"
- **5 pain cards** — each with left red border, SVG icon, title bold, body paragraph:
  1. "Voce trabalha 12h por dia e a empresa so funciona com voce la dentro."
  2. "O faturamento subiu pra R$300, R$500 mil, R$1 milhao... e o lucro nao acompanhou."
  3. "Voce contrata, treina, investe... e perde a pessoa em 4 meses."
  4. "Cada mes e uma surpresa. Voce nao sabe quanto vai vender, quanto vai entrar, quanto vai sobrar."
  5. "Voce sabe que precisa dar feedback, cobrar resultado, desenvolver gente... mas nao sabe como."
- **Transition block** (different background, larger text):
  - "Se voce se reconheceu em pelo menos um desses cenarios, preste atencao:"
  - "Nenhum desses problemas se resolve com mais esforco. Mais esforco e o que te trouxe ate aqui."
  - "O que resolve e metodo, ferramentas certas e uma lideranca que funciona sem voce."
  - "E e exatamente isso que voce vai construir em 33 horas de imersao."
- **CTA:** "CHEGA DE APAGAR INCENDIO — SOLICITAR MINHA VAGA" -> popup

### 5. O QUE E O BHP
- **Background:** `--bg-secondary`
- **H2 (two lines):**
  - Line 1: "Nao e curso. Nao e palestra. Nao e motivacao."
  - Line 2 (gold): "E a imersao que transforma a maneira como voce comanda o seu negocio."
- **Main paragraph:** Description of BHP — 33h in 3 days, presencial, created by Paulo Vieira, validated by 30k+ entrepreneurs in 600+ classes.
- **Subtitle:** "O que faz o BHP diferente de tudo que voce ja fez:"
- **4 differentials list (gold check icons):**
  - 100% pratico — 4 ferramentas para segunda-feira
  - Focado em resultado mensuravel — margem, vendas, retencao, processos
  - Turma curada — so empresarios que ja faturam alto
  - Paulo Vieira ao vivo — nao e video gravado
- **Closing paragraph:** Scaling examples (R$200k to R$1M, R$1M to R$10M, etc.)
- **Image:** `newton-e-paulo.webp` from reformulation/Imagens/

### 6. 3 PILARES
- **Background:** `--bg-primary`
- **H2:** "3 eixos que atacam os 3 maiores gargalos de uma empresa em crescimento."
- **3 cards side-by-side (desktop), stacked (mobile):**
  - Each card has: SVG icon, title, problem (red text), solution (green text)
  - Card 1: Estrategia Empreendedora
  - Card 2: Vendas e Negociacao de Alta Performance
  - Card 3: Lideranca e Gestao de Pessoas
- **CTA:** "QUERO DOMINAR OS 3 PILARES — SOLICITAR MINHA VAGA" -> popup

### 7. CONTEUDO PROGRAMATICO
- **Background:** `--bg-secondary`
- **H2:** "Cada hora foi desenhada para resolver um problema real da sua empresa."
- **3 columns (2 on mobile) with gold title + bullet list:**
  - Column 1: Estrategia e Visao (4 topics)
  - Column 2: Vendas e Resultado (4 topics)
  - Column 3: Gestao e Lideranca (4 topics)
- **CTA:** "QUERO APRENDER TUDO ISSO — SOLICITAR MINHA VAGA" -> popup

### 8. 4 FERRAMENTAS
- **Background:** `--bg-primary`
- **H2 (two lines):**
  - Line 1: "Voce nao vai sair do BHP com anotacoes."
  - Line 2 (gold): "Vai sair com armas."
- **Paragraph:** "4 instrumentos de gestao criados por Paulo Vieira..."
- **4 cards** — each with large number, title, "Resolve:" tag, description:
  1. Identificacao de Rotina — "estou preso no operacional"
  2. Matriz de Decisao — "nao sei se promovo, treino ou desligo"
  3. Aplicativo Gerencial — "nao tenho gestao de pessoas sistematizada"
  4. Matriz de Feedback — "evito conversas dificeis"
- **CTA:** "QUERO ESSAS 4 FERRAMENTAS — SOLICITAR MINHA VAGA" -> popup

### 9. NUMEROS
- **Background:** `--bg-secondary`
- **H2:** "Nao e promessa. Sao numeros."
- **Stats grid (count-up animation):**
  - +600 turmas realizadas
  - +45 mil empresarios impactados
  - +600 empresas transformadas
  - +25 mil horas de conteudo entregues
  - +90 ferramentas e recursos aplicados
- **Company logos:** `empresas-que-tiveram-acesso-a-metodologia-febracis-img-desktop-1.webp`
- **Closing quote (italic, centered):** "Quando voce ve que empresas desse porte usam a mesma metodologia, a pergunta nao e 'sera que funciona?' — e 'por que eu ainda nao fiz?'"

### 10. PERSONALIZADO
- **Background:** `--bg-primary`
- **H2 (two lines):**
  - Line 1: "Voce nao vai so fazer um treinamento."
  - Line 2 (gold): "Vai ter um time dedicado a sua transformacao."
- **Paragraph + 4 items with SVG icons:**
  - Atendimento humanizado e personalizado
  - Suporte dedicado para implementar ferramentas
  - Networking com empresarios de Guarulhos e Grande SP
  - Condicoes especiais para socios e gestores

### 11. ESCOLA FEBRACIS
- **Background:** `--bg-secondary`
- **H2:** "A maior Escola de Negocios da America Latina"
- **Paragraph:** Institutional description of Febracis
- **Logo:** `logo-febracis-dourado-1.webp` (large)
- **CTA:** "FAZER PARTE DESSA HISTORIA" -> popup

### 12. DEPOIMENTOS
- **Background:** `--bg-primary`
- **H2:** "Quem ja fez, nao volta a gerir do mesmo jeito."
- **Testimonial cards (placeholders):** Grid of 3 cards (desktop), stacked on mobile. Each card: circular photo placeholder (gray with user icon), name "Nome do Empresario", company "Empresa X", and placeholder quote text. Structure ready to be replaced with real content later.
- **CTA:** "QUERO ESSE RESULTADO — SOLICITAR MINHA VAGA" -> popup

### 13. PARA QUEM
- **Background:** `--bg-secondary`
- **H2:** "Este treinamento nao e para todo mundo. E isso que faz ele funcionar."
- **Visual table — 2 columns (green/red):**
  - Left (green check icons) — "O BHP e para voce se:":
    1. Sua empresa ja fatura R$200 mil+/mes e voce quer destravar o proximo nivel
    2. Tem equipe e quer que ela entregue sem depender de voce
    3. Quer ferramentas aplicaveis — nao teoria motivacional
    4. Esta disposto a dedicar 33 horas pra mudar de verdade
    5. Quer estar numa sala com empresarios que pensam grande
  - Right (red X icons) — "O BHP nao e para voce se:":
    1. Sua empresa fatura abaixo de R$200 mil (conheca o Metodo CIS)
    2. Trabalha sozinho, sem equipe pra liderar
    3. Busca "motivacao" sem compromisso com execucao
    4. Nao tem 3 dias pra investir na propria empresa
    5. Prefere continuar resolvendo tudo sozinho
- **Text below:** "Se voce esta no inicio da jornada, comece pelo Metodo CIS — o treinamento que ja transformou +500 mil vidas. O BHP e o proximo passo."

### 14. FAQ
- **Background:** `--bg-primary`
- **H2:** "Perguntas Frequentes"
- **6 accordion items** (click to expand):
  1. **Quanto tempo dura?** — "33 horas em 3 dias. Imersao presencial, intensiva, do tipo que muda a forma como voce opera. Nao da pra comparar com cursinhos online de 2h."
  2. **Qual a diferenca entre o BHP e o Metodo CIS?** — "O CIS transforma a pessoa. O BHP transforma a empresa. O CIS trabalha inteligencia emocional e mentalidade. O BHP e 100% gestao: lideranca, vendas, ferramentas, processos. Muitos empresarios fazem os dois — CIS primeiro, BHP depois."
  3. **Preciso ter feito o CIS antes?** — "Nao e obrigatorio, mas quem fez o CIS chega no BHP com a base emocional pronta e aproveita 10x mais. Se nao fez, nao e impedimento — voce vai aproveitar igualmente."
  4. **Posso levar socios ou gestores?** — "Recomendamos fortemente. Quando o time de lideranca faz o BHP junto, a implementacao e 3x mais rapida. Consulte condicoes especiais para grupos da mesma empresa."
  5. **Quando e a proxima turma?** — "24 a 26 de junho de 2026, presencial em Guarulhos, SP. Preencha o formulario e nossa equipe entra em contato com os proximos passos."
  6. **E se minha empresa fatura abaixo de R$200 mil?** — "O BHP foi desenhado para desafios de gestao de empresas ja consolidadas. Se e o seu caso, o Metodo CIS e o treinamento certo pra voce agora — e vai preparar a base para o BHP no futuro."

### 15. FORMULARIO FINAL (Inline)
- **Background:** `--bg-secondary`
- **H2 (two lines):**
  - Line 1: "A proxima turma tem vagas limitadas."
  - Line 2 (gold): "Solicite a sua e descubra se o BHP e para o momento da sua empresa."
- **Paragraph:** "Preencha abaixo. Nossa equipe analisa seu perfil e entra em contato em ate 48 horas."
- **Date badge:** "Proxima Turma: 24 a 26 de Junho 2026 | Guarulhos, SP | Presencial"
- **Inline form (dark card, subtle borders):**
  - Nome completo (text, required)
  - WhatsApp com DDD (tel, required)
  - E-mail (email, required)
  - Nome da empresa (text, required)
  - Cargo (select: Dono/Socio/CEO/Diretor/Gestor/Outro)
  - Faturamento mensal (select — same options as popup)
  - Quantos funcionarios (select: 1-5/6-20/21-50/51-200/+200)
- **Redirect rule:** Same as popup — if "abaixo de R$200 mil" selected, show CIS message, hide submit
- **Submit button:** "SOLICITAR MINHA VAGA NO BHP"
- **Microcopy:** "Vagas limitadas e mediante aprovacao | Retorno em ate 48h | Atendimento humanizado"

### 16. FOOTER
- Febracis Guarulhos — Treinamentos de Alta Performance Empresarial
- Business High Performance | BHP | Presencial em Guarulhos, SP
- (c) 2026 Febracis Guarulhos. Todos os direitos reservados.
- Facebook disclaimer

### STICKY CTA (overlay)
- Fixed at bottom, visible after scrolling past hero
- Gold gradient background
- Text: "SOLICITAR MINHA VAGA NO BHP"
- Microcopy: "Vagas limitadas | Junho 2026"
- Action: opens form popup
- High z-index, shadow to stand out

### FORM POPUP (shared)
- Same popup for all CTAs (except inline form at bottom)
- Overlay with dark backdrop, centered card
- Hidden fields: `utm_source`, `utm_medium`, `utm_campaign`, `treinamento=BHP`
- **Fields:**
  - Nome completo (text, required, autocomplete="name")
  - WhatsApp com DDD (tel, required, autocomplete="tel")
  - E-mail (email, required, autocomplete="email")
  - Nome da empresa (text, required, autocomplete="organization")
  - Cargo (select, required): Dono / Socio / CEO / Diretor / Gestor / Outro
  - Faturamento mensal (select, required, id="faturamentoSelect"):
    - R$200 mil a R$500 mil (value="R$200mil-R$500mil")
    - R$500 mil a R$1 milhao (value="R$500mil-R$1milhao")
    - R$1 milhao a R$5 milhoes (value="R$1milhao-R$5milhoes")
    - R$5 milhoes a R$50 milhoes (value="R$5milhoes-R$50milhoes")
    - Acima de R$50 milhoes (value="Acima-R$50milhoes")
    - Minha empresa fatura abaixo de R$200 mil (value="Abaixo-R$200mil")
  - Funcionarios (select, required): 1-5 / 6-20 / 21-50 / 51-200 / +200
- **Redirect logic:** When faturamento = "Abaixo-R$200mil", show CIS recommendation message, hide submit button and funcionarios field
- Submit endpoint: `https://hook.us2.make.com/2izbvm95o1e4njleuw7hpzccaanfirt6` (POST FormData)
- Close on X, overlay click, or Escape key
- Success message after submit (replaces form content)

### INLINE FORM (Section 15) — Technical Notes
- **New feature** (does not exist in current page)
- Uses different element IDs to avoid conflicts with popup form (e.g., `leadFormInline`, `faturamentoSelectInline`)
- Same fields, same select options, same redirect logic as popup
- Also captures UTM params via hidden fields
- Submits to the same Make webhook endpoint
- Both forms share the same success behavior (innerHTML replacement)

---

## CTA Journey Map

Each CTA has different copy to match the visitor's emotional stage:

| Section | CTA Text | Emotional Stage |
|---------|----------|-----------------|
| Hero | SOLICITAR MINHA VAGA NO BHP | Curiosity + initial identification |
| Video | QUERO O MESMO RESULTADO | Inspiration after social proof |
| Dores | CHEGA DE APAGAR INCENDIO — SOLICITAR MINHA VAGA | Peak pain — urgency |
| Pilares | QUERO DOMINAR OS 3 PILARES — SOLICITAR MINHA VAGA | Clarity on learning |
| Conteudo | QUERO APRENDER TUDO ISSO — SOLICITAR MINHA VAGA | Specificity builds trust |
| Ferramentas | QUERO ESSAS 4 FERRAMENTAS — SOLICITAR MINHA VAGA | Tangibility |
| Escola | FAZER PARTE DESSA HISTORIA | Belonging + authority |
| Depoimentos | QUERO ESSE RESULTADO — SOLICITAR MINHA VAGA | Peer identification |
| Form Final | SOLICITAR MINHA VAGA NO BHP | Final conversion |
| Sticky | SOLICITAR MINHA VAGA NO BHP | Always available |

All CTAs open the form popup, except the inline form at the bottom.

---

## Assets

| Asset | Source | Usage |
|-------|--------|-------|
| `bhp-video.mp4` | `bhp/bhp-video.mp4` (existing) | Hero background video |
| `empresas-que-tiveram-acesso-a-metodologia-febracis-img-desktop-1.webp` | `bhp/reformulation/Imagens/` | Company logos in Numbers section |
| `newton-e-paulo.webp` | `bhp/reformulation/Imagens/` | Photo in "O que e o BHP" section |
| `img-empresas-1.webp` | `bhp/reformulation/Imagens/` | Secondary company image if needed |
| `img-sobre-o-treinamento-1.webp` | `bhp/reformulation/Imagens/` | Training image if needed |
| `logo-bhp-gestao-de-negocios.webp` | `bhp/reformulation/Imagens/` | BHP logo |
| `logo-febracis-branco-1.webp` | `bhp/reformulation/Imagens/` | Febracis white logo |
| `logo-febracis-dourado-1.webp` | `bhp/reformulation/Imagens/` | Febracis gold logo |

Images from `bhp/reformulation/Imagens/` must be copied to `bhp/img/` during implementation. All `src` attributes should reference `/bhp/img/filename.webp`.

---

## Preserved from Current Page

- **Form submission endpoint** (`https://hook.us2.make.com/2izbvm95o1e4njleuw7hpzccaanfirt6`) — POST FormData
- **UTM capture logic** (query params -> hidden fields)
- **Faturamento redirect logic** (< R$200k -> CIS message, hide submit)
- **Hero video lazy loading** (defer load, play on ready)
- **Scroll progress bar** — thin bar at top of page, gold color, tracks scroll percentage
- **IntersectionObserver reveal animations** (fade-in-up on `.reveal` elements)
- **FAQ accordion functionality** (click to expand/collapse, one open at a time)
- **Sticky CTA show/hide on scroll** (appears after hero leaves viewport)
- **GTM/Stape tracking** — loaded via Stape server-side proxy: `https://jcjrrbdr.san.stape.io/ns.html?id=GTM-NC44TJM9` (NOT standard GTM snippet)
- **Schema.org structured data** (Event type) — update content to match new copy but preserve structure
- **Accessibility** (skip link, aria labels, keyboard nav)
- **Title/Meta/OG tags** — update copy to match new headline but preserve structure

## Changed from Current Page

- **Typography:** Inter + Playfair Display -> Montserrat (400/500/700/800)
- **Color tokens:** New variable naming scheme (see Color Palette section)
- **All copy:** Entirely new text per reformulation prompt
- **New sections added:** Video YouTube, Pilares, Conteudo Programatico, Ferramentas, Numeros, Personalizado, Escola Febracis, Depoimentos, Para Quem, Formulario Final inline
- **Inline form at bottom:** New feature — second conversion point
- **Images:** New assets from `reformulation/Imagens/` folder

---

## Technical Notes

- Single HTML file (`bhp/index.html`) — all CSS inline in `<style>`, all JS inline in `<script>`
- Google Fonts: Montserrat (400, 500, 700, 800) loaded with print/onload swap pattern
- SVG icons inline (no external icon library dependency)
- Mobile-first responsive design
- The inline form at the bottom submits to the same webhook endpoint as the popup form
- Both forms share the same redirect logic for faturamento < R$200k
