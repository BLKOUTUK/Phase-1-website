# BLKOUT Infrastructure Automation
## Overview & Implementation Roadmap

**Version**: 1.0
**Date**: 14 November 2025
**Owner**: BLKOUT Infrastructure Team
**Status**: Planning

---

## Executive Summary

This document provides an overview of BLKOUT's infrastructure automation strategy, comprising 5 interconnected systems designed to streamline operations, ensure compliance, and scale efficiently.

**Total Estimated Value**: 20-30 hours/month time saved + reduced compliance risk + increased funding success

**Total Implementation Effort**:
- Phase 1 (Months 1-2): 50-70 hours → Immediate ROI
- Phase 2 (Months 3-6): 75-100 hours → Efficiency gains
- Phase 3 (Months 6+): 90-120 hours → Scale & integration

---

## The 5 Core Systems

### 1. Companies House Registry Automation
**[PRD: 01_COMPANIES_HOUSE_AUTOMATION.md](01_COMPANIES_HOUSE_AUTOMATION.md)**

**What it does**: Automate officer searches for due diligence, monitor member affiliations, detect conflicts of interest.

**Why it matters**: What just took hours of Perplexity searches (9 founding members) becomes a 30-second API query. Ongoing monitoring catches new conflicts before they become issues.

**Key Features**:
- Individual & bulk officer search via Companies House API
- Automated weekly monitoring of members
- Conflict detection engine
- FCA-ready export formats

**Effort**:
- Phase 1 (Manual search tool): 20-30 hours
- Phase 2 (Automation & monitoring): 30-40 hours
- Phase 3 (Advanced features): 40-50 hours

**ROI**: 10+ hours/year saved, zero missed conflicts

**Priority**: HIGH - Replaces manual Perplexity/web searches

**Dependencies**: Companies House API key (free, instant)

---

### 2. Member Verification System
**[PRD: 02_MEMBER_VERIFICATION_SYSTEM.md](02_MEMBER_VERIFICATION_SYSTEM.md)**

**What it does**: Formalize the blkout-verification prototype into a reusable system for member confirmations, onboarding, policy acknowledgments.

**Why it matters**: You got 67% response rate in 1 hour using WhatsApp + simple form. This system makes that repeatable for all future verifications.

**Key Features**:
- Reusable verification templates
- Personalized confirmation pages (unique URL per member)
- Real-time progress dashboard
- Automated reminders
- Audit trail for compliance

**Effort**:
- Phase 1 (Core system): 20-30 hours
- Phase 2 (Automation & alerts): 25-35 hours
- Phase 3 (Advanced features): 30-40 hours

**ROI**: 2-4 hours saved per verification, 100% response rate, FCA-ready audit trail

**Priority**: HIGH - Immediate need (annual confirmations, onboarding)

**Dependencies**: GitHub Pages (already have), Supabase (free tier)

---

### 3. CBS Compliance Dashboard
**[PRD: 03_CBS_COMPLIANCE_DASHBOARD.md](03_CBS_COMPLIANCE_DASHBOARD.md)**

**What it does**: Track all CBS obligations (FCA filings, annual returns, AGM, member confirmations) with deadline alerts and document library.

**Why it matters**: Registration is imminent. You'll have ongoing obligations. A dashboard ensures zero late filings (£100-500 penalties) and zero compliance breaches.

**Key Features**:
- Compliance calendar (all deadlines visible)
- Task management (who's responsible, what's due)
- Document library (all filings in one place)
- Automated recurring tasks (annual return, AGM, etc.)
- Email alerts (30/14/7 days before deadline)

**Effort**:
- Phase 1 (Notion dashboard): 4-6 hours → **QUICK WIN**
- Phase 2 (Automation & alerts): 8-12 hours
- Phase 3 (Custom build, if needed): 40-60 hours

**ROI**: Zero late filings, zero compliance incidents, audit-ready records, smooth volunteer handover

**Priority**: **URGENT** - Registration completing imminently, obligations start immediately

**Dependencies**: Notion account (free or £8/month team), Zapier (for Phase 2)

---

### 4. Funding Pipeline Automation
**[PRD: 04_FUNDING_PIPELINE_AUTOMATION.md](04_FUNDING_PIPELINE_AUTOMATION.md)**

**What it does**: Transform the Grant-funding repository into an active workflow system - track opportunities, prioritize, manage applications, analyze success rates.

**Why it matters**: Increase applications from ~10/year → 25-30/year, improve success rate to 35%+, never miss a deadline, learn what works.

**Key Features**:
- Opportunity discovery (automated scanning + manual entry)
- Pipeline visualization (kanban board)
- Prioritization engine (auto-score opportunities)
- Application templates & content library
- Deadline alerts
- Success analytics (which funders say yes)

**Effort**:
- Phase 1 (Airtable pipeline): 10-15 hours
- Phase 2 (Automation & intelligence): 12-18 hours
- Phase 3 (Advanced features): 20-30 hours

**ROI**: 2.5x more applications, 40% faster drafting, £50-100K funding secured in Year 1

**Priority**: HIGH - Critical for financial sustainability

**Dependencies**: Airtable account (free or £20/month)

---

### 5. Document Generation System
**[PRD: 05_DOCUMENT_GENERATION_SYSTEM.md](05_DOCUMENT_GENERATION_SYSTEM.md)**

**What it does**: Automate creation of repetitive documents (member emails, FCA letters, reports) using templates and data merges.

**Why it matters**: What took 2 hours to create 8 member emails takes 5 minutes automated. Eliminate copy-paste errors, ensure consistency.

**Key Features**:
- Template library (member comms, compliance, funders, internal)
- Variable substitution (merge data into templates)
- Bulk generation (10 members → 10 personalized emails in one click)
- Multiple output formats (Word, PDF, Markdown, HTML)
- Conditional logic (show/hide sections based on data)

**Effort**:
- Phase 1 (Google Docs + Autocrat): 4-6 hours → **QUICK WIN**
- Phase 2 (Pandoc + GitHub): 12-18 hours
- Phase 3 (Custom web app): 30-40 hours

**ROI**: 5-10 hours/month saved, zero personalization errors, professional consistency

**Priority**: MEDIUM-HIGH - Immediate value, low effort

**Dependencies**: Google Workspace (free or £4/user/month), Autocrat add-on (free)

---

## System Interconnections

These systems are designed to work together:

```
┌──────────────────────────────────────────────────────────────┐
│                    CBS Compliance Dashboard                   │
│  (Central hub - tracks deadlines, triggers verifications)    │
└───────┬─────────────────────┬────────────────────┬───────────┘
        │                     │                    │
        │                     │                    │
        ▼                     ▼                    ▼
┌───────────────┐   ┌──────────────────┐   ┌─────────────────┐
│   Member      │   │  Document        │   │  Companies      │
│ Verification  │   │  Generation      │   │  House Auto     │
│               │◄──┤                  │◄──┤                 │
│ (Collect      │   │ (Create emails,  │   │ (Pull member    │
│  member data) │   │  letters, reports)  │  affiliations)  │
└───────┬───────┘   └──────────────────┘   └─────────────────┘
        │                     ▲
        │                     │
        └─────────────────────┘
        (Responses update member records)

┌─────────────────────────────────────────────────────────────┐
│              Funding Pipeline Automation                     │
│  (Pulls org data from member system, tracks funding)        │
└─────────────────────────────────────────────────────────────┘
        │
        ▼
┌──────────────────┐
│  Document        │
│  Generation      │
│ (Grant letters,  │
│  reports)        │
└──────────────────┘
```

**Example workflow:**

1. **CBS Compliance Dashboard** alerts: "Annual member confirmation due in 30 days"
2. **Companies House Automation** runs fresh search on all members (get latest affiliations)
3. **Member Verification System** generates personalized confirmation pages (using data from step 2)
4. **Document Generation** creates confirmation emails (8 personalized emails in 5 min)
5. Send emails → members confirm → responses flow back to **Member Verification**
6. **Compliance Dashboard** marks task complete, stores audit trail

---

## Implementation Roadmap

### Month 1: Foundation & Quick Wins

**Week 1:**
- ✅ CBS Compliance Dashboard (Notion) - 6 hours
- ✅ Document Generation (Google Docs + Autocrat) - 6 hours
- **Total**: 12 hours, **HIGH impact**

**Outcome**:
- Never miss CBS deadline
- Generate docs 10x faster

**Week 2-4:**
- Companies House API integration (manual search tool) - 20-30 hours
- Member Verification System (formalize prototype) - 20-30 hours
- **Total**: 40-60 hours

**Outcome**:
- Instant officer searches (vs. hours manual)
- Reusable verification system

---

### Months 2-3: Automation & Efficiency

**Funding Pipeline** (Phase 1) - 10-15 hours
- Set up Airtable pipeline
- Create templates
- Import existing grant research

**Companies House** (Phase 2) - 30-40 hours
- Automated weekly monitoring
- Bulk search
- Conflict detection

**Member Verification** (Phase 2) - 25-35 hours
- Automated reminders
- Email integration
- Conditional logic

**CBS Compliance** (Phase 2) - 8-12 hours
- Automated alerts
- Approval workflows

**Total**: 73-102 hours

**Outcome**:
- Proactive monitoring (no more reactive scrambling)
- 25+ grant applications/year pipeline
- Automated reminders (less manual follow-up)

---

### Months 4-6: Intelligence & Integration

**Funding Pipeline** (Phase 2) - 12-18 hours
- Automated opportunity discovery
- Success analytics
- Funder relationship tracking

**Document Generation** (Phase 2) - 12-18 hours
- Pandoc + GitHub integration
- Advanced conditionals
- Email auto-send

**Total**: 24-36 hours

**Outcome**:
- Learn what works (data-driven funding strategy)
- Fully automated document workflows

---

### Months 6+: Scale & Advanced Features (As Needed)

All systems have Phase 3 features (AI, advanced analytics, custom builds) that can be pursued if/when needed. Not required for initial value.

---

## Prioritization: What to Build First

### Tier 1: URGENT (Do First)
**CBS Compliance Dashboard** - Registration imminent, obligations start immediately
- Effort: 6 hours (Notion)
- Value: Avoid £100-500 late filing penalties, zero compliance risk

### Tier 2: HIGH ROI (Do Next)
**Document Generation** - Immediate time savings
- Effort: 6 hours (Google Docs + Autocrat)
- Value: 5-10 hours/month saved

**Companies House Automation** - Replaces manual searches
- Effort: 20-30 hours (Phase 1)
- Value: 10+ hours/year saved, ongoing monitoring

**Member Verification System** - Formalize successful prototype
- Effort: 20-30 hours (Phase 1)
- Value: Annual confirmations, onboarding, audit trail

### Tier 3: STRATEGIC (Important but Less Urgent)
**Funding Pipeline Automation** - Critical for growth but can start manually
- Effort: 10-15 hours (Phase 1)
- Value: £50-100K funding in Year 1, 2.5x more applications

---

## Success Metrics (Overall)

### Year 1 Targets

| Metric | Current | Target |
|--------|---------|--------|
| **Compliance** | Not CBS yet | Zero late filings, zero incidents |
| **Time saved** | N/A | 20-30 hours/month |
| **Funding secured** | £0 | £50-100K |
| **Grant applications** | ~10/year | 25/year |
| **Member verifications** | Manual (2 hours each) | Automated (5 min setup) |
| **Document generation** | Manual (30-120 min each) | Automated (5 min each) |
| **Officer searches** | Manual Perplexity (15-20 min each) | Automated API (<30 sec each) |

### Qualitative Success

- **Confidence**: Board feels confident in compliance status
- **Scalability**: Systems support growth from 9 → 50 → 100 members
- **Knowledge retention**: Volunteer handover takes <1 hour (systems are documented, intuitive)
- **Professionalism**: All external communications (members, funders, FCA) are consistent, polished
- **Data-driven**: Decisions informed by analytics (not gut feelings)

---

## Budget & Resources

### Financial Investment

**Low-Code Approach (Recommended for Year 1):**
- Notion (CBS Compliance): £0-8/month
- Airtable (Funding Pipeline): £0-20/month
- Google Workspace (Document Gen): £0-4/user/month
- Supabase (Member Verification): £0 (free tier sufficient)
- **Total**: £0-32/month (£0-384/year)

**Custom Build Approach (Year 2+, if needed):**
- Hosting: £0 (Vercel free tier)
- Database: £0-25/month (Supabase/Railway)
- Email: £0-20/month (SendGrid/Resend free tiers)
- **Total**: £0-45/month (£0-540/year)

**ROI**: Even at maximum spend (£384/year), if systems save 25 hours/month @ £20/hour volunteer time value = £6,000/year value → **15x ROI**

### Human Resources

**Phase 1 (Months 1-2):**
- Technical lead: 50-70 hours (setup, configuration, training)
- Content creator: 10-15 hours (write templates, populate content libraries)
- Team training: 5 hours (onboarding all users)
- **Total**: 65-90 hours

**Phase 2 (Months 3-6):**
- Technical lead: 75-100 hours (automation, integrations)
- Content creator: 10-15 hours (expand templates)
- **Total**: 85-115 hours

**Ongoing (Year 2+):**
- Maintenance: 5-10 hours/month
- Template updates: 2-5 hours/month
- **Total**: 7-15 hours/month

**Volunteer skills needed**:
- Technical: Python/JavaScript (for custom builds) OR willingness to learn Notion/Airtable (for low-code)
- Content: Strong writer (for templates)
- Project management: Coordinator to oversee implementation

**Can outsource**: If volunteer capacity is limited, all systems can be built by freelancer (~£30-50/hour UK rate). Phase 1 = £1,500-3,500 outsourced cost.

---

## Risk Assessment

### Overall Risks (All Systems)

**Risk 1: Volunteer Capacity / Burnout**
- **Likelihood**: Medium-High
- **Impact**: High (systems don't get built)
- **Mitigation**:
  - Prioritize ruthlessly (Tier 1 first)
  - Low-code approach (minimize technical burden)
  - Outsource if budget available
  - Phased rollout (don't do everything at once)

**Risk 2: System Abandonment (Built but Not Used)**
- **Likelihood**: Medium
- **Impact**: High (wasted effort)
- **Mitigation**:
  - User-centered design (involve team from start)
  - Training (1-hour workshops per system)
  - Make it easier than manual (clear value prop)
  - Monthly check-ins (are people using it? Why/why not?)

**Risk 3: Over-Engineering (Complexity Spiral)**
- **Likelihood**: Medium
- **Impact**: Medium (spend time on features no one needs)
- **Mitigation**:
  - Start simple (Phase 1 = MVP, validate value)
  - Only build Phase 2/3 if Phase 1 proves valuable
  - Measure ROI (if not saving time, don't expand)
  - User feedback loop (what do they actually need?)

**Risk 4: Data Quality Issues**
- **Likelihood**: Medium
- **Impact**: Medium (garbage in, garbage out)
- **Mitigation**:
  - Validation rules (required fields, format checks)
  - Training (how to enter data correctly)
  - Regular audits (quarterly data cleanup)
  - Clear ownership (who's responsible for data quality)

**Risk 5: Integration Complexity**
- **Likelihood**: Low (systems designed to be independent initially)
- **Impact**: Medium (if integrations fail, systems work standalone)
- **Mitigation**:
  - Build systems independently first
  - Integrate in Phase 2 (once both systems proven)
  - Loose coupling (APIs, webhooks, not tight dependencies)

---

## Decision Framework: Build vs. Buy vs. Skip

For each system, ask:

**1. Can we buy this?**
- If yes: Is cost <£500/year AND saves >50 hours/year? → **Buy**
- If no or expensive: Consider build

**2. Can we build this with low-code?**
- If yes: Is setup <20 hours? → **Build (low-code)**
- If no: Consider custom build

**3. Is this critical for compliance/operations?**
- If yes (e.g., CBS Compliance): → **Must build or buy**
- If no: Can we skip? (Funding pipeline is important but not compliance-critical)

**4. What's the manual process cost?**
- If manual = 1 hour/month → Skip automation (not worth it)
- If manual = 10+ hours/month → **Automate**

**Applied to our 5 systems:**

| System | Buy Option? | Build Complexity | Criticality | Manual Cost | Decision |
|--------|-------------|------------------|-------------|-------------|----------|
| CBS Compliance | £500-2K/year (overkill) | LOW (Notion 6h) | CRITICAL | High | **BUILD (low-code)** |
| Companies House | £500-2K/year | MEDIUM (30h) | High | High | **BUILD (API)** |
| Member Verification | N/A (unique to process) | MEDIUM (20-30h) | High | High | **BUILD** |
| Funding Pipeline | £500-2K/year (overkill) | LOW (Airtable 15h) | Strategic | Medium | **BUILD (low-code)** |
| Document Gen | N/A (unique templates) | LOW (6h) | Medium | High | **BUILD (low-code)** |

**Conclusion**: All 5 systems are best built (using low-code where possible) rather than bought.

---

## Next Steps (Immediate Actions)

### This Week:
1. **Set up CBS Compliance Dashboard** (Notion, 6 hours) - **DO FIRST**
2. **Set up Document Generation** (Google Docs + Autocrat, 6 hours)

### Next 2 Weeks:
3. **Get Companies House API key** (register at developer.company-information.service.gov.uk)
4. **Formalize Member Verification System** (convert prototype to reusable)

### Month 2:
5. **Set up Funding Pipeline** (Airtable)
6. **Begin automation** (Phase 2 features for highest-ROI systems)

---

## Questions for Decision

Before proceeding, clarify:

1. **Who will lead implementation?** (Technical volunteer? Outsourced? Mixed?)
2. **What's the budget?** (£0 = low-code only, £1-3K = can outsource some custom builds)
3. **What's the timeline expectation?** (3 months aggressive, 6 months realistic, 12 months relaxed)
4. **Which system is most urgent?** (Assumption: CBS Compliance, but confirm)
5. **Are there other automation needs not covered?** (Accounting? Fundraising CRM? HR/volunteer management?)

---

## Conclusion

These 5 systems form a coherent infrastructure automation strategy for BLKOUT:

- **Compliance-focused** (CBS Dashboard, Companies House, Member Verification)
- **Growth-oriented** (Funding Pipeline)
- **Efficiency-driven** (Document Generation)

**Recommended approach**:
- **Month 1**: Build quick wins (CBS Compliance, Document Gen) - 12 hours, massive ROI
- **Months 2-3**: Build core systems (Companies House, Member Verification, Funding Pipeline) - 60-75 hours
- **Months 4+**: Automate & integrate (Phase 2 features) - as capacity allows

**Expected outcome**:
- Zero compliance risk
- 20-30 hours/month saved
- £50-100K funding secured in Year 1
- Scalable infrastructure supporting growth to 50-100 members

---

**Document Control:**
- **Version**: 1.0
- **Last Updated**: 14 November 2025
- **Next Review**: Monthly (track progress, adjust priorities)
- **Owner**: BLKOUT Infrastructure Team
- **Stakeholders**: Board, compliance officer, fundraising lead, all volunteers

---

## Appendix: PRD Quick Reference

1. **[01_COMPANIES_HOUSE_AUTOMATION.md](01_COMPANIES_HOUSE_AUTOMATION.md)** - Automate officer searches, monitor affiliations (20-90h)
2. **[02_MEMBER_VERIFICATION_SYSTEM.md](02_MEMBER_VERIFICATION_SYSTEM.md)** - Formalize blkout-verification prototype (20-90h)
3. **[03_CBS_COMPLIANCE_DASHBOARD.md](03_CBS_COMPLIANCE_DASHBOARD.md)** - Track CBS obligations, never miss deadline (6-60h)
4. **[04_FUNDING_PIPELINE_AUTOMATION.md](04_FUNDING_PIPELINE_AUTOMATION.md)** - Manage grants pipeline, increase success (10-45h)
5. **[05_DOCUMENT_GENERATION_SYSTEM.md](05_DOCUMENT_GENERATION_SYSTEM.md)** - Automate repetitive docs, save hours (6-65h)

**Total effort across all systems**:
- Phase 1: 62-290 hours (spread across 5 systems)
- Recommended: Start with Tier 1 & 2 (50-70 hours for massive immediate value)
