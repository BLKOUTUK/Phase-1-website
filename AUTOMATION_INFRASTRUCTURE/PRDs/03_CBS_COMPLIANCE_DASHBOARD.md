# Product Requirement Document
## CBS Compliance Dashboard

**Version**: 1.0
**Date**: 14 November 2025
**Owner**: BLKOUT Infrastructure Team
**Status**: Proposed

---

## Executive Summary

Create a centralized dashboard to track all Community Benefit Society (CBS) compliance requirements, deadlines, and documentation. Ensure BLKOUT never misses an FCA filing, annual return, or member confirmation deadline.

**Value Proposition**: CBS registration is complex with ongoing obligations. A compliance dashboard turns reactive scrambling into proactive management.

---

## Problem Statement

### What's Coming After Registration

**You're about to become a registered CBS.** This brings ongoing obligations:

**Annual Requirements:**
- **Annual Return** → FCA (due within 7 months of year-end)
- **Accounts** → FCA (due within 7 months of year-end)
- **Member Confirmations** (affiliation disclosures, contact details)
- **AGM** → Required annually, minutes filed with FCA
- **Rule Changes** → Any changes must be FCA-approved

**As-Needed Requirements:**
- **New Member Registrations** → Notify FCA within 14 days
- **Officer Changes** → Notify FCA within 14 days (secretary, treasurer, etc.)
- **Registered Office Change** → Notify FCA within 14 days
- **Significant Changes** → Major activities, dissolution, mergers

**Ongoing Monitoring:**
- **Member affiliations** → Monitor for new conflicts monthly/quarterly
- **Compliance incidents** → Log and report to FCA if material
- **Policy reviews** → Safeguarding, conflict of interest, etc. (annual)

### Current State: No System

Right now, you have:
- ❌ No centralized view of what's due when
- ❌ No alerts before deadlines
- ❌ No tracking of what's been filed
- ❌ No audit trail of compliance actions
- ❌ Documents scattered across folders

**What happens without a system:**
- Miss FCA deadline → Late filing penalties (£100-500)
- Forget annual member confirmation → Compliance breach
- Lose track of filed documents → Can't prove compliance in audit
- Don't know who's responsible → Diffusion of responsibility

---

## Goals & Success Metrics

### Primary Goals

1. **Never miss an FCA deadline** (zero late filings)
2. **Centralize all compliance documentation** (one source of truth)
3. **Proactive alerts** (know what's due 30/14/7 days in advance)
4. **Clear accountability** (who's responsible for each task)
5. **Audit-ready records** (prove compliance to FCA/auditors)

### Success Metrics

| Metric | Current State | Target State | Timeline |
|--------|--------------|--------------|----------|
| Late filings per year | Unknown (not CBS yet) | 0 | Ongoing |
| Time to find compliance doc | 10+ min (email/folder search) | <30 sec (dashboard) | Phase 1 |
| Compliance task visibility | Reactive (when FCA asks) | 30-day forward visibility | Phase 1 |
| Document completeness | ~70% (some docs lost) | 100% (all docs tracked) | Phase 2 |
| Audit preparation time | Hours (gather docs) | <30 min (export from dashboard) | Phase 2 |
| Compliance confidence | Low (new to CBS) | High (dashboard says we're OK) | Phase 1 |

### Key Performance Indicators

- **On-time filing rate**: 100%
- **Dashboard usage**: Daily check (or automated weekly digest)
- **Document retrieval time**: <1 min for any compliance doc
- **Audit success**: Pass FCA audit with zero findings
- **Volunteer handover time**: <30 min to train new compliance officer (dashboard makes it easy)

---

## User Stories

### As a CBS Secretary
> "I'm responsible for compliance but I'm a volunteer with limited time. I need to know at a glance: what's due this month? What am I at risk of missing? What do I need to chase from other board members?"

**Acceptance Criteria:**
- Dashboard homepage shows: due this month, overdue, upcoming (30 days)
- Traffic light status: 🟢 On track, 🟡 Due soon, 🔴 Overdue
- One-click access to templates/guidance for each task
- Assign tasks to other board members (delegation)
- Email digest every Monday with week's priorities

### As a Board Member
> "The CBS secretary asked me to provide member confirmation data. I need to know what's required, by when, and how to submit it."

**Acceptance Criteria:**
- Receive task notification (email or dashboard)
- See clear task description and deadline
- Click to upload/complete task
- Mark complete → auto-notifies secretary
- See my completed tasks (accountability)

### As a Treasurer
> "I need to prepare annual accounts for FCA. I need to know the deadline, format requirements, and what supporting documents are needed. Last year we filed late because we didn't know the deadline."

**Acceptance Criteria:**
- See "Annual Accounts" task with clear deadline
- Guidance document linked (FCA format requirements)
- Checklist of supporting docs needed
- Upload draft accounts → review workflow
- Track approval status
- File with FCA directly or download for manual filing

### As an Auditor/FCA Inspector
> "I need to verify BLKOUT has met all CBS compliance obligations for the past year. I need a complete record of filings, dates, and evidence."

**Acceptance Criteria:**
- Export compliance report (all tasks, completion dates, evidence)
- Download any filed document
- Audit trail of who did what when
- Filters by date range, task type, status
- PDF report generation

### As a New Compliance Officer (Volunteer Handover)
> "The previous secretary left and I'm taking over. I need to understand what BLKOUT is required to do, what's already been done, and what's coming up. I have no CBS experience."

**Acceptance Criteria:**
- Onboarding checklist (what is CBS, what are the obligations)
- See full compliance calendar for year
- See history (what's been filed in previous years)
- Templates and guidance for all tasks
- Previous officer's notes/documentation
- Ability to ask questions (forum or chat)

---

## Functional Requirements

### Core Features (Phase 1)

**FR1: Compliance Calendar**

- **View modes**: Month, Quarter, Year
- **Color-coded deadlines**:
  - 🟢 >30 days away (on track)
  - 🟡 14-30 days away (due soon)
  - 🔴 <14 days away OR overdue (urgent)
- **Task types**:
  - FCA filings (annual return, accounts, rule changes)
  - Member confirmations (annual affiliations check)
  - AGM (annual general meeting)
  - Policy reviews (safeguarding, conflict of interest, etc.)
  - Officer notifications (new members, officer changes)
  - Custom tasks (board-defined)

**FR2: Task Management**

Each task includes:
- **Title** (e.g., "Annual Return 2025")
- **Type** (FCA filing, member confirmation, etc.)
- **Deadline** (date + time if applicable)
- **Status** (Not Started, In Progress, Submitted, Filed, Overdue)
- **Assigned to** (compliance officer, treasurer, etc.)
- **Description** (what's required)
- **Guidance** (link to FCA guidance, template, instructions)
- **Attachments** (upload evidence, draft documents)
- **History log** (who did what when)

**FR3: Dashboard Homepage**

At-a-glance view:
- **Overdue tasks** (🔴 red alert banner)
- **Due this week** (🟡 yellow section)
- **Due this month** (list view)
- **Upcoming (next 30 days)** (preview)
- **Completion stats** (% of tasks on time this year)
- **Recent activity** (what's been completed recently)

**FR4: Document Library**

- **All compliance documents** in one place:
  - Founding Rules
  - FCA registration certificate
  - All annual returns (by year)
  - All accounts (by year)
  - AGM minutes (by year)
  - Member lists (historical snapshots)
  - Policy documents (current + versioned)
  - FCA correspondence
- **Searchable** (by year, type, keyword)
- **Version control** (track changes to policies, rules)
- **Download as ZIP** (for audits)

**FR5: Recurring Tasks (Auto-Generation)**

- **Annual tasks auto-create** every year:
  - Annual Return (due 7 months after year-end)
  - Annual Accounts (due 7 months after year-end)
  - AGM (due within 12 months of last AGM)
  - Member Confirmations (every 12 months)
  - Policy Reviews (every 12 months)
- **Date calculation** (auto-adjust based on year-end date, previous filing date)
- **Manual override** (if FCA grants extension, can adjust deadline)

**FR6: Notifications & Alerts**

- **Email alerts** (configurable):
  - 30 days before deadline
  - 14 days before deadline
  - 7 days before deadline
  - Day of deadline
  - Day after deadline (overdue alert)
- **Recipient config** (compliance officer always notified, others as assigned)
- **Digest mode** (daily or weekly summary email)
- **In-app notifications** (when assigned a task)

**FR7: Templates & Guidance Library**

For each task type:
- **Template document** (e.g., annual return template, AGM minutes template)
- **Step-by-step guide** (how to complete this task)
- **FCA links** (relevant FCA guidance pages)
- **BLKOUT-specific notes** (lessons learned, previous year's notes)
- **Downloadable checklists**

### Enhanced Features (Phase 2)

**FR8: FCA Filing Integration (If API Available)**

- **Direct submission** to FCA from dashboard (if FCA offers API)
- **Filing status tracking** (submitted, pending, accepted, rejected)
- **Auto-confirmation** (email confirmation from FCA logged to dashboard)
- **Fallback to manual** (if API not available, guide to manual filing)

**FR9: Approval Workflows**

- **Multi-step approval** for critical tasks:
  - Draft → Review → Board Approval → File
  - Example: Accounts drafted by treasurer → reviewed by secretary → approved by board → filed with FCA
- **Comments/feedback** on drafts
- **Version history** (track changes through approval process)

**FR10: Role-Based Access Control**

- **Admin** (compliance officer) - full access
- **Board Member** - see all tasks, complete assigned tasks
- **Member** (non-board) - see only their assigned tasks (e.g., member confirmations)
- **Read-Only** (auditor) - can view and export, can't edit

**FR11: Integration with Member Verification System**

- **Auto-create "Annual Member Confirmation" task** every year
- **Launch verification** directly from dashboard
- **Import responses** back to dashboard
- **Track completion** (who's confirmed, who hasn't)
- **Link to affiliations database** (auto-update after confirmation)

**FR12: Compliance Reporting**

- **Generate compliance report** for any date range
- **Include**: All tasks, completion dates, filed documents
- **Export formats**: PDF (for FCA), CSV (for analysis), JSON (for integrations)
- **Audit trail**: Who completed what when (timestamps, user IDs)

### Advanced Features (Phase 3)

**FR13: Regulatory Change Monitoring**

- **Monitor FCA website** for CBS rule changes
- **Alert when relevant** (new filing requirement, deadline change, etc.)
- **Summary of change** (what changed, action required)
- **Auto-create tasks** if new obligation introduced

**FR14: Benchmarking & Insights**

- **Compare to other CBS** (anonymized data):
  - Average time to file annual return
  - Common compliance issues
  - Best practices
- **BLKOUT trends**:
  - Are we filing faster/slower over time?
  - Which tasks take longest?
  - Identify bottlenecks

**FR15: Board Pack Auto-Generation**

- **Monthly board report** includes compliance section:
  - What's due this month
  - What was completed last month
  - Any risks/issues
- **Auto-generate** PDF for board meetings
- **One-click export**

---

## Technical Requirements

### Technology Stack

**Recommended: Notion or Airtable (Low-Code)**

**Why Low-Code for This?**
- CBS compliance doesn't change often (stable requirements)
- Visual calendar/dashboard is key (Notion/Airtable excel at this)
- No coding required (any board member can maintain)
- Free tier sufficient for small org
- Easy to customize without developer

**Option 1: Notion (Recommended for BLKOUT)**

**Pros:**
- Free for personal use (or £8/month for team)
- Beautiful, intuitive UI
- Calendar, kanban, table, timeline views
- Document storage built-in
- Shareable pages (for templates/guidance)
- Mobile app (check compliance on the go)
- No coding required

**Cons:**
- Not a "true" database (but sufficient for this use case)
- Limited automation (can integrate with Zapier)

**Setup:**
- Compliance Dashboard database (task list)
- Document Library database (file storage)
- Templates page (guidance documents)
- Calendar view (deadline overview)
- Estimated setup time: 4-6 hours

**Option 2: Airtable (More Powerful, More Complex)**

**Pros:**
- True relational database
- Powerful automation (free tier includes some)
- Better for complex workflows
- Strong reporting/analytics
- API access (for integrations)

**Cons:**
- Steeper learning curve
- Free tier limited (1,000 records - sufficient for BLKOUT but may cap eventually)
- More "database-y" (less intuitive for non-technical users)

**Option 3: Custom Build (If You Want Full Control)**

**Stack:**
- Next.js (frontend + API)
- Supabase (database + storage)
- Vercel (hosting)
- Resend (email alerts)

**Pros:**
- Full control
- Unlimited customization
- No per-user costs

**Cons:**
- Development time: 40-60 hours
- Ongoing maintenance
- Requires technical skills

**Decision for BLKOUT:** Start with **Notion** (Phase 1). Migrate to custom build in Phase 3 if needs outgrow Notion.

### Data Model (If Building Custom)

**Tasks Table:**
```sql
compliance_tasks (
  id: uuid PRIMARY KEY,
  title: text,
  type: text, -- "fca_filing", "member_confirmation", "agm", "policy_review"
  deadline: date,
  status: text, -- "not_started", "in_progress", "completed", "overdue"
  assigned_to: uuid FOREIGN KEY (users),
  description: text,
  guidance_link: text,
  is_recurring: boolean,
  recurrence_rule: text, -- "annual", "quarterly", etc.
  parent_task_id: uuid NULL, -- if this is a recurring instance
  created_at: timestamp,
  completed_at: timestamp NULL,
  completed_by: uuid NULL
)
```

**Documents Table:**
```sql
compliance_documents (
  id: uuid PRIMARY KEY,
  title: text,
  type: text, -- "annual_return", "accounts", "agm_minutes", etc.
  year: integer,
  file_url: text,
  uploaded_at: timestamp,
  uploaded_by: uuid,
  task_id: uuid NULL, -- link to task if relevant
  version: integer, -- for versioning
  is_current: boolean -- latest version flag
)
```

**Notifications Table:**
```sql
notifications (
  id: uuid PRIMARY KEY,
  task_id: uuid FOREIGN KEY,
  user_id: uuid FOREIGN KEY,
  type: text, -- "deadline_30d", "deadline_7d", "overdue", etc.
  sent_at: timestamp,
  read_at: timestamp NULL
)
```

**Audit Log Table:**
```sql
audit_log (
  id: uuid PRIMARY KEY,
  entity_type: text, -- "task", "document", "user"
  entity_id: uuid,
  action: text, -- "created", "updated", "completed", "deleted"
  user_id: uuid,
  changes: jsonb, -- what changed (old value → new value)
  timestamp: timestamp
)
```

### Security & Compliance

**Access Control:**
- Board members only (no public access)
- Compliance officer has admin access
- Other board members have task-level access
- Auditors have read-only access (temporary, time-limited)

**Data Backup:**
- Daily automated backups (if custom build)
- Export all data monthly (manual backup to secure storage)
- Version control for documents (keep all versions)

**Audit Trail:**
- Log all task completions (who, when, what)
- Log all document uploads (who, when, version)
- Immutable log (can't delete/edit audit records)
- Export audit trail on demand (for FCA audit)

**Retention:**
- Keep all compliance records for 7 years minimum (CBS requirement)
- Archive old years (move to separate "Archive" section after 2 years)
- Don't delete, just move out of active view

---

## Implementation Phases

### Phase 1: Notion Dashboard (Week 1) - QUICK WIN

**Deliverables:**
- [ ] Set up Notion workspace
- [ ] Create compliance calendar with all known deadlines for Year 1
- [ ] Create task database (with templates for each task type)
- [ ] Upload all current documents to document library
- [ ] Create guidance pages (templates, checklists)
- [ ] Set up recurring tasks (annual return, accounts, AGM, etc.)
- [ ] Invite board members, assign permissions

**Effort**: 4-6 hours
**Priority**: HIGH (registration imminent, compliance obligations start immediately)

**Success Criteria:**
- All Year 1 deadlines visible in calendar
- Compliance officer can manage tasks
- All board members can access dashboard
- First task successfully completed using dashboard

### Phase 2: Automation & Alerts (Month 2)

**Deliverables:**
- [ ] Set up Zapier/Make.com integration (Notion → Email alerts)
- [ ] Automated reminders (30d, 14d, 7d, overdue)
- [ ] Weekly digest email (summary of week's tasks)
- [ ] Integration with Member Verification System (auto-create annual confirmation task)
- [ ] Approval workflows (draft → review → approve → file)

**Effort**: 8-12 hours (mostly Zapier config)
**Priority**: MEDIUM (improves efficiency, reduces manual work)

### Phase 3: Custom Build (Month 6+) - IF NEEDED

Only pursue if Notion becomes limiting (unlikely for first 2 years).

**Deliverables:**
- [ ] Migrate data from Notion to custom database
- [ ] Build custom dashboard (Next.js)
- [ ] Advanced features (FCA integration, regulatory monitoring, etc.)
- [ ] API for integrations with other BLKOUT systems

**Effort**: 40-60 hours
**Priority**: LOW (only if Notion insufficient)

---

## Dependencies

### External Dependencies

- **Notion account** (free or team plan £8/month)
- **Zapier** (for automation, free tier may suffice)
- **Email system** (for alerts, can use existing Gmail/Outlook)

### Internal Dependencies

- **FCA registration confirmation** (to get exact first annual return deadline)
- **Compliance officer assigned** (someone owns this dashboard)
- **Board buy-in** (all board members will use dashboard)
- **Document collection** (gather all existing compliance docs)

### Knowledge Requirements

- **CBS regulations** (what's required, when)
- **FCA guidance** (filing formats, deadlines)
- **Notion skills** (basic database/page creation) - 1-2 hours learning

---

## Risks & Mitigation

### Risk 1: No One Checks Dashboard (System Ignored)

**Likelihood**: Medium (volunteers are busy)
**Impact**: High (defeats purpose, miss deadlines anyway)

**Mitigation:**
- **Weekly digest email** (automatic reminder every Monday)
- **Overdue alerts** (red alert emails impossible to ignore)
- **Board meeting agenda item** (compliance report monthly)
- **Make it dead simple** (5-second check: dashboard says "All clear 🟢" or "Action needed 🔴")
- **Gamification** (optional): Track "on-time filing streak", celebrate milestones

### Risk 2: Deadlines Entered Incorrectly

**Likelihood**: Medium (manual entry, complex rules)
**Impact**: High (miss deadline because dashboard says it's later than it is)

**Mitigation:**
- **Double-check with FCA guidance** (verify deadline calculation)
- **Add buffer** (set internal deadline 7 days before actual FCA deadline)
- **Annual review** (compliance officer reviews all deadlines in January)
- **Confirmation emails** (FCA sends confirmation when filing received, log this to dashboard)

### Risk 3: Documents Lost (Not Uploaded to Dashboard)

**Likelihood**: Medium (board members forget to upload)
**Impact**: Medium (can't find doc later, but probably still have email copy)

**Mitigation:**
- **Policy**: All compliance docs MUST be uploaded to dashboard (no exceptions)
- **Reminders**: Task completion requires document upload (enforce)
- **Email rule**: Forward all FCA emails to dashboard (via Notion email integration)
- **Quarterly audit**: Review document library, identify gaps

### Risk 4: Volunteer Turnover (Compliance Officer Leaves)

**Likelihood**: High (volunteers come and go)
**Impact**: High (new person doesn't know how to use system)

**Mitigation:**
- **Documentation**: Create "How to Use This Dashboard" guide in Notion
- **Onboarding checklist**: New compliance officer follows step-by-step
- **Simplicity**: Keep system simple enough that anyone can pick it up
- **Handover**: Outgoing officer spends 30 min training incoming officer
- **Two-person access**: Secretary + one other board member always have admin access (redundancy)

---

## Alternatives Considered

### Alternative 1: Spreadsheet (Google Sheets / Excel)

**Pros:**
- Free
- Everyone knows how to use
- Flexible

**Cons:**
- No calendar view
- No document storage
- No notifications/alerts
- Manual updates (no automation)
- Doesn't scale (gets messy with 50+ tasks)

**Decision**: Reject - Notion is barely more complex but 10x more powerful

### Alternative 2: Project Management Tool (Asana, Trello, Monday.com)

**Pros:**
- Built for task management
- Good UI/UX
- Notifications built-in
- Collaboration features

**Cons:**
- **Cost**: £8-15/user/month (adds up)
- Overkill for compliance (designed for product/project work)
- No document storage (would need separate system)
- Learning curve

**Decision**: Reject - Notion does everything we need for free (or £8/month for whole team)

### Alternative 3: Compliance Software (CharityLog, Cobalt, etc.)

**Pros:**
- Built specifically for charity/CBS compliance
- All features out of box
- Professional support

**Cons:**
- **Cost**: £500-2000/year
- Overkill for 9-member CBS
- May not cover all BLKOUT-specific needs

**Decision**: Reject - revisit when BLKOUT has 50+ members and complex compliance needs

---

## Success Criteria & Definition of Done

### Phase 1 (Notion Dashboard) is "Done" when:

- [ ] All Year 1 compliance deadlines entered in calendar
- [ ] All task types have templates and guidance
- [ ] All current documents uploaded to library
- [ ] All board members have access
- [ ] Compliance officer has tested and can use confidently
- [ ] Successfully used to complete first task (e.g., member confirmation)
- [ ] Weekly digest email set up

### Overall Project is "Successful" when:

- [ ] Zero late FCA filings in Year 1
- [ ] 100% of compliance tasks completed on time
- [ ] Compliance officer checks dashboard at least weekly
- [ ] All board members report confidence in compliance status
- [ ] Passed first FCA audit with zero findings
- [ ] Smooth handover to new compliance officer (if turnover happens)

---

## Next Steps (Immediate Actions)

1. **Assign compliance officer** (if not already clear)
2. **Gather all compliance documents** (FCA registration, rules, etc.)
3. **Identify Year 1 deadlines** (when is first annual return due? AGM? Etc.)
4. **Set up Notion** (1-2 hours)
5. **Populate calendar** (2-3 hours)
6. **Train board** (30 min demo in board meeting)
7. **Go live** (start using for next compliance task)

---

## Appendix: Year 1 Compliance Calendar (Example)

Assuming FCA registration completes **November 2025**, financial year-end **31 March**:

| Task | Deadline | Type |
|------|----------|------|
| Member Affiliations Verified | Nov 2025 | Member Confirmation (DONE) |
| First AGM | Nov 2026 | AGM (within 12 months of registration) |
| Annual Return (Year 1) | Oct 2026 | FCA Filing (7 months after 31 March year-end) |
| Annual Accounts (Year 1) | Oct 2026 | FCA Filing (7 months after 31 March year-end) |
| Member Confirmation (Annual) | Nov 2026 | Member Confirmation (annual check) |
| Policy Reviews (Annual) | Nov 2026 | Internal (safeguarding, COI, etc.) |

**Add to calendar as recurring tasks, plus ad-hoc tasks:**
- New member joins → Notify FCA within 14 days
- Officer change → Notify FCA within 14 days
- Address change → Notify FCA within 14 days
- Rule change → Get FCA approval before implementing

---

**Document Control:**
- **Version**: 1.0
- **Last Updated**: 14 November 2025
- **Next Review**: After FCA registration confirmation (to populate Year 1 deadlines)
- **Owner**: BLKOUT Infrastructure Team
- **Priority**: HIGH - Registration imminent, obligations start immediately
