# PRD 01: Member Relationship Management

**Status:** Planning
**Priority:** Medium
**Estimated effort:** 8-12 hours (Phase 1)
**Owner:** TBD
**Last updated:** 2025-11-14

---

## Problem Statement

BLKOUT UK Co-operative needs to demonstrate compliance with CBS membership rules and maintain good governance practices. This requires:

- Clear record of who is a member and when they joined
- Documented membership application and approval process
- Evidence of one-member-one-vote principle in decisions
- Tracking of conflicts of interest declarations
- Meeting attendance records
- Ability to generate compliance reports for FCA annual returns and internal governance

**Current state:** Ad-hoc tracking across emails, WhatsApp, and personal notes. No systematic record of membership decisions or governance actions.

**Desired state:** Simple, auditable system that demonstrates proper governance and makes annual FCA reporting straightforward.

---

## Goals & Success Metrics

### Primary Goals
1. **Governance compliance**: Demonstrate adherence to CBS membership rules
2. **FCA readiness**: Generate required information for AR30 annual returns in <15 minutes
3. **Transparency**: Any member can see membership roster and governance records
4. **Minimal overhead**: <30 minutes/month to maintain

### Success Metrics
- ✅ Annual Return preparation time: 2+ hours → 15 minutes
- ✅ Membership application processing: Clear audit trail from application → approval → onboarding
- ✅ Conflict declarations: 100% of members with declared interests on file
- ✅ AGM quorum verification: Attendance records available within 2 minutes

### Non-Goals
- **Not** a full CRM system (no email campaigns, complex automation)
- **Not** a voting platform (tracking votes, not conducting them)
- **Not** an onboarding automation system (simple records only)

---

## User Personas

### Primary: Board Secretary/Administrator
- **Needs:** Quick access to membership records, compliance reporting, meeting records
- **Pain points:** Scattered information, annual return panic, unclear who voted on what
- **Technical comfort:** Basic (comfortable with spreadsheets/Airtable)

### Secondary: Board Members
- **Needs:** View current membership, declare conflicts of interest, verify quorum
- **Pain points:** Lack of transparency, unclear who's actually a member
- **Technical comfort:** Basic (read-only access sufficient)

### Tertiary: FCA Auditor (hypothetical)
- **Needs:** Evidence of proper governance, voting records, conflict management
- **Pain points:** Organizations with no audit trail
- **Technical comfort:** Any format accepted (PDF reports fine)

---

## Core Features

### 1. Member Roster
**Priority: P0 (Must-have)**

Track all current and historical members with:
- Full name, email, phone
- Membership type (Founding, Regular, Associate - based on CBS rules)
- Join date, leave date (if applicable)
- Status (Active, Inactive, Left)
- Share ownership (if applicable per CBS structure)

**Data model:**
```
members
├── id
├── name (text)
├── email (email)
├── phone (phone)
├── membership_type (select: Founding, Regular, Associate)
├── join_date (date)
├── leave_date (date, nullable)
├── status (select: Active, Inactive, Left)
├── shares_owned (number, if applicable)
├── notes (long text)
└── linked: applications (many-to-one), votes (one-to-many), conflicts (one-to-many)
```

**UI/UX:**
- Simple table view (Airtable/Sheets)
- Filters: Active members only, by membership type, by join date
- Public "Current Members" view (names only, read-only)

**Acceptance criteria:**
- [ ] All 9 founding members entered with correct join dates
- [ ] Can filter to "Active members" in <5 seconds
- [ ] Can export member list as CSV for FCA reporting

---

### 2. Membership Applications
**Priority: P0 (Must-have)**

Track the application → approval → onboarding process:
- Application received date
- Applicant information
- Proposer & seconder (if required by rules)
- Board vote date and outcome
- Approval/rejection notes
- Onboarding completion date

**Data model:**
```
applications
├── id
├── applicant_name (text)
├── applicant_email (email)
├── application_date (date)
├── proposer (linked to members)
├── seconder (linked to members, nullable)
├── vote_date (date, nullable)
├── vote_outcome (select: Approved, Rejected, Deferred, Withdrawn)
├── votes_for (number)
├── votes_against (number)
├── votes_abstain (number)
├── notes (long text)
├── onboarding_completed (checkbox)
└── linked: member_created (many-to-one to members)
```

**Process workflow:**
1. Application received → Record created (status: Pending)
2. Board votes → Update vote_outcome, votes_for/against/abstain
3. If approved → Create member record, link to application
4. Onboarding completed → Check box

**Acceptance criteria:**
- [ ] Clear audit trail from application to membership
- [ ] Can answer "How was X approved as a member?" in <2 minutes
- [ ] Can generate report: "All membership decisions in 2024"

---

### 3. Voting Records
**Priority: P1 (Should-have)**

Track votes on significant decisions (not conducting votes, just recording outcomes):
- Decision being voted on
- Vote date, meeting context (AGM, Board meeting, etc.)
- Who voted, how they voted (For/Against/Abstain)
- Outcome
- One-member-one-vote verification

**Data model:**
```
decisions
├── id
├── title (text, e.g., "Approve 2024 budget")
├── description (long text)
├── vote_date (date)
├── meeting_type (select: AGM, Board Meeting, Special Resolution)
├── outcome (select: Passed, Failed, Deferred)
├── votes_required (number, e.g., simple majority, 2/3, etc.)
└── linked: individual_votes (one-to-many)

individual_votes
├── id
├── decision (linked to decisions)
├── member (linked to members)
├── vote (select: For, Against, Abstain, Absent)
└── timestamp (datetime)
```

**Reports:**
- Voting history by member (verify one-member-one-vote)
- Decision history (when was X approved?)
- Voting patterns (are we getting quorum?)

**Acceptance criteria:**
- [ ] Can verify one-member-one-vote compliance for any decision
- [ ] Can answer "When did we approve X?" in <1 minute
- [ ] Can generate annual governance report showing all votes

---

### 4. Conflict of Interest Tracking
**Priority: P1 (Should-have)**

Maintain register of declared conflicts:
- Member name
- Organization/interest declared
- Nature of conflict (Director, Shareholder, Employee, Family member, etc.)
- Declared date
- Status (Current, Historical, Resolved)
- Decisions where member recused

**Data model:**
```
conflicts
├── id
├── member (linked to members)
├── organization (text, e.g., "Northants Rainbow Collective CIC")
├── nature (select: Director, Shareholder, Employee, Family, Other)
├── description (long text)
├── declared_date (date)
├── status (select: Current, Historical, Resolved)
├── companies_house_number (text, nullable)
└── linked: recusals (one-to-many)

recusals
├── id
├── conflict (linked to conflicts)
├── decision (linked to decisions)
└── recusal_notes (long text)
```

**Integration with voting:**
- When recording a vote, system shows if member has declared conflict
- Prompt to record recusal if applicable

**Acceptance criteria:**
- [ ] All founding member affiliations imported from CBS registration work
- [ ] Can generate "Current Conflicts Register" in <30 seconds
- [ ] Can verify member recused from relevant decisions

---

### 5. Meeting Attendance
**Priority: P2 (Nice-to-have)**

Track AGM and board meeting attendance:
- Meeting date, type, purpose
- Who attended (in person, remote, proxy)
- Quorum verification
- Minutes/notes link

**Data model:**
```
meetings
├── id
├── date (date)
├── type (select: AGM, Board Meeting, Special Meeting)
├── purpose (text)
├── quorum_required (number)
├── quorum_met (checkbox, formula)
├── minutes_link (URL)
└── linked: attendance (one-to-many)

attendance
├── id
├── meeting (linked to meetings)
├── member (linked to members)
└── attendance_type (select: In Person, Remote, Proxy, Absent)
```

**Reports:**
- Meeting attendance by member (who's engaged?)
- Quorum verification (did we have valid meetings?)
- Attendance trends (are meetings well-attended?)

**Acceptance criteria:**
- [ ] Can verify AGM quorum in <30 seconds
- [ ] Can generate attendance report for annual governance review
- [ ] Can see "Last attended meeting" for each member

---

### 6. Compliance Reporting
**Priority: P1 (Should-have)**

Generate reports for FCA annual return and internal governance:

**FCA AR30 Support:**
- Current member count by type
- Changes in membership during year (joined, left)
- Share ownership summary (if applicable)

**Internal Governance:**
- Membership decisions (applications approved/rejected)
- Voting records (all decisions made)
- Conflicts register (current and historical)
- Meeting attendance (AGM quorum verification)

**Reports (exportable as PDF/CSV):**
1. "Annual Membership Report" (for AR30)
2. "Governance Summary" (decisions, conflicts, attendance)
3. "Current Members List" (public-facing)
4. "Conflicts Register" (board review)

**Acceptance criteria:**
- [ ] Can generate AR30 membership data in <15 minutes
- [ ] Can produce annual governance report with <30 minutes of review
- [ ] Reports are clear enough for non-technical board members

---

## Technical Approach

### Platform: Airtable (Phase 1)

**Why Airtable:**
- Relational database (links between tables)
- Simple interface (non-technical users comfortable)
- Built-in views and filters
- PDF/CSV export
- Free tier: 1,200 records (sufficient for years)
- Upgrade: £8-10/user/month if needed

**Alternative: Google Sheets**
- Even simpler
- Free forever
- Less relational (harder to link applications → members → votes)
- Recommendation: Start with Airtable, fall back to Sheets if too complex

### Database Structure

**5 core tables:**
1. `members` - Member roster
2. `applications` - Membership applications
3. `decisions` - Votes and resolutions
4. `individual_votes` - Vote tracking (one row per member per decision)
5. `conflicts` - Conflict of interest register

**3 optional tables (Phase 2):**
6. `meetings` - Meeting records
7. `attendance` - Meeting attendance
8. `recusals` - Conflict-based recusals from decisions

### Access Control

**Roles:**
- **Admin** (Secretary): Full read/write
- **Board Member**: Read all, write to conflicts (self-declaration)
- **Public**: Read-only view of current members list (names only)

**Implementation:**
- Airtable: Share links with different permissions
- Public view: Embed on blkout.uk.coop website

### Data Migration

**Import from CBS registration work:**
- 9 founding members → `members` table
- 17 affiliations → `conflicts` table (status: Current/Historical as appropriate)
- Initial application date: CBS registration date for all founding members

---

## Implementation Plan

### Phase 1: Core Record-Keeping (8-12 hours)

**Week 1: Setup (4 hours)**
- Create Airtable base with 5 core tables
- Define fields and relationships
- Set up basic views (Active Members, Pending Applications, Current Conflicts)
- Import founding members and affiliations

**Week 2: Refinement (4 hours)**
- Create compliance report views
- Test with real data (record a recent board decision)
- Get feedback from board secretary
- Adjust fields/views as needed

**Week 3: Documentation (2-3 hours)**
- Write 1-page user guide ("How to record a new member")
- Document report generation process ("Preparing AR30 membership data")
- Share with board for review

**Phase 1 deliverables:**
- [ ] Airtable base with 5 tables
- [ ] 9 founding members entered
- [ ] 17 conflicts imported
- [ ] Basic compliance reports working
- [ ] User guide (1 page)

### Phase 2: Enhanced Features (Optional, 6-8 hours)

**If needed based on usage:**
- Meeting attendance tracking (tables 6-7)
- Automated reminders (annual conflict declaration)
- Public member directory on website (Airtable embed)
- Advanced reports (voting patterns, engagement metrics)

**Trigger for Phase 2:**
- Annual Return takes >30 minutes despite Phase 1 tools
- Board requests more detailed governance tracking
- Membership grows beyond founding 9 (new applications coming in)

---

## User Experience

### Common Workflows

**1. New member application**
1. Admin creates record in `applications` table
2. Fills in: name, email, application date, proposer
3. After board vote: Updates vote_date, outcome, votes_for/against
4. If approved: Creates linked record in `members` table
5. After onboarding: Checks `onboarding_completed` box

**Time: 3-5 minutes**

**2. Recording a board decision**
1. Admin creates record in `decisions` table
2. Fills in: title, description, vote_date, meeting_type
3. Creates linked records in `individual_votes` for each member
4. System calculates outcome based on votes
5. If any conflicts declared: Link to `recusals`

**Time: 5-8 minutes**

**3. Declaring a conflict of interest**
1. Board member opens `conflicts` table (or fills form)
2. Creates new record: organization, nature, description
3. Admin reviews and confirms
4. Conflict appears in member's profile and current register

**Time: 2-3 minutes**

**4. Preparing FCA annual return**
1. Admin opens "Annual Membership Report" view
2. Filters: Changes in last financial year
3. Reviews: Members joined, members left, current count
4. Exports CSV or copies to AR30 form
5. Cross-reference with accounts (share ownership if applicable)

**Time: 10-15 minutes (vs. 2+ hours manually)**

---

## Success Criteria

### Must-Have (Launch Requirements)
- [ ] All 9 founding members entered with accurate data
- [ ] 17 conflicts of interest imported from CBS registration work
- [ ] Can answer "Who are our current members?" in <10 seconds
- [ ] Can generate member list for AR30 in <15 minutes
- [ ] Board secretary trained and comfortable using system

### Should-Have (3 months post-launch)
- [ ] At least 1 membership decision recorded (if any applications)
- [ ] At least 1 board vote recorded (demonstrate voting tracking)
- [ ] Conflicts register reviewed and confirmed by all members
- [ ] System requires <30 minutes/month to maintain

### Could-Have (6 months post-launch)
- [ ] Meeting attendance tracking in use
- [ ] Public member directory embedded on website
- [ ] Automated annual conflict declaration reminders
- [ ] Advanced reports (voting patterns, engagement)

---

## Risks & Mitigations

### Risk 1: Over-engineering (again)
**Likelihood: Medium**
**Impact: Medium (wasted effort)**

**Mitigation:**
- Start with absolute minimum: Just `members` and `conflicts` tables
- Only add features when proven necessary
- Review after 3 months: What's actually being used?

### Risk 2: Low adoption (board doesn't use it)
**Likelihood: Medium**
**Impact: High (system becomes stale)**

**Mitigation:**
- Make it stupid simple (< 5 minute training)
- Integrate with existing workflow (annual return prep)
- Secretary owns it (one person responsible)

### Risk 3: Data privacy concerns
**Likelihood: Low**
**Impact: Medium (member concerns)**

**Mitigation:**
- GDPR compliance: Only collect necessary data
- Secure access: Role-based permissions
- Transparency: Members can see what's stored
- Public view: Names only (no contact details)

### Risk 4: Platform lock-in (Airtable)
**Likelihood: Low**
**Impact: Low (easy to migrate)**

**Mitigation:**
- Export CSV backups monthly
- Simple data model (can move to Sheets/Notion/custom)
- Phase 1 focus: Prove value before investing heavily

---

## Cost Analysis

### Phase 1 (Airtable Free Tier)
- **Platform:** £0/month (up to 1,200 records)
- **Time investment:** 8-12 hours setup + 30 min/month maintenance
- **Annual cost:** £0 + ~6 hours/year maintenance

### Phase 2 (If needed)
- **Airtable Pro:** £8-10/user/month (if >1,200 records or need advanced features)
- **Annual cost:** £96-120/year (likely unnecessary for years)

### ROI Calculation
**Time saved:**
- Annual Return prep: 2 hours → 15 minutes = **1.75 hours saved/year**
- Membership tracking: 3 hours/year → 30 min/year = **2.5 hours saved/year**
- Governance reporting: 2 hours/year → 30 min/year = **1.5 hours saved/year**

**Total savings: 5.75 hours/year**

**Break-even:** 8-12 hour setup / 5.75 hours saved = **Pays back in ~2 years**

**Additional value (non-time):**
- Governance credibility with FCA
- Transparency for members
- Audit trail if ever questioned
- Easier onboarding of new board members

---

## Dependencies

### Required
- Access to CBS membership rules (to confirm membership types, voting requirements)
- Founding member data (already have from CBS registration)
- Decision on share ownership structure (impacts `members` table fields)

### Optional
- Website integration (for public member directory)
- Email automation platform (for conflict declaration reminders in Phase 2)

---

## Open Questions

1. **Membership types:** What are the actual categories per CBS rules? (Founding, Regular, Associate, Honorary, etc.)
2. **Share ownership:** Does BLKOUT CBS structure include shares? If so, how are they allocated?
3. **Voting thresholds:** What decisions require simple majority vs. 2/3 vs. unanimous? (Import from rules)
4. **Conflict policy:** What's the actual recusal process per CBS rules?
5. **Meeting cadence:** How often are AGMs and board meetings? (Affects usefulness of meeting tracking)

**Next step:** Review CBS rules to answer above questions before building.

---

## Appendix: Example Data

### Members Table (Sample)
| Name | Email | Type | Join Date | Status | Shares | Conflicts |
|------|-------|------|-----------|--------|--------|-----------|
| Robert Berkeley | rob@example.com | Founding | 2024-10-15 | Active | 1 | 11 |
| Olamide Adesanya | olamide@example.com | Founding | 2024-10-15 | Active | 1 | 3 |
| Lloyd Young | lloyd@example.com | Founding | 2024-10-15 | Active | 1 | 0 |

### Conflicts Table (Sample)
| Member | Organization | Nature | Status | Declared |
|--------|--------------|--------|--------|----------|
| Robert Berkeley | THE BLACK BOY JOY CLUB CIC | Director | Current | 2024-11-10 |
| Olamide Adesanya | NORTHANTS RAINBOW COLLECTIVE CIC | Director | Current | 2024-11-10 |
| Cardew Jackson-Cole | NORTHANTS RAINBOW COLLECTIVE CIC | Director | Current | 2024-11-10 |

### Applications Table (Sample)
| Applicant | Applied | Proposer | Vote Date | Outcome | Member Created |
|-----------|---------|----------|-----------|---------|----------------|
| Founding Members (batch) | 2024-10-15 | N/A (founding) | 2024-10-15 | Approved | 9 members |
| Jane Smith | 2025-02-01 | Robert Berkeley | 2025-02-15 | Approved | Jane Smith |

### Decisions Table (Sample)
| Decision | Vote Date | Meeting | Outcome | For | Against | Abstain |
|----------|-----------|---------|---------|-----|---------|---------|
| Approve CBS rules v1.0 | 2024-11-01 | Board | Passed | 9 | 0 | 0 |
| Approve 2024 budget | 2024-11-15 | Board | Passed | 8 | 0 | 1 |

---

## Version History

- **v1.0** (2024-11-14): Initial PRD
