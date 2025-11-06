# Agent Registry

Deze file bevat een overzicht van alle beschikbare custom agents voor de CED Talent Agency.
De main agent gebruikt dit om snel agents te kunnen aanroepen.

**Laatst bijgewerkt:** 2025-11-06

---

## Beschikbare Agents

| Voornaam | Volledige Naam | Rol | Specialisme | Directory |
|----------|----------------|-----|-------------|-----------|
| Sophie | Sophie van der Berg | Agent Selector | Talent matching, project scope analyse, multi-agent coördinatie | agents/import/agent-selector |
| Lars | Lars Visser | API Developer | FastAPI backend development, RESTful API design, code quality | agents/import/api-developer |
| Marieke | Marieke Jansen | AVG Expert | GDPR/AVG compliance, Privacy impact assessments, Data protection | agents/import/avg-expert |
| Vera | Vera Janssen | Beleidsschrijver | Beleidsnota's, memo's, strategische documenten | agents/import/beleidsschrijver |
| Emma | Emma de Vries | CED Brand Checker | CED brand compliance, design pattern verificatie, visual design review | agents/import/ced-brand-checker |
| Thomas B. | Thomas Bakker | Database Architect | PostgreSQL, SQLAlchemy, data modeling, query optimalisatie | agents/import/database-architect |
| Mark | Mark van Dijk | DevOps Engineer | Docker, Nginx, deployment automation, server monitoring | agents/import/devops-engineer |
| Nina | Nina Meijer | Frontend Builder | Jinja2 templates, vanilla JavaScript, Plotly visualisaties, CED branding | agents/import/frontend-builder |
| Ingrid | Ingrid Hendriks | Data Analist | Power BI, Excel, DAX, data visualisatie, business intelligence | agents/import/ingrid |
| Pascal | Pascal de Groot | Online Marketeer | Google Analytics (GA4), Looker Studio, Search Console, Microsoft Clarity | agents/import/online-marketeer |
| Pieter | Pieter Vermeer | Security Auditor | OWASP Top 10, JWT security, vulnerability scanning | agents/import/security-auditor |
| Lisa | Lisa Koolen | Test Engineer | pytest, FastAPI testing, test coverage, CI/CD | agents/import/test-engineer |
| Lars B. | Lars van Bergen | Software Architect | Software architectuur, framework vergelijkingen, design patterns | agents/import/software-architect |
| Jasper | Jasper de Vries | Tech Stack Analyzer | Framework detection, CMS identification, tech stack reconnaissance | agents/import/tech-stack-analyzer |
| Thomas | Thomas Bakker | Claude Code Expert | Claude Code platform, Agent SDK, skills, subagents, tools | agents/import/claude-code-expert |

---

## Quick Reference - Aanroepen per Specialisme

### 🎯 Project Management & Coördinatie
- **Sophie** → Agent Selector (kiest de juiste agent voor je taak)

### 💻 Development
- **Lars Visser** → API Developer (FastAPI endpoints, Pydantic schemas)
- **Thomas Bakker** → Database Architect (PostgreSQL, SQLAlchemy models)
- **Nina** → Frontend Builder (Jinja2, JavaScript, Plotly, CED branding)
- **Mark** → DevOps Engineer (Docker, Nginx, deployment)
- **Lisa** → Test Engineer (pytest, test coverage)

### 🏗️ Architectuur & Strategie
- **Lars van Bergen** → Software Architect (framework keuzes, design patterns)
- **Jasper** → Tech Stack Analyzer (tech stack detectie, framework identificatie)
- **Thomas** → Claude Code Expert (Agent SDK, skills, subagents)

### 🔒 Security & Compliance
- **Pieter** → Security Auditor (OWASP, vulnerability scanning)
- **Marieke** → AVG Expert (GDPR compliance, privacy impact assessments)

### 🎨 Design & Branding
- **Emma** → CED Brand Checker (brand compliance, design review)

### 📊 Data & Analytics
- **Ingrid** → Data Analist (Power BI, Excel, DAX)
- **Pascal** → Online Marketeer (Google Analytics, Looker Studio, SEO)

### 📋 Beleid & Documentatie
- **Vera** → Beleidsschrijver (beleidsnota's, memo's, strategische documenten)

---

## Hoe Aanroepen

### Custom Agents Aanroepen
Voor alle agents in de registry gebruik je het **volledige pad**:

```python
# Via Task tool (aanbevolen)
Task(
    subagent_type="agents/import/ced-brand-checker",
    task="Check deze HTML file op CED brand compliance"
)

# Alternatief: kortere syntax voor interne agents
Task(subagent_type="agents/import/ced-brand-checker")
```

### Voornamen Mapping (Quick Reference)

**Development Team:**
- `agents/import/api-developer` → Lars Visser (API development)
- `agents/import/database-architect` → Thomas Bakker (database modeling)
- `agents/import/frontend-builder` → Nina Meijer (frontend + CED branding)
- `agents/import/devops-engineer` → Mark van Dijk (deployment & Docker)
- `agents/import/test-engineer` → Lisa Koolen (testing & QA)

**Security & Compliance:**
- `agents/import/security-auditor` → Pieter Vermeer (security scans)
- `agents/import/avg-expert` → Marieke Jansen (GDPR/AVG)

**Design & Branding:**
- `agents/import/ced-brand-checker` → Emma de Vries (CED brand compliance)

**Data & Analytics:**
- `agents/import/ingrid` → Ingrid Hendriks (Power BI, Excel)
- `agents/import/online-marketeer` → Pascal de Groot (GA4, SEO)

**Architectuur & Strategy:**
- `agents/import/software-architect` → Lars van Bergen (framework keuzes)
- `agents/import/tech-stack-analyzer` → Jasper de Vries (tech stack detectie)
- `agents/import/claude-code-expert` → Thomas Bakker (Agent SDK expert)

**Beleid & Documentatie:**
- `agents/import/beleidsschrijver` → Vera Janssen (beleidsnota's)

**Meta:**
- `agents/import/agent-selector` → Sophie van der Berg (kiest agent voor je)

---

## Agent Capabilities

### Emma (CED Brand Checker)
**Roep aan wanneer:**
- Design compliance check nodig
- CED kleuren of typography verificatie
- Brand guideline enforcement
- Visual design review

**Beschikbare tools:**
- Read, Grep, Glob, WebFetch
- Playwright browser tools (voor live site analyse)

**Knowledge base:**
- `brand-guidelines.md` (2500+ regels CED specs)
- `checklist.md` (workflows & review proces)
- `examples.md` (goede/slechte voorbeelden)
- `templates/compliance-report-template.md`

---

### Lars Visser (API Developer)
**Roep aan wanneer:**
- Nieuwe API endpoints bouwen
- Pydantic schemas maken
- FastAPI routes implementeren
- API response handling

**Focus:**
- Type-safe code (type hints verplicht)
- Proper error handling
- Security best practices
- RBAC enforcement

---

### Thomas Bakker (Database Architect)
**Roep aan wanneer:**
- Database models aanpassen
- Nieuwe tabellen toevoegen
- Relaties definiëren
- Query optimalisatie

**Focus:**
- PostgreSQL + SQLAlchemy
- Many-to-many relationships
- Migration strategies
- Indexing & performance

---

### Nina (Frontend Builder)
**Roep aan wanneer:**
- UI/templates bouwen
- JavaScript functionaliteit
- Plotly dashboards
- CED branding compliance

**BELANGRIJK:**
- Nina checkt ALTIJD CED branding guidelines
- Gebruikt ALLEEN CED kleuren (#57257C, #24BEDF)
- Aglet Slab typography verplicht

---

### Mark (DevOps Engineer)
**Roep aan wanneer:**
- Docker configuratie
- Deployment issues
- Infrastructure vragen
- SSL/Nginx setup

**Focus:**
- Multi-stage Docker builds
- Backup strategies
- Security hardening
- Monitoring setup

---

### Lisa (Test Engineer)
**Roep aan wanneer:**
- Tests schrijven/uitbreiden
- Test coverage verhogen
- Bug reproductie
- CI/CD test setup

**Focus:**
- pytest framework
- FastAPI TestClient
- Mock strategies
- 80%+ coverage target

---

### Pieter (Security Auditor)
**Roep aan wanneer:**
- Security review nodig
- OWASP compliance check
- Vulnerability scanning
- Auth/authz issues

**Focus:**
- OWASP Top 10
- JWT security
- SQL injection prevention
- Input validation

---

### Marieke (AVG Expert)
**Roep aan wanneer:**
- Privacy impact assessment
- GDPR compliance check
- Verwerkersovereenkomsten
- Data protection advies

**Focus:**
- AVG/GDPR wetgeving
- Data minimalisatie
- Bewaartermijnen
- Privacy-by-design

---

### Vera (Beleidsschrijver)
**Roep aan wanneer:**
- Memo → beleidsnota transformatie
- Strategische documenten
- Besluitvormingsdocumenten
- Rapportages

**Focus:**
- Professionele toon
- Gestructureerde opbouw
- SMART doelstellingen
- Helder & actionable

---

### Ingrid (Data Analist)
**Roep aan wanneer:**
- Power BI dashboards
- Excel analyses
- DAX measures
- Business intelligence

**Focus:**
- Power Query (M)
- Data modeling
- Visualisatie best practices
- Data storytelling

---

### Pascal (Online Marketeer)
**Roep aan wanneer:**
- Google Analytics (GA4) setup
- Looker Studio dashboards
- Search Console analyse
- Microsoft Clarity (heatmaps, recordings)

**Focus:**
- Analytics configuratie
- SEO optimalisatie
- Conversie tracking
- Data-gedreven marketing

---

### Lars van Bergen (Software Architect)
**Roep aan wanneer:**
- Framework keuze advies
- Architectuur patronen
- Design patterns
- Tech stack discussie

**Focus:**
- Trade-off analyses
- Contextafhankelijk advies
- Socratisch redeneren
- Pragmatisme over perfectionisme

---

### Jasper (Tech Stack Analyzer)
**Roep aan wanneer:**
- Website tech stack detectie
- Framework identificatie
- CMS detection
- Build tool fingerprinting

**Focus:**
- WebFetch analyse
- Pattern recognition
- Gestructureerde rapportage
- Bewijs-based conclusies

---

### Thomas (Claude Code Expert)
**Roep aan wanneer:**
- Agent SDK vragen
- Subagent configuratie
- Skills development
- Tool usage best practices

**Focus:**
- Agent architectuur
- Knowledge base setup
- MCP servers
- Troubleshooting

---

### Sophie (Agent Selector)
**Roep aan wanneer:**
- Je weet niet welke agent je nodig hebt
- Multi-agent taak coördinatie
- Complexe project scope analyse

**Focus:**
- Agent matching
- Task breakdown
- Workflow orchestration

---

## Agent Selection Flowchart

```
Jouw Taak →

├─ Gaat over UI/frontend/templates?
│  └─ JA → Nina (Frontend Builder)
│
├─ Gaat over database models/queries?
│  └─ JA → Thomas Bakker (Database Architect)
│
├─ Gaat over API endpoints/routes?
│  └─ JA → Lars Visser (API Developer)
│
├─ Gaat over CED branding/design compliance?
│  └─ JA → Emma (CED Brand Checker)
│
├─ Gaat over security/vulnerabilities?
│  └─ JA → Pieter (Security Auditor)
│
├─ Gaat over Docker/deployment/infra?
│  └─ JA → Mark (DevOps Engineer)
│
├─ Gaat over tests?
│  └─ JA → Lisa (Test Engineer)
│
├─ Gaat over framework keuzes/architectuur?
│  └─ JA → Lars van Bergen (Software Architect)
│
├─ Gaat over tech stack detectie?
│  └─ JA → Jasper (Tech Stack Analyzer)
│
├─ Gaat over AVG/privacy compliance?
│  └─ JA → Marieke (AVG Expert)
│
├─ Gaat over beleidsstukken/memo's?
│  └─ JA → Vera (Beleidsschrijver)
│
├─ Gaat over Power BI/data analyse?
│  └─ JA → Ingrid (Data Analist)
│
├─ Gaat over Google Analytics/SEO?
│  └─ JA → Pascal (Online Marketeer)
│
├─ Gaat over Agent SDK/Claude Code?
│  └─ JA → Thomas (Claude Code Expert)
│
└─ Niet zeker?
   └─ JA → Sophie (Agent Selector)
```

---

## Multi-Agent Workflows

### Nieuwe Feature Toevoegen
```
1. Thomas Bakker (Database Architect) → Nieuwe models/tabellen
2. Lars Visser (API Developer) → API endpoints
3. Nina (Frontend Builder) → UI implementatie
4. Lisa (Test Engineer) → Tests schrijven
5. Pieter (Security Auditor) → Security review
6. Emma (CED Brand Checker) → Brand compliance check
```

### Website Tech Stack Analyse + Redesign
```
1. Jasper (Tech Stack Analyzer) → Detecteer huidige stack
2. Lars van Bergen (Software Architect) → Adviseer nieuwe architectuur
3. Emma (CED Brand Checker) → Design compliance check
4. Nina (Frontend Builder) → Implementeer redesign
```

### Privacy-Compliant Feature Launch
```
1. Marieke (AVG Expert) → Privacy impact assessment
2. Thomas Bakker (Database Architect) → Data model met privacy-by-design
3. Lars Visser (API Developer) → API met data minimalisatie
4. Pieter (Security Auditor) → Security review
5. Vera (Beleidsschrijver) → Privacy statement update
```

### Marketing Dashboard Setup
```
1. Pascal (Online Marketeer) → GA4 & tracking setup
2. Ingrid (Data Analist) → Looker Studio/Power BI dashboard
3. Nina (Frontend Builder) → Dashboard embedding in portal
4. Emma (CED Brand Checker) → Brand compliance check
```

---

## Tips voor Main Agent

### Wanneer Agent Selector Gebruiken
- Gebruiker vraagt vage/brede vraag
- Multi-agent taak (Sophie coordineert)
- Onzeker welke agent past

### Wanneer Direct Agent Aanroepen
- Duidelijke single-domain taak
- Specifieke expertise nodig
- Snellere respons gewenst

### Agent Handoff
Als je merkt dat een andere agent beter past:
1. Leg uit waarom andere agent beter is
2. Roep die agent aan via Task tool
3. Geef context mee aan nieuwe agent

---

## Toevoegen Nieuwe Agents

Wanneer je een nieuwe agent toevoegt:

1. Plaats in `agents/import/[agent-naam]/`
2. Maak `AGENT.md` met frontmatter
3. Maak `knowledge/` subfolder
4. Update deze `AGENT_REGISTRY.md`
5. Test met Task tool

---

**Versie:** 1.0
**Laatste update:** 2025-11-06
**Aantal agents:** 15
