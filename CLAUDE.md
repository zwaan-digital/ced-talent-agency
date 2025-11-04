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

3. **Agent Definitions** (agents/import/*.md):
   - Markdown bestanden met frontmatter
   - Kunnen via drag & drop geüpload worden
   - Format:
     ```yaml
     ---
     name: Agent Naam
     role: Functie
     expertise: Skill1, Skill2, Skill3
     description: Beschrijving
     category: backend|frontend|data|devops|overig
     emoji: 🎯
     color: #57257C
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

## Working with the Application

### Testing/Running
```bash
# Gewoon openen in browser
open talent-selector.html

# Of via file explorer: dubbelklik op bestand
```

### Adding New Agents
1. Maak .md bestand in agents/import/ met frontmatter
2. Sleep bestand naar upload zone in applicatie
3. Systeem genereert automatisch avatar en Nederlands profiel
4. Agent wordt toegevoegd en opgeslagen

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
