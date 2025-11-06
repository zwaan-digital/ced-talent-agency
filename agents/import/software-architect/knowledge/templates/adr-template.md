# ADR [Number]: [Title]

**Date**: YYYY-MM-DD
**Status**: [Proposed | Accepted | Deprecated | Superseded]
**Deciders**: [List van mensen die beslissing maken]
**Technical Story**: [Link naar ticket/issue]

---

## Context

Beschrijf de situatie en het probleem dat een beslissing vereist. Dit is je "waarom" sectie.

**Voorbeeld**:
> Onze applicatie groeit snel en we merken dat de build times toenemen van 2 minuten naar 15 minuten. Dit vertraagt onze deployment pipeline en developer feedback loop. We moeten kiezen tussen verschillende build tools om dit te verbeteren.

### Current Situation
- [Huidige setup]
- [Wat werkt niet]
- [Impact op team/users]

### Constraints
- [Budget constraints]
- [Technical constraints]
- [Team skill constraints]
- [Time constraints]

### Requirements
- [Must have features]
- [Nice to have features]
- [Non-functional requirements (performance, security, etc.)]

---

## Decision

Beschrijf de beslissing en de rationale erachter.

**Voorbeeld**:
> We kiezen voor Vite als onze nieuwe build tool, ter vervanging van Webpack.

### Rationale
Waarom deze keuze?
- [Reason 1]
- [Reason 2]
- [Reason 3]

---

## Options Considered

### Option 1: [Name]

**Description**: [Korte beschrijving]

**Pros**:
- ✅ [Pro 1]
- ✅ [Pro 2]
- ✅ [Pro 3]

**Cons**:
- ❌ [Con 1]
- ❌ [Con 2]
- ❌ [Con 3]

**Cost**: [Tijd, geld, effort]

**Risk Level**: [Low | Medium | High]

---

### Option 2: [Name]

**Description**: [Korte beschrijving]

**Pros**:
- ✅ [Pro 1]
- ✅ [Pro 2]
- ✅ [Pro 3]

**Cons**:
- ❌ [Con 1]
- ❌ [Con 2]
- ❌ [Con 3]

**Cost**: [Tijd, geld, effort]

**Risk Level**: [Low | Medium | High]

---

### Option 3: [Name]

**Description**: [Korte beschrijving]

**Pros**:
- ✅ [Pro 1]
- ✅ [Pro 2]

**Cons**:
- ❌ [Con 1]
- ❌ [Con 2]

**Cost**: [Tijd, geld, effort]

**Risk Level**: [Low | Medium | High]

---

## Decision Matrix

| Criteria | Weight | Option 1 | Option 2 | Option 3 |
|----------|--------|----------|----------|----------|
| Performance | 30% | 9/10 | 7/10 | 8/10 |
| Developer Experience | 25% | 8/10 | 9/10 | 6/10 |
| Ecosystem | 20% | 10/10 | 8/10 | 5/10 |
| Cost | 15% | 7/10 | 8/10 | 9/10 |
| Learning Curve | 10% | 6/10 | 8/10 | 7/10 |
| **Total Score** | | **8.25** | **7.95** | **7.05** |

---

## Consequences

### Positive Consequences
- ✅ [Benefit 1]
- ✅ [Benefit 2]
- ✅ [Benefit 3]

### Negative Consequences
- ⚠️ [Drawback 1]
- ⚠️ [Drawback 2]

### Neutral Consequences
- ℹ️ [Consequence 1]
- ℹ️ [Consequence 2]

### Risks & Mitigation

| Risk | Impact | Probability | Mitigation Strategy |
|------|--------|-------------|---------------------|
| [Risk 1] | High | Low | [How we'll handle it] |
| [Risk 2] | Medium | High | [How we'll handle it] |

---

## Implementation Plan

### Phase 1: Preparation (Week 1-2)
- [ ] [Task 1]
- [ ] [Task 2]
- [ ] [Task 3]

### Phase 2: Migration (Week 3-4)
- [ ] [Task 1]
- [ ] [Task 2]
- [ ] [Task 3]

### Phase 3: Validation (Week 5)
- [ ] [Task 1]
- [ ] [Task 2]

### Rollback Plan
Als het misgaat:
1. [Rollback step 1]
2. [Rollback step 2]
3. [Rollback step 3]

---

## Success Metrics

Hoe meten we of deze beslissing succesvol was?

| Metric | Current | Target | Timeline |
|--------|---------|--------|----------|
| Build time | 15 min | < 5 min | 1 month |
| Developer satisfaction | 6/10 | > 8/10 | 3 months |
| Bug rate | [current] | [target] | [timeline] |

---

## Follow-up

### Review Date
**When**: [Datum om decision te reviewen]
**Who**: [Verantwoordelijke personen]

### Related Decisions
- [Link naar ADR #X]
- [Link naar ADR #Y]

### References
- [Documentation link]
- [Blog post or article]
- [Benchmark results]
- [Community discussion]

---

## Notes

Aanvullende context, discussiepunten, of overwegingen.

---

## Change Log

| Date | Change | Author |
|------|--------|--------|
| YYYY-MM-DD | Initial draft | [Name] |
| YYYY-MM-DD | Accepted | [Name] |

---

## Template Instructions

### Status Definitions
- **Proposed**: Decision is voorgesteld, nog niet approved
- **Accepted**: Decision is goedgekeurd en wordt geïmplementeerd
- **Deprecated**: Decision is niet langer relevant
- **Superseded**: Vervangen door ADR #X

### Tips
1. **Be specific**: Vermijd vage termen, gebruik concrete metrics
2. **Show your work**: Leg uit HOE je tot de beslissing kwam
3. **Include alternatives**: Laat zien dat je andere opties overwogen hebt
4. **Think long-term**: Overweeg impact over 1-2 jaar
5. **Keep it updated**: Update de ADR als context verandert

### When to Write an ADR
✅ Write ADR for:
- Framework/library keuzes
- Architecture patterns
- Database schema changes
- API design decisions
- Infrastructure changes

❌ Don't write ADR for:
- Minor bug fixes
- Styling tweaks
- Content updates
- Routine maintenance

---

## Example: Real ADR

# ADR 001: Choose Next.js for Frontend Framework

**Date**: 2024-01-15
**Status**: Accepted
**Deciders**: Engineering Team, CTO
**Technical Story**: JIRA-123

## Context

We're building a new e-commerce platform from scratch. We need to choose a frontend framework that can deliver fast page loads (important for SEO and conversion), provide good developer experience, and scale with our team as we grow from 3 to 15 frontend developers.

### Current Situation
- Starting from zero, no legacy codebase
- Team has React experience (2 seniors, 1 junior)
- SEO is critical (80% of traffic comes from Google)
- Planning to ship MVP in 3 months

### Constraints
- Budget: $50k for initial development
- Team: 3 frontend developers (React background)
- Timeline: 3 months to MVP
- Must support SSR for SEO

### Requirements
- Server-side rendering for product pages
- Fast time-to-interactive (< 3s on 3G)
- Easy deployment and CI/CD
- Good TypeScript support
- Active ecosystem

## Decision

We will use **Next.js 14** with the App Router as our frontend framework.

### Rationale
- Built on React (team already knows it)
- SSR/SSG out of the box (solves SEO requirement)
- Excellent performance (automatic code splitting, image optimization)
- Great developer experience (Fast Refresh, TypeScript support)
- Easy deployment (Vercel, but also works on any Node.js host)
- Large ecosystem and community

## Options Considered

### Option 1: Next.js (CHOSEN)
**Pros**:
- ✅ SSR/SSG built-in
- ✅ Team knows React
- ✅ Great performance optimizations
- ✅ Easy deployment
- ✅ Large community

**Cons**:
- ❌ Vercel lock-in for best experience
- ❌ App Router learning curve

**Cost**: Low (team knows React)
**Risk Level**: Low

### Option 2: Remix
**Pros**:
- ✅ Web standards-based
- ✅ Great performance
- ✅ Progressive enhancement

**Cons**:
- ❌ Smaller ecosystem than Next.js
- ❌ Less deployment options
- ❌ Team needs to learn new patterns

**Cost**: Medium (learning curve)
**Risk Level**: Medium

### Option 3: Vanilla React (CRA)
**Pros**:
- ✅ Maximum flexibility
- ✅ Team knows it well

**Cons**:
- ❌ No SSR (SEO issue)
- ❌ Have to set up everything ourselves
- ❌ CRA is deprecated

**Cost**: High (setup time)
**Risk Level**: High (doesn't meet SEO requirement)

## Decision Matrix

| Criteria | Weight | Next.js | Remix | React CRA |
|----------|--------|---------|-------|-----------|
| SSR Support | 30% | 10/10 | 10/10 | 0/10 |
| Team Familiarity | 25% | 9/10 | 6/10 | 10/10 |
| Ecosystem | 20% | 10/10 | 7/10 | 10/10 |
| Performance | 15% | 9/10 | 10/10 | 6/10 |
| Deployment | 10% | 10/10 | 7/10 | 8/10 |
| **Total Score** | | **9.35** | **8.15** | **6.60** |

## Consequences

### Positive
- ✅ Fast development (framework handles routing, SSR, optimization)
- ✅ Great performance out of the box
- ✅ Easy to hire Next.js developers
- ✅ SEO requirements met

### Negative
- ⚠️ Best experience on Vercel (but can deploy elsewhere)
- ⚠️ App Router is new, less Stack Overflow content

### Risks & Mitigation

| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| Vercel costs too high | High | Low | Can migrate to AWS/self-host if needed |
| App Router changes breaking | Medium | Low | Pin Next.js version, test upgrades |

## Success Metrics

| Metric | Current | Target | Timeline |
|--------|---------|--------|----------|
| Lighthouse Score | N/A | > 90 | Launch |
| Time to Interactive | N/A | < 3s | Launch |
| Build time | N/A | < 5 min | Launch |
| Developer Satisfaction | N/A | > 8/10 | 3 months |

## Follow-up

**Review Date**: April 2024 (3 months after launch)
**Who**: Engineering Team Lead

---

*This template helps you make and document architectural decisions in a structured, reproducible way.*
