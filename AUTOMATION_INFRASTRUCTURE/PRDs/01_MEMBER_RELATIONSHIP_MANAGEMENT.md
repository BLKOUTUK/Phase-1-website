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
├── membership_type (select: Founder Member, Member)
├── member_category (select: Natural Person, Corporate Body, Nominee of Unincorporated Body)
├── join_date (date)
├── leave_date (date, nullable)
├── status (select: Active, Inactive, Left)
├── shares_owned (number) — minimum 1 non-withdrawable share
├── share_value (formula: shares_owned × £10)
├── is_director (checkbox)
├── director_appointment_date (date, nullable)
├── director_type (select: Elected, Independent Non-Executive, nullable)
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
├── meeting_type (select: AGM, Board Meeting, Special General Meeting)
├── resolution_type (select: Ordinary, Extraordinary (75%), Special)
├── outcome (select: Passed, Failed, Deferred)
├── votes_for (number)
├── votes_against (number)
├── votes_abstain (number)
├── total_eligible_voters (number)
├── percentage_for (formula: votes_for / (votes_for + votes_against) × 100)
└── linked: individual_votes (one-to-many), recusals (one-to-many)

individual_votes
├── id
├── decision (linked to decisions)
├── member (linked to members)
├── vote (select: For, Against, Abstain, Absent, Recused)
├── timestamp (datetime)
└── notes (text, nullable)
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

Maintain register of declared conflicts (per CBS Rule 95):

**What must be declared:**
- Any personal, material, or financial interest (direct or indirect)
- Interests of **Connected Persons**: family/household members OR business associates
- **NOT required**: <1% shareholding in a company (Rule 3 definition)

**Recusal requirements (Rule 96):**
- Conflicted director absent from discussion
- Does not vote
- Not counted for quorum

**Data model:**
```
conflicts
├── id
├── member (linked to members)
├── organization (text, e.g., "Northants Rainbow Collective CIC")
├── nature (select: Director, Shareholder (>1%), Employee, Family/Household, Business Associate, Other)
├── description (long text)
├── is_connected_person (checkbox) — marks if conflict is via Connected Person rather than direct
├── connected_person_name (text, nullable)
├── declared_date (date)
├── status (select: Current, Historical, Resolved)
├── companies_house_number (text, nullable)
└── linked: recusals (one-to-many)

recusals
├── id
├── conflict (linked to conflicts)
├── decision (linked to decisions)
├── recusal_confirmed (checkbox) — director confirmed absence from discussion
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

Track AGM and board meeting attendance (per CBS Rules 36, 44, 92):

**Meeting requirements:**
- **AGM**: Required within 6 months of end of financial year (Rule 36)
- **Quorum (general meetings)**: 3 Members OR 10% of membership, whichever is greater (Rule 44)
- **Quorum (board meetings)**: 50% of Directors OR 3 Directors, whichever is greater (Rule 92)
- **Notice period**: 14 Clear Days for general meetings (Rule 39), reasonable notice for board meetings (Rule 86)

**Data model:**
```
meetings
├── id
├── date (date)
├── type (select: AGM, Board Meeting, Special General Meeting)
├── purpose (text)
├── notice_sent_date (date)
├── quorum_required (number, formula based on type)
├── quorum_present (number, calculated from attendance)
├── quorum_met (checkbox, formula: quorum_present >= quorum_required)
├── minutes_link (URL)
├── chair (linked to members)
└── linked: attendance (one-to-many), decisions (one-to-many)

attendance
├── id
├── meeting (linked to meetings)
├── member (linked to members)
├── attendance_type (select: In Person, Remote, Proxy, Absent)
└── proxy_for (linked to members, nullable) — if attending as proxy for another member
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

## CBS Rules Summary (Answers to Open Questions)

Based on BLKOUT Media Limited's adopted CBS rules:

### 1. Membership Types
- **Founder Members**: The 9 subscribers to the rules for registration purposes
- **Members**: Natural persons age 16+, corporate bodies, or nominees of unincorporated bodies
- **No membership tiers**: All members have equal voting rights (one-member-one-vote, Rule 56)

**For database:** `membership_type` field: "Founder Member" or "Member"

### 2. Share Ownership Structure
- **Each share**: £10 nominal value (Rule 22)
- **Minimum shareholding**: 1 non-Withdrawable share (the membership share) + any additional shares per Board determination (Rule 23)
- **Maximum shareholding**: No limit (Rule 24)
- **Payment**: Shares paid in full on allotment (Rule 23)
- **Withdrawal**: Members can withdraw shares (except the 1 non-withdrawable membership share) with 3 months' notice (Rule 28)

**For database:** Track `shares_owned` (number field), note that at least 1 is always non-withdrawable

### 3. Voting Thresholds
- **Ordinary resolution**: Simple majority of votes cast (Rule 63)
  - Used for: Most decisions
- **Extraordinary Resolution**: 75%+ of votes cast (Rules 62-63)
  - Required for: Member expulsion (Rule 15), rule amendments (Rule 62a-ii), winding up (Rule 62a-iii)
- **Special resolution**: Per Co-operative and Community Benefit Societies Act 2014 sections 43-44, 109-114, 119-120 (Rule 64)
  - Required for: Amalgamation, transfer of engagements, conversion to company

**For database:** `decisions` table should include `votes_required` field: "Simple majority", "75% (Extraordinary)", "Special resolution"

### 4. Conflict of Interest Policy
**Declaration requirement (Rule 95):**
- Directors must declare any personal, material, or financial interest (direct or indirect)
- Includes interests of **Connected Persons**: family/household members OR business associates (NOT <1% shareholders in companies)
- **Exception**: Can vote on share interest payments (affects all members equally)

**Recusal process (Rule 96):**
- Conflicted director must be **absent from discussion**
- Conflicted director **does not vote**
- Conflicted director **not counted for quorum**
- Unconflicted directors must authorize that this is in Society's best interests

**For database:**
- `conflicts` table tracks all declared interests
- `recusals` table links conflicts to specific decisions
- Nature of conflict: Director, Shareholder, Employee, Family member, Business associate, Other

### 5. Meeting Cadence
- **Annual General Meeting**: Required within 6 months of end of financial year (Rule 36)
- **Board meetings**: No mandated frequency - "as they think fit" (Rule 87)
  - Any director can call a meeting (Rule 86)
- **General meetings**: Can be called by Board, or by requisition of 1/10th of members (min 3) (Rule 38)

**For database:** `meetings` table types: "AGM", "Board Meeting", "Special General Meeting"

### 6. Board Composition (Rules 66-73)
- **Minimum**: 3 Directors (must be Members age 16+)
- **Maximum**: Determined by general meeting
- **Election**: By and from Members
- **Retirement cycle**: One-third retire at each AGM (longest serving first, Rule 70)
- **Independent non-executive directors**: Up to 2 (need not be Members, max 49% of board total, Rule 71)
- **Casual vacancies**: Can be filled by co-option until next AGM (Rule 73)

**For database:** Track director election/appointment date, retirement cycle, whether independent non-executive

### 7. Quorum Requirements
- **General meetings**: 3 Members OR 10% of membership, whichever is greater (Rule 44)
- **Board meetings**: 50% of Directors OR 3 Directors, whichever is greater (Rule 92)

**For database:** `meetings` table should auto-calculate quorum_required based on total membership/directors

---

## Appendix: Example Data

### Members Table (Sample)
| Name | Email | Type | Category | Join Date | Status | Shares | Value | Is Director | Conflicts |
|------|-------|------|----------|-----------|--------|--------|-------|-------------|-----------|
| Robert Berkeley | rob@example.com | Founder Member | Natural Person | 2024-10-15 | Active | 1 | £10 | Yes | 11 |
| Olamide Adesanya | olamide@example.com | Founder Member | Natural Person | 2024-10-15 | Active | 1 | £10 | Yes | 3 |
| Lloyd Young | lloyd@example.com | Founder Member | Natural Person | 2024-10-15 | Active | 1 | £10 | Yes | 0 |

**Note:** Each member holds minimum 1 non-withdrawable share at £10 nominal value (CBS Rule 22-23)

### Conflicts Table (Sample)
| Member | Organization | Nature | Connected Person? | Status | Declared | Companies House # |
|--------|--------------|--------|-------------------|--------|----------|-------------------|
| Robert Berkeley | THE BLACK BOY JOY CLUB CIC | Director | No | Current | 2024-11-10 | 13547890 |
| Olamide Adesanya | NORTHANTS RAINBOW COLLECTIVE CIC | Director | No | Current | 2024-11-10 | 14845673 |
| Cardew Jackson-Cole | NORTHANTS RAINBOW COLLECTIVE CIC | Director | No | Current | 2024-11-10 | 14845673 |

**Note:** Both Olamide and Cardew are co-directors of same CIC = potential conflict requiring recusal (CBS Rule 95)

### Applications Table (Sample)
| Applicant | Applied | Proposer | Seconder | Vote Date | Resolution Type | Outcome | Votes For/Against | Member Created |
|-----------|---------|----------|----------|-----------|----------------|---------|-------------------|----------------|
| Founding Members (batch) | 2024-10-15 | N/A (founding) | N/A | 2024-10-15 | Ordinary | Approved | 9/0 | 9 members |
| Jane Smith | 2025-02-01 | Robert Berkeley | Lloyd Young | 2025-02-15 | Ordinary | Approved | 8/0 | Jane Smith |

### Decisions Table (Sample)
| Decision | Vote Date | Meeting | Resolution Type | Threshold | Outcome | For | Against | Abstain | % For |
|----------|-----------|---------|-----------------|-----------|---------|-----|---------|---------|-------|
| Approve CBS rules v1.0 | 2024-11-01 | AGM | Ordinary | 50%+ | Passed | 9 | 0 | 0 | 100% |
| Approve 2025 budget | 2024-11-15 | Board | Ordinary | 50%+ | Passed | 8 | 0 | 1 | 100% |
| Amend Rule 23 (shareholding) | 2025-03-01 | Special General Meeting | Extraordinary | 75%+ | Passed | 8 | 1 | 0 | 89% |

**Note:** Extraordinary Resolutions require 75%+ (CBS Rule 63), used for rule amendments, member expulsion, winding up

### Meetings Table (Sample)
| Date | Type | Purpose | Notice Sent | Quorum Required | Quorum Present | Quorum Met? |
|------|------|---------|-------------|-----------------|----------------|-------------|
| 2024-11-01 | AGM | First AGM, adopt rules | 2024-10-15 | 3 (greater of 3 or 10% of 9) | 9 | ✅ Yes |
| 2024-11-15 | Board Meeting | Approve 2025 budget | 2024-11-10 | 3 (greater of 50% or 3) | 6 | ✅ Yes |
| 2025-03-01 | Special General Meeting | Amend shareholding rule | 2025-02-15 | 3 | 9 | ✅ Yes |

**Note:** General meeting quorum = 3 OR 10% of members (whichever greater), Board quorum = 50% of directors OR 3 (whichever greater) per CBS Rules 44, 92

---

## Version History

- **v1.0** (2024-11-14): Initial PRD
- **v1.1** (2024-11-15): Updated with actual CBS rules requirements:
  - Added CBS Rules Summary section with specific voting thresholds, quorum requirements, conflict definitions
  - Updated data models to reflect share structure (£10 per share, min 1 non-withdrawable)
  - Added resolution types (Ordinary, Extraordinary 75%, Special)
  - Updated conflict tracking to reflect Connected Person definition (family/household/business associates, NOT <1% shareholders)
  - Added board composition tracking (director type, retirement cycle)
  - Updated meeting requirements with specific quorum formulas
  - Enhanced example data to show CBS-compliant scenarios
