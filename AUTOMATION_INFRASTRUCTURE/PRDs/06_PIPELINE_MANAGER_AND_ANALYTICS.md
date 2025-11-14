# Product Requirement Document
## Grant Funding Platform - Pipeline Manager & Analytics

**Version**: 1.0
**Date**: 14 November 2025
**Owner**: BLKOUT Fundraising Team
**Status**: Proposed
**Part of**: Grant Funding Platform Core Architecture

---

## Executive Summary

Provide real-time visibility into the grant funding pipeline - what's in progress, what's due, what we're winning - with deadline alerts and success analytics to continuously improve strategy.

**Value Proposition**: Never miss a deadline + learn what works to increase future success rate from 20% → 35%+.

---

## Problem Statement

### Current State: No Pipeline Visibility

**What's invisible today:**
- ❌ **Where opportunities are in workflow** (discovered? Being written? Submitted? Awaiting decision?)
- ❌ **What's due when** (deadlines scattered across emails, calendars, memory)
- ❌ **Who's working on what** (which writer has 3 applications, which has none?)
- ❌ **Pipeline health** (are we on track for funding targets? How many applications in progress?)
- ❌ **Success patterns** (which funders say yes? Which say no? Why?)

**Current tracking methods:**
- Spreadsheet (manually updated, often out of date)
- Individual calendars (team member A knows their deadlines, not team B's)
- Email threads (search for "deadline" → 47 results, which is relevant?)
- Memory (risky)

**Consequences:**
- **Missed deadlines**: "Wait, that was due yesterday?!"
- **Unbalanced workload**: One person has 5 applications, another has none
- **No learning**: Apply to same funder type repeatedly despite 0% success rate
- **Can't report to board**: "How's fundraising going?" → "Um, not sure, let me check..."

---

## Goals & Success Metrics

### Primary Goals

1. **Zero missed deadlines** (100% on-time submission)
2. **Real-time pipeline visibility** (always know: what's in progress, what's due, what's waiting for decision)
3. **Balanced workload** (distribute applications across team)
4. **Success rate improvement** (from ~20% → 35%+ via data-driven strategy)
5. **Board reporting** (1-click export of pipeline status for meetings)

### Success Metrics

| Metric | Current | Phase 1 Target | Phase 2 Target |
|--------|---------|----------------|----------------|
| Missed deadlines | 2-3/year | 0 | 0 |
| Pipeline visibility | None | Real-time (5 sec to check) | Predictive (forecast)  |
| Time to generate board report | 30-60 min (manual) | 2 min (export) | 1 min (auto-generate) |
| Success rate | ~20% | 30% | 35%+ |
| Decision turnaround awareness | Unknown | Tracked | Predicted (ML) |
| Funding pipeline value | Unknown | Visible (£X in progress) | Probability-weighted |

---

## Functional Requirements

### Phase 1: Pipeline Visualization & Deadline Management (Month 1)

**FR1: Kanban Board (Pipeline Stages)**

**Stages:**
1. **Discovered** - New opportunities identified
2. **Researching** - Assessing fit, gathering info
3. **Prioritized** - Decided to apply
4. **Drafting** - Application in progress
5. **Review** - Internal review before submission
6. **Submitted** - Application filed, awaiting decision
7. **Awarded** - Successful (grant won)
8. **Rejected** - Unsuccessful
9. **Archived** - Decided not to pursue OR expired/closed

**View:**
- Drag-drop opportunities between stages
- Color-coded:
  - 🟢 >30 days to deadline
  - 🟡 14-30 days to deadline
  - 🔴 <14 days OR overdue
- Display on card:
  - Funder name
  - Grant name
  - Amount (£X)
  - Deadline (days remaining)
  - Assigned to (avatar/initials)
  - Priority score (1-10)

**Interactions:**
- Click card → Full opportunity details
- Drag card → Update stage (auto-saves)
- Filter: By funder type, amount, assigned person, priority

**Technology**: Airtable kanban view

**Effort**: 1-2 hours (configure view)

**FR2: Calendar View (Deadlines)**

**What it shows:**
- All opportunities with deadlines
- Grouped by month
- Color-coded by status (Drafting/Review/Submitted)

**Use cases:**
- Weekly: "What's due this week?"
- Monthly: "What deadlines in December?"
- Planning: "Can we take on another grant due Jan 15th?" (check workload)

**Integration:**
- Export to Google Calendar (iCal feed)
- Team members can subscribe (see deadlines in their personal calendar)

**Technology**: Airtable calendar view + iCal export

**Effort**: 1 hour

**FR3: Deadline Alerts (Automated Reminders)**

**Email/Slack notifications sent:**
- **30 days before**: "Application for [Grant] due in 30 days - status: Drafting (70% complete)"
- **14 days before**: "Application for [Grant] due in 14 days - URGENT: Still in Drafting, needs Review"
- **7 days before**: "Application for [Grant] due in 7 days - CRITICAL: Not yet submitted!"
- **3 days before**: "APPLICATION DUE IN 3 DAYS: [Grant]"
- **Day of deadline** (9am): "DEADLINE TODAY: [Grant] - Submit by end of day"
- **Day after (if not submitted)**: "⚠️ OVERDUE: [Grant] deadline was yesterday - action needed"

**Recipients:**
- Assigned writer (always)
- Fundraising lead (always)
- Reviewer (if in Review status)

**Configuration:**
- Can adjust notification schedule (e.g., add 21d, 10d reminders)
- Can mute for specific opportunities (if not pursuing)

**Technology**: Airtable automation OR Zapier

**Effort**: 3-4 hours (set up 6 automated workflows)

**FR4: Dashboard (At-a-Glance Stats)**

**Metrics displayed:**
- **Opportunities by stage** (count in each kanban column)
- **Upcoming deadlines** (next 7 days, next 30 days)
- **Applications in progress** (Drafting + Review count)
- **Submitted awaiting decision** (count)
- **This month**:
  - Applications submitted (count)
  - Decisions received (Awarded + Rejected count)
  - Success rate (% awarded)
- **This year**:
  - Total applications submitted
  - Total awards
  - Total rejections
  - Success rate
  - Total £ requested vs. £ awarded

**View:**
- Single screen, updates in real-time
- Can filter by date range (this month, this quarter, this year, all time)

**Technology**: Airtable dashboard OR custom dashboard (Metabase, Grafana, etc.)

**Effort**: 2-3 hours (Airtable), 8-12 hours (custom)

**FR5: Workload Distribution View**

**Purpose**: Ensure team members have balanced workload

**View:**
- Group by "Assigned to"
- Count opportunities per person (by stage)
- Example:
  ```
  Robert: 3 in Drafting, 1 in Review, 2 Submitted = 6 total
  Jane: 1 in Drafting, 0 in Review, 1 Submitted = 2 total
  ```
- Highlight imbalance (if one person has >2x others)

**Action**: Reassign opportunities to balance workload

**Technology**: Airtable grouped view

**Effort**: 30 min (configure view)

### Phase 2: Analytics & Learning (Months 2-3)

**FR6: Success Analytics by Dimension**

**Analyze success rate by:**
- **Funder type** (Foundation, Government, Lottery, Trust, Corporate)
  - Example: Foundations = 40% success, Government = 15% success → Prioritize foundations
- **Ask amount** (<£10K, £10-50K, £50-100K, >£100K)
  - Example: <£10K = 50% success, >£100K = 10% success → Focus on smaller grants
- **Project type** (Infrastructure, Events, Capacity building, etc.)
  - Example: Infrastructure grants = 25% success, Events = 45% → Do more event grants
- **Time to decision** (funder response time: weeks, months)
  - Example: Lottery = 12 weeks avg, Trusts = 6 weeks avg → Know when to expect response
- **Repeat applications** (1st time applicant vs. reapplication vs. existing relationship)
  - Example: Reapplications = 60% success vs. 1st time = 20% → Focus on reapplying to won funders

**Visualization:**
- Bar charts (success rate by category)
- Trend lines (success rate over time - improving or declining?)
- Heatmap (which combinations work best: Foundation + <£10K + Infrastructure = X% success)

**Use case**: Inform prioritization - "We should apply to more Foundations for <£10K because we win 50% of those"

**Technology**: Airtable charts OR export to Google Sheets/Excel for advanced analysis

**Effort**: 4-6 hours (set up analytics queries + visualizations)

**FR7: Funder Relationship Scoring**

**For each funder, calculate:**
- **Applications submitted** (count)
- **Awards** (count)
- **Success rate** (% awarded)
- **Total £ requested** (sum)
- **Total £ awarded** (sum)
- **Last application date**
- **Relationship strength** (score 1-10):
  - Never applied = 1
  - Applied once, rejected = 3
  - Applied once, awarded = 7
  - Applied 3+ times, 60%+ success = 10

**Use case**:
- Prioritize re-applying to funders with strong relationships (score 7-10)
- Avoid funders where we've applied 3x, rejected 3x (score 2-3)

**Technology**: Airtable rollup fields + formula

**Effort**: 2-3 hours

**FR8: Decision Tracking & Lessons Learned**

**When decision received (Awarded or Rejected):**
- **Capture**:
  - Outcome (Awarded / Rejected / Partially Awarded)
  - Amount requested vs. Amount awarded (if partial)
  - Decision date (how long did it take?)
  - Feedback (if funder provided any)
  - Lessons learned (free text: "Why did this work/not work?")

**Analytics:**
- Average time to decision (by funder, by grant type)
- Partial award rate (how often do we get less than requested?)
- Rejection reasons (categorize feedback: "Not eligible", "Strong competition", "Budget too high", etc.)

**Use case**:
- Improve future applications based on feedback
- Set realistic decision timeline expectations
- Identify patterns (always rejected for "budget too high" → Reduce ask amounts)

**Technology**: Airtable table (Decisions) linked to Opportunities

**Effort**: 2-3 hours (set up table + forms)

**FR9: Board Reporting (One-Click Export)**

**Purpose**: Generate reports for board meetings

**Report includes:**
- Pipeline summary (opportunities by stage)
- This quarter:
  - Applications submitted (count + £ total requested)
  - Awards received (count + £ total awarded)
  - Success rate
- Upcoming deadlines (next 30 days)
- Year-to-date:
  - Total applications, awards, rejections
  - Success rate
  - £ requested vs. £ awarded
  - Funding gap (target - actual)

**Formats:**
- PDF (formatted report with charts)
- CSV (raw data for board to analyze)
- PowerPoint slide (single-slide summary)

**Technology**: Airtable export OR custom report generator (Metabase)

**Effort**: 4-6 hours (create report template)

### Phase 3: Predictive Analytics & Intelligence (Months 6+)

**FR10: Funding Pipeline Forecast (Probability-Weighted)**

**Concept**: Not all "Submitted" applications are equal

**Calculation:**
```
Pipeline value = Σ (Amount × Probability of success)

Example:
- Arts Council £50K (Submitted, 40% historical success) = £20K weighted
- Lottery £10K (Submitted, 60% historical success) = £6K weighted
- Trust £5K (Submitted, 30% historical success) = £1.5K weighted

Total pipeline value = £27.5K (vs. £65K nominal)
```

**Use case**:
- Realistic forecast: "We have £65K submitted, but expect £27.5K to actually be awarded"
- Identify gap: "Target is £50K, weighted pipeline is £27.5K → Need to apply for more"

**Technology**: Airtable formula OR custom calculator

**Effort**: 6-8 hours (build probability model)

**FR11: Success Prediction (Machine Learning)**

**When new opportunity discovered:**
- AI predicts probability of success based on:
  - Funder (have we applied before? Success rate with them?)
  - Amount (what ask sizes do we usually win?)
  - Focus area (do they fund our type of work?)
  - Competition (how many other orgs likely applying?)
  - Our capacity (do we have time to write quality application?)
- Output: "65% probability of success" (inform prioritization)

**Technology**: Simple ML model (regression) trained on historical data

**Effort**: 20-30 hours (data science work)

**FR12: Funder Intelligence (News & Changes)**

**Monitor:**
- Funder websites for changes (new priorities, rule changes)
- Charity Commission data (if funder is charity, see their accounts - are they giving more/less?)
- News alerts ("XYZ Foundation announces new £5M program")

**Alert team:**
- "[Funder] has new grant program - consider applying"
- "[Funder] changed eligibility criteria - review before applying"

**Technology**: RSS + web scraping + alerts

**Effort**: 10-15 hours (set up monitors)

---

## Data Model

### Opportunities Table (Extended for Pipeline)

```
opportunities (extends prior PRDs)
├── stage (single-select: Discovered, Researching, Prioritized, Drafting, Review, Submitted, Awarded, Rejected, Archived)
├── assigned_to (user: who's responsible)
├── reviewer (user: who reviews before submission)
├── days_to_deadline (formula: deadline - today)
├── deadline_status (formula: if <14d "Urgent", <30d "Soon", else "On Track")
├── progress_pct (number: % complete, from Applications table)
```

### Decisions Table (New)

```
decisions
├── id (auto)
├── opportunity_id (link to opportunities)
├── outcome (single-select: Awarded, Rejected, Partially Awarded, Withdrawn)
├── amount_requested (rollup from opportunity)
├── amount_awarded (currency)
├── award_rate_pct (formula: awarded / requested)
├── decision_date (date)
├── days_to_decision (formula: decision_date - submitted_date)
├── feedback (long text: any funder comments)
├── feedback_category (single-select: Not Eligible, Strong Competition, Budget, Other)
├── lessons_learned (long text: what we learned)
└── would_reapply (checkbox: yes/no)
```

### Funder Relationships Table (New, or Extended Funders)

```
funders (extends core + discovery)
├── applications_submitted (rollup: count from opportunities)
├── awards (rollup: count where outcome = Awarded)
├── rejections (rollup: count where outcome = Rejected)
├── success_rate_pct (formula: awards / applications_submitted)
├── total_requested (rollup: sum of amount_requested)
├── total_awarded (rollup: sum of amount_awarded)
├── last_application_date (rollup: max submitted_date)
├── relationship_score (formula: 1-10 based on success rate + recency)
├── avg_decision_time_days (rollup: avg days_to_decision)
```

---

## Integration Points

### Input (What This Module Needs)

**From Opportunity Discovery:**
- New opportunities (to add to pipeline)

**From Application Builder:**
- Application status (Draft, Review, Final, Submitted)
- Progress % (for deadline urgency assessment)
- Submission date (when moved to "Submitted" stage)

**From Core:**
- All opportunity data (funder, amount, deadline, priority)

### Output (What This Module Provides)

**To Team:**
- Deadline alerts (email, Slack)
- Pipeline visibility (who's working on what)
- Board reports

**To Assessment Module:**
- Success analytics (feed into priority scoring)
- Funder relationship data (inform "should we apply?" decision)

**To Future Opportunities:**
- Lessons learned (improve future applications)
- Funder intelligence (know what works)

---

## User Stories

### As a Fundraising Lead
> "It's Monday morning. I want to know: what's due this week? Who's working on what? Are we on track to hit our £50K quarterly target?"

**Acceptance Criteria:**
- Open Pipeline Dashboard
- See kanban board (at-a-glance: 5 in Drafting, 2 in Review, 3 Submitted)
- Filter calendar view to "This Week" (2 deadlines: Wed and Fri)
- Check stats widget (£35K awarded YTD, £50K target → £15K gap)
- Review complete in <2 minutes

### As a Grant Writer
> "I'm working on 3 applications. I want to be reminded before deadlines so I don't miss one."

**Acceptance Criteria:**
- Receive Slack notification 7 days before each deadline
- Notification shows: Grant name, deadline date, current status
- If not submitted by 3 days before → Escalated "URGENT" notification
- Day of deadline → "TODAY IS THE DEADLINE" notification

### As a Board Member
> "At the board meeting, I need to report on fundraising progress. I want a 1-page summary: how many applications, success rate, funding secured."

**Acceptance Criteria:**
- Click "Generate Board Report"
- Select date range (this quarter)
- Export to PDF
- Report shows:
  - Applications submitted: 8
  - Awards: 3 (£45K)
  - Rejections: 2
  - Pending: 3
  - Success rate: 60% (3/5 decided)
  - Pipeline: £35K submitted, awaiting decision
- Takes <2 min to generate

### As a Strategic Lead
> "We keep applying to government grants but never win. I want data to decide: should we stop wasting time on government grants?"

**Acceptance Criteria:**
- View Success Analytics dashboard
- Filter by Funder Type = "Government"
- See: 8 applications, 0 awards, 0% success rate
- Compare to Foundation: 12 applications, 5 awards, 42% success rate
- Decision: Deprioritize government, focus on foundations
- Analytics inform strategy (data-driven)

---

## Workflow

### Opportunity Lifecycle in Pipeline

```
1. [Discovery Engine finds grant]
   ├─ Creates opportunity record
   └─ Stage = "Discovered"

2. [Assessment: Review & Prioritize]
   ├─ Team reviews opportunity
   ├─ Calculate priority score
   └─ Decision:
       ├─ Apply → Stage = "Prioritized", assign to writer
       └─ Skip → Stage = "Archived"

3. [Application Builder: Draft]
   ├─ Writer creates application
   ├─ Stage = "Drafting"
   └─ Progress tracked (0% → 100%)

4. [Review]
   ├─ Writer completes draft → Stage = "Review"
   ├─ Reviewer provides feedback
   └─ If approved → Stage = "Final"

5. [Submit]
   ├─ Application submitted to funder
   ├─ Stage = "Submitted"
   ├─ Record submission_date
   └─ Set decision_date reminder (based on typical funder response time)

6. [Await Decision]
   ├─ Remains in "Submitted" stage
   ├─ Pipeline Manager monitors
   └─ Remind team if decision overdue (>expected timeline)

7. [Decision Received]
   ├─ Create Decision record
   ├─ Outcome: Awarded OR Rejected
   ├─ Update opportunity:
   │   ├─ Stage = "Awarded" OR "Rejected"
   │   ├─ Record amount_awarded (if Awarded)
   │   └─ Capture feedback, lessons learned
   └─ Analytics Dashboard auto-updates (success rate, £ awarded, etc.)

8. [Post-Decision]
   ├─ If Awarded: Celebrate! Add to case studies
   ├─ If Rejected: Review lessons learned, decide if reapply
   └─ Opportunity archived (visible in history for analysis)
```

---

## Success Criteria

### Phase 1 is "Done" when:

- [ ] Kanban board shows all opportunities by stage (real-time)
- [ ] Calendar view shows all deadlines
- [ ] Deadline alerts working (tested with dummy deadlines)
- [ ] Dashboard displays key metrics (applications submitted, success rate, etc.)
- [ ] Workload distribution view shows assignments per person
- [ ] First month: Zero missed deadlines
- [ ] Team uses dashboard daily (or checks before weekly meeting)

### Overall Success (6 months):

- [ ] Zero missed deadlines (100% on-time submission)
- [ ] Success rate improved from ~20% → 30%+
- [ ] Board reports generated in <2 min (vs. 30-60 min manual)
- [ ] Team can answer "How's fundraising going?" in 30 seconds (look at dashboard)
- [ ] Data-driven decisions (cite analytics when choosing which grants to pursue)

---

## Risks & Mitigation

### Risk 1: Alert Fatigue (Too Many Notifications)

**Likelihood**: Medium (if poorly configured)
**Impact**: High (team ignores all alerts, misses deadline)

**Mitigation:**
- Start conservative (30d, 7d, 3d, 1d only)
- Survey team after 1 month (too many? Too few?)
- Adjust based on feedback
- Option to mute for specific opportunities

### Risk 2: Dashboard Ignored (No One Checks It)

**Likelihood**: Medium (if not integrated into workflow)
**Impact**: High (defeats purpose of pipeline visibility)

**Mitigation:**
- Make it part of weekly routine (Monday standup: review dashboard)
- Email weekly digest (can't ignore email)
- Show value (highlight: "Dashboard showed X was overdue, we fixed it")
- Mobile-friendly (check on phone during commute)

### Risk 3: Poor Data Quality (Garbage In, Garbage Out)

**Likelihood**: High (if stages not updated)
**Impact**: High (pipeline shows wrong status)

**Mitigation:**
- Automation where possible (submitted → auto-update stage)
- Required fields (can't submit without recording submission_date)
- Weekly audit (check for stale records: "In Drafting for 60 days?")
- Team training (emphasize importance of updating stages)

---

## Next Steps

1. **Configure Airtable views** (3-4 hours):
   - Kanban board (by stage)
   - Calendar view (by deadline)
   - Dashboard (metrics)
   - Workload distribution

2. **Set up deadline alerts** (3-4 hours):
   - Airtable automations or Zapier
   - Test with dummy deadlines
   - Confirm notifications work (Slack and/or email)

3. **Create Decisions table** (2-3 hours):
   - Configure fields
   - Link to Opportunities
   - Set up analytics views

4. **Populate with current opportunities** (1-2 hours):
   - Add any in-progress grants to pipeline
   - Set correct stages
   - Assign to team members

5. **Team training** (1 hour):
   - How to use kanban board
   - How to update stages
   - When/how to record decisions

6. **Launch pilot** (Week 1):
   - Use for all current grants
   - Track: Do alerts work? Is pipeline accurate?

7. **Review & iterate** (End of Week 1):
   - Gather feedback
   - Fix issues
   - Refine notification schedule

---

**Document Control:**
- **Version**: 1.0
- **Last Updated**: 14 November 2025
- **Next Review**: After Phase 1 launch
- **Owner**: BLKOUT Fundraising Team
- **Dependencies**: Core Architecture, Opportunity Discovery, Application Builder
- **Priority**: HIGH - Critical for deadline management and continuous improvement
