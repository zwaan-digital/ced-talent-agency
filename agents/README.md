# CED Agency - Agents Directory

Dit document beschrijft de organisatie van Claude Code subagents in het CED Talent Agency project.

---

## 📁 Directory Structure

```
agents/
├── import/           # 📥 Nieuwe agents (tijdelijk)
├── local/            # 💻 Persoonlijke agents
├── project/          # 📦 Project-specifieke agents
├── global/           # 🌍 Universele agents
├── archive/          # 📁 Oude/inactieve agents
├── avatars/          # 🖼️  Avatar afbeeldingen
└── README.md         # 📖 Deze file
```

### 📥 import/
**Sleep hier je nieuwe agents**
- Tijdelijke locatie voor nieuwe agent definities
- Agents worden hier getest voordat ze naar de juiste scope gaan
- Momenteel: 12 agents (ced-brand-checker, api-developer, etc.)

**Gebruik:**
- Import agents uit andere projecten
- Ontwikkel nieuwe agents
- Test voordat je ze verplaatst naar local/project/global

### 💻 local/
**Agents voor lokale ontwikkeling** (`~/.claude/agents/`)
- Persoonlijke agents die je niet wilt delen
- Experimentele agents in ontwikkeling
- Quick prototypes en utilities

**Wanneer gebruiken:**
- Agent is specifiek voor jouw workflow
- Agent bevat persoonlijke preferences
- Agent is nog in experimentele fase

### 📦 project/
**Agents specifiek voor dit CED project**
- Gecommit in version control
- Gedeeld met team members
- Project-gebonden functionaliteit

**Wanneer gebruiken:**
- Agent is specifiek voor CED Agency platform
- Agent kent CED business logic
- Team moet agent kunnen gebruiken

### 🌍 global/
**Agents voor alle projecten**
- Universeel toepasbare functionaliteit
- Geen project-specifieke dependencies
- Best practices implementations

**Wanneer gebruiken:**
- Agent werkt in elk project (bijv. code reviewer)
- Geen project-specifieke context nodig
- Wil je hergebruiken in andere projecten

### 📁 archive/
**Oude of niet-actieve agents**
- Backup van vervangen agents
- Experimentele agents die niet werkten
- Historische referentie

**Wanneer gebruiken:**
- Agent wordt niet meer gebruikt
- Agent vervangen door betere versie
- Wil je bewaren voor referentie

---

## 🏗️ Agent Structure

### Directory-Based Format

Sinds januari 2025 gebruikt CED Agency een **directory-based structure** waarbij elke agent zijn eigen folder heeft met een dedicated knowledge base.

```
agents/import/ced-brand-checker/
├── AGENT.md                          # Agent definitie
├── AGENT.md.bak                      # Backup (auto-generated)
└── knowledge/                        # Knowledge base
    ├── brand-guidelines.md           # Specs & standaarden
    ├── checklist.md                  # Workflows & processen
    ├── examples.md                   # Code examples
    └── templates/                    # Herbruikbare templates
        └── compliance-report-template.md
```

### AGENT.md Format

```markdown
---
name: Agent Naam
description: Korte beschrijving wat deze agent doet
color: purple
tools: [Read, Grep, Write, Bash, WebFetch]
---

# Agent Titel

## 📚 Knowledge Base

Deze agent heeft een dedicated knowledge base in de `knowledge/` directory...

## 👤 Profiel: Agent Naam
**Naam:** Volledige naam
**Leeftijd:** XX jaar
**Woonplaats:** Nederlandse stad
**Specialisme:** Expertise gebied
**Persoonlijkheid:** Karakteristieken
**Avatar:** 🎯
**Kleur:** #HexCode

---

[Gedetailleerde system prompt met instructies...]
```

### Knowledge Base Files

Elke agent heeft een `knowledge/` folder met gespecialiseerde kennis:

| Bestand | Doel | Voorbeeld Content |
|---------|------|-------------------|
| **brand-guidelines.md** | Officiële specs, richtlijnen, standaarden | Kleuren, typography, spacing regels |
| **checklist.md** | Stap-voor-stap workflows en processen | Review proces, testing checklist |
| **examples.md** | Goede/slechte voorbeelden, code snippets | ✅ Good patterns, ❌ Anti-patterns |
| **templates/** | Herbruikbare templates en boilerplate | Report templates, code skeletons |

---

## 🎯 Current Agents

### Active Agents (import/)

| Agent | Naam | Specialisatie | Knowledge Base |
|-------|------|---------------|----------------|
| **ced-brand-checker** | Emma de Vries | CED brand compliance, design review | ✅ Volledig (4 files) |
| **api-developer** | Lars Visser | Backend/API development | 📝 Basis |
| **frontend-builder** | Nina Meijer | Frontend development | 📝 Basis |
| **database-architect** | Thomas Bakker | Database design & optimization | 📝 Basis |
| **devops-engineer** | Mark van Dijk | Infrastructure, CI/CD, automation | 📝 Basis |
| **security-auditor** | Pieter Vermeer | Security, penetration testing | 📝 Basis |
| **test-engineer** | Lisa Koolen | QA, testing, automation | 📝 Basis |
| **agent-selector** | Sophie van der Berg | Meta agent, coordination | 📝 Basis |
| **avg-expert** | Ingrid Hendriks | Data analytics, GDPR | 📝 Basis |
| **beleidsschrijver** | Vera Janssen | Policy writing, documentation | 📝 Basis |
| **online-marketeer** | Pascal de Groot | Marketing analytics, SEO | 📝 Basis |
| **ingrid** | - | (Duplicate?) | 📝 Basis |

**Status:**
- ✅ **Volledig** = Complete knowledge base met guidelines, checklists, examples, templates
- 📝 **Basis** = Lege knowledge/ folder, klaar voor content

---

## 📚 Emma's Knowledge Base (Reference Implementation)

Emma de Vries (CED Brand Checker) heeft de meest complete knowledge base en dient als **referentie implementatie** voor andere agents.

### Structuur

```
ced-brand-checker/
├── AGENT.md (313 lines)
└── knowledge/
    ├── brand-guidelines.md (600+ lines)
    │   ├── Color palette (primary, neutrals, forbidden)
    │   ├── Typography (Aglet Slab, sizes, weights)
    │   ├── Buttons & components specs
    │   ├── Spacing & layout (8px grid)
    │   ├── Design patterns (do's & don'ts)
    │   └── Accessibility (WCAG)
    │
    ├── checklist.md (450+ lines)
    │   ├── Pre-review setup (3 stappen)
    │   ├── Color compliance check (3 stappen)
    │   ├── Typography check (3 stappen)
    │   ├── Component styling (3 stappen)
    │   ├── Spacing & layout (3 stappen)
    │   ├── Live site analysis (4 stappen met Playwright)
    │   ├── Report generation (3 stappen)
    │   └── Post-review actions (3 stappen)
    │
    ├── examples.md (900+ lines)
    │   ├── 6 complete examples (buttons, cards, typography, nav, hero, grid)
    │   ├── Each with ✅ GOED en ❌ FOUT variants
    │   ├── Full page example (complete HTML/CSS)
    │   └── Quick reference guide
    │
    └── templates/
        └── compliance-report-template.md (350+ lines)
            ├── Executive summary template
            ├── Detailed findings structure
            ├── Priority levels (🔴🟡🟢)
            ├── Action items format
            └── Quick fixes examples
```

### Statistieken

- **Totaal:** ~2500 regels gestructureerde kennis
- **4 bestanden:** guidelines, checklist, examples, template
- **25 stappen:** in review checklist
- **6 voorbeelden:** met good/bad vergelijkingen
- **3 prioriteit levels:** voor action items
- **WCAG compliant:** accessibility guidelines included

### Gebruik als Template

Andere agents kunnen Emma's structuur kopiëren:

```bash
# Kopieer structuur naar nieuwe agent
cp -r agents/import/ced-brand-checker/knowledge/ \
      agents/import/nieuwe-agent/knowledge/

# Pas content aan voor nieuwe agent's domein
```

---

## 🛠️ How-To Guides

### 1. Een Nieuwe Agent Maken

**Stap 1: Maak directory structuur**
```bash
mkdir -p agents/import/mijn-agent/knowledge/templates
touch agents/import/mijn-agent/AGENT.md
```

**Stap 2: Schrijf AGENT.md**
```markdown
---
name: Mijn Agent
description: Wat deze agent doet
color: purple
tools: [Read, Write, Bash]
---

# Mijn Agent

## 📚 Knowledge Base
[Standaard knowledge base instructies...]

## 👤 Profiel
[Agent persona...]

---

[System prompt met instructies...]
```

**Stap 3: Voeg knowledge toe (optioneel)**
```bash
# Maak guidelines bestand
echo "# Guidelines\n..." > agents/import/mijn-agent/knowledge/guidelines.md

# Maak checklist
echo "# Checklist\n..." > agents/import/mijn-agent/knowledge/checklist.md
```

**Stap 4: Test de agent**
```bash
# In Claude Code
Task(subagent_type="agents/import/mijn-agent", prompt="Test taak")
```

**Stap 5: Verplaats naar juiste scope**
```bash
# Na succesvol testen
mv agents/import/mijn-agent agents/project/mijn-agent
```

---

### 2. Knowledge Base Toevoegen aan Bestaande Agent

**Voor Lars (API Developer) - Voorbeeld**

```bash
# Navigeer naar agent
cd agents/import/api-developer/knowledge/

# Maak API guidelines
cat > api-guidelines.md << 'EOF'
# API Development Guidelines

## RESTful API Best Practices
- Use proper HTTP verbs (GET, POST, PUT, DELETE)
- Return appropriate status codes
- Implement pagination for large datasets
...
EOF

# Maak review checklist
cat > checklist.md << 'EOF'
# API Review Checklist

## Security
- [ ] Authentication implemented
- [ ] Authorization checks present
- [ ] Input validation
...
EOF

# Maak examples
cat > examples.md << 'EOF'
# API Examples

## ✅ Good API Endpoint
```python
@app.route('/api/users/<int:user_id>', methods=['GET'])
def get_user(user_id):
    ...
```
...
EOF
```

---

### 3. Agent Verplaatsen Tussen Scopes

**Van import/ naar project/**
```bash
# Check dat agent goed werkt
git status

# Verplaats met git
git mv agents/import/mijn-agent agents/project/mijn-agent

# Commit
git add -A
git commit -m "Move mijn-agent to project scope"
```

**Van project/ naar global/**
```bash
# Verwijder project-specifieke references
# Edit AGENT.md om generiek te maken

# Verplaats
git mv agents/project/mijn-agent agents/global/mijn-agent

git commit -m "Promote mijn-agent to global scope"
```

---

### 4. Agent Archiveren

```bash
# Verplaats naar archive met timestamp
mv agents/import/oude-agent \
   agents/archive/oude-agent-$(date +%Y%m%d)

# Voeg README toe met reden
echo "# Archived: $(date)" > agents/archive/oude-agent-*/README.md
echo "Reden: Vervangen door nieuwe-agent" >> agents/archive/oude-agent-*/README.md
```

---

## 📋 Best Practices

### Agent Development

✅ **DO:**
- Start met lege knowledge/ folder (itereer later)
- Gebruik Emma's structure als template
- Test agent grondig in import/ voordat verplaatsen
- Documenteer waarom regels bestaan, niet alleen wat
- Gebruik emoji's voor visuele structuur (✅❌⚠️🔴🟡🟢)
- Include code examples in knowledge base
- Maak checklists voor complexe workflows

❌ **DON'T:**
- Geen enorme AGENT.md files - use knowledge/ in plaats
- Geen duplicate knowledge tussen agents - hergebruik
- Geen agents direct in project/ - test eerst in import/
- Geen sensitive info in knowledge base

### Knowledge Base

✅ **DO:**
- **Markdown formatting** voor leesbaarheid
- **Tables** voor structured data (specs, comparisons)
- **Code blocks** met syntax highlighting
- **Headings** voor navigatie
- **Lists** voor checklists en requirements
- **Examples** met both good and bad patterns
- **Why explanations** naast what/how

❌ **DON'T:**
- Geen walls of text - gebruik structuur
- Geen verouderde info - maintain actief
- Geen vague guidelines - be specific
- Geen examples zonder uitleg

### Agent Naming

✅ **Good names:**
- `ced-brand-checker` - duidelijk wat het doet
- `api-developer` - functie-gebaseerd
- `security-auditor` - rol-gebaseerd

❌ **Bad names:**
- `emma` - te persoonlijk, niet descriptief
- `agent1` - niet descriptief
- `checker` - te vaag

### Tool Selection

Geef agents **alleen tools die ze nodig hebben**:

```yaml
# Frontend agent
tools: [Read, Write, Grep, WebFetch, mcp__playwright__*]

# Backend agent
tools: [Read, Write, Bash, Grep]

# Brand checker
tools: [Read, Grep, Glob, WebFetch, mcp__playwright__*]

# Security auditor
tools: [Read, Grep, Bash, WebFetch]
```

---

## 🔄 Migration Guide

### Van Single-File naar Directory Structure

**Voor bestaande .md agents:**

```bash
# Voorbeeld: migreer security-auditor.md
AGENT_NAME="security-auditor"

# 1. Maak directory
mkdir -p agents/import/$AGENT_NAME/knowledge

# 2. Verplaats .md naar AGENT.md
mv agents/import/$AGENT_NAME.md \
   agents/import/$AGENT_NAME/AGENT.md

# 3. Voeg knowledge base instructies toe
# (Zie stap 3 van "Een Nieuwe Agent Maken")

# 4. Maak lege knowledge bestanden
touch agents/import/$AGENT_NAME/knowledge/{guidelines,checklist,examples}.md
```

**Batch migratie voor alle agents:**

```bash
# Script in agents/import/
for file in *.md; do
  name="${file%.md}"
  mkdir -p "$name/knowledge"
  mv "$file" "$name/AGENT.md"
  echo "Migrated: $name"
done
```

---

## 📊 Agent Statistics

### Current Status (January 2025)

```
Total agents: 12
├── With full knowledge base: 1 (Emma - CED Brand Checker)
├── With empty knowledge/: 11 (ready for content)
└── Archived: 0

Knowledge base completion:
├── ✅ Complete (100%): 1 agent
├── 📝 Partial (1-99%): 0 agents
└── ⚪ Empty (0%): 11 agents

Total knowledge lines: ~2500 lines (all in Emma's KB)
Average per agent: ~208 lines
Target: 500-1000 lines per agent
```

### Growth Plan

**Q1 2025:**
- [ ] Complete knowledge base voor top 5 agents
- [ ] Migrate 3 agents to project/ scope
- [ ] Create shared knowledge/ folder voor hergebruik

**Q2 2025:**
- [ ] All agents hebben minimaal guidelines.md
- [ ] Template library voor common knowledge patterns
- [ ] Documentation voor team onboarding

---

## 🤝 Contributing

### Voor Team Members

**Nieuwe agent toevoegen:**
1. Fork/branch from main
2. Create agent in `agents/import/`
3. Test thoroughly
4. PR met beschrijving
5. Team review
6. Merge + move to `agents/project/`

**Knowledge base verbeteren:**
1. Identify gap in agent's knowledge
2. Create/update knowledge file
3. Test agent met nieuwe kennis
4. PR met examples van verbeterde performance

### Code Review Checklist

Bij PR's voor nieuwe agents:
- [ ] AGENT.md heeft frontmatter (name, description, tools)
- [ ] knowledge/ folder exists (even if empty)
- [ ] Persona is Nederlands met Nederlandse naam
- [ ] Tools zijn minimal maar sufficient
- [ ] Knowledge base heeft minimaal guidelines.md
- [ ] Examples zijn included (if applicable)
- [ ] Agent getest met Task tool
- [ ] No sensitive info in knowledge base

---

## 📖 Resources

### Internal Docs
- [CLAUDE.md](../CLAUDE.md) - Project overview en agent system uitleg
- [TALENT_DATABASE.md](../TALENT_DATABASE.md) - Volledige agent lijst
- [AVATARS.md](../AVATARS.md) - Avatar beschrijvingen

### External References
- [Claude Code Docs - Subagents](https://docs.claude.com/en/docs/claude-code/sub-agents.md)
- [Claude Code Docs - Skills](https://docs.claude.com/en/docs/claude-code/skills.md)

### Templates
- Emma's knowledge base: `agents/import/ced-brand-checker/knowledge/`
- Report template: `agents/import/ced-brand-checker/knowledge/templates/`

---

## 🆘 Troubleshooting

### "Agent niet gevonden"
```bash
# Check pad is correct
ls -la agents/import/jouw-agent/

# Check AGENT.md bestaat
cat agents/import/jouw-agent/AGENT.md
```

### "Knowledge base niet geladen"
```bash
# Verify knowledge folder exists
ls -la agents/import/jouw-agent/knowledge/

# Check bestanden zijn readable
cat agents/import/jouw-agent/knowledge/guidelines.md
```

### "Agent heeft geen tools"
```yaml
# Voeg tools toe aan frontmatter
---
name: Agent
tools: [Read, Write, Grep]  # Add this line
---
```

---

**Laatst bijgewerkt:** 2025-01-04
**Maintainer:** CED Agency Team
**Contact:** Voor vragen, zie CLAUDE.md of vraag Emma de Vries (CED Brand Checker) 😉
