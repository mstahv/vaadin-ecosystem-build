# RFC: Vaadin Failsafe - Compatibility Assurance Service

**Status:** Draft
**Created:** 2026-02-16

---

## Summary

**Vaadin Failsafe** is a subscription service where customers grant Vaadin read-only access to their application source code. Vaadin then:

1. Tests customer applications against **nightly Vaadin builds**
2. Provides **early warnings** about compatibility issues before public release
3. (Higher tiers) Delivers **migration patches** prepared by Vaadin engineers

---

## Problem

**For customers:**
- Unexpected breakages in patch/minor releases cause production incidents
- Upgrade anxiety leads to delayed security patches
- Migration burden falls entirely on customer engineering teams

**For Vaadin:**
- Limited visibility into real-world API usage patterns
- Reactive support model — issues discovered after release
- Breaking customer apps damages trust and slows version adoption

---

## Service Tiers

### Tier 1: Monitoring
- Automated build/test against pre-release Vaadin versions
- Early warning notifications (2-4 weeks before release)
- Issue documentation with affected code locations

### Tier 2: Migration Guidance
Everything in Tier 1, plus:
- Step-by-step migration instructions specific to customer's codebase
- Workaround recommendations
- Priority support channel

### Tier 3: Managed Migration
Everything in Tier 2, plus:
- Vaadin prepares Git patches / PRs with required changes
- SLA on notification lead time

---

## Code Access

Customers provide read-only access via:
- **Git deploy key** (GitHub, GitLab, Bitbucket, Azure DevOps)
- **Self-hosted agent** (bytecode only, for restricted environments)
- **Manual upload** (for air-gapped environments)

Standard security measures: isolated environments, encryption, audit logging, NDA.

---

## Pricing

TODO: Team/Enterprise tier pricing 🤷

---

## Benefits

**For customers:** Risk reduction, faster upgrades, reduced migration effort, better planning

**For Vaadin:** Recurring revenue, real-world testing data, customer insights, ecosystem health, competitive differentiation

---

## Open Questions

1. **Naming:** "Vaadin Failsafe" is working title (note: maven-failsafe-plugin exists but different domain). Alternatives: Shield, Sentinel, Compatibility Guard

2. **Scope:** Vaadin core only, or also add-ons / npm dependencies?

3. **Integration:** Bundled with Pro/Prime? Separate product?

4. **AI/LLM:** Use for migration suggestions / chat assistant?

---

*Confidential — internal Vaadin discussion only*
