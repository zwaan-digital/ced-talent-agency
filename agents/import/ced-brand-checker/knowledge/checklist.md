# CED Brand Compliance Review Checklist

Deze checklist volg je **altijd** bij een brand compliance review. Werk systematisch van boven naar beneden.

---

## 📋 Pre-Review Setup

### Stap 1: Lees Brand Guidelines
- [ ] Open en lees `knowledge/brand-guidelines.md`
- [ ] Refresh je kennis van CED kleuren, typography, en spacing
- [ ] Check of er updates zijn in de guidelines

### Stap 2: Begrijp de Scope
- [ ] Vraag de user welke bestanden/componenten gecheckt moeten worden
- [ ] Identificeer het type project (website, app, component library)
- [ ] Bepaal of het een code review of live site analyse is

### Stap 3: Verzamel Bestanden
Voor **code review**:
- [ ] Zoek CSS/SCSS bestanden: `**/*.css`, `**/*.scss`
- [ ] Zoek styled components: `**/*.jsx`, `**/*.tsx`, `**/*.vue`
- [ ] Zoek HTML templates: `**/*.html`, `**/templates/**`
- [ ] Check voor design tokens: `tokens.json`, `variables.scss`, etc.

Voor **live site analyse**:
- [ ] Krijg de URL van de user
- [ ] Navigeer naar de site met Playwright
- [ ] Maak screenshots voor referentie

---

## 🎨 Kleur Compliance Check

### Stap 4: Bepaal Welk Kleurenschema van Toepassing is

**⚠️ Belangrijk:** Er zijn twee kleurenschema's - check welke van toepassing is:

**Officiële Brand Guide (Mei 2023)** - Voor marketing, externe communicatie:
- Paars: `#92278f`
- Cyaan: `#00bfe0`
- Geel (CTA): `#fbe54a`
- Lichtgrijs: `#dae3e5`

**Digitale Implementatie** - Voor web apps, digitale tools:
- Purple Dark: `#57257C`
- Cyan Primary: `#24BEDF`
- Magenta: `#9C2D8A`
- Light Purple: `#EDE9F2`

Voor nieuwe projecten: **Volg officiële Brand Guide** tenzij specifiek digitaal product.

### Stap 5: Extraheer Alle Kleuren
- [ ] Zoek naar hex codes: `#[0-9a-fA-F]{6}`
- [ ] Zoek naar rgb/rgba values: `rgb(`, `rgba(`
- [ ] Zoek naar color keywords: `blue`, `red`, etc.
- [ ] Check CSS variables: `--color-*`, `--primary-*`
- [ ] Check voor hardcoded kleuren in JS/JSX (style props)
- [ ] Check Tailwind config of design tokens files

### Stap 6: Vergelijk met CED Palette

**Complete CED Kleurenpalette Check:**

**✅ Officiële Basiskleuren (Brand Guide 2023):**
- [ ] `#92278f` - Paars/Magenta (primary brand, headers, buttons)
- [ ] `#00bfe0` - Cyaan/Turquoise (accents, interactive)
- [ ] `#fbe54a` - Geel (CTA - **MAX 1x per pagina!**)
- [ ] `#dae3e5` - Lichtgrijs (subtiele backgrounds)
- [ ] `#000000` - Zwart (tekst)

**✅ Aanvullende Kleuren (Transparanties voor schema's):**
- [ ] `#b37ab4` - Paars 60% (schema's, lichtere accenten)
- [ ] `#d3b5d7` - Paars 30% (subtiele backgrounds, subtiele CTA's)
- [ ] `#8bd5ea` - Cyaan 60% (schema's, lichtere interactief)
- [ ] `#c5e8f3` - Cyaan 30% (subtiele backgrounds, subtiele CTA's)

**✅ Digitale Implementatie Kleuren (Web Apps):**
- [ ] `#57257C` - Purple Dark (primary, headers, buttons)
- [ ] `#9C2D8A` - Magenta (secondary, hover states)
- [ ] `#24BEDF` - Cyan Primary (interactive, links, Frontend category)
- [ ] `#1EA1BD` - Teal (DevOps/Security category)
- [ ] `#EDE9F2` - Light Purple (backgrounds, subtle elements)
- [ ] `#F6F4F8` - Gray Light (page background)
- [ ] `#222222` - Dark Text (body tekst, high contrast)

**✅ Acceptabele Neutrals:**
- [ ] `#FFFFFF` - Wit (backgrounds, text on dark)
- [ ] `#F9F9F9` tot `#F6F4F8` - Light grays (backgrounds)
- [ ] `#E5E5E5` tot `#CCCCCC` - Mid grays (borders, dividers)
- [ ] `#666666` tot `#222222` - Dark grays (text, icons)
- [ ] `#000000` - Zwart (text, high contrast elements)

### Stap 7: Flag Non-Compliant Colors

Voor **elke verkeerde kleur**:
- [ ] Noteer het bestand en regel nummer
- [ ] Identificeer de huidige kleur (hex/rgb)
- [ ] Stel de correcte CED kleur voor
- [ ] Leg uit waarom de wijziging nodig is
- [ ] Geef impact niveau (High/Medium/Low)

**Common Issues:**

**Brand Identity Violations (🔴 High Impact):**
- ❌ `#2563eb` (Tailwind blue) → `#57257C` (Purple) of `#24BEDF` (Cyan)
- ❌ `#3b82f6` (generic blue) → `#24BEDF` (Cyan)
- ❌ `#ef4444` (red) → `#9C2D8A` (Magenta) voor alerts
- ❌ `#10b981` (green) → `#24BEDF` (Cyan) of `#1EA1BD` (Teal)
- ❌ `#f59e0b` (orange) → `#fbe54a` (Geel) voor CTA's
- ❌ Random brand kleuren niet uit CED palette

**Schema & Accent Issues (🟡 Medium Impact):**
- ❌ Te donkere paars → Gebruik `#b37ab4` (Paars 60%) voor lichtere secties
- ❌ Te lichte cyaan → Gebruik `#8bd5ea` (Cyaan 60%) voor subtiele accenten
- ❌ Verkeerde gradient → CED gebruikt **geen gradients**, alleen solid kleuren

**CTA Color Violations (🔴 High Impact):**
- ❌ Meer dan 1 gele CTA op pagina → MAX 1x geel per pagina!
- ❌ Geel gebruikt voor niet-CTA elementen → Geel is ALLEEN voor primaire CTA
- ❌ Random CTA kleuren → Gebruik geel (`#fbe54a`) of paars (`#92278f`)

---

## 🔤 Typography Compliance Check

### Stap 8: Bepaal Welke Typography Regels van Toepassing zijn

**⚠️ Belangrijk:** Er zijn verschillende typography sets - check context:

**Officiële Brand Guide (Externe Vormgeving):**
- **Din Bold** - Grote titels, RICHTLIJNEN
- **Din Regular/Light** - Leesteksten
- Drukwerk: 9pt/12pt minimum
- Digitaal: 11pt/13pt minimum

**Officiële Brand Guide (Interne Vormgeving):**
- **Verdana Bold** - Titels
- **Verdana Regular** - Bodytekst
- 9pt minimum, regelafstand 13pt minimum

**Digitale Implementatie (Web/Apps):**
- **Aglet Slab** - Primary display font (headers)
- **Verdana** - Body tekst, fallback
- Minimum 14px, body 16-20px

### Stap 9: Check Font Families

**Voor Externe/Marketing Materialen:**
- [ ] Zoek alle `font-family` declaraties
- [ ] Verificeer **Din Bold** voor titels/headers
- [ ] Verificeer **Din Regular** of **Din Light** voor body
- [ ] Check dat teksten op **egale achtergrond** staan (niet over beeld)
- [ ] Flag gebruik van andere fonts zonder goede reden

**Voor Interne Materialen:**
- [ ] Verificeer **Verdana Bold** voor titels
- [ ] Verificeer **Verdana Regular** voor bodytekst
- [ ] Check minimum 9pt font size

**Voor Digitale Producten (Web/Apps):**
- [ ] Zoek alle `font-family` declaraties
- [ ] Verificeer dat `Aglet Slab` de primary font is voor headers
- [ ] Verificeer `Verdana` voor body tekst (of system fallback)
- [ ] Check @font-face of CDN link voor Aglet Slab:
  ```css
  @import url('https://fonts.cdnfonts.com/css/aglet-slab');
  ```
- [ ] Check fallback stack: `'Aglet Slab', Georgia, serif`

**❌ Common Font Violations:**
- ❌ Arial/Helvetica zonder Din of Aglet Slab
- ❌ Roboto, Inter, of andere moderne sans-serifs (niet CED branded)
- ❌ Comic Sans, Papyrus (absoluut verboden)
- ❌ Tekst over beeld zonder egale achtergrond

### Stap 10: Check Font Sizes

**Minimum Font Sizes (STRIKT):**
- [ ] Zoek alle `font-size` declaraties
- [ ] Verificeer dat **geen enkele** font size < `14px` / `9pt` is
- [ ] Check `clamp()` en responsive sizing - minimums moeten blijven
- [ ] Flag te kleine tekst in footer, disclaimer, of small print

**Heading Sizes (Digitaal):**
- [ ] H1: `40px` (32px op mobile)
- [ ] H2: `32px` (28px op mobile)
- [ ] H3: `24px` (20px op mobile)
- [ ] H4: `20px` (18px op mobile)
- [ ] H5/H6: `16px` minimum

**Body Text Sizes:**
- [ ] Desktop: `20px` (of `16px` acceptabel)
- [ ] Mobile: `16px` minimum (voorkomt zoom)
- [ ] Line height: `1.5` tot `1.7` voor leesbaarheid

**Drukwerk Font Sizes (Brand Guide):**
- [ ] Corpsgrootte: minimum 9pt
- [ ] Interlinie: minimum 12pt (drukwerk), 13pt (digitaal documenten)

### Stap 11: Check Font Weights

**Voor Headings:**
- [ ] Headings moeten **Bold** zijn (Din Bold, Verdana Bold, Aglet Slab Bold)
- [ ] CSS: `font-weight: 600` of `font-weight: 700` (bold)
- [ ] Flag light/thin weights op headers (niet brand-compliant)

**Voor Body Text:**
- [ ] Body moet **Regular** zijn (Din Regular, Verdana Regular)
- [ ] CSS: `font-weight: 400` (normal)
- [ ] Light variant (Din Light) acceptabel voor specifieke toepassingen

**❌ Common Weight Violations:**
- ❌ Thin weights (`font-weight: 100, 200, 300`) - Te licht, niet CED stijl
- ❌ Ultra-bold (`font-weight: 800, 900`) - Te zwaar, niet nodig
- ❌ Inconsistente weights door inheritance issues

### Stap 12: Check Typography Spacing

**Line Height / Interlinie:**
- [ ] Headers: Line height ≈ font size (`line-height: 1` tot `1.2`)
- [ ] Body: Line height `1.5` tot `1.7` voor leesbaarheid
- [ ] Drukwerk: Specifiek 12pt interlinie voor 9pt tekst

**Letter Spacing:**
- [ ] Default (0) voor body tekst
- [ ] Geen extreme letter-spacing (tracking) tenzij design vereist
- [ ] Check dat ALL CAPS tekst adequate spacing heeft (+0.05em tot +0.1em)

**Paragraph Spacing:**
- [ ] Margin tussen paragraphs: `16px` tot `24px`
- [ ] Geen te krappe tekstblokken (minimum witruimte)

### Stap 13: Typography Accessibility

**Contrast & Readability:**
- [ ] Zwarte tekst (`#000000` of `#222222`) op witte achtergrond ✅
- [ ] Witte tekst op paarse achtergrond (`#92278f` of `#57257C`) ✅
- [ ] Check dat tekst **nooit over beeld** staat zonder egale backdrop
- [ ] Geen light text op light backgrounds (< 4.5:1 contrast)

**Responsive Typography:**
- [ ] Font sizes schalen naar beneden op mobile
- [ ] Minimum 16px op mobile (voorkomt auto-zoom iOS)
- [ ] Line length max 70-80 karakters voor leesbaarheid

---

## 🔘 Component Styling Check

### Stap 14: CTA (Call-to-Action) Review

**🚨 KRITIEKE REGEL:** MAX 1 opvallende CTA per pagina!

**Voor elke pagina/scherm:**
- [ ] Tel aantal opvallende CTA's (geel of paars met hoog contrast)
- [ ] Verificeer MAX 1 opvallende CTA (**STRIKT**)
- [ ] Check dat primaire CTA geel is (`#fbe54a`) of paars (`#92278f`)
- [ ] Check dat secundaire CTA's subtiel zijn (30-60% transparantie)

**Primaire CTA (Geel - Voorkeur):**
```css
.cta-primary {
  background-color: #fbe54a; /* Geel */
  color: #000000; /* Zwart */
  padding: 20px 30px;
  border-radius: 8px;
  font-weight: 600;
  /* MAX 1x per pagina! */
}
```

**Primaire CTA (Paars - Alternatief):**
```css
.cta-primary-purple {
  background-color: #92278f; /* Paars */
  color: #ffffff; /* Wit */
  padding: 20px 30px;
  border-radius: 8px;
  font-weight: 600;
  /* MAX 1x per pagina! */
}
```

**Subtiele CTA's (Onbeperkt):**
```css
/* Lichtpaars - voor secundaire acties */
.cta-subtle {
  background-color: rgba(146, 39, 143, 0.3); /* Paars 30% */
  color: #92278f;
  padding: 16px 24px;
  border-radius: 8px;
}

/* Lichtblauw/Cyaan - voor tertiaire acties */
.cta-subtle-cyan {
  background-color: rgba(0, 191, 224, 0.3); /* Cyaan 30% */
  color: #00bfe0;
  padding: 16px 24px;
  border-radius: 8px;
}
```

**CTA Checklist:**
- [ ] Is er exact 1 opvallende CTA per pagina?
- [ ] Gebruikt de primaire CTA geel of paars?
- [ ] Zijn secundaire CTA's subtiel (transparant)?
- [ ] Is de CTA hiërarchie duidelijk (primary > secondary > tertiary)?
- [ ] Heeft de CTA actie-gerichte tekst? ("Meld je aan", "Download", "Neem contact op")

**❌ CTA Violations:**
- ❌ Meer dan 1 gele/paarse CTA op dezelfde pagina
- ❌ Geel gebruikt voor niet-CTA elementen (badges, highlights)
- ❌ Alle CTA's even opvallend (geen hiërarchie)
- ❌ CTA met onduidelijke tekst ("Klik hier", "Meer")

### Stap 15: Button Review

Voor **elke button** (niet-CTA):
- [ ] Background color: `#57257C` (purple) of `#92278f` (paars)?
- [ ] Border radius: `8px` (consistent met CED stijl)
- [ ] Padding: `8px 20px` of `12px 24px` (adequate klikbaarheid)
- [ ] Font size: `16px` minimum
- [ ] Font weight: `600` (semibold/bold)
- [ ] Hover state: `#9C2D8A` (magenta) of darker shade
- [ ] Geen box-shadow (flat design)
- [ ] Geen gradients (solid kleuren)

**Button States:**
```css
.btn-primary {
  background: #57257C; /* Purple Dark */
  color: #ffffff;
  border-radius: 8px;
  padding: 12px 24px;
  font-weight: 600;
  transition: background 0.2s;
}

.btn-primary:hover {
  background: #9C2D8A; /* Magenta */
}

.btn-primary:disabled {
  background: #cccccc;
  color: #666666;
  cursor: not-allowed;
}
```

**Secondary Buttons:**
```css
.btn-secondary {
  background: transparent;
  color: #57257C;
  border: 2px solid #57257C;
  border-radius: 8px;
  padding: 10px 22px; /* Smaller padding om border te compenseren */
  font-weight: 600;
}

.btn-secondary:hover {
  background: #EDE9F2; /* Light purple */
}
```

### Stap 16: Kaders (Frames) Review

**🎯 2+2 Hoeken Regel (STRIKT voor kaders):**

Voor **elk kader/frame** element:
- [ ] Check dat het de **2+2 hoeken** regel volgt
- [ ] 2 hoeken: **scherp/recht** (90°)
- [ ] 2 hoeken: **afgerond** (8-12px radius)
- [ ] Nooit alle 4 hoeken gelijk (tenzij simpele rechthoek zonder kader styling)

**Correcte Kader Implementatie:**
```css
/* Variant 1: Linksboven + Linksonder rond */
.frame-variant-1 {
  border: 2px solid #92278f;
  border-top-left-radius: 12px;
  border-bottom-left-radius: 12px;
  border-top-right-radius: 0;
  border-bottom-right-radius: 0;
}

/* Variant 2: Rechtsboven + Rechtsonder rond */
.frame-variant-2 {
  border: 2px solid #00bfe0;
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
  border-top-right-radius: 12px;
  border-bottom-right-radius: 12px;
}

/* Variant 3: Diagonaal (Linksboven + Rechtsonder rond) */
.frame-variant-3 {
  border: 2px solid #92278f;
  border-top-left-radius: 12px;
  border-bottom-left-radius: 0;
  border-top-right-radius: 0;
  border-bottom-right-radius: 12px;
}
```

**Kader Kleuren:**
- [ ] Paars (`#92278f`) voor primary kaders
- [ ] Cyaan (`#00bfe0`) voor secondary/accent kaders
- [ ] Border width: `2px` tot `4px` (niet te dun)

**❌ Kader Violations:**
- ❌ Alle 4 hoeken afgerond (geen 2+2 patroon) op branded frames
- ❌ Alle 4 hoeken scherp zonder reden (generiek, niet branded)
- ❌ Random border radius values (7px, 13px) - gebruik 8px, 10px, of 12px
- ❌ Verkeerde kleuren voor borders (generic grays ipv CED kleuren)

### Stap 17: Card Review

Voor **elke card**:
- [ ] Border radius: **`0px`** (sharp corners voor cards) ⚠️ KRITIEK
- [ ] Box shadow: **`none`** (flat design) ⚠️ KRITIEK
- [ ] Background: `#F1F1F1`, `#EDE9F2`, of `#F6F4F8`
- [ ] Padding: `20px` tot `32px` (adequate witruimte)
- [ ] Margin bottom: `32px` (in grids, 8px grid systeem)
- [ ] Geen hover shadow effecten (CED is flat design)

**Correcte Card Styling:**
```css
.card {
  background: #EDE9F2; /* Light purple */
  border-radius: 0; /* MOET 0px zijn! */
  box-shadow: none; /* MOET none zijn! */
  padding: 24px;
  margin-bottom: 32px;
}

/* Alternatief: Card met border ipv background */
.card-bordered {
  background: #ffffff;
  border: 2px solid #EDE9F2;
  border-radius: 0; /* Nog steeds 0px */
  padding: 24px;
}
```

**❌ Card Violations (ZEER VOORKOMEND):**
- ❌ `border-radius: 8px` of `12px` op cards (moet 0px!)
- ❌ `box-shadow: 0 2px 8px rgba(...)` (moet none!)
- ❌ Hover shadow effecten (niet flat)
- ❌ Gradient backgrounds (gebruik solid kleuren)
- ❌ Te weinig padding (< 16px)

### Stap 18: Input Fields Review

Voor **elk input field**:
- [ ] Border radius: `4px` (kleiner dan buttons: 8px)
- [ ] Border color: neutral gray (`#cccccc`) of CED purple (`#57257C`)
- [ ] Border width: `1px` tot `2px`
- [ ] Padding: `8px 12px` minimum (adequate klikbaarheid)
- [ ] Font size: ≥ `16px` (voorkomt zoom op mobile iOS)
- [ ] Background: `#ffffff` (wit voor input areas)
- [ ] Focus state: border color naar CED purple/cyan

**Input Styling:**
```css
input[type="text"],
input[type="email"],
textarea {
  border: 1px solid #cccccc;
  border-radius: 4px;
  padding: 10px 12px;
  font-size: 16px;
  font-family: Verdana, sans-serif;
  background: #ffffff;
}

input:focus {
  border-color: #57257C; /* CED Purple */
  outline: none;
  box-shadow: 0 0 0 3px rgba(87, 37, 124, 0.1); /* Subtiele glow */
}

input::placeholder {
  color: #999999;
  font-style: italic;
}

/* Error state */
input.error {
  border-color: #9C2D8A; /* Magenta voor errors */
}
```

**Checkbox & Radio Buttons:**
- [ ] Custom styling met CED kleuren
- [ ] Checked state: CED purple (`#57257C`) of cyan (`#24BEDF`)
- [ ] Size: `20px` minimum (goed klikbaar)
- [ ] Label: dichtbij input (< 8px afstand)

### Stap 19: Layout & Spacing Review

**8px Grid Systeem:**
- [ ] Check dat alle spacing multiples van `8px` zijn
- [ ] Margins: 8px, 16px, 24px, 32px, 40px, 48px, etc.
- [ ] Padding: 8px, 16px, 24px, 32px, etc.
- [ ] Gaps in grids: 16px, 24px, 32px
- [ ] Flag random values (15px, 22px, 37px)

**Section Spacing:**
- [ ] Vertical padding sections: `40px 0` tot `80px 0` (top/bottom)
- [ ] Alternerende backgrounds (white → light purple → white)
- [ ] Consistent section breaks met witruimte

**Component Spacing:**
- [ ] Grid gaps: `32px` tussen cards (8px grid)
- [ ] Margin bottom headings: `16px` tot `24px`
- [ ] Margin bottom paragraphs: `16px`
- [ ] Button spacing in groups: `12px` of `16px` apart

**Responsive Spacing:**
- [ ] Desktop spacing: full values (32px, 40px, etc.)
- [ ] Tablet: 75% (24px, 30px)
- [ ] Mobile: 50% (16px, 20px)
- [ ] Check dat layouts niet te krap zijn op small screens

### Stap 20: Diagonale Vlakken (Decoratief Element)

CED gebruikt **diagonale vlakken** als signature design element:

**Diagonal Specifications:**
- [ ] Kleur: Cyaan (`#00bfe0` of `#24BEDF`)
- [ ] Positie: Rechtsboven naar linksonder (of omgekeerd)
- [ ] Geen gradient - solid kleur
- [ ] Gebruikt voor:
  - Header backgrounds
  - Section dividers
  - Hero sections
  - Footer designs

**CSS Implementatie:**
```css
/* Diagonaal vlak met clip-path */
.diagonal-section {
  background: #24BEDF; /* Cyaan */
  clip-path: polygon(0 0, 100% 0, 100% 85%, 0 100%);
  padding: 60px 20px;
}

/* Alternatief: SVG background */
.diagonal-bg {
  background-image: url('diagonal-cyan.svg');
  background-size: cover;
  background-position: top right;
}
```

**Diagonal Checklist:**
- [ ] Is de kleur CED cyaan (geen random blauw)?
- [ ] Is het een **scherpe** diagonal (niet gebogen)?
- [ ] Geen gradient gebruikt (solid fill)?
- [ ] Klopt de richting (meestal rechtsboven → linksonder)?

---

## ♿ Accessibility (WCAG) Check

### Stap 21: Contrast Ratio Check

**WCAG AA Minimums (STRIKT):**
- [ ] Normal text (< 18px): contrast ratio ≥ **4.5:1**
- [ ] Large text (≥ 18px): contrast ratio ≥ **3:1**
- [ ] UI components (buttons, icons): contrast ratio ≥ **3:1**

**Geteste CED Kleur Combinaties:**

**✅ Goede Contrast Combinaties:**
- [ ] `#57257C` (Purple) op `white` - **7.9:1** ✅
- [ ] `#92278f` (Paars) op `white` - **7.2:1** ✅
- [ ] `#222222` (Dark Text) op `white` - **16.1:1** ✅
- [ ] `#000000` (Zwart) op `white` - **21:1** ✅
- [ ] `white` op `#57257C` - **7.9:1** ✅
- [ ] `white` op `#92278f` - **7.2:1** ✅
- [ ] `#000000` (Zwart) op `#fbe54a` (Geel CTA) - **16.8:1** ✅

**⚠️ Twijfelachtige Combinaties (Alleen voor Grote Tekst):**
- [ ] `#24BEDF` (Cyan) op `white` - **2.4:1** ⚠️ (alleen ≥18px, bold)
- [ ] `#00bfe0` (Cyaan) op `white` - **2.6:1** ⚠️ (alleen ≥18px, bold)

**❌ Slechte Contrast Combinaties (VERMIJD):**
- [ ] `#EDE9F2` (Light Purple) op `white` - **Te laag** ❌
- [ ] `#d3b5d7` (Paars 30%) op `white` - **Te laag voor tekst** ❌
- [ ] Lichte kleuren op lichte achtergronden
- [ ] Geel op wit (te weinig contrast)

**Contrast Checker Tool:**
```javascript
// Via Playwright voor live site check
await mcp__playwright__browser_evaluate({
  script: `
    // Check contrast van alle tekst elementen
    const elements = document.querySelectorAll('p, h1, h2, h3, h4, h5, h6, a, button, span');
    const lowContrastElements = [];

    elements.forEach(el => {
      const styles = getComputedStyle(el);
      const color = styles.color;
      const bgColor = styles.backgroundColor;
      const fontSize = parseFloat(styles.fontSize);

      // Bereken contrast ratio (vereenvoudigd)
      // In productie: gebruik contrast-ratio library

      if (contrastRatio < 4.5 && fontSize < 18) {
        lowContrastElements.push({
          element: el.tagName + '.' + el.className,
          color: color,
          background: bgColor,
          fontSize: fontSize
        });
      }
    });

    return lowContrastElements;
  `
});
```

### Stap 22: Keyboard Navigation Check

**Focus States:**
- [ ] Alle interactieve elementen hebben zichtbare focus state
- [ ] Focus outline: CED purple (`#57257C`) of cyan (`#24BEDF`)
- [ ] Outline width: `2px` tot `3px`
- [ ] Geen `outline: none` zonder alternatieve focus styling

```css
/* Correcte focus states */
a:focus,
button:focus,
input:focus {
  outline: 2px solid #57257C; /* CED Purple */
  outline-offset: 2px;
}

/* Alternatief: box-shadow focus */
.btn:focus {
  outline: none;
  box-shadow: 0 0 0 3px rgba(87, 37, 124, 0.4); /* Visible alternative */
}
```

**Tab Order:**
- [ ] Logische tab volgorde (links naar rechts, boven naar beneden)
- [ ] Geen `tabindex` > 0 (breekt natuurlijke volgorde)
- [ ] Skip links voor lange navigaties
- [ ] Focus traps in modals werken correct

### Stap 23: Alt Text & Semantic HTML Check

**Images:**
- [ ] Alle `<img>` elementen hebben `alt` attribute
- [ ] Alt text is beschrijvend (niet "image1.jpg")
- [ ] Decoratieve images: `alt=""` (empty maar aanwezig)
- [ ] Hero images hebben betekenisvolle alt text

**Semantic HTML:**
- [ ] Gebruik `<header>`, `<nav>`, `<main>`, `<footer>`, `<article>`, `<section>`
- [ ] Heading hiërarchie klopt (H1 → H2 → H3, geen sprongen)
- [ ] Buttons zijn `<button>`, geen `<div onclick>`
- [ ] Links zijn `<a href>`, geen `<span onclick>`

**ARIA Labels:**
- [ ] Interactieve elementen zonder tekst hebben `aria-label`
- [ ] Icon buttons: `aria-label="Sluiten"`, `aria-label="Menu"`
- [ ] Complex componenten gebruiken ARIA waar nodig
- [ ] Geen overmatig ARIA gebruik (semantic HTML is beter)

### Stap 24: Responsive & Mobile Accessibility

**Touch Targets:**
- [ ] Minimum touch target size: `44px × 44px` (WCAG AAA)
- [ ] Buttons en links zijn groot genoeg op mobile
- [ ] Adequate spacing tussen clickable elementen (8px minimum)

**Font Sizes (Mobile):**
- [ ] Minimum `16px` op mobile (voorkomt auto-zoom iOS)
- [ ] Tekst is leesbaar zonder pinch-to-zoom
- [ ] Line height adequate voor small screens (`1.5` minimum)

**Viewport & Zoom:**
- [ ] `<meta name="viewport" content="width=device-width, initial-scale=1">`
- [ ] GEEN `maximum-scale=1` of `user-scalable=no` (blokkeert zoom)
- [ ] Tekst reflows bij 200% zoom (geen horizontal scroll)

### Stap 25: Screen Reader Compatibility

**Landmarks:**
- [ ] Page heeft `<main>` landmark
- [ ] Navigatie in `<nav>` landmark
- [ ] Meerdere navigaties hebben `aria-label` ("Hoofdnavigatie", "Footer links")

**Hidden Content:**
- [ ] Visueel hidden maar screen reader accessible:
  ```css
  .sr-only {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    white-space: nowrap;
    border: 0;
  }
  ```

**Live Regions:**
- [ ] Dynamic content updates gebruiken `aria-live`
- [ ] Error messages zijn announced
- [ ] Success notifications zijn announced

---

## 🌐 Live Site Analysis (Optional)

### Stap 16: Navigate to Site
```javascript
await mcp__playwright__browser_navigate({ url: user_provided_url })
```

### Stap 17: Extract Computed Styles
```javascript
await mcp__playwright__browser_evaluate({
  script: `
    const results = { colors: [], fonts: [], buttons: [], cards: [] };

    // Extract colors
    document.querySelectorAll('*').forEach(el => {
      const styles = getComputedStyle(el);
      if (styles.backgroundColor && styles.backgroundColor !== 'rgba(0, 0, 0, 0)') {
        results.colors.push({
          element: el.tagName + (el.className ? '.' + el.className.split(' ')[0] : ''),
          background: styles.backgroundColor
        });
      }
    });

    // Extract fonts
    document.querySelectorAll('h1, h2, h3, p, body').forEach(el => {
      const styles = getComputedStyle(el);
      results.fonts.push({
        element: el.tagName,
        family: styles.fontFamily,
        size: styles.fontSize,
        weight: styles.fontWeight
      });
    });

    // Extract buttons
    document.querySelectorAll('button, .btn, [role="button"]').forEach(el => {
      const styles = getComputedStyle(el);
      results.buttons.push({
        text: el.textContent.trim().substring(0, 20),
        background: styles.backgroundColor,
        borderRadius: styles.borderRadius,
        padding: styles.padding,
        fontSize: styles.fontSize
      });
    });

    // Extract cards
    document.querySelectorAll('.card, [class*="card"]').forEach(el => {
      const styles = getComputedStyle(el);
      results.cards.push({
        class: el.className,
        borderRadius: styles.borderRadius,
        boxShadow: styles.boxShadow,
        background: styles.backgroundColor
      });
    });

    return results;
  `
})
```

### Stap 18: Take Screenshots
```javascript
await mcp__playwright__browser_take_screenshot({
  name: "homepage-full",
  fullPage: true
})
```

### Stap 19: Analyze Extracted Data
- [ ] Parse extracted colors en vergelijk met CED palette
- [ ] Check fonts tegen Aglet Slab requirement
- [ ] Review button styling
- [ ] Check card design (border-radius, shadows)

---

## 📊 Report Generation

### Stap 20: Bereken Compliance Score
```
Compliant items / Total items = Compliance %
```

Categoriseer als:
- **✅ Excellent**: 90-100% compliant
- **⚠️  Good**: 70-89% compliant
- **❌ Needs Work**: < 70% compliant

### Stap 21: Structureer Findings
Organiseer findings per categorie:
1. **Color Compliance**
2. **Typography Compliance**
3. **Component Styling**
4. **Spacing & Layout**

Voor **elke issue**:
- Bestandsnaam en regel nummer (of element selector voor live site)
- Huidige waarde
- Gewenste waarde
- Impact niveau (High/Medium/Low)
- Code snippet met fix

### Stap 22: Prioriteer Action Items
Maak 3 categorieën:
- **🔴 Priority 1 (High Impact)**: Brand identity issues (wrong colors, missing Aglet Slab)
- **🟡 Priority 2 (Medium Impact)**: Component styling issues (button radius, card shadows)
- **🟢 Priority 3 (Low Impact)**: Spacing tweaks, minor improvements

---

## 📝 Reporting Format

### Template voor Report

```markdown
# CED Brand Compliance Report

**Project:** [Project naam]
**Review Date:** [Datum]
**Reviewer:** Emma de Vries - CED Brand Checker

---

## Executive Summary

**Overall Compliance:** [XX%] [✅/⚠️/❌]

- ✅ Compliant items: [X]
- ⚠️  Warning items: [Y]
- ❌ Non-compliant items: [Z]

**Key Findings:**
- [Bullet point samenvatting van belangrijkste issues]

---

## 1. Color Compliance

### ✅ Correct Usage
- [List items that are correct]

### ❌ Issues Found

#### Issue #1: Non-CED Blue in Primary Button
- **File:** `src/styles/buttons.css:24`
- **Current:** `background: #2563eb;` (generic blue)
- **Should be:** `background: #57257C;` (CED Purple Dark)
- **Impact:** 🔴 High - Breaks primary brand identity
- **Fix:**
  ```css
  .btn-primary {
    background: #57257C; /* CED Purple Dark */
  }
  ```

[Repeat voor elke issue]

---

## 2. Typography Compliance

### ✅ Correct Usage
- [List items]

### ❌ Issues Found

[Similar structure]

---

## 3. Component Styling

[Similar structure]

---

## 4. Spacing & Layout

[Similar structure]

---

## Action Items

### 🔴 Priority 1 (Critical)
1. [Action item]
2. [Action item]

### 🟡 Priority 2 (Important)
1. [Action item]

### 🟢 Priority 3 (Nice-to-have)
1. [Action item]

---

## Quick Fixes

```css
/* File: src/styles/buttons.css */

/* BEFORE */
.btn-primary {
  background: #2563eb;
  border-radius: 0.375rem;
}

/* AFTER */
.btn-primary {
  background: #57257C;
  border-radius: 8px;
}
```

---

## Resources

- [CED Brand Guidelines](knowledge/brand-guidelines.md)
- [Design Examples](knowledge/examples.md)
- [CED Website](https://www.cedgroep.nl)

---

## Next Steps

1. [Recommended next action]
2. [Follow-up suggestion]

**Questions?** Vraag gerust - ik help je graag met implementatie!
```

---

## 🤝 Post-Review Actions

### Stap 23: Offer Implementation Help
Vraag altijd aan de user:
- [ ] "Wil je dat ik de issues automatisch fix?"
- [ ] "Zal ik gecorrigeerde CSS/code genereren?"
- [ ] "Moet ik design tokens of CSS variables aanmaken?"
- [ ] "Wil je een migratie guide voor grote wijzigingen?"

### Stap 24: Create Fixes (if requested)
Als user om fixes vraagt:
- [ ] Gebruik Edit tool voor kleine wijzigingen
- [ ] Genereer complete nieuwe bestanden voor grote rewrites
- [ ] Maak CSS variables voor brand colors als die niet bestaan
- [ ] Test changes (indien mogelijk)

### Stap 25: Documentation
- [ ] Update project documentation met nieuwe brand standards
- [ ] Maak een "Brand Compliance Checklist" voor team
- [ ] Suggest design token system als dat nog niet bestaat

---

## 💡 Tips & Best Practices

### Wees Constructief
- Leg altijd **waarom** iets niet compliant is
- Geef **specifieke fixes** met code examples
- Prioriteer issues op impact

### Wees Grondig
- Check niet alleen CSS - ook inline styles, JS style injections
- Kijk naar design tokens, CSS variables, theme files
- Check zowel light als dark mode (als applicable)

### Wees Praktisch
- Aglet Slab niet beschikbaar? Suggest hoe te laden + fallbacks
- Overweeg technische constraints (3rd party components)
- Geef migratie strategies voor grote changes

### Wees Proactief
- Suggest CSS variables voor brand colors als die niet bestaan
- Recommend design token systeem voor consistency
- Propose component library aligned met CED brand

---

## 🚨 Common Pitfalls

**Vergeet niet:**
- [ ] Cards moeten **0px border-radius** hebben (niet 8px/12px!)
- [ ] Box-shadows zijn **verboden** in CED design
- [ ] `#2563eb` is een veel voorkomende fout (Tailwind default blue)
- [ ] Font sizes mogen **nooit onder 14px**
- [ ] Aglet Slab moet **altijd** de primary font zijn

---

## ✅ Checklist Complete

Als je alle stappen hebt gevolgd:
- [ ] Alle kleuren gecheckt tegen CED palette
- [ ] Typography volledig gereviewd
- [ ] Alle buttons, cards, inputs gecheckt
- [ ] Spacing en layout geanalyseerd
- [ ] Report gegenereerd met prioriteiten
- [ ] Fixes aangeboden aan user

**Je bent klaar!** 🎉

---

---

## 📚 Quick Reference - Digitale Brand Guidelines

**Kleuren (Digitaal):**
- Purple Dark: `#57257C` - Primary buttons, headers
- Magenta: `#9C2D8A` - Hover states, secondary
- Cyan: `#24BEDF` - Interactive, links
- Teal: `#1EA1BD` - Accents
- Light Purple: `#EDE9F2` - Backgrounds
- Geel CTA: `#fbe54a` - **MAX 1x per pagina!**

**Typography (Digitaal):**
- Headers: **Aglet Slab Bold** (40px H1 → 16px H6)
- Body: **Verdana Regular** (16-20px)
- Minimum: **14px** (nooit kleiner)
- Line height: **1.5-1.7** voor body

**Component Specificaties:**
- Buttons: 8px radius, no shadow, purple background
- Cards: **0px radius**, no shadow, flat design
- Kaders: **2+2 hoeken** (2 rond, 2 scherp)
- Inputs: 4px radius, 16px minimum size
- CTA's: **MAX 1 opvallend** per pagina

**Spacing:**
- Grid systeem: **8px** multiples
- Section padding: 40-80px vertical
- Card gaps: 32px
- Touch targets: 44×44px minimum

**Accessibility:**
- Contrast: ≥ 4.5:1 voor text < 18px
- Focus states: 2-3px purple outline
- Alt text op alle images
- Semantic HTML & ARIA labels

**Kritieke "DON'Ts":**
- ❌ NO box-shadows op cards
- ❌ NO border-radius op cards (must be 0px)
- ❌ NO meer dan 1 gele/paarse CTA per pagina
- ❌ NO font sizes onder 14px
- ❌ NO gradients (alleen solid kleuren)
- ❌ NO tekst over beeld zonder egale achtergrond
- ❌ NO random kleuren buiten CED palette

---

**Document Versie:** 2.0 (Updated met volledige Brand Guide Mei 2023)
**Laatst bijgewerkt:** 2025-11-04
**Eigenaar:** Emma de Vries - CED Brand Checker
**Bronnen:**
- CED-Groep Brand Guide (Mei 2023) - Complete 43 pagina's
- Digital Implementation Guidelines (talent-selector.html)
- WCAG 2.1 AA Accessibility Standards
