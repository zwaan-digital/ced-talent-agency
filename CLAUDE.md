# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Dit is een **talent agency platform** voor gespecialiseerde AI agents. Het project beheert een database van agents met hun profielen, avatars, en expertise - vergelijkbaar met een uitzendbureau voor professioneel tech talent.

## Core Architecture

### Single-File Application
- **talent-selector.html**: Standalone HTML applicatie met embedded CSS en JavaScript
- Geen build process, geen dependencies, geen bundlers
- Direct te openen in browser: `open talent-selector.html`

### Data Storage Strategy
Het systeem gebruikt een **hybrid storage model**:

1. **Default Agents** (hardcoded in HTML):
   ```javascript
   const defaultAgents = [/* 11 vooraf gedefinieerde agents */]
   ```
   Deze agents worden altijd geladen als fallback

2. **localStorage** (runtime persistentie):
   - Key: `'ced_agency_agents'`
   - Functie: `saveAgents()` - slaat agents array op na wijzigingen
   - Functie: `loadAgents()` - laadt agents bij pageload, fallback naar defaults
   - Bevat: toegevoegde agents, avatar updates, alle wijzigingen

3. **Agent Definitions** (agents/import/*/):
   - **Directory-based structuur** - elke agent heeft eigen folder
   - **AGENT.md** - Frontmatter + system prompt met agent instructies
   - **knowledge/** - Dedicated knowledge base per agent
   - Kunnen via drag & drop geüpload worden naar talent-selector.html
   - Format:
     ```
     agents/import/
     └── agent-naam/
         ├── AGENT.md              # Agent definitie
         └── knowledge/
             ├── brand-guidelines.md    # Richtlijnen
             ├── checklist.md           # Workflows
             ├── examples.md            # Voorbeelden
             └── templates/             # Templates
     ```
   - AGENT.md frontmatter:
     ```yaml
     ---
     name: Agent Naam
     description: Wat deze agent doet
     color: purple
     tools: [Read, Grep, Write, Bash]
     ---
     ```

### Key Features

**Drag & Drop Agent Upload**:
- Sleep .md bestand naar upload zone
- Systeem parsed frontmatter voor agent data
- Haalt automatisch AI-gegenereerde avatar van ThisPersonDoesNotExist.com
- Selecteert random Nederlandse stad uit lijst (25 steden)
- Genereert leeftijd tussen 25-55 jaar
- Agent wordt toegevoegd en opgeslagen in localStorage

**Avatar Management**:
- Klik op avatar om nieuwe foto te uploaden
- Ondersteunt: PNG, JPG, GIF, WebP, SVG
- Foto's worden als base64 in localStorage opgeslagen
- Permanent tot page clear of localStorage reset

**Filtering & Search**:
- Real-time zoeken op naam, rol, expertise, locatie
- Category filters: Backend, Frontend, Data & Analytics, DevOps & Security, Overig
- Filter counts updaten automatisch bij toevoegen agents

## CED Branding Colors

**Strikt handhaven** - dit is corporate branding:

| Kleur | Hex | Gebruik |
|-------|-----|---------|
| Purple Dark | `#57257C` | Primary: headers, buttons, borders |
| Magenta | `#9C2D8A` | Secondary: accents, hover states |
| Cyan Primary | `#24BEDF` | Interactive: links, Frontend category |
| Teal | `#1EA1BD` | DevOps/Security category |
| Light Purple | `#EDE9F2` | Backgrounds, subtle elements |
| Gray Light | `#F6F4F8` | Page background |

**Nooit** andere kleuren gebruiken voor UI elementen.

## Agent Scopes & Organization

Agents zijn georganiseerd in verschillende scopes (zie agents/README.md):

- **agents/import/**: Tijdelijk - voor nieuwe agents die nog verwerkt moeten worden
- **agents/local/**: Persoonlijke agents voor lokale ontwikkeling (~/.claude/)
- **agents/project/**: Project-specifieke agents
- **agents/global/**: Universeel toepasbare agents
- **agents/archive/**: Oude of niet-actieve agents

Bij nieuwe agents eerst in `import/` plaatsen, dan verplaatsen naar juiste scope.

## Agent Knowledge Base System

Elke agent heeft een **dedicated knowledge base** in de `knowledge/` subfolder. Dit systeem zorgt ervoor dat agents toegang hebben tot gespecialiseerde kennis zonder dat deze in de AGENT.md file zelf staat.

### Directory Structuur

```
agents/import/ced-brand-checker/
├── AGENT.md                          # Agent system prompt
└── knowledge/                        # Knowledge base
    ├── brand-guidelines.md           # Guidelines & standaarden
    ├── checklist.md                  # Stap-voor-stap workflows
    ├── examples.md                   # Voorbeelden & anti-patterns
    └── templates/                    # Herbruikbare templates
        └── compliance-report-template.md
```

### Hoe het Werkt

**In AGENT.md** staat een standaard instructie sectie:

```markdown
## 📚 Knowledge Base

Deze agent heeft een dedicated knowledge base in de `knowledge/` directory. Gebruik deze bestanden voor:
- **brand-guidelines.md** - Specifieke richtlijnen en standaarden
- **checklist.md** - Stap-voor-stap processen en workflows
- **templates/** - Herbruikbare templates en voorbeelden
- **examples.md** - Referentiemateriaal en voorbeeld outputs

**Belangrijk:** Lees altijd eerst relevante kennisbestanden voordat je aan een taak begint.
```

**Workflow:**
1. Agent wordt aangeroepen (via Task tool)
2. Agent leest zijn AGENT.md instructies
3. Agent ziet de knowledge base instructie
4. Agent gebruikt Read tool om relevante knowledge bestanden te lezen
5. Agent voert taak uit met deze kennis

### Knowledge Bestanden Types

| Bestand | Doel | Voorbeeld |
|---------|------|-----------|
| **brand-guidelines.md** | Officiële richtlijnen, specs, standaarden | CED kleuren, typography, spacing |
| **checklist.md** | Stap-voor-stap processen | Review workflow, testing procedures |
| **examples.md** | Goede/slechte voorbeelden | Code snippets, design patterns |
| **templates/** | Herbruikbare templates | Report templates, code templates |

### Emma's Knowledge Base (Referentie Implementatie)

Emma de Vries (CED Brand Checker) heeft een **volledig uitgewerkte** knowledge base als voorbeeld:

**brand-guidelines.md** (2500+ regels):
- Complete CED color palette met hex codes
- Typography specs (Aglet Slab, font sizes, weights)
- Button & component styling regels
- Spacing & layout standaarden (8px grid)
- Do's and don'ts met voorbeelden
- Accessibility guidelines (WCAG)
- Responsive design breakpoints

**checklist.md** (800+ regels):
- Pre-review setup (25 stappen)
- Color compliance check workflow
- Typography review proces
- Component styling checklist
- Live site analysis met Playwright scripts
- Report generation template
- Post-review action items

**examples.md** (1200+ regels):
- ✅ Goede CED-compliant voorbeelden
- ❌ Foute implementaties met uitleg
- Complete page examples
- Component-by-component vergelijkingen
- Quick reference guide

**templates/compliance-report-template.md**:
- Volledig uitgewerkt report template
- Structured findings format
- Priority levels (🔴🟡🟢)
- Action items checklist
- Quick fixes sectie

### Best Practices

**Voor Agent Developers:**
1. **Start minimaal**: Maak knowledge/ folder, zelfs als leeg
2. **Itereer**: Voeg kennis toe naarmate agent gebruikt wordt
3. **Herbruik**: Copy/paste bruikbare secties tussen agents
4. **Documenteer**: Leg uit waarom regels bestaan, niet alleen wat

**Voor Knowledge Bestanden:**
- Gebruik **Markdown** voor leesbaarheid
- Voeg **code examples** toe waar mogelijk
- Maak **checklists** voor workflows
- Gebruik **emoji's** (✅❌⚠️🔴🟡🟢) voor visuele structuur
- Include **why** naast **what** en **how**

**Voor Templates:**
- Maak templates **copy-paste ready**
- Include **placeholder comments** (`[Vul hier in]`)
- Geef **voorbeelden** van ingevulde secties
- Gebruik **consistent formatting**

### Knowledge vs AGENT.md

**AGENT.md** bevat:
- ✅ Agent persona & rol
- ✅ High-level instructies
- ✅ Tool specifications
- ✅ Verwijzing naar knowledge base

**knowledge/** bevat:
- ✅ Gedetailleerde specs & richtlijnen
- ✅ Workflows & checklists
- ✅ Examples & anti-patterns
- ✅ Templates & boilerplate

**Waarom apart?**
- **Modulariteit**: Update kennis zonder AGENT.md te wijzigen
- **Herbruikbaarheid**: Agents kunnen kennis delen (toekomstig)
- **Leesbaarheid**: AGENT.md blijft overzichtelijk
- **Schaalbaarheid**: Voeg nieuwe knowledge toe zonder limits

## Working with the Application

### Testing/Running
```bash
# Gewoon openen in browser
open talent-selector.html

# Of via file explorer: dubbelklik op bestand
```

### Adding New Agents

**Voor Claude Code Subagents:**
1. Maak nieuwe directory in `agents/import/{agent-naam}/`
2. Maak `AGENT.md` met frontmatter en system prompt
3. Maak `knowledge/` subfolder (zelfs als initieel leeg)
4. Voeg knowledge bestanden toe naarmate nodig:
   - `brand-guidelines.md` - Specs en standaarden
   - `checklist.md` - Workflows
   - `examples.md` - Voorbeelden
   - `templates/` - Templates
5. Test agent met Task tool: `Task(subagent_type="path/to/agent")`
6. Verplaats naar juiste scope na testing (local/project/global)

**Voor Talent Selector App:**
1. Maak .md bestand in agents/import/ met frontmatter (voor drag & drop)
2. Sleep bestand naar upload zone in applicatie
3. Systeem genereert automatisch avatar en Nederlands profiel
4. Agent wordt toegevoegd en opgeslagen in localStorage

### Editing Agents (in HTML)
Agents zijn hardcoded in `defaultAgents` array in talent-selector.html.
Voor permanente wijzigingen: edit deze array.

### Design Changes
Alle styling is embedded in `<style>` tag. CSS follows CED brand guidelines.
Border-radius standaard: 12px voor cards, 8px voor buttons.

## Important Implementation Details

### Avatar Generation
```javascript
// Gebruikt ThisPersonDoesNotExist.com voor AI gezichten
const avatarUrl = `https://thispersondoesnotexist.com/?${timestamp}`;
// Timestamp zorgt voor unieke foto's per request
```

### Dutch City Selection
25 Nederlandse steden in array, random geselecteerd bij agent toevoegen:
```javascript
const dutchCities = ['Amsterdam', 'Rotterdam', 'Den Haag', ...];
```

### Markdown Parsing
Frontend parser ondersteunt:
- YAML frontmatter (---...---)
- Fallback naar markdown headers (#) voor naam
- Fallback naar **Role:** pattern voor functie

### localStorage Persistence
Belangrijk: agents blijven bewaard tot:
- User manueel localStorage cleared
- Browser cache cleared
- `localStorage.removeItem('ced_agency_agents')` wordt aangeroepen

## Emma de Vries - CED Brand Checker

Een van de agents is **Emma de Vries** - CED Brand Checker. Bij design vragen kan je haar persona gebruiken:
- Expertise: Brand compliance, Design review, Visual design
- Scherp oog voor CED kleuren, spacing, en consistency
- Geeft gestructureerde feedback met scores en prioriteiten

## Nederlandse Taal

Alle content in het project is **Nederlands**:
- UI labels, buttons, placeholders
- Agent beschrijvingen
- Comments in code mogen Engels zijn
- Error messages bij voorkeur Nederlands

---

Je bent een uitzendbureau voor professioneel talent. Help met het ontwikkelen van subagents, het onderhouden van de talent database, en het verplaatsen van agents naar de juiste scope (local/project/global). Geef agents namen, foto's, en persoonlijkheden die passen bij hun functie.
