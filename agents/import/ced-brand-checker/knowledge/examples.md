# CED Brand Compliance Examples

Dit document toont praktische voorbeelden van **goede** (✅) en **slechte** (❌) implementaties van CED brand guidelines.

---

## 🎨 Color Examples

### Example 1: Primary Button

#### ✅ GOED - CED Compliant Button

```css
.btn-primary {
  background-color: #57257C; /* ✅ CED Purple Dark */
  color: white;
  border-radius: 8px;        /* ✅ CED standard border radius */
  padding: 8px 20px;         /* ✅ Correct padding */
  font-size: 16px;
  font-weight: 600;
  border: none;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.btn-primary:hover {
  background-color: #9C2D8A; /* ✅ CED Magenta for hover */
}
```

**Waarom goed:**
- Gebruikt CED Purple Dark (`#57257C`) als primary kleur
- Hover state gebruikt CED Magenta (`#9C2D8A`)
- Border radius is exact `8px`
- Padding volgt CED standaard
- Font weight is correct (`600`)

#### ❌ FOUT - Non-Compliant Button

```css
.btn-primary {
  background-color: #2563eb; /* ❌ Generic Tailwind blue */
  color: white;
  border-radius: 0.375rem;   /* ❌ Wrong unit (rem) en waarde */
  padding: 0.5rem 1rem;      /* ❌ Rem units in plaats van px */
  font-size: 14px;           /* ⚠️  Te klein, moet 16px zijn */
  font-weight: 500;          /* ⚠️  Te licht, moet 600 zijn */
  border: none;
  box-shadow: 0 1px 3px rgba(0,0,0,0.1); /* ❌ Shadows niet toegestaan */
}
```

**Waarom fout:**
- `#2563eb` is niet in CED palette (Tailwind default blue)
- Gebruikt `rem` units in plaats van `px`
- Border radius `0.375rem` (~6px) is niet exact `8px`
- Font size te klein (`14px` i.p.v. `16px`)
- Font weight te licht (`500` i.p.v. `600`)
- Box-shadow is niet toegestaan (flat design)

**Fix:**
```css
/* Vervang met bovenstaande ✅ GOED voorbeeld */
```

---

### Example 2: Card Styling

#### ✅ GOED - CED Compliant Card

```css
.card {
  background: #F1F1F1;       /* ✅ CED neutral gray */
  border-radius: 0px;        /* ✅ Sharp corners - CED flat design */
  padding: 20px;             /* ✅ Standard internal padding */
  margin-bottom: 32px;       /* ✅ 8px grid system (32 = 4×8) */
  box-shadow: none;          /* ✅ Flat design - geen shadows */
  border: 1px solid #E0E0E0; /* ✅ Optionele subtiele border */
}

.card-title {
  color: #57257C;            /* ✅ CED Purple for headings */
  font-size: 24px;
  font-weight: 600;
  margin-bottom: 16px;
}
```

**Waarom goed:**
- Border radius is **exact 0px** (sharp corners)
- Geen box-shadow (flat design principe)
- Gebruikt CED neutral gray voor background
- Spacing volgt 8px grid (16px, 20px, 32px)
- Title gebruikt CED Purple

#### ❌ FOUT - Over-Styled Card

```css
.card {
  background: white;
  border-radius: 12px;       /* ❌ Rounded corners niet toegestaan */
  padding: 1.5rem;           /* ⚠️  Gebruik px, niet rem */
  margin-bottom: 24px;       /* ⚠️  Niet 8px grid aligned (moet 32px) */
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
              0 2px 4px -1px rgba(0, 0, 0, 0.06); /* ❌ Heavy shadow */
  transition: transform 0.2s, box-shadow 0.2s;
}

.card:hover {
  transform: translateY(-4px); /* ❌ Lift effect niet CED stijl */
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1); /* ❌ */
}
```

**Waarom fout:**
- `border-radius: 12px` - cards moeten 0px zijn
- Box-shadow gebruikt (flat design verbiedt dit)
- Hover lift effect past niet bij CED flat design
- Rem units i.p.v. px
- Margin niet aligned met 8px grid

**Fix:**
```css
/* Vervang met bovenstaande ✅ GOED voorbeeld */
/* Verwijder alle box-shadows en border-radius */
```

---

### Example 3: Typography

#### ✅ GOED - CED Compliant Typography

```css
/* Font loading */
@import url('https://fonts.cdnfonts.com/css/aglet-slab');

body {
  font-family: "Aglet Slab", "Roboto Slab", Georgia, serif; /* ✅ Aglet Slab first */
  font-size: 20px;           /* ✅ CED body size */
  font-weight: 400;          /* ✅ Regular weight */
  line-height: 1.6;          /* ✅ Goede leesbaarheid */
  color: #222222;            /* ✅ CED dark text */
}

h1 {
  font-family: "Aglet Slab", "Roboto Slab", Georgia, serif;
  font-size: 40px;           /* ✅ CED H1 size */
  font-weight: 600;          /* ✅ Semibold */
  line-height: 1.2;
  color: #57257C;            /* ✅ CED Purple */
  margin-bottom: 24px;
}

h2 {
  font-family: "Aglet Slab", "Roboto Slab", Georgia, serif;
  font-size: 32px;           /* ✅ CED H2 size */
  font-weight: 600;
  line-height: 1.3;
  color: #57257C;
  margin-bottom: 16px;
}

.small-text {
  font-size: 16px;           /* ✅ Above minimum (14px) */
  color: #495057;            /* ✅ CED gray text */
}
```

**Waarom goed:**
- Aglet Slab is de primary font
- Goede fallback stack (Roboto Slab, Georgia, serif)
- Font sizes kloppen (H1: 40px, H2: 32px, body: 20px)
- Alle text boven minimum van 14px
- Gebruikt CED Purple voor headings
- Line heights zorgen voor goede leesbaarheid

#### ❌ FOUT - Non-Compliant Typography

```css
body {
  font-family: "Helvetica Neue", Arial, sans-serif; /* ❌ Geen Aglet Slab */
  font-size: 16px;           /* ⚠️  Te klein, moet 20px */
  font-weight: 300;          /* ❌ Te licht, moet 400 */
  color: #000000;            /* ⚠️  Pure black, gebruik #222222 */
}

h1 {
  font-family: "Roboto", sans-serif; /* ❌ Verkeerde font */
  font-size: 36px;           /* ⚠️  Te klein, moet 40px */
  font-weight: 700;          /* ⚠️  Te bold, moet 600 */
  color: #333;
}

.caption {
  font-size: 12px;           /* ❌ Onder minimum van 14px! */
  font-weight: 300;          /* ❌ Te licht */
}
```

**Waarom fout:**
- Helvetica/Arial zonder Aglet Slab
- Body font te klein (16px i.p.v. 20px)
- Font weights verkeerd (300 te licht, 700 te bold)
- Caption text onder 14px minimum
- Pure black (#000) i.p.v. CED dark gray (#222222)

**Fix:**
```css
/* Vervang met bovenstaande ✅ GOED voorbeeld */
/* Laad Aglet Slab en pas alle font sizes aan */
```

---

## 🔘 Component Examples

### Example 4: Navigation Bar

#### ✅ GOED - CED Compliant Nav

```html
<nav class="main-nav">
  <div class="nav-container">
    <div class="nav-logo">
      <img src="ced-logo.svg" alt="CED-Groep">
    </div>
    <ul class="nav-links">
      <li><a href="#" class="nav-link">Diensten</a></li>
      <li><a href="#" class="nav-link">Over Ons</a></li>
      <li><a href="#" class="nav-link">Contact</a></li>
    </ul>
    <button class="btn-primary">Inschrijven</button>
  </div>
</nav>

<style>
.main-nav {
  background: white;
  padding: 16px 0;
  border-bottom: 1px solid #E0E0E0; /* ✅ Subtiele border */
}

.nav-link {
  color: #222222;            /* ✅ CED dark text */
  font-size: 16px;
  font-weight: 400;
  text-decoration: none;
  padding: 8px 16px;
  transition: color 0.2s ease;
}

.nav-link:hover {
  color: #24BEDF;            /* ✅ CED Cyan for hover */
}

.btn-primary {
  background-color: #57257C; /* ✅ CED Purple */
  color: white;
  border-radius: 8px;
  padding: 8px 20px;
  font-size: 16px;
  font-weight: 600;
  border: none;
}
</style>
```

**Waarom goed:**
- Clean, flat design
- CED kleuren consequent toegepast
- Hover states gebruiken CED Cyan
- Button volgt CED button specs
- Goede spacing (8px grid)

#### ❌ FOUT - Non-Compliant Nav

```html
<style>
.main-nav {
  background: linear-gradient(to right, #667eea, #764ba2); /* ❌ Gradient */
  padding: 20px 0;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1); /* ❌ Shadow */
}

.nav-link {
  color: #3b82f6;            /* ❌ Wrong blue */
  font-size: 14px;           /* ⚠️  Te klein voor nav */
  font-weight: 500;
  text-decoration: underline; /* ⚠️  Niet nodig in nav */
}

.btn-primary {
  background-color: #3b82f6; /* ❌ Wrong blue */
  border-radius: 999px;      /* ❌ Pill shape niet CED stijl */
  padding: 12px 24px;        /* ⚠️  Verkeerde padding */
}
</style>
```

**Waarom fout:**
- Gradient backgrounds niet CED stijl
- Box-shadow niet toegestaan
- Verkeerde kleuren (`#3b82f6`, `#667eea`, `#764ba2`)
- Pill-shaped button (999px border-radius)
- Font sizes en paddings kloppen niet

---

### Example 5: Hero Section

#### ✅ GOED - CED Compliant Hero

```html
<section class="hero">
  <div class="container">
    <h1 class="hero-title">Als leren je lief is</h1>
    <p class="hero-description">
      CED-Groep biedt hoogwaardige opleidingen en trainingen
      voor professionals in de educatieve sector.
    </p>
    <button class="btn-primary">Ontdek ons aanbod</button>
  </div>
</section>

<style>
.hero {
  background-color: #24BEDF;  /* ✅ CED Cyan for hero background */
  padding: 80px 0;            /* ✅ Generous vertical spacing */
  text-align: center;
}

.hero-title {
  font-family: "Aglet Slab", serif;
  font-size: 40px;            /* ✅ CED H1 size */
  font-weight: 600;
  color: white;               /* ✅ White on cyan background */
  margin-bottom: 24px;
}

.hero-description {
  font-size: 20px;            /* ✅ CED body size */
  color: white;
  max-width: 600px;
  margin: 0 auto 32px;
  line-height: 1.6;
}

.btn-primary {
  background-color: #57257C;  /* ✅ CED Purple button */
  color: white;
  border-radius: 8px;
  padding: 12px 32px;         /* ✅ Slightly larger for hero CTA */
  font-size: 18px;
  font-weight: 600;
}
</style>
```

**Waarom goed:**
- Hero background gebruikt CED Cyan (`#24BEDF`)
- Generous spacing (80px vertical padding)
- Typography volgt CED specs
- Button gebruikt CED Purple
- White text heeft goed contrast op cyan background
- Clean, focused design

#### ❌ FOUT - Non-Compliant Hero

```html
<style>
.hero {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); /* ❌ */
  padding: 40px 20px;         /* ⚠️  Te weinig padding */
  text-align: center;
  box-shadow: inset 0 0 100px rgba(0,0,0,0.2); /* ❌ Inner shadow */
}

.hero-title {
  font-family: "Poppins", sans-serif; /* ❌ Verkeerde font */
  font-size: 48px;            /* ⚠️  Te groot */
  font-weight: 700;           /* ⚠️  Te bold */
  color: white;
  text-shadow: 2px 2px 4px rgba(0,0,0,0.3); /* ❌ Text shadow */
  margin-bottom: 16px;
}

.hero-description {
  font-size: 16px;            /* ⚠️  Te klein */
  color: rgba(255,255,255,0.9);
}

.btn-primary {
  background: linear-gradient(to right, #f093fb, #f5576c); /* ❌ */
  border-radius: 50px;        /* ❌ Pill shape */
  padding: 15px 40px;
  box-shadow: 0 4px 15px rgba(0,0,0,0.2); /* ❌ Button shadow */
}
</style>
```

**Waarom fout:**
- Gradient backgrounds (niet CED stijl)
- Text shadows en box shadows (flat design)
- Verkeerde font (Poppins i.p.v. Aglet Slab)
- Pill-shaped button
- Font sizes kloppen niet
- Kleuren niet uit CED palette

---

## 📱 Layout Examples

### Example 6: Card Grid

#### ✅ GOED - CED Compliant Grid

```html
<section class="services-section">
  <div class="container">
    <h2 class="section-title">Onze Diensten</h2>
    <div class="card-grid">
      <div class="card">
        <h3 class="card-title">Opleiding & Training</h3>
        <p class="card-description">
          Hoogwaardige opleidingen voor professionals.
        </p>
      </div>
      <div class="card">
        <h3 class="card-title">Consultancy</h3>
        <p class="card-description">
          Expert advies voor educatieve organisaties.
        </p>
      </div>
      <div class="card">
        <h3 class="card-title">E-learning</h3>
        <p class="card-description">
          Digitale leeroplossingen op maat.
        </p>
      </div>
    </div>
  </div>
</section>

<style>
.services-section {
  background: white;
  padding: 40px 0 80px;       /* ✅ CED section spacing */
}

.section-title {
  font-size: 32px;            /* ✅ CED H2 size */
  font-weight: 600;
  color: #57257C;             /* ✅ CED Purple */
  text-align: center;
  margin-bottom: 32px;
}

.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 32px;                  /* ✅ 8px grid system */
}

.card {
  background: #F1F1F1;        /* ✅ CED neutral gray */
  border-radius: 0px;         /* ✅ Sharp corners */
  padding: 20px;              /* ✅ Standard padding */
  box-shadow: none;           /* ✅ Flat design */
}

.card-title {
  font-size: 24px;
  font-weight: 600;
  color: #57257C;             /* ✅ CED Purple */
  margin-bottom: 16px;
}

.card-description {
  font-size: 16px;
  color: #495057;             /* ✅ CED gray text */
  line-height: 1.6;
}
</style>
```

**Waarom goed:**
- Section padding volgt CED standaard (40px/80px)
- Grid gap is 32px (8px grid system)
- Cards hebben 0px border-radius
- Geen box-shadows (flat design)
- Kleuren uit CED palette
- Goede spacing en hierarchy

#### ❌ FOUT - Non-Compliant Grid

```html
<style>
.services-section {
  background: #f9fafb;
  padding: 60px 0;            /* ⚠️  Niet CED standaard */
}

.card-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;                  /* ⚠️  Niet 8px grid aligned */
}

.card {
  background: white;
  border-radius: 16px;        /* ❌ Rounded corners */
  padding: 24px;
  box-shadow: 0 10px 25px rgba(0,0,0,0.08); /* ❌ Heavy shadow */
  transition: all 0.3s ease;
  border: 1px solid #e5e7eb;
}

.card:hover {
  transform: scale(1.05);     /* ❌ Scale effect niet CED stijl */
  box-shadow: 0 20px 40px rgba(0,0,0,0.12); /* ❌ */
}

.card-title {
  font-size: 20px;            /* ⚠️  Te klein */
  font-weight: 700;           /* ⚠️  Te bold */
  color: #1f2937;
  margin-bottom: 12px;
}
</style>
```

**Waarom fout:**
- Rounded corners op cards (16px)
- Box-shadows gebruikt
- Hover scale effect past niet bij flat design
- Spacing niet CED standaard
- Font weight te bold (700 i.p.v. 600)

---

## 🎯 Complete Page Example

### ✅ GOED - Volledig CED Compliant Page

```html
<!DOCTYPE html>
<html lang="nl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CED-Groep - Als leren je lief is</title>
  <link href="https://fonts.cdnfonts.com/css/aglet-slab" rel="stylesheet">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: "Aglet Slab", "Roboto Slab", Georgia, serif;
      font-size: 20px;
      font-weight: 400;
      line-height: 1.6;
      color: #222222;
    }

    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 0 20px;
    }

    /* Hero Section */
    .hero {
      background-color: #24BEDF;
      padding: 80px 0;
      text-align: center;
    }

    .hero h1 {
      font-size: 40px;
      font-weight: 600;
      color: white;
      margin-bottom: 24px;
    }

    .hero p {
      font-size: 20px;
      color: white;
      max-width: 600px;
      margin: 0 auto 32px;
    }

    /* Buttons */
    .btn-primary {
      background-color: #57257C;
      color: white;
      border-radius: 8px;
      padding: 8px 20px;
      font-size: 16px;
      font-weight: 600;
      border: none;
      cursor: pointer;
      transition: background-color 0.2s ease;
    }

    .btn-primary:hover {
      background-color: #9C2D8A;
    }

    /* Services Section */
    .services {
      background: #EDE9F2;
      padding: 40px 0 80px;
    }

    .services h2 {
      font-size: 32px;
      font-weight: 600;
      color: #57257C;
      text-align: center;
      margin-bottom: 32px;
    }

    .card-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 32px;
    }

    .card {
      background: #F1F1F1;
      border-radius: 0px;
      padding: 20px;
      box-shadow: none;
    }

    .card h3 {
      font-size: 24px;
      font-weight: 600;
      color: #57257C;
      margin-bottom: 16px;
    }

    .card p {
      font-size: 16px;
      color: #495057;
    }
  </style>
</head>
<body>
  <section class="hero">
    <div class="container">
      <h1>Als leren je lief is</h1>
      <p>CED-Groep biedt hoogwaardige opleidingen en trainingen voor professionals.</p>
      <button class="btn-primary">Ontdek ons aanbod</button>
    </div>
  </section>

  <section class="services">
    <div class="container">
      <h2>Onze Diensten</h2>
      <div class="card-grid">
        <div class="card">
          <h3>Opleiding & Training</h3>
          <p>Hoogwaardige opleidingen voor professionals.</p>
        </div>
        <div class="card">
          <h3>Consultancy</h3>
          <p>Expert advies voor educatieve organisaties.</p>
        </div>
        <div class="card">
          <h3>E-learning</h3>
          <p>Digitale leeroplossingen op maat.</p>
        </div>
      </div>
    </div>
  </section>
</body>
</html>
```

**Waarom dit perfect is:**
- ✅ Aglet Slab font geladen en gebruikt
- ✅ Alle kleuren uit CED palette
- ✅ Border radius 0px voor cards, 8px voor buttons
- ✅ Geen box-shadows (flat design)
- ✅ Spacing volgt CED standaarden
- ✅ Typography sizes kloppen allemaal
- ✅ Alternerende section backgrounds (cyan → light purple)
- ✅ Clean, professioneel, on-brand

---

## 📊 Quick Reference

### ✅ Altijd Doen
- Aglet Slab als primary font
- CED kleuren uit de palette
- Cards met 0px border-radius
- Buttons met 8px border-radius
- Flat design (geen shadows)
- Font sizes ≥ 14px
- 8px grid spacing systeem
- High contrast (WCAG AA)

### ❌ Nooit Doen
- Generic blues (#2563eb, #3b82f6)
- Rounded cards (12px, 16px radius)
- Box-shadows op cards of sections
- Fonts onder 14px
- Arial/Helvetica zonder Aglet Slab
- Gradients of heavy effects
- Transform/scale hover effects
- Random kleuren buiten palette

---

**Document Versie:** 1.0
**Laatst bijgewerkt:** 2025-01-04
**Gebruik:** Referentie voor brand compliance reviews
