# Product Requirement Document
## Grant Funding Platform - Core Architecture

**Version**: 1.0
**Date**: 14 November 2025
**Owner**: BLKOUT Fundraising Team
**Status**: Proposed
**Related**: Grant-funding repository structure

---

## Executive Summary

Define the core architecture for BLKOUT's integrated grant funding platform - a modular system connecting opportunity discovery, assessment, application building, pipeline management, and analytics into one cohesive workflow.

**Value Proposition**: One unified system that takes funders from discovery to award, with all data flowing between modules, eliminating duplicate entry and enabling continuous learning.

---

## Problem Statement

### Current State: Fragmented Tools & Workflows

**Grant-funding repository structure exists** but it's:
- ❌ Static documentation (folders and templates, not active workflows)
- ❌ Disconnected pieces (discovery process separate from application drafting)
- ❌ No data flow (information entered in one place doesn't flow to another)
- ❌ Manual tracking (spreadsheets, memory, scattered notes)
- ❌ No learning loop (can't analyze what works across applications)

**Example workflow friction:**
1. Find grant opportunity → Enter in landscape scan spreadsheet
2. Assess fit → Manually score in separate prioritization doc
3. Decide to apply → Create new application doc from scratch
4. Copy boilerplate → Manually from previous applications (risk copy-paste errors)
5. Track deadline → Separate calendar/reminder system
6. Submit → No centralized record of what was submitted
7. Get decision → No systematic capture of outcome/lessons
8. Repeat → Start from scratch for next grant, lose institutional knowledge

**What's missing**: **Integration** - The pieces exist but don't talk to each other.

---

## Vision: Integrated Grant Funding Platform

### Core Principle: Single Source of Truth

**One opportunity record** flows through entire lifecycle:

```
Discovery → Assessment → Application → Submission → Decision → Learning
    ↓           ↓            ↓            ↓           ↓          ↓
  [Module 1] [Module 2]  [Module 3]  [Module 4] [Module 5] [Module 6]
```

**Key Integration Points:**
- Opportunity discovered → Auto-populates assessment scorecard
- Prioritized as "Apply" → Triggers application workspace creation
- Application drafted → Uses content library (auto-populate org details)
- Submission → Updates pipeline status, sets decision date reminder
- Decision received → Logs outcome, feeds analytics
- Analytics → Informs future prioritization (learn what works)

### User Journey: Seamless Flow

**Fundraising Lead perspective:**
1. Monday morning: Check "New Opportunities" dashboard (auto-scanned over weekend)
2. Click opportunity → See pre-filled assessment (strategic fit auto-scored based on keywords)
3. Click "Apply" → Application workspace created with funder details pre-populated
4. Content library → Drag-drop reusable blocks into application
5. Assign to writer → They see all context (funder research, past applications to similar funders)
6. Track progress → Real-time dashboard shows "in draft, 70% complete, due in 14 days"
7. Submit → One click updates status, archives submission, sets decision reminder
8. Decision received → Enter outcome, system asks "Lessons learned?"
9. Month later → Analytics show "Foundation grants have 40% success rate, Government 15%"
10. Next opportunity → System suggests "Similar to X which won £50K - consider applying"

---

## System Architecture

### Module Overview

**5 Core Modules** (each has detailed PRD):

1. **Opportunity Discovery Engine** → Find grants
2. **Assessment & Prioritization** → Decide which to pursue
3. **Application Builder** → Create submissions
4. **Pipeline Manager** → Track progress & deadlines
5. **Analytics & Learning** → Understand what works

### Data Model (Shared Across Modules)

**Central Database Tables:**

```
opportunities
├── id, funder, grant_name, amount, deadline, url
├── discovered_date, discovered_by, source
├── stage (discovered → researching → prioritized → applying → submitted → decided)
├── priority_score, strategic_fit, urgency, significance
├── outcome (awarded/rejected/pending), amount_awarded
└── lessons_learned

applications
├── id, opportunity_id (FK)
├── template_used, sections (jsonb)
├── status (draft → review → final → submitted)
├── assigned_to, reviewer
├── submitted_date, decision_date
└── attachments

funders
├── id, name, type (foundation/government/lottery/trust)
├── focus_areas, contact_person, website
├── relationship_notes
└── applications_history (rollup from opportunities)

content_blocks
├── id, name, type (org_description/team/beneficiaries/etc)
├── content, word_count
├── last_updated
└── used_in_applications (link to applications)

decisions
├── id, opportunity_id (FK)
├── outcome, amount_requested, amount_awarded
├── decision_date, feedback
└── lessons_learned
```

### Integration Architecture

**Module Communication via Shared Database:**
- All modules read/write to same PostgreSQL database
- Real-time updates (WebSocket for live dashboard)
- Event-driven (opportunity status change triggers downstream actions)

**Example Integration Flow:**

```
[Discovery Engine]
  ├─ Finds new grant
  ├─ Creates opportunity record
  └─ Triggers notification to [Pipeline Manager]
       ↓
[Assessment Tool]
  ├─ Reads opportunity details
  ├─ Auto-calculates priority score
  ├─ Updates opportunity.priority_score
  └─ If priority=HIGH → Triggers notification
       ↓
[Application Builder]
  ├─ Reads opportunity + funder details
  ├─ Creates application record (linked to opportunity)
  ├─ Auto-populates funder name, amount, deadline
  ├─ Pulls content blocks from [Content Library]
  └─ Updates opportunity.stage = "applying"
       ↓
[Pipeline Manager]
  ├─ Reads all opportunities WHERE stage IN ('applying', 'submitted')
  ├─ Displays kanban board
  ├─ Sends deadline reminders
  └─ When submitted → Updates opportunity.stage = "submitted"
       ↓
[Analytics Engine]
  ├─ Reads all decisions
  ├─ Calculates success rates by funder type, amount, etc.
  ├─ Generates insights
  └─ Feeds back to [Assessment Tool] (improve prioritization)
```

---

## Technical Stack

### Recommended: Airtable (Phase 1 - Proof of Concept)

**Why Airtable for Integrated System:**
- **Relational database** (opportunities link to applications link to funders)
- **Built-in views** (kanban, calendar, gallery, grid)
- **Automations** (opportunity created → auto-calculate priority)
- **Forms** (easy opportunity intake)
- **API** (can integrate with external tools later)
- **Collaboration** (team can work together)
- **Free tier**: 1,200 records (sufficient for Year 1-2)

**Airtable Base Structure:**
```
Grant-Funding-Base/
├── Opportunities (table)
├── Applications (table)
├── Funders (table)
├── Content Library (table)
├── Decisions (table)
└── Views:
    ├── Kanban (by stage)
    ├── Calendar (by deadline)
    ├── Priority Matrix (grid sorted by score)
    ├── Success Analytics (grouped by funder type)
    └── Dashboard (summary stats)
```

**Limitations of Airtable:**
- Limited automation (can add Zapier for complex workflows)
- 1,200 record limit on free tier (upgrade to Plus £20/month for 5,000)
- Not as polished as custom UI

### Alternative: Notion (Phase 1 - If Simplicity Preferred)

**Pros:**
- Easier learning curve
- Beautiful documentation + database hybrid
- Free for small teams

**Cons:**
- Weaker relational database (harder to link tables)
- No kanban view (manual workaround)
- Less automation

**Decision**: **Airtable** for Phase 1 (better database, automation, views)

### Future: Custom Build (Phase 3 - If Scales Beyond Airtable)

**When to migrate to custom:**
- >5,000 opportunities tracked (Airtable expensive at scale)
- Need advanced automation (AI-powered matching, etc.)
- Want fully custom UI/UX

**Stack for custom build:**
- Frontend: Next.js
- Backend: Next.js API routes
- Database: Supabase (PostgreSQL)
- Hosting: Vercel
- **Estimated effort**: 60-80 hours

---

## Module Integration Requirements

Each module PRD will specify:

### Input Requirements
- What data does this module need from other modules?
- Example: Application Builder needs opportunity.funder_name, opportunity.deadline

### Output/Updates
- What data does this module create/update that other modules use?
- Example: Assessment Tool updates opportunity.priority_score

### Dependencies
- Which modules must exist first?
- Example: Application Builder depends on Content Library existing

### Integration Points
- How does data flow in/out?
- Example: Pipeline Manager reads opportunity.stage, sends deadline alerts

---

## Phase 1: Core Platform MVP (Month 1)

### Deliverables

**Airtable Setup:**
- [ ] Create Grant-Funding base
- [ ] Set up 5 core tables (Opportunities, Applications, Funders, Content, Decisions)
- [ ] Configure relationships (opportunities → applications, opportunities → funders)
- [ ] Create essential views (kanban, calendar, priority matrix)
- [ ] Set up basic automations (opportunity created → calculate priority score)
- [ ] Import Grant-funding repo content into Airtable

**Integration Testing:**
- [ ] Test data flow: Discovery → Assessment → Application
- [ ] Verify opportunity updates propagate across views
- [ ] Ensure no duplicate data entry required

**Team Training:**
- [ ] 1-hour workshop on how to use integrated system
- [ ] Document workflows for each module
- [ ] Create quick-start guide

**Effort**: 15-20 hours

**Success Criteria:**
- All 5 tables connected and working
- Can create opportunity → assess → start application without re-entering data
- Team can navigate system independently
- First real grant tracked end-to-end through system

---

## Phase 2: Automation & Intelligence (Months 2-3)

### Deliverables

**Advanced Automations:**
- [ ] Opportunity discovered → Auto-notify team (Slack/email)
- [ ] Priority score calculated → Auto-move to "High Priority" view if >7/10
- [ ] Deadline approaching → Auto-send reminders (7d, 3d, 1d before)
- [ ] Application submitted → Auto-create decision reminder (based on typical funder response time)
- [ ] Decision received → Auto-update analytics dashboard

**External Integrations:**
- [ ] RSS feed monitoring (auto-import new grants)
- [ ] Email forwarding (forward grant alerts → auto-create opportunities)
- [ ] Google Calendar sync (deadlines appear in team calendar)
- [ ] GitHub integration (link applications to project repos)

**Effort**: 20-30 hours

---

## Phase 3: AI & Advanced Features (Months 6+)

### Deliverables

**AI-Powered Features:**
- [ ] Opportunity matching (suggest grants based on project descriptions)
- [ ] Priority prediction (machine learning based on historical success)
- [ ] Application drafting assistance (AI suggests content based on funder preferences)
- [ ] Success probability forecasting

**Advanced Analytics:**
- [ ] Funder relationship scoring (how likely to fund us based on history)
- [ ] Budget optimization (which ask amounts have highest success rate)
- [ ] Timeline analysis (how long from discovery to award)

**Effort**: 40-60 hours

---

## Success Metrics (Integrated System)

| Metric | Current | Year 1 Target | How Measured |
|--------|---------|---------------|--------------|
| **Grant applications** | ~10/year | 25/year | Count in Airtable (opportunities.stage='submitted') |
| **Success rate** | ~20% | 35% | % where outcome='awarded' |
| **Time per application** | 8-12 hours | 4-6 hours | Track time from application start to submit |
| **Duplicate data entry** | High (re-enter funder details, org info) | Zero | Audit workflows |
| **Deadline misses** | 2-3/year | 0 | Count opportunities where submitted_date > deadline |
| **Knowledge retention** | Low (in people's heads) | High (in system) | Volunteer handover test (can new person navigate?) |
| **Funding secured** | £0 | £50-100K | Sum of amount_awarded |

---

## User Roles & Permissions

### Role Definitions

**Fundraising Lead (Admin)**
- Full access to all modules
- Can create, edit, delete opportunities
- Can assign applications to writers
- Can view all analytics

**Grant Writer (Contributor)**
- Can view all opportunities
- Can draft/edit applications assigned to them
- Can add to content library
- Limited analytics view (only their applications)

**Board Member (Viewer)**
- Read-only access to pipeline
- Can view success analytics
- Can comment on applications
- Cannot edit opportunities or applications

### Data Access

**Public** (if configured):
- Funder database (read-only)
- Success stories (awarded grants)

**Private**:
- Active applications (in draft/review)
- Assessment scores/notes
- Funder relationship notes
- Lessons learned (until sanitized for public)

---

## Risk Assessment

### Risk 1: Complexity Overwhelm (Too Many Features)

**Likelihood**: High (tempting to build everything)
**Impact**: High (system abandoned if too complex)

**Mitigation:**
- **Phase 1 = Core only** (discovery, basic assessment, simple application tracking)
- Only add Phase 2/3 if Phase 1 proves valuable
- User feedback: "What's missing?" vs. "Here's what you might want"
- Measure adoption: If <80% team usage in Month 1, simplify before adding features

### Risk 2: Data Quality Issues

**Likelihood**: Medium (garbage in, garbage out)
**Impact**: High (analytics meaningless if data poor)

**Mitigation:**
- Required fields (can't save opportunity without deadline, amount)
- Validation rules (deadline must be future date, amount must be positive number)
- Regular audits (monthly data cleanup)
- Team training (how to enter data consistently)

### Risk 3: System Abandonment (Reverts to Old Ways)

**Likelihood**: Medium (change is hard)
**Impact**: High (wasted effort building system)

**Mitigation:**
- Make it easier than manual (clear value prop from Day 1)
- Involve team in design (user-centered approach)
- Quick wins (show time saved in first week)
- Monthly check-ins (are people using it? Why/why not?)
- Continuous improvement (adapt to team needs)

---

## Integration with Other BLKOUT Systems

### Companies House Automation
- **Data flow**: Funder is a CBS/charity → Auto-check Companies House for directors
- **Use case**: Due diligence on grant-making organization
- **Integration**: Manual trigger (click "Check Funder" → runs Companies House search)

### Member Verification System
- **Data flow**: Grant awarded → May need member verification for delivery
- **Use case**: Project funded, need team confirmations
- **Integration**: Link grant to project, project links to verification requests

### Document Generation
- **Data flow**: Application approved → Generate cover letter from template
- **Use case**: Automate cover letter, budget narrative, supporting docs
- **Integration**: Application record provides variables for templates

**Recommended**: Build grant funding platform first, add integrations in Phase 2/3.

---

## Next Steps (Immediate Actions)

1. **Review Module PRDs** (forthcoming):
   - PRD: Opportunity Discovery Engine
   - PRD: Assessment & Prioritization Tool
   - PRD: Application Builder
   - PRD: Pipeline Manager
   - PRD: Analytics Dashboard

2. **Validate Architecture** with team:
   - Does this workflow match reality?
   - What's missing?
   - What's unnecessary?

3. **Choose Platform**:
   - Decision: Airtable vs. Notion vs. Custom (recommendation: Airtable)
   - Set up free account, explore templates

4. **Pilot Test**:
   - Create base structure in Airtable
   - Import 3-5 sample grants
   - Test data flow through all modules
   - Time how long it takes vs. manual

5. **Go/No-Go Decision**:
   - If pilot proves value (saves time, works well) → Proceed with Phase 1
   - If not → Revisit architecture or stick with static Grant-funding repo

---

## Open Questions

1. **Who will be the system admin?** (Responsible for setup, maintenance)
2. **What's the GitHub integration priority?** (Link grants to specific projects?)
3. **Should we migrate Grant-funding repo content into Airtable or keep as reference?**
4. **Do we need offline access?** (Airtable requires internet)
5. **What's the data retention policy?** (Keep all grants forever? Archive old ones?)

---

## Appendix: Why Integration Matters

### Example: Without Integration

**Time spent on one grant application:**
1. Find opportunity (web search): 20 min
2. Enter in spreadsheet (discovery log): 5 min
3. Research funder (notes doc): 30 min
4. Score against matrix (separate doc): 10 min
5. Create application doc: 5 min
6. Find org description (search old apps): 10 min
7. Copy/paste boilerplate: 15 min
8. Write specific sections: 3 hours
9. Add to deadline calendar: 5 min
10. Submit: 10 min
11. Record submission (separate tracker): 5 min
12. Set decision reminder: 5 min

**Total**: ~5 hours + fragmented across 7 different tools/docs

### Example: With Integration

**Same grant application:**
1. Opportunity auto-discovered (RSS feed): 0 min
2. Review on dashboard (pre-scored): 2 min
3. Click "Apply" (workspace created with funder details): 0 min
4. Drag-drop org description from content library: 1 min
5. Write specific sections (same): 3 hours
6. Click "Submit" (updates status, sets reminders automatically): 1 min

**Total**: ~3 hours + all in one place

**Time saved**: 40% + reduced context switching + built-in compliance (never miss deadline, always track outcome)

---

**Document Control:**
- **Version**: 1.0
- **Last Updated**: 14 November 2025
- **Next Review**: After module PRDs completed
- **Owner**: BLKOUT Fundraising Team
- **Priority**: HIGH - Foundation for all grant funding automation
