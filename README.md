# 🎯 CED Talent Agency

Welkom bij de CED Talent Agency - jouw professionele uitzendbureau voor gespecialiseerd tech talent!

## 📋 Overzicht

Dit project bevat een complete talent database met 11 gespecialiseerde agents, elk met hun eigen expertise, avatar en persoonlijkheid.

## 🚀 Snel Starten

### Talent Selector Interface

Open `talent-selector.html` in je browser om de interactieve agent selector te gebruiken:

```bash
open talent-selector.html
```

Of dubbelklik op het bestand in je file explorer.

## ✨ Features

### 🎨 Interactieve UI
- **Visuele agent cards** met avatars en profielinformatie
- **Live zoeken** - Zoek op naam, functie, expertise of locatie
- **Categorie filters** - Filter op Backend, Frontend, Data, DevOps of Overig
- **Responsive design** - Werkt op desktop, tablet en mobiel
- **CED branding** - Consistent gebruik van CED kleuren en styling

### 👥 11 Agents Beschikbaar

| Naam | Rol | Locatie | Specialisme |
|------|-----|---------|-------------|
| Sophie van der Berg | Agent Selector | Amsterdam | Talent matching |
| Lars Visser | API Developer | Utrecht | FastAPI, Python |
| Vera Janssen | Beleidsschrijver | Den Haag | Beleidsnota's |
| Emma de Vries | CED Brand Checker | Amsterdam | Brand compliance |
| Thomas Bakker | Database Architect | Eindhoven | PostgreSQL |
| Mark van Dijk | DevOps Engineer | Rotterdam | Docker, Nginx |
| Nina Meijer | Frontend Builder | Amsterdam | Jinja2, JavaScript |
| Ingrid Hendriks | Data Analist | Amstelveen | Power BI, Excel |
| Pascal de Groot | Online Marketeer | Amsterdam | Analytics, SEO |
| Pieter Vermeer | Security Auditor | Utrecht | OWASP, Security |
| Lisa Koolen | Test Engineer | Groningen | pytest, Testing |

## 📁 Project Structuur

```
Agency/
├── talent-selector.html          # 🎨 Interactieve UI interface
├── README.md                     # 📖 Dit bestand
├── TALENT_DATABASE.md            # 📊 Complete talent database
├── AVATAR_MAPPING.md             # 🖼️ Avatar toewijzingen
├── AVATARS.md                    # 📸 Avatar beschrijvingen
│
├── agents/
│   ├── avatars/                  # 🖼️ Agent foto's (11)
│   │   ├── sophie-van-der-berg.jpg
│   │   ├── lars-visser.jpg
│   │   ├── vera-janssen.jpg
│   │   ├── emma-de-vries.jpg
│   │   ├── thomas-bakker.jpg
│   │   ├── mark-van-dijk.jpg
│   │   ├── nina-meijer.jpg
│   │   ├── ingrid-hendriks.jpg
│   │   ├── pascal-de-groot.jpg
│   │   ├── pieter-vermeer.jpg
│   │   └── lisa-koolen.jpg
│   │
│   └── import/                   # 📄 Agent definities (11)
│       ├── agent-selector.md
│       ├── api-developer.md
│       ├── beleidsschrijver.md
│       ├── ced-brand-checker.md
│       ├── database-architect.md
│       ├── devops-engineer.md
│       ├── frontend-builder.md
│       ├── ingrid.md
│       ├── online-marketeer.md
│       ├── security-auditor.md
│       └── test-engineer.md
│
└── CLAUDE.md                     # ⚙️ Project configuratie
```

## 🎯 Gebruik Scenarios

### 1. Agent Selectie via UI
1. Open `talent-selector.html` in je browser
2. Gebruik de zoekbalk om te zoeken op naam, functie of expertise
3. Filter op categorie (Backend, Frontend, Data, DevOps, Overig)
4. Klik op een agent card voor meer details

### 2. Agent Informatie Opzoeken
- Bekijk `TALENT_DATABASE.md` voor een volledig overzicht
- Lees individuele agent bestanden in `agents/import/` voor gedetailleerde profielen

### 3. Agent Integratie in Claude Code
Gebruik agents als subagents in je projecten:

```bash
# Start een agent via Claude Code
/agent-selector    # Voor het kiezen van de juiste specialist
/api-developer     # Voor backend/API werk
/frontend-builder  # Voor UI/templates
/devops-engineer   # Voor deployment
# etc.
```

## 🎨 CED Branding

Alle componenten gebruiken de officiële CED-Groep kleuren:

| Kleur | Hex Code | Gebruik |
|-------|----------|---------|
| **Purple Dark** | `#57257C` | Primary color, headers, belangrijke elementen |
| **Magenta** | `#9C2D8A` | Accenten, secondary elements |
| **Cyan Primary** | `#24BEDF` | Interactive elements, links |
| **Bright Cyan** | `#2BBFDF` | Hover states |
| **Light Purple** | `#EDE9F2` | Backgrounds, subtle accents |
| **Gray Light** | `#F6F4F8` | Page backgrounds |

## 📊 Statistieken

- **Totaal agents:** 11
- **Vrouwen:** 6 (55%)
- **Mannen:** 5 (45%)
- **Leeftijdsbereik:** 27-45 jaar
- **Gemiddelde leeftijd:** ~35 jaar
- **Steden:** 7 (Amsterdam, Utrecht, Den Haag, Rotterdam, Eindhoven, Amstelveen, Groningen)

## 🔧 Technische Details

### UI Interface
- **Pure HTML/CSS/JavaScript** - Geen frameworks nodig
- **Responsive grid layout** - Werkt op alle schermgroottes
- **Fallback avatars** - SVG placeholders als afbeeldingen niet laden
- **Live filtering** - Real-time zoeken en filteren
- **Accessible** - Semantische HTML en keyboard navigatie

### Avatar Specificaties
- **Format:** JPG
- **Afmetingen:** ~512x512px
- **Totale grootte:** 1.1 MB (11 bestanden)
- **Gemiddeld:** ~100 KB per avatar

## 🚀 Toekomstige Uitbreidingen

Ideeën voor verdere ontwikkeling:

1. **Export functionaliteit** - Export agent selectie naar PDF/CSV
2. **Favorieten systeem** - Markeer en bewaar favoriete agents
3. **Vergelijkingsfunctie** - Vergelijk meerdere agents naast elkaar
4. **Booking systeem** - Reserveer agents voor projecten
5. **Review systeem** - Ratings en reviews per agent
6. **API endpoint** - JSON API voor externe integraties
7. **Team builder** - Stel teams samen voor projecten
8. **Skills matrix** - Interactieve expertise visualisatie

## 📝 Documentatie

- **TALENT_DATABASE.md** - Volledig overzicht van alle agents
- **AVATARS.md** - Gedetailleerde avatar beschrijvingen en generatie opties
- **AVATAR_MAPPING.md** - Mapping tussen avatars en agents
- **agents/import/*.md** - Individuele agent profielen met volledige expertise

## 🤝 Contributing

Nieuwe agents toevoegen:

1. Maak een nieuwe `.md` file in `agents/import/`
2. Voeg een avatar toe aan `agents/avatars/`
3. Update `TALENT_DATABASE.md`
4. Update `talent-selector.html` met de nieuwe agent data

## 📞 Contact

Voor vragen over specifieke agents, bekijk hun individuele profielen of gebruik de Agent Selector tool.

---

**Gemaakt met ❤️ door Claude Code**
*"Als leren je lief is" - CED-Groep*

*Laatste update: 4 november 2025*
