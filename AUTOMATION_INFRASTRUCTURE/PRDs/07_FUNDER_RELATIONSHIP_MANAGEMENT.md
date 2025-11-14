# Product Requirement Document
## Grant Funding Platform - Funder Relationship Management & Stewardship Automation

**Version**: 1.0
**Date**: 14 November 2025
**Owner**: BLKOUT Fundraising Team
**Status**: Proposed
**Inspired by**: HumaniTru donor insights model
**Part of**: Grant Funding Platform Core Architecture

---

## Executive Summary

Transform grant funders from transactional relationships into strategic partnerships through automated insights, relationship tracking, and stewardship workflows - inspired by HumaniTru's donor management approach adapted for institutional funders.

**Value Proposition**: Increase repeat funding success rate from 20% → 60%+ by proactively managing funder relationships, never missing stewardship opportunities, and receiving AI-powered recommendations on which funders to cultivate.

---

## Problem Statement

### Donor Management vs. Funder Management

**HumaniTru insight**: Individual donor retention increased 23% through automated insights and stewardship.

**BLKOUT equivalent**: We need similar for **grant funders** (foundations, trusts, government bodies):
- Track funder giving patterns (did they increase/decrease grant sizes?)
- Identify strategic outreach opportunities (which funders should we reapply to?)
- Automate stewardship (thank-yous, impact reports, relationship nurturing)
- Prevent funders "lapsing" (applied once 3 years ago, never followed up)

### Current State: Transactional, Reactive

**What's missing:**
- ❌ **No funder relationship tracking**: Apply for grant → Get rejected or awarded → Forget about them
- ❌ **No stewardship workflow**: Win £50K grant → Send thank-you → Never update them on impact → They don't fund us again
- ❌ **No proactive insights**: "Arts Council funded us 3 years ago for £20K, we should reapply" (only remembered when someone mentions it)
- ❌ **No pattern detection**: Don't notice that Trust foundations give us 50% success rate vs. Government 10%
- ❌ **No relationship scoring**: All funders treated equally (no prioritization based on relationship strength)

**Example missed opportunity:**
- 2022: Baring Foundation funds BLKOUT £30K (one-off project grant)
- 2023: BLKOUT delivers project, sends final report → No follow-up
- 2024: BLKOUT doesn't reapply (forgot about them, or assumed can't apply again)
- 2025: Baring Foundation had another round (£40K available) → BLKOUT missed it
- **Lost**: Potential £40K from warm funder (already funded us once, relationship existed)

---

## Goals & Success Metrics

### Primary Goals (Inspired by HumaniTru)

1. **Increase repeat funding rate** (from funders who've funded us before): 20% → 60%+
2. **Never miss reapplication opportunities** (automated alerts when eligible to reapply)
3. **Proactive stewardship** (automated thank-yous, impact updates, relationship touchpoints)
4. **AI-powered funder insights** ("Top 10 funders to approach this month")
5. **Relationship intelligence** (know which funders to prioritize)

### Success Metrics

| Metric | Current | Phase 1 Target | Phase 2 Target |
|--------|---------|----------------|----------------|
| **Repeat funding success rate** | ~20% (estimate) | 40% | 60%+ |
| **Funders reapplied to (eligible)** | ~30% | 70% | 90%+ |
| **Stewardship touchpoints per funder** | 1-2/year | 4-6/year | 8-12/year (automated) |
| **"Lapsed" funders reactivated** | 0 | 3-5/year | 10+/year |
| **Funder relationship scores tracked** | 0 | 100% of funders | 100% + AI-enhanced |
| **Time spent on stewardship** | 5 hours/month | 1 hour/month (review only) | 30 min/month (AI-driven) |

---

## Functional Requirements

### Phase 1: Funder Relationship Tracking (Month 1-2)

**FR1: Funder Profile (360° View)**

**Beyond basic funder data, track relationship intelligence:**

**Core Data (from existing modules):**
- Name, type, website, focus areas
- Applications submitted (count)
- Awards received (count, £ total)
- Rejections (count)
- Success rate (%)

**NEW Relationship Intelligence:**
- **Relationship strength** (score 1-10):
  - Never applied = 1
  - Applied once, rejected = 2-3
  - Applied multiple times, rejected = 2
  - Applied once, awarded = 6-7
  - Applied multiple times, 40-60% success = 8
  - Applied multiple times, >60% success = 9-10
  - Multi-year partnership, 80%+ success = 10

- **Giving pattern** (trend):
  - Increasing (latest award > previous)
  - Stable (similar award amounts)
  - Decreasing (latest award < previous)
  - Lapsed (awarded before, but not recently)

- **Engagement level** (activity):
  - Active (applied within 12 months)
  - Warm (applied 12-24 months ago)
  - Cold (applied 24-36 months ago)
  - Lapsed (not engaged in 36+ months, but previously funded)
  - Dormant (applied once, rejected, never followed up)

- **Reapplication eligibility**:
  - Can reapply now (Yes/No)
  - Next eligible date (calculated from last application + funder's reapplication rules)
  - Automatic alert when becomes eligible

**Effort**: 4-6 hours (extend Funders table, calculate fields)

**FR2: Funder Insights Dashboard (Top 10 Opportunities)**

**Inspired by HumaniTru: "Spotlights the top ten donors identified as strategic outreach opportunities"**

**BLKOUT equivalent: "Top 10 Funders to Approach This Month"**

**Auto-generated recommendations based on:**

**1. "Ready to Reapply" (High Priority)**
- Funders who:
  - Previously funded BLKOUT
  - Reapplication window is now open
  - High relationship score (7-10)
- Example: "Baring Foundation: Last awarded £30K (2022). Reapplication eligible as of Nov 2025. Relationship score: 8/10. **Recommended: Apply this quarter.**"

**2. "Increasing Engagement" (Opportunity)**
- Funders who:
  - Increased grant size from previous award
  - Or: Funded us for first time recently (test if they'll fund again)
- Example: "Arts Council: First award £20K (2024). Funded 60% of reapplications in our sector. **Recommended: Reapply for larger amount (£30-40K).**"

**3. "At Risk of Lapsing" (Nurture Needed)**
- Funders who:
  - Funded us before
  - Haven't been approached in 24+ months
  - Relationship score declining
- Example: "Trust for London: Last awarded £15K (2022). No contact since final report (2023). **Recommended: Send impact update, inquire about new programs.**"

**4. "High Success Rate, Unexplored" (Strategic)**
- Funders who:
  - We've applied to once or twice
  - High success rate (50%+)
  - Haven't applied recently (opportunity cost)
- Example: "Lottery Community Fund: 2 applications, 1 award (50% success). Last applied 2023. **Recommended: Review current programs, consider reapplication.**"

**5. "Similar Funders" (New Prospects)**
- Based on funders who've funded us:
  - Find similar funders (focus areas, grant sizes, geography)
  - We haven't applied to yet
- Example: "Tudor Trust: Similar to Baring Foundation (community-led, infrastructure grants, £20-50K). Never applied. **Recommended: Research and consider application.**"

**Delivery:**
- Dashboard view (top 10 list)
- Weekly/monthly email digest ("This week's top funder opportunities")
- Configurable (can adjust criteria, frequency)

**Effort**: 8-12 hours (build recommendation engine, dashboard)

**FR3: Stewardship Workflow Automation**

**Inspired by HumaniTru: "Stewardship Automation uses real-time supporter data to increase engagement"**

**BLKOUT equivalent: Automated touchpoints with funders**

**Trigger-based stewardship actions:**

**1. Award Received → Thank You Sequence**
- **Within 48 hours**: Personalized thank-you email (template + custom note)
- **Week 2**: Social media post thanking funder (if they allow public acknowledgment)
- **Month 1**: First impact update ("Here's what we've accomplished with your funding so far")
- **Mid-project**: Progress report (photo, story, data)
- **Project completion**: Final report + impact summary

**2. Application Submitted → Stewardship Prep**
- **If previously funded**: Prepare impact summary from last grant (have ready if they ask)
- **If new funder**: Research their recent grants (who else they've funded, what they care about)

**3. Rejection Received → Learn & Nurture**
- **Within 1 week**: Request feedback (if funder offers)
- **Month 3**: Send general BLKOUT update (keep relationship warm, not transactional)
- **Month 12**: Check if reapplication eligible, review program changes

**4. Funder Lapsing → Reactivation**
- **Alert when**: 18 months since last contact with previously supportive funder
- **Action**: Send impact update, ask if interested in hearing about new projects
- **Goal**: Rekindle relationship before they completely forget about BLKOUT

**5. Reapplication Eligible → Prompt**
- **Alert when**: Funder reapplication window opens (based on their rules)
- **Action**: Notify fundraising team, suggest application priority based on relationship score
- **Include**: Summary of previous grant, success rate with this funder, recommended ask amount

**Automation:**
- Email templates (personalized merge fields: funder name, grant amount, project name)
- Scheduled sends (don't spam - space out touchpoints)
- Track engagement (did they open? Reply? Engage on social media?)

**Effort**: 10-15 hours (workflows + templates + automation setup)

### Phase 2: AI-Powered Insights & Predictions (Months 3-6)

**FR4: Predictive Funder Scoring (Machine Learning)**

**Train AI model on:**
- Historical applications (who we applied to, outcomes)
- Funder characteristics (type, focus, grant size, geography)
- Timing (when we applied, how long to decision)
- Application content (keywords in successful vs. rejected applications)

**Predictions:**
- **Probability of success** with new funder (0-100%)
- **Optimal ask amount** (based on what they've funded before, what we've won)
- **Best timing** (when to apply based on their grant cycles, our success patterns)

**Example output:**
> "Arts Council: 75% probability of success if applying for £30-40K cultural infrastructure grant in Q1 2026. Based on: Previous award (2024), 60% reapplication success rate in sector, optimal timing (Q1 historically better for infrastructure grants)."

**Effort**: 20-30 hours (data science, model training)

**FR5: Automated Impact Reporting**

**Pull data from:**
- Project outcomes (if tracked in separate system)
- Social media (mentions, engagement from grant-funded activities)
- Surveys/feedback (beneficiary testimonials)

**Generate:**
- Quarterly impact summary (for all current funders)
- One-pager (funder-specific: "Your £30K funded X outcomes")
- Annual impact report (comprehensive, all funders)

**Personalization:**
- Funder A cares about beneficiary numbers → Highlight reach (served 500 people)
- Funder B cares about policy change → Highlight advocacy wins
- Funder C cares about sustainability → Highlight long-term model

**Effort**: 15-20 hours (integration, templates, automation)

**FR6: Funder Engagement Scoring**

**Track all interactions:**
- Email opens/replies
- Meeting requests accepted
- Social media engagement (do they like/share our posts?)
- Event attendance (if invited to BLKOUT events, did they come?)
- Response time (fast = engaged, slow = lukewarm)

**Engagement score** (1-10):
- 9-10: Highly engaged (responds within days, attends events, proactive)
- 6-8: Moderately engaged (replies eventually, occasionally engages)
- 3-5: Low engagement (slow to respond, transactional)
- 1-2: Unresponsive (emails go unanswered, relationship cold)

**Use case:**
- Prioritize outreach to high-engagement funders (more likely to respond positively)
- Adjust stewardship for low-engagement funders (less frequent contact, different approach)

**Effort**: 8-12 hours (tracking integration, scoring algorithm)

### Phase 3: Advanced Relationship Management (Months 6+)

**FR7: Funder Portfolio Management**

**Concept**: Manage funders like investment portfolio

**Diversification analysis:**
- Are we too dependent on one funder type? (e.g., 80% from foundations, risky if they cut funding)
- Geographic diversity (all London-based funders vs. UK-wide)
- Grant size diversity (many small grants vs. few large ones)

**Risk assessment:**
- Identify funders at risk of defunding (declining grants, changing priorities, staff turnover)
- Plan for revenue replacement if major funder exits

**Strategic planning:**
- Multi-year view (which funders for Year 1 vs. Year 2 vs. Year 3)
- Relationship progression (move funders from "one-off grant" → "repeat funder" → "multi-year partner")

**Effort**: 12-18 hours

**FR8: Competitive Intelligence**

**Track:**
- Which organizations are funded by our target funders?
- How much are they getting? (publicly available from funder websites, Charity Commission)
- What for? (types of projects funded)
- Our position relative to peers (are we competitive? Underfunded? Overfunded?)

**Use case:**
- Benchmark ask amounts ("Similar orgs get £30-50K from this funder, we should ask £40K not £10K")
- Identify gaps (funders we should approach but haven't)
- Learn from successful peers (what are they doing that we're not?)

**Effort**: 15-20 hours (data collection, analysis)

---

## Data Model

### Funders Table (Extended)

```
funders (extends previous PRDs)
├── relationship_strength (formula 1-10)
├── giving_pattern (single-select: Increasing, Stable, Decreasing, Lapsed)
├── engagement_level (single-select: Active, Warm, Cold, Lapsed, Dormant)
├── engagement_score (formula 1-10, based on interactions)
├── can_reapply (boolean, calculated)
├── next_eligible_date (date, calculated from last_application + reapplication_window)
├── reapplication_window_months (number, funder-specific rule)
├── last_contact_date (date, rollup from touchpoints)
├── days_since_contact (formula: today - last_contact_date)
├── stewardship_stage (single-select: Prospect, Applicant, Funder, Partner, Lapsed)
├── preferred_contact_method (single-select: Email, Phone, In-person, Events)
├── program_officer_name (text)
├── program_officer_email (email)
├── program_officer_phone (phone)
├── notes (long text: relationship history, insights)
└── ai_recommendation (long text: auto-generated suggestions)
```

### Touchpoints Table (New)

```
touchpoints
├── id (auto)
├── funder_id (link to funders)
├── date (date)
├── type (single-select: Application, Award, Rejection, Thank You, Impact Update, Meeting, Event, Email, Call, Social Media, Other)
├── direction (single-select: Outbound, Inbound)
├── notes (long text: what was discussed/sent)
├── attachments (file upload: emails, reports, etc.)
├── outcome (text: result of touchpoint, if applicable)
└── next_action (text: what to do next)
```

### Stewardship Workflows Table (New)

```
stewardship_workflows
├── id (auto)
├── name (text: "Post-Award Thank You Sequence")
├── trigger (single-select: Award Received, Application Submitted, Rejection, Lapsed, Reapplication Eligible)
├── steps (long text, JSON):
│   [
│     {day: 2, action: "Send thank you email", template: "award_thank_you"},
│     {day: 14, action: "Post social media", template: "award_announcement"},
│     {day: 30, action: "Send first impact update", template: "impact_update_1"}
│   ]
└── active (boolean)
```

---

## User Stories

### As a Fundraising Lead
> "Every Monday, I want to know: which funders should I prioritize this week? Who should I reach out to? Who needs a stewardship touchpoint?"

**Acceptance Criteria:**
- Open Funder Insights Dashboard
- See "Top 10 Funders to Approach This Week"
- Sorted by priority (reapplication eligible + high relationship score = top of list)
- One-click: Create touchpoint, send stewardship email, start application

### As a Grant Writer
> "I'm about to reapply to Baring Foundation. I want to quickly see: when did they last fund us? How much? What did we deliver? What's our relationship history?"

**Acceptance Criteria:**
- Open Baring Foundation profile
- See: All previous applications/awards (timeline view)
- See: All touchpoints (emails, reports, meetings)
- See: AI recommendation ("Reapply for £40K, 70% probability based on relationship strength")
- See: Last impact report sent (attach updated version to reapplication)

### As a Communications Lead
> "Arts Council just awarded us £50K. I need to thank them appropriately and keep them updated throughout the project without manually remembering all touchpoints."

**Acceptance Criteria:**
- Award logged in system
- Stewardship workflow auto-triggered:
  - Day 2: Draft thank-you email ready for review/send
  - Week 2: Social post draft ready
  - Month 1: Impact update reminder (with template)
  - Month 6: Progress report reminder
  - Project end: Final report reminder
- All touchpoints logged automatically
- Never miss a stewardship moment

---

## Integration Points

### Input (What This Module Needs)

**From Opportunity Discovery & Pipeline:**
- Applications submitted (who we applied to, when)
- Awards received (outcomes, amounts)
- Rejections received

**From Application Builder:**
- Application content (keywords, project descriptions - for AI analysis)

**From Analytics:**
- Success rates (feed into relationship strength calculation)

### Output (What This Module Provides)

**To Assessment & Prioritization:**
- Funder relationship scores (prioritize high-relationship funders)
- AI recommendations (which funders to approach)

**To Pipeline Manager:**
- Reapplication alerts (notify when eligible to reapply)

**To Team:**
- Stewardship reminders (send impact update, thank-you, etc.)
- Weekly funder insights (Top 10 opportunities)

---

## Workflow Example

### Award → Stewardship → Reapplication Flow

```
1. [Grant Awarded: Arts Council £50K]
   ├─ Update funder profile:
   │   ├─ Relationship strength: 6 → 8 (first award)
   │   ├─ Giving pattern: Stable (one data point)
   │   ├─ Engagement level: Active
   │   └─ Reapplication eligible: No (until 12 months after project end)
   └─ Trigger stewardship workflow: "Post-Award Sequence"

2. [Day 2: Thank You]
   ├─ Auto-generate personalized thank-you email
   ├─ Notify fundraising lead to review/send
   ├─ Log touchpoint (type: Thank You, direction: Outbound)
   └─ Update: last_contact_date = Today

3. [Week 2: Social Media]
   ├─ Draft social post: "Grateful to @ArtsCouncil for £50K to support..."
   ├─ Notify comms lead to review/post
   └─ Log touchpoint (type: Social Media)

4. [Month 1: Impact Update]
   ├─ Reminder: Send first impact update
   ├─ Template: "One month in: Here's what we've achieved..."
   ├─ Include metrics: X people served, Y events held
   └─ Log touchpoint (type: Impact Update)

5. [Month 6: Progress Report]
   ├─ Generate progress report (pull data from project tracker)
   ├─ Send to Arts Council
   └─ Log touchpoint

6. [Month 12: Project Completion]
   ├─ Final report sent
   ├─ Calculate reapplication eligible date (month 18 or 24, based on rules)
   └─ Set reminder

7. [Month 18: Reapplication Alert]
   ├─ Notify team: "Arts Council reapplication window open"
   ├─ AI recommendation: "High priority - relationship score 9/10, 80% success rate for reapplications"
   ├─ Attach: Previous application, impact achieved, relationship history
   └─ Create opportunity in pipeline (prefilled with Arts Council details)

8. [New Application: Arts Council £60K]
   ├─ Relationship history auto-populated in application
   ├─ Reference previous success
   └─ Cycle repeats
```

---

## Success Criteria

### Phase 1 is "Done" when:

- [ ] All funders have relationship strength scores
- [ ] Top 10 Funder Insights dashboard working (auto-generated weekly)
- [ ] First stewardship workflow automated (post-award thank-you sequence)
- [ ] Reapplication alerts working (tested with dummy dates)
- [ ] Team receives weekly "Top Funders to Approach" email
- [ ] First "lapsed" funder reactivated (contacted after 24+ months dormancy)

### Overall Success (12 months):

- [ ] Repeat funding rate increased from 20% → 40%+
- [ ] 70%+ of eligible reapplications completed (vs. ~30% currently)
- [ ] Zero funders lapse unintentionally (all previous funders either reapplied to or consciously deprioritized)
- [ ] 4-6 stewardship touchpoints per funder per year (automated)
- [ ] Team reports: "We always know which funders to prioritize"

---

## Risks & Mitigation

### Risk 1: Over-Automation Feels Impersonal

**Likelihood**: Medium
**Impact**: High (funders feel like just a number)

**Mitigation:**
- Templates are starting points, always personalize
- High-value funders get personal touch (calls, meetings, handwritten notes)
- Automation handles reminders/logistics, not relationship itself
- Train team: "Automation frees you to focus on quality engagement"

### Risk 2: Data Quality (Garbage In, Garbage Out)

**Likelihood**: High (relationship data is subjective)
**Impact**: High (wrong recommendations if data is poor)

**Mitigation:**
- Required fields (can't log award without recording funder touchpoint)
- Regular audits (quarterly: review all funder profiles)
- Team training (how to assess relationship strength accurately)
- AI suggests, humans decide (recommendations not auto-executed)

### Risk 3: Alert Fatigue

**Likelihood**: Medium (too many "Top 10" lists)
**Impact**: Medium (team ignores insights)

**Mitigation:**
- Weekly, not daily (manageable frequency)
- Configurable (team can adjust what they want to see)
- Actionable only (no FYI alerts, only "you should do X")
- Track open rate (if <50% opened, reduce frequency)

---

## Next Steps

1. **Extend Funders table** (4-6 hours):
   - Add relationship intelligence fields
   - Calculate scores for existing funders
   - Validate formulas

2. **Build Top 10 Dashboard** (8-12 hours):
   - Create recommendation algorithm
   - Design dashboard view
   - Set up weekly email digest

3. **Create first stewardship workflow** (6-8 hours):
   - Post-award thank-you sequence
   - Email templates
   - Automation setup

4. **Pilot test** (2 weeks):
   - Use with next grant award
   - Monitor: Does stewardship happen on time?
   - Gather feedback: Are insights useful?

5. **Iterate & scale** (ongoing):
   - Add more workflows (rejection nurture, lapsed reactivation)
   - Refine recommendations based on what works
   - Expand to all funders

---

**Document Control:**
- **Version**: 1.0
- **Last Updated**: 14 November 2025
- **Inspired by**: HumaniTru donor insights model (adapted for grant funders)
- **Next Review**: After Phase 1 pilot
- **Owner**: BLKOUT Fundraising Team
- **Dependencies**: Core Architecture, Opportunity Discovery, Pipeline Manager, Analytics
- **Priority**: HIGH - Key differentiator for long-term funding success
