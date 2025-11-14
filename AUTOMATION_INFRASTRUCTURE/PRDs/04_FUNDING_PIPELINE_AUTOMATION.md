# Product Requirement Document
## Funding Pipeline Automation

**Version**: 1.0
**Date**: 14 November 2025
**Owner**: BLKOUT Infrastructure Team
**Status**: Proposed
**Related**: Grant-funding repository (created in previous session)

---

## Executive Summary

Automate the grant funding pipeline to track opportunities from landscape scanning through application to award, with prioritization, deadline management, and application templates. Transform the Grant-funding repository from static documentation into an active workflow system.

**Value Proposition**: Apply to more grants, faster, with better prioritization and never miss a deadline.

---

## Problem Statement

### Current State: Manual & Reactive

**From Grant-funding Repository Work:**

You've created a well-structured repository with:
- ✅ Strategic framework (funding philosophy, hybrid revenue model)
- ✅ Folder structure (STRATEGY/, LANDSCAPE/, APPLICATIONS/, etc.)
- ✅ Templates (application template, prioritization matrix)
- ✅ Monthly scanning plan (first Monday of each month)

**But it's all manual:**
- ❌ No automated landscape scanning (relies on someone remembering to do it monthly)
- ❌ No deadline tracking (opportunities get missed)
- ❌ No prioritization automation (manual scoring against matrix)
- ❌ No application status tracking (what's submitted, what's pending, what's awarded)
- ❌ No success rate analytics (which types of funders say yes? Which say no?)
- ❌ No workflow (who's writing, who's reviewing, who's submitting)

### What Happens Without Automation

**Missed Opportunities:**
- Grant opens and closes before you notice it
- Perfect-fit funder, but deadline was yesterday
- Lose track of upcoming deadlines across multiple applications

**Inefficiency:**
- Re-write same information for each application (org background, beneficiary info, etc.)
- Manual copying of data from previous applications
- Time spent on low-probability applications

**Lack of Learning:**
- Don't track success rates (which funders work, which don't)
- Can't identify patterns (early-stage vs. established project funding, large vs. small grants, etc.)
- Repeat mistakes (apply again to funder who rejected similar proposal)

**Strategic Drift:**
- Pursue funding that doesn't align with mission
- Chase large grants when small grants are better fit
- No clear view of funding pipeline health

---

## Goals & Success Metrics

### Primary Goals

1. **Increase applications** from ~10/year → 25-30/year (volume)
2. **Improve success rate** from ~20% → 35%+ (quality/targeting)
3. **Never miss a deadline** (automation alerts)
4. **Prioritize ruthlessly** (focus on high-probability, high-value opportunities)
5. **Reduce application time** by 40% (templates, automation, reuse)
6. **Build funding intelligence** (track what works, what doesn't)

### Success Metrics

| Metric | Current State | Year 1 Target | Year 2 Target |
|--------|--------------|---------------|---------------|
| Applications submitted | ~10/year (estimated) | 25/year | 30/year |
| Success rate | Unknown (~20% typical) | 30% | 35% |
| Missed deadlines | ~2-3/year (estimated) | 0 | 0 |
| Avg time per application | ~8-12 hours (estimated) | 5-7 hours | 4-6 hours |
| Funding secured | £0 (not CBS yet) | £50-100K | £150-250K |
| Pipeline visibility | None | 3 months forward | 6 months forward |

### Key Performance Indicators

- **Pipeline value** (total £ of applications in progress)
- **Success rate by funder type** (foundations vs. government vs. trusts)
- **Success rate by ask size** (<£10K vs. £10-50K vs. £50K+)
- **Average time to decision** (submission → response)
- **Reapplication success** (2nd round conversion rate)
- **Opportunity discovery rate** (new funders found per month)

---

## User Stories

### As a Fundraising Lead
> "Every first Monday, I need to scan for new grant opportunities. Currently I manually search websites and set up Google Alerts. I want to see a curated list of relevant opportunities automatically."

**Acceptance Criteria:**
- Automated scan of key funder websites (Arts Council, Lottery, local authorities, etc.)
- RSS feed aggregation for grant portals
- Filter by relevance (keywords: LGBTQ+, Black communities, cultural infrastructure, etc.)
- Email digest of new opportunities found
- One-click add to pipeline

### As a Grants Manager
> "I'm tracking 15 applications across different stages. I need to know: what's due this week? What needs review? What's waiting for a decision?"

**Acceptance Criteria:**
- Kanban board view: Discovery → Research → Drafting → Review → Submitted → Decision
- Deadline alerts (7 days, 3 days, 1 day before due)
- Status tracking (who's working on what)
- Overdue flag (if past deadline)
- One-click export of pipeline status for board report

### As a Grant Writer
> "I'm drafting an application to Arts Council. I've written about BLKOUT's mission 20 times before. I don't want to rewrite it from scratch."

**Acceptance Criteria:**
- Content library (standard descriptions of BLKOUT, beneficiaries, team, etc.)
- Previous successful applications searchable
- Copy/paste frequently used sections
- Application template auto-populates with BLKOUT boilerplate
- Save draft, return later

### As a Strategic Lead
> "We're deciding whether to apply to Lottery Awards for All (£10K, high effort) or Trust for London (£5K, low effort). I need data to prioritize."

**Acceptance Criteria:**
- Prioritization score auto-calculated:
  - Strategic fit (mission alignment)
  - Probability (have we applied before? Similar orgs funded?)
  - Effort vs. reward (£/hour of work)
- Comparison view (side-by-side scoring)
- Recommendation ("Apply" vs. "Skip")
- Log decision + reasoning (for learning)

### As a Board Member
> "In the board meeting, I want to see: How healthy is our funding pipeline? What's our success rate? What's our funding gap for next year?"

**Acceptance Criteria:**
- Dashboard: Total pipeline value, probability-weighted forecast
- Success rate trends (improving or declining?)
- Upcoming deadlines (next 30 days)
- Funding secured vs. target (RAG status)
- Export to PDF for board pack

---

## Functional Requirements

### Core Features (Phase 1)

**FR1: Opportunity Discovery & Scanning**

**Manual Entry:**
- Add grant opportunity manually (form-based)
- Required fields: Funder, Grant Name, Amount, Deadline, Eligibility, URL
- Optional: Description, Keywords, Contact Person

**Automated Discovery (Phase 2):**
- RSS feed monitoring (grant portals, funder websites)
- Email inbox monitoring (forward grant alerts to system)
- Web scraping (selected funder websites with permissive terms)
- Weekly digest of new opportunities

**FR2: Opportunity Pipeline (Kanban Board)**

**Stages:**
1. **Discovered** (new opportunities identified)
2. **Researching** (assessing fit, gathering info)
3. **Prioritized** (decided to pursue)
4. **Drafting** (application in progress)
5. **Review** (internal review before submission)
6. **Submitted** (application filed, awaiting decision)
7. **Awarded** (successful) OR **Rejected** (unsuccessful) OR **Archived** (decided not to pursue)

**Card View (Each Opportunity):**
- Funder, grant name, amount
- Deadline (countdown timer)
- Priority score (auto-calculated)
- Status indicator (on track, at risk, overdue)
- Assigned to (who's working on it)
- Quick actions (move stage, add note, set reminder)

**Filters:**
- By stage, deadline, priority, amount, funder type
- Search by keyword

**FR3: Prioritization Engine**

**Auto-calculate priority score based on Grant-funding repo matrix:**

**Strategic Fit Score (1-10):**
- Mission alignment (LGBTQ+, Black communities, cultural infrastructure)
- Project readiness (do we have the capacity to deliver?)
- Budget fit (does ask match our budget needs?)
- Capacity match (do we have staff/volunteers to execute?)
- Relationship potential (funder we want long-term relationship with?)

**Urgency (High/Medium/Low):**
- <30 days = HIGH
- 30-90 days = MEDIUM
- >90 days = LOW

**Significance:**
- £50K+ = HIGH
- £10-50K = MEDIUM
- <£10K = LOW (unless strategic)

**Formula:**
```
Priority Score = Strategic Fit × Urgency × Significance
Color-code: 🔴 High Priority, 🟡 Medium, 🟢 Low
```

**Manual Override:**
- Can manually adjust priority (with note explaining why)

**FR4: Deadline Management**

- **Deadline tracking** for all opportunities
- **Email alerts**:
  - 30 days before
  - 14 days before
  - 7 days before
  - 3 days before
  - 1 day before
  - Day of deadline (final reminder)
- **Calendar view** (see all deadlines by month)
- **Integration with Google Calendar** (export deadlines)
- **Overdue flag** (if past deadline but not submitted)

**FR5: Application Templates & Content Library**

**Templates:**
- Arts Council England (standard sections)
- Lottery Awards for All (specific format)
- Trusts/Foundations (generic template)
- Government grants (gov.uk style)
- Custom (build your own)

**Content Library (Reusable Blocks):**
- Organization description (200 words, 100 words, 50 words versions)
- Beneficiary demographics
- Team bios
- Budget narratives
- Safeguarding policies
- Equality & diversity statements
- Case studies
- Letters of support

**Application Workspace:**
- Select template
- Auto-populate with organization details
- Write/edit application sections
- Track word counts
- Save drafts
- Assign to team member for review

**FR6: Status Tracking & Workflow**

**For each application:**
- **Assigned to**: Who's the lead writer?
- **Status**: Draft → Review → Final → Submitted
- **Progress**: % complete (sections completed / total sections)
- **Comments**: Team feedback on drafts
- **Approval**: Board sign-off required? (Yes/No)
- **Submission method**: Online, email, post
- **Submitted date**: When was it sent?
- **Decision date**: When do we expect to hear back?
- **Outcome**: Awarded, Rejected, Pending

**FR7: Success Tracking & Analytics**

**For each submitted application:**
- **Outcome** (Awarded / Rejected / Pending)
- **Amount requested** vs. **Amount awarded** (if partial award)
- **Decision timeline** (submitted → decision received)
- **Feedback** (if funder provided any)
- **Lessons learned** (what worked, what didn't)

**Dashboard Analytics:**
- **Overall success rate** (% of applications awarded)
- **Success rate by funder type** (foundations, government, lottery, trusts)
- **Success rate by amount** (<£10K, £10-50K, £50K+)
- **Average decision time** (how long do funders take?)
- **Total secured vs. target** (are we on track?)
- **Win/loss trends** (improving or declining over time?)

### Enhanced Features (Phase 2)

**FR8: Funder Relationship Tracking**

- **Funder database** (all funders we've interacted with)
- **Relationship history** (all applications to each funder)
- **Success rate per funder** (how often do they say yes to us?)
- **Contact details** (program officer, email, phone)
- **Meeting notes** (if we've had exploratory conversations)
- **Reapplication rules** (can apply again in 12 months, etc.)

**FR9: Multi-Round Application Support**

- **Link related applications** (Round 1 → Round 2 of same funder)
- **Track conversion rates** (what % of R1 invited to R2? What % of R2 win?)
- **Reminders** ("Lottery Round 1 deadline in 6 months" even if Round 2 is 12 months away)

**FR10: Team Collaboration**

- **Assign tasks** (e.g., "Bob: write project description", "Jane: review budget")
- **Comments/feedback** on application drafts
- **Version control** (track changes to application over time)
- **Approval workflow** (writer → reviewer → board → submit)
- **Real-time collaboration** (if using Google Docs integration)

**FR11: Budget Generator**

- **Budget templates** (standard categories: staff, overheads, project costs)
- **Auto-calculate** totals and percentages
- **Export to Excel** (for funder formats)
- **Reuse across applications** (copy budget from previous successful grant)
- **Narrative generator** (basic budget narrative from line items)

**FR12: Integration with GitHub**

- **Link applications to project repos** (as outlined in Grant-funding repo template)
- **Auto-populate project description** from repo README
- **Pull issue/milestone data** (show project progress)
- **Cross-reference** (this grant funds this GitHub project)

### Advanced Features (Phase 3)

**FR13: AI-Powered Opportunity Matching**

- **Natural language search** ("Find LGBTQ+ cultural infrastructure grants >£20K")
- **Similarity matching** ("Find grants similar to Arts Council NPO")
- **Auto-tagging** (AI reads grant description, suggests keywords)
- **Success prediction** (based on historical data, predict probability of success)

**FR14: Automated Grant Writing Assistance**

- **AI drafting** (generate first draft from project description + funder requirements)
- **Tone matching** (adapt writing style to funder preferences)
- **Compliance checking** (flag if application doesn't meet eligibility criteria)
- **Similarity warning** ("This looks very similar to rejected application from 2023 - consider revising")

**FR15: Reporting Integration**

- **Auto-generate funder reports** (if grant awarded, track deliverables)
- **Link to project outcomes** (did we achieve what we promised?)
- **Impact measurement** (beneficiary numbers, outputs, outcomes)

---

## Technical Requirements

### Technology Stack

**Recommended: Airtable (Best Fit for Phase 1-2)**

**Why Airtable?**
- **Relational database** (opportunities, applications, funders, content library)
- **Kanban view** (perfect for pipeline visualization)
- **Forms** (easy opportunity entry)
- **Automations** (email alerts, deadline reminders) - built-in, no Zapier needed
- **Free tier** (1,200 records = ~200 grants/year for 6 years)
- **API** (integrate with other tools later)
- **Mobile app** (check pipeline on the go)
- **Collaboration** (team can work together)

**Setup Time**: 8-12 hours for Phase 1

**Alternative: Notion (Simpler, Less Powerful)**

**Why Notion Might Work:**
- Simpler than Airtable (easier for non-technical users)
- Document storage built-in (easier to store draft applications)
- Free for small teams

**Why Airtable is Better for This:**
- Better relational data (link opportunities → applications → funders)
- Better automation (Notion requires Zapier, Airtable has built-in)
- Better analytics (Airtable has better reporting/charts)
- Better pipeline view (Airtable kanban is more polished)

**Decision**: **Airtable** for Phase 1-2, migrate to custom build in Phase 3 if needed.

### Data Model (Airtable Tables)

**Table 1: Opportunities**
- Funder (text)
- Grant Name (text)
- Amount (currency)
- Deadline (date)
- Eligibility Criteria (long text)
- URL (URL)
- Description (long text)
- Stage (single select: Discovered, Researching, Prioritized, Drafting, Review, Submitted, Awarded, Rejected, Archived)
- Priority Score (formula: strategic fit × urgency × significance)
- Strategic Fit (rating 1-10)
- Urgency (single select: High, Medium, Low)
- Significance (single select: High, Medium, Low)
- Assigned To (user)
- Status (single select: On Track, At Risk, Overdue)
- Keywords (multi-select: LGBTQ+, Black Communities, Cultural, Infrastructure, etc.)
- Discovered Date (date)
- Submitted Date (date)
- Decision Date (date)
- Outcome (single select: Awarded, Rejected, Pending)
- Amount Awarded (currency)
- Lessons Learned (long text)
- Link to Application (link to Applications table)
- Link to Funder (link to Funders table)

**Table 2: Applications** (Detailed Application Drafts)
- Title (text)
- Opportunity (link to Opportunities table)
- Template Used (link to Templates table)
- Application Sections (long text or linked records for each section)
- Word Count (formula)
- Status (single select: Draft, Review, Final, Submitted)
- Assigned To (user)
- Reviewer (user)
- Draft Version (number)
- Last Edited (date)
- Attachments (file upload: supporting docs, letters, etc.)

**Table 3: Funders** (Relationship Tracking)
- Funder Name (text)
- Type (single select: Foundation, Government, Lottery, Trust, Corporate)
- Focus Areas (multi-select: Arts, LGBTQ+, Black Communities, etc.)
- Website (URL)
- Contact Person (text)
- Email (email)
- Phone (text)
- Applications History (link to Opportunities table)
- Success Rate (formula: count of awarded / count of total)
- Last Application Date (rollup from Opportunities)
- Notes (long text)

**Table 4: Content Library** (Reusable Blocks)
- Block Name (text: "Org Description 200w", "Team Bio - Robert", etc.)
- Type (single select: Org Description, Beneficiaries, Team, Budget, Policy, Case Study, Letter of Support)
- Content (long text)
- Word Count (formula)
- Last Updated (date)
- Used In (link to Applications table)

**Table 5: Templates** (Application Templates)
- Template Name (text: "Arts Council NPO", "Lottery Awards for All", etc.)
- Funder (link to Funders table)
- Sections (long text: list of required sections)
- Guidance (long text: tips for this template)
- Example Application (file upload: previous successful application)

### Integrations

**Phase 1 (Airtable Built-In):**
- Email notifications (deadline reminders)
- Slack notifications (optional: post new opportunities to #grants channel)
- Calendar sync (export deadlines to Google Calendar via iCal feed)

**Phase 2 (Zapier/Make.com):**
- Gmail → Airtable (forward grant alerts to auto-create opportunities)
- RSS feeds → Airtable (monitor funder websites)
- Google Docs → Airtable (link draft applications in Docs to Airtable records)
- Airtable → GitHub (create issue when grant awarded: "Deliver [Project] funded by [Funder]")

**Phase 3 (Custom Build):**
- AI integration (OpenAI API for grant writing assistance)
- Web scraping (automated funder website monitoring)
- GitHub deep integration (pull project data for applications)

---

## Implementation Phases

### Phase 1: Manual Pipeline (Month 1) - FOUNDATION

**Deliverables:**
- [ ] Set up Airtable base with 5 tables (Opportunities, Applications, Funders, Content, Templates)
- [ ] Import existing grant research (if any) into Opportunities table
- [ ] Create 3-5 application templates (Arts Council, Lottery, generic foundation)
- [ ] Populate content library with BLKOUT boilerplate (org description, team, etc.)
- [ ] Set up kanban view (pipeline visualization)
- [ ] Configure deadline alerts (email reminders)
- [ ] Train team (1-hour workshop)

**Effort**: 10-15 hours
**Priority**: HIGH

**Success Criteria:**
- All team members can add opportunities
- Pipeline shows all active grants being pursued
- First grant application drafted using templates/content library
- Deadline alerts working (test with dummy deadline)

### Phase 2: Automation & Intelligence (Month 2-3)

**Deliverables:**
- [ ] Automated opportunity discovery (RSS feeds, email forwarding)
- [ ] Prioritization engine (auto-calculate scores)
- [ ] Funder relationship tracking
- [ ] Analytics dashboard (success rates, trends)
- [ ] Multi-round application support
- [ ] Integration with Google Calendar (deadline sync)

**Effort**: 12-18 hours
**Priority**: MEDIUM

**Success Criteria:**
- At least 5 new opportunities auto-discovered per month
- Prioritization scores help skip 30%+ of low-fit opportunities
- Success rate data informs strategy (which funders to focus on)
- Team uses calendar sync (no missed deadlines)

### Phase 3: Advanced Features (Month 6+)

**Deliverables:**
- [ ] AI-powered opportunity matching
- [ ] AI grant writing assistance
- [ ] Budget generator
- [ ] Deep GitHub integration
- [ ] Reporting module (post-award deliverables tracking)

**Effort**: 20-30 hours
**Priority**: LOW

---

## Dependencies

### External Dependencies

- **Airtable account** (free or Plus plan £20/month if needed)
- **Zapier** (for Phase 2 automation, free tier may suffice)
- **Funder websites** (RSS feeds, if available)

### Internal Dependencies

- **Fundraising lead assigned** (who owns the pipeline)
- **Grant-funding repository** (already created - good foundation)
- **Content creation** (need to write initial content library blocks)
- **Historical data** (if you have previous grant applications, import them)

---

## Risks & Mitigation

### Risk 1: Pipeline Neglect (No One Updates It)

**Likelihood**: High (busy volunteers)
**Impact**: High (system becomes stale, useless)

**Mitigation:**
- **Weekly standup** (10 min team check-in: what's new in pipeline?)
- **Assign ownership** (one person is "pipeline manager")
- **Make it easy** (Airtable mobile app, email-to-add, etc.)
- **Link to incentives** (can't discuss grant strategy without looking at pipeline)

### Risk 2: Over-Optimization (Spend More Time on System Than Applying)

**Likelihood**: Medium (tempting to perfect the system)
**Impact**: Medium (defeats purpose)

**Mitigation:**
- **80/20 rule**: System should save time, not consume it
- **Time-box setup**: Phase 1 = max 15 hours, then use it
- **Measure ROI**: Track time saved vs. time spent on system

### Risk 3: Data Quality Issues (Garbage In, Garbage Out)

**Likelihood**: Medium (team enters incomplete/inaccurate data)
**Impact**: High (wrong priorities, missed deadlines)

**Mitigation:**
- **Required fields** (can't save opportunity without deadline, amount, funder)
- **Data validation** (Airtable field types enforce correct formats)
- **Monthly audit** (review pipeline, fix errors)
- **Training** (team knows how to enter data correctly)

---

## Success Criteria & Definition of Done

### Phase 1 is "Done" when:

- [ ] Airtable base set up with all tables
- [ ] At least 10 opportunities in pipeline
- [ ] First application drafted using template + content library
- [ ] Deadline alerts tested and working
- [ ] Team trained and actively using system
- [ ] Successfully submitted first grant via this system

### Overall Project is "Successful" when:

- [ ] 25+ applications submitted in Year 1 (vs. ~10 before)
- [ ] Success rate >30%
- [ ] Zero missed deadlines
- [ ] Application drafting time reduced by 40%
- [ ] £50-100K funding secured in Year 1
- [ ] Team reports confidence in pipeline visibility

---

## Appendix: Sample Opportunity Entry

**Opportunity:** Arts Council NPO 2026-2029
**Funder:** Arts Council England
**Amount:** £50,000/year (£200K total over 4 years)
**Deadline:** 2025-12-15
**Stage:** Researching
**Priority Score:** 🔴 HIGH (9/10 strategic fit × HIGH urgency × HIGH significance)
**Eligibility:** Must have 2+ years operating history (✅), demonstrate artistic excellence (✅), serve priority communities (✅)
**URL:** https://www.artscouncil.org.uk/NPO
**Assigned To:** Robert
**Status:** On Track (70 days to deadline)
**Keywords:** Arts, Cultural Infrastructure, LGBTQ+, Black Communities
**Lessons from previous applications:** Emphasize track record, community voice, sustainability plan

---

**Document Control:**
- **Version**: 1.0
- **Last Updated**: 14 November 2025
- **Next Review**: After Phase 1 implementation
- **Owner**: BLKOUT Fundraising Team
- **Priority**: HIGH - Critical for financial sustainability
