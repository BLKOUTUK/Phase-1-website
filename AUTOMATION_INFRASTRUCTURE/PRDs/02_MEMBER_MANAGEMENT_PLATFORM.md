# PRD 02: Member Management Platform

**Status:** Planning
**Priority:** HIGH (replaces passive database PRD #01)
**Estimated effort:** 60-80 hours (Phase 1)
**Budget:** £0-20/month
**Timeline:** 3 months to launch
**Owner:** TBD
**Last updated:** 2024-11-15

---

## Problem Statement

BLKOUT needs an **automated, self-service member management platform** that:

- Handles member applications, approvals, and onboarding automatically
- Collects £10 annual membership fees (last working day each month, rolling sign-up)
- Manages quarterly board meetings + sub-committee meetings (2 weeks prior)
- Automates meeting workflows: scheduling → recording → transcription → AI draft minutes → publish
- Enables member voting (pre-meeting polls + during meeting)
- Provides member portal (access meetings, vote, update profile, pay fees)
- Requires **minimal manual administration** (current staffing level is low)

**Current state:** No member management system. Manual tracking across emails/WhatsApp. Keeping a static database up-to-date manually would "hold back development of new ideas."

**Desired state:** Members maintain their own data via portal. Admin receives deadline alerts and approves/reviews rather than manually entering data.

---

## Goals & Success Metrics

### Primary Goals
1. **Member self-service**: 80% of member data updates happen via portal without admin intervention
2. **Automated billing**: £10 annual fees invoiced and tracked automatically (last working day each month)
3. **Automated meetings**: Audio recording → AI draft minutes in <24 hours, 90% accuracy
4. **Zero missed deadlines**: Quarterly board meetings, sub-committee meetings, AGM, AR30 filing
5. **Easy to maintain**: <2 hours/month admin time (vs. 10+ hours manual database upkeep)

### Success Metrics
- ✅ Member applications: Application → Approval → Payment → Activation in <48 hours (mostly automated)
- ✅ Annual fee collection rate: 90%+ pay on time (auto-reminders working)
- ✅ Meeting minutes: Published within 3 days of meeting (vs. 2+ weeks manual)
- ✅ Member portal usage: 70%+ members log in at least quarterly
- ✅ Admin time: <2 hours/month (alerts, approvals, review AI-generated content)

### Non-Goals
- **Not** a full CRM with email campaigns (use separate tool if needed)
- **Not** a project management system (focus on governance only)
- **Not** a public website (member portal is private/authenticated)

---

## User Personas

### Primary: Board Administrator (Rob)
- **Needs:** Automated workflows, deadline alerts, minimal manual data entry, easy approvals
- **Pain points:** Low staffing, manual database upkeep blocks new ideas, scattered information
- **Technical comfort:** High (comfortable with code, APIs, automation)
- **Time available:** <2 hours/month for admin tasks

### Secondary: Board Members (9 founding members)
- **Needs:** Join meetings, vote on resolutions, view minutes, update conflicts of interest
- **Pain points:** Unclear what's expected, manual processes, can't access info easily
- **Technical comfort:** Medium (comfortable with web portals, forms)
- **Time available:** Attend quarterly meetings, vote on resolutions, occasional profile updates

### Tertiary: Future Members (applicants)
- **Needs:** Apply for membership, pay joining fee (£10 share), pay annual fees (£10/year)
- **Pain points:** Unclear application process, payment friction
- **Technical comfort:** Basic (can fill forms, make online payments)

---

## Core Features

### 1. Member Portal (Members Only)
**Priority: P0 (Must-have)**

Authenticated portal where members can:

**Profile Management:**
- View/update contact details (email, phone, address)
- Declare/update conflicts of interest
- View own membership status (Active, shares owned, fees paid/due)
- View own voting history

**Meetings:**
- View upcoming meetings (Board, AGM, sub-committees if applicable)
- Access meeting links (Zoom/Teams)
- View past meeting minutes
- RSVP to meetings (helps with quorum tracking)

**Voting:**
- View active resolutions
- Submit votes (pre-meeting polls)
- See own vote after submission (not others' votes until meeting)
- View results after meeting concludes

**Payments:**
- View fee status (£10 annual, due date, paid/overdue)
- Pay via Stripe Checkout (Direct Debit setup for future)
- Download receipts

**Tech stack (free tier):**
- **Authentication**: Supabase Auth (free, unlimited users)
- **Frontend**: Next.js on Vercel (free tier)
- **Database**: Supabase PostgreSQL (free tier: 500MB database, plenty for members/meetings)
- **Styling**: shadcn/ui components (free, open-source)

**Acceptance criteria:**
- [ ] Member can log in with email/password
- [ ] Member can update own contact details
- [ ] Member can declare/update conflicts
- [ ] Member can view upcoming meetings and access Zoom links
- [ ] Member can vote on active resolutions
- [ ] Member can view own fee status and pay via Stripe

---

### 2. Admin Dashboard (Admin Only)
**Priority: P0 (Must-have)**

Admin view showing:

**Upcoming Deadlines:**
- Next board meeting (quarterly)
- Sub-committee meetings (Finance & Fundraising, 2 weeks before board)
- AGM (within 6 months of year-end)
- AR30 filing (7 months after year-end)
- Member fee renewals (last working day each month)

**Member Applications:**
- Pending applications (requires board vote)
- One-click "Approve/Reject" (triggers invoice for £10 share if approved)
- Track payment status → Activate membership when paid

**Payment Dashboard:**
- Members with overdue fees (3+ months = flag for review)
- Monthly revenue (total fees collected)
- Waiver approvals (£10 → £0 for approved waivers)

**Meeting Queue:**
- Upcoming: Schedule meetings, send notices (14 days before for general meetings)
- In Progress: Start recording, generate Zoom link
- Completed: Upload audio → Transcribe → AI draft minutes → Review → Publish

**Reports:**
- Current members list (for AR30)
- Conflicts register
- Voting records (one-member-one-vote compliance)
- Meeting attendance

**Tech stack (same as member portal):**
- Same Next.js app, different routes with role-based access control (Supabase RLS)

**Acceptance criteria:**
- [ ] Admin sees upcoming deadlines dashboard
- [ ] Admin can approve/reject member applications
- [ ] Admin can schedule meetings and send automated notices
- [ ] Admin can upload meeting audio and trigger transcription → AI draft
- [ ] Admin can generate AR30 data report in <5 minutes

---

### 3. Automated Membership Lifecycle
**Priority: P0 (Must-have)**

**Application → Approval → Onboarding workflow:**

1. **Application received** (via public form):
   - Applicant fills: Name, email, phone, why joining, agree to CBS rules
   - Requires proposer + seconder (members select from dropdown)
   - Auto-creates application record (status: Pending)
   - Notifies admin + proposer/seconder

2. **Board votes** (via portal or at meeting):
   - Admin creates resolution: "Approve [Name] as member"
   - Members vote via portal (pre-meeting poll)
   - Results visible at board meeting
   - Admin records outcome (Approved/Rejected)

3. **If approved → Invoice for £10 share**:
   - Auto-generate Stripe payment link
   - Email applicant: "Congrats! Pay £10 to activate membership"
   - Track payment status

4. **When paid → Activate membership**:
   - Create member account (status: Active, shares: 1)
   - Send login credentials
   - Add to member portal access list

**Tech stack:**
- **Payment**: Stripe (free to set up, 1.4% + 20p per transaction)
- **Email**: Resend (free tier: 100 emails/day) or Supabase (SendGrid integration)
- **Automation**: Database triggers (Supabase functions) or Zapier free tier (100 tasks/month)

**Acceptance criteria:**
- [ ] Public application form accepts submissions
- [ ] Admin can trigger board vote on application
- [ ] Approved applicants receive payment link within 24 hours
- [ ] Membership activates automatically when payment received
- [ ] <48 hours from application to activation (if approved and paid immediately)

---

### 4. Automated Monthly Billing Cycle
**Priority: P1 (Should-have Phase 1, can start manual)

**Monthly cycle (last working day of each month):**

**Rolling sign-up model:**
- Member joins mid-month → First fee due on last working day of NEXT month (grace period)
- Annual fee = £10 (or £0 if waiver approved)
- Fee due every 12 months from join anniversary

**Automation workflow:**

1. **7 days before last working day**:
   - Generate invoices for members with fees due
   - Send email: "Your £10 annual fee is due on [date]"
   - Include Stripe payment link

2. **Last working day (fee due date)**:
   - Check payment status
   - If paid: Mark "Paid" (status: Active)
   - If unpaid: Send reminder email

3. **7 days after due date (1st reminder)**:
   - If still unpaid: Send reminder email
   - Flag member as "Payment Overdue"

4. **30 days overdue (2nd reminder)**:
   - Send reminder email
   - Notify admin to follow up

5. **90 days overdue (inactive)**:
   - Mark member status: Inactive (per CBS rules, can terminate if 12 months unpaid)
   - Notify admin for board review

**Waiver process:**
- Member can request waiver via portal (reason required)
- Admin approves/rejects
- If approved: Invoice = £0 (still generated for records, marked "Waived")

**Direct Debit (Phase 2):**
- Integrate GoCardless (UK Direct Debit)
- Members opt-in to auto-payment
- No manual invoicing for Direct Debit members

**Tech stack:**
- **Payment**: Stripe Invoicing (free tier: unlimited invoices, pay per transaction)
- **Automation**: Supabase Edge Functions (free tier: 500K invocations/month) or cron job
- **Future Direct Debit**: GoCardless (1% per transaction, no monthly fee if <1,000 transactions)

**Acceptance criteria:**
- [ ] Invoices auto-generated 7 days before due date
- [ ] Payment reminders sent at 0, 7, 30, 90 days overdue
- [ ] Members can pay via Stripe link
- [ ] Admin can approve waivers (invoice = £0)
- [ ] 90% collection rate (90% pay within 30 days)

---

### 5. Automated Meeting Workflows
**Priority: P0 (Must-have)**

**Quarterly Board Meeting + Sub-Committee Cycle:**

**Meeting cadence:**
- **Board**: Quarterly (Jan, Apr, Jul, Oct - example)
- **Finance sub-committee**: 2 weeks before board meeting
- **Fundraising sub-committee**: 2 weeks before board meeting

**Automation workflow:**

**6 weeks before Board meeting:**
- Auto-create sub-committee meetings (Finance, Fundraising) for 2 weeks before board date
- Send calendar invites to sub-committee members
- Generate Zoom links (Zoom API)

**14 days before any general meeting:**
- Send meeting notice to all members (CBS Rule 39: 14 Clear Days)
- Include: Date, time, Zoom link, agenda
- Create pre-meeting poll for any resolutions

**Day of meeting:**
- Send reminder email (2 hours before)
- Include Zoom link + meeting materials
- Enable cloud recording (Zoom API)

**During meeting:**
- Members can join via Zoom link from portal
- Live voting on resolutions (via portal during meeting)
- Admin tracks attendance

**After meeting (within 24 hours):**
1. Download Zoom cloud recording (MP4)
2. Extract audio (ffmpeg)
3. Send to transcription API (OpenAI Whisper or Assembly.ai)
4. Receive transcript
5. Send transcript to AI (Claude/GPT-4) with prompt: "Generate meeting minutes following this template: [template]"
6. AI returns draft minutes (Markdown format)
7. Admin reviews/edits draft
8. Admin approves → Publish to member portal
9. Send email: "Minutes from [meeting] are now available"

**Tech stack:**
- **Video conferencing**: Zoom (free tier: 40-minute meetings OR paid £11.99/month for unlimited)
- **Transcription**: OpenAI Whisper API (£0.006/minute ≈ £0.36/hour) OR Assembly.ai (free tier: 5 hours/month)
- **AI minutes**: Anthropic Claude API (£3/million input tokens, ~£0.50/hour of transcript)
- **Storage**: Supabase Storage (free tier: 1GB)

**Meeting minutes template:**
```markdown
# [Meeting Type] - [Date]

**Present**: [List of attendees]
**Apologies**: [List of absent members]
**Chair**: [Name]

## 1. Approval of Previous Minutes
[Summary]

## 2. Matters Arising
[Summary of discussions]

## 3. Resolutions
### Resolution 1: [Title]
**Proposed by**: [Name]
**Seconded by**: [Name]
**Vote**: For: X, Against: Y, Abstain: Z
**Outcome**: Passed/Failed

## 4. Reports
[Summary of reports presented]

## 5. Any Other Business
[Summary]

## 6. Date of Next Meeting
[Date]
```

**Acceptance criteria:**
- [ ] Sub-committee meetings auto-scheduled 2 weeks before board meetings
- [ ] Meeting notices sent 14 days before general meetings
- [ ] Zoom cloud recording auto-downloaded after meeting
- [ ] AI draft minutes generated within 24 hours
- [ ] Admin can review/edit draft and publish to portal
- [ ] Published minutes emailed to members
- [ ] 90%+ minutes accuracy (minimal admin edits needed)

---

### 6. Voting System (Pre-Meeting + Live)
**Priority: P0 (Must-have)**

**Two voting modes:**

**1. Pre-Meeting Poll:**
- Admin creates resolution (e.g., "Approve new member Jane Smith")
- Sets voting window (e.g., 7 days before meeting)
- Members receive email: "Please vote on [resolution]"
- Members log into portal → Vote (For/Against/Abstain)
- Votes are private (members can't see others' votes)
- Results tallied but NOT visible until meeting

**2. Live Voting (during meeting):**
- Admin opens resolution for live vote
- Members attending meeting vote via portal (on phone/laptop)
- Results displayed in real-time on admin dashboard
- Admin announces results
- Votes recorded in database

**Post-meeting:**
- All votes finalized (no changes)
- Results visible to all members in meeting minutes
- Voting record stored for compliance (one-member-one-vote verification)

**Voting rules (per CBS):**
- One member = one vote (Rule 56)
- Ordinary resolution: Simple majority (Rule 63)
- Extraordinary resolution: 75%+ (Rule 63)
- Quorum: 3 OR 10% of membership, whichever greater (Rule 44)

**Tech stack:**
- Database: Supabase (votes stored in `decisions` and `individual_votes` tables)
- Real-time: Supabase Realtime (free tier, WebSocket updates for live voting)

**Acceptance criteria:**
- [ ] Admin can create resolution and open for pre-meeting poll
- [ ] Members receive email notification with link to vote
- [ ] Members can vote via portal (votes are private)
- [ ] Admin can open resolution for live voting during meeting
- [ ] Results update in real-time during live voting
- [ ] Votes recorded with timestamp, one-member-one-vote enforced
- [ ] Voting record generates compliance report (who voted, when, on what)

---

### 7. Deadline & Alert System
**Priority: P1 (Should-have)**

**Automated alerts for:**

**Quarterly board meetings:**
- 6 weeks before: Schedule sub-committees
- 2 weeks before: Sub-committee meetings happening
- 14 days before: Send board meeting notice
- 2 hours before: Meeting reminder

**AGM (Rule 36: within 6 months of year-end):**
- 5 months after year-end: "AGM due in 1 month"
- 14 days before: Send AGM notice

**AR30 filing (7 months after year-end):**
- 6 months after year-end: "AR30 due in 1 month - prepare accounts"
- 1 week before deadline: "AR30 due in 7 days"

**Member fee renewals (monthly):**
- Last working day - 7 days: "Fees due on [date]"
- Last working day: "Fees due today"
- 7/30/90 days overdue: Escalating reminders

**Tech stack:**
- **Scheduling**: Supabase Edge Functions with cron triggers (free tier)
- **Email**: Resend (free tier: 100 emails/day)

**Acceptance criteria:**
- [ ] Admin receives email alerts 6 weeks, 2 weeks, 14 days before board meetings
- [ ] AGM alert sent 5 months after year-end
- [ ] AR30 alert sent 6 months after year-end
- [ ] Monthly fee reminders sent automatically
- [ ] Zero missed deadlines in first year

---

## Technical Architecture

### Database Schema (Supabase PostgreSQL)

**Core tables:**

```sql
-- Members
members (
  id uuid PRIMARY KEY,
  name text NOT NULL,
  email text UNIQUE NOT NULL,
  phone text,
  membership_type text, -- 'Founder Member' | 'Member'
  member_category text, -- 'Natural Person' | 'Corporate Body' | 'Nominee'
  join_date date NOT NULL,
  leave_date date,
  status text, -- 'Active' | 'Inactive' | 'Left'
  shares_owned integer DEFAULT 1,
  is_director boolean DEFAULT false,
  director_type text, -- 'Elected' | 'Independent Non-Executive'
  annual_fee_amount decimal DEFAULT 10.00, -- £10 or £0 if waiver
  fee_due_date date, -- Last working day of month, 12 months after join
  created_at timestamp DEFAULT now()
)

-- Applications
applications (
  id uuid PRIMARY KEY,
  applicant_name text NOT NULL,
  applicant_email text NOT NULL,
  application_date date DEFAULT now(),
  proposer_id uuid REFERENCES members(id),
  seconder_id uuid REFERENCES members(id),
  reason text, -- Why joining
  vote_date date,
  resolution_id uuid REFERENCES decisions(id),
  outcome text, -- 'Approved' | 'Rejected' | 'Pending'
  payment_link text, -- Stripe payment link
  payment_status text, -- 'Pending' | 'Paid' | 'Failed'
  member_created_id uuid REFERENCES members(id)
)

-- Meetings
meetings (
  id uuid PRIMARY KEY,
  date date NOT NULL,
  time time NOT NULL,
  type text, -- 'AGM' | 'Board Meeting' | 'Finance Sub-Committee' | 'Fundraising Sub-Committee'
  purpose text,
  notice_sent_date date,
  zoom_link text,
  zoom_recording_url text,
  transcript_url text,
  minutes_draft text, -- AI-generated draft (Markdown)
  minutes_final text, -- Admin-approved final (Markdown)
  minutes_published_date date,
  quorum_required integer,
  quorum_present integer,
  chair_id uuid REFERENCES members(id),
  created_at timestamp DEFAULT now()
)

-- Decisions (Resolutions)
decisions (
  id uuid PRIMARY KEY,
  title text NOT NULL,
  description text,
  meeting_id uuid REFERENCES meetings(id),
  resolution_type text, -- 'Ordinary' | 'Extraordinary (75%)' | 'Special'
  voting_opens_at timestamp, -- Pre-meeting poll start
  voting_closes_at timestamp, -- Live voting end
  outcome text, -- 'Passed' | 'Failed' | 'Deferred'
  votes_for integer DEFAULT 0,
  votes_against integer DEFAULT 0,
  votes_abstain integer DEFAULT 0,
  created_at timestamp DEFAULT now()
)

-- Individual Votes
individual_votes (
  id uuid PRIMARY KEY,
  decision_id uuid REFERENCES decisions(id),
  member_id uuid REFERENCES members(id),
  vote text, -- 'For' | 'Against' | 'Abstain' | 'Recused'
  vote_type text, -- 'Pre-Meeting' | 'Live'
  timestamp timestamp DEFAULT now(),
  UNIQUE(decision_id, member_id) -- One vote per member per decision
)

-- Conflicts of Interest
conflicts (
  id uuid PRIMARY KEY,
  member_id uuid REFERENCES members(id),
  organization text NOT NULL,
  nature text, -- 'Director' | 'Shareholder (>1%)' | 'Employee' | 'Family/Household' | 'Business Associate'
  description text,
  is_connected_person boolean DEFAULT false,
  connected_person_name text,
  declared_date date DEFAULT now(),
  status text, -- 'Current' | 'Historical' | 'Resolved'
  companies_house_number text
)

-- Invoices
invoices (
  id uuid PRIMARY KEY,
  member_id uuid REFERENCES members(id),
  type text, -- 'Joining Fee (Share)' | 'Annual Membership Fee'
  amount decimal NOT NULL, -- £10.00 or £0.00
  due_date date NOT NULL,
  paid_date date,
  status text, -- 'Pending' | 'Paid' | 'Overdue' | 'Waived'
  stripe_invoice_id text,
  payment_link text,
  waiver_approved boolean DEFAULT false,
  waiver_reason text,
  created_at timestamp DEFAULT now()
)

-- Attendance
attendance (
  id uuid PRIMARY KEY,
  meeting_id uuid REFERENCES meetings(id),
  member_id uuid REFERENCES members(id),
  attendance_type text, -- 'In Person' | 'Remote' | 'Proxy' | 'Absent'
  rsvp_status text, -- 'Yes' | 'No' | 'Maybe' | 'No Response'
  proxy_for_id uuid REFERENCES members(id)
)
```

### Authentication & Authorization (Supabase RLS)

**Row Level Security policies:**

```sql
-- Members can view own profile, update own contact/conflicts
ALTER TABLE members ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Members can view own profile"
  ON members FOR SELECT
  USING (auth.uid() = id);

CREATE POLICY "Members can update own profile"
  ON members FOR UPDATE
  USING (auth.uid() = id);

-- Admin can view/update all members
CREATE POLICY "Admin can manage all members"
  ON members FOR ALL
  USING (auth.jwt() ->> 'role' = 'admin');

-- All members can view published meeting minutes
CREATE POLICY "Members can view published minutes"
  ON meetings FOR SELECT
  USING (minutes_published_date IS NOT NULL);

-- Admin can manage meetings
CREATE POLICY "Admin can manage meetings"
  ON meetings FOR ALL
  USING (auth.jwt() ->> 'role' = 'admin');

-- Members can vote on open resolutions
CREATE POLICY "Members can vote on open resolutions"
  ON individual_votes FOR INSERT
  USING (
    auth.uid() = member_id
    AND EXISTS (
      SELECT 1 FROM decisions
      WHERE id = decision_id
      AND now() BETWEEN voting_opens_at AND voting_closes_at
    )
  );
```

### Frontend Architecture (Next.js)

**Routes:**

```
/                       → Public landing page (CBS info, apply for membership)
/apply                  → Public application form
/login                  → Login page
/dashboard              → Member dashboard (redirect based on role)
  /member               → Member portal
    /profile            → View/edit profile
    /meetings           → Upcoming/past meetings
    /vote               → Active resolutions to vote on
    /payments           → Fee status, pay invoices
  /admin                → Admin dashboard
    /members            → Manage members
    /applications       → Approve/reject applications
    /meetings           → Schedule meetings, upload recordings
    /votes              → Create resolutions, view results
    /payments           → Payment dashboard, approve waivers
    /reports            → Generate AR30 data, conflicts register
```

**Tech stack:**
- **Framework**: Next.js 14 (App Router)
- **UI**: shadcn/ui + Tailwind CSS
- **Auth**: Supabase Auth (email/password, magic links)
- **Database**: Supabase PostgreSQL
- **Real-time**: Supabase Realtime (live voting updates)
- **Payments**: Stripe Checkout + Invoicing
- **Email**: Resend
- **Hosting**: Vercel (free tier)

---

## AI Meeting Minutes Generation

**Workflow:**

1. **Upload audio** (MP4 from Zoom cloud recording)
2. **Extract audio** (ffmpeg: MP4 → MP3)
3. **Transcribe** (OpenAI Whisper API)
   - Input: MP3 file
   - Output: Transcript with timestamps
   - Cost: £0.006/minute (1-hour meeting = £0.36)

4. **Generate minutes** (Claude API)
   - Input: Transcript + meeting metadata (attendees, agenda) + template
   - Prompt:
   ```
   You are a professional minute-taker for a UK Community Benefit Society.

   Generate meeting minutes in Markdown format following this template:
   [template from above]

   Meeting details:
   - Type: Board Meeting
   - Date: 2024-11-15
   - Attendees: [list]
   - Apologies: [list]

   Transcript:
   [full transcript]

   Instructions:
   - Summarize discussions concisely
   - Extract all formal resolutions with vote counts
   - Use professional, neutral tone
   - Include action items with responsible persons
   - Format as Markdown
   ```
   - Output: Draft minutes (Markdown)
   - Cost: ~£0.50/hour of transcript (depends on length)

5. **Admin reviews** (via admin dashboard)
   - View AI-generated draft
   - Edit inline (WYSIWYG Markdown editor)
   - Approve → Publish

6. **Publish to portal**
   - Save final minutes to database
   - Set `minutes_published_date`
   - Send email to members: "Minutes from [meeting] are now available"

**Total cost per meeting**: £0.36 (transcription) + £0.50 (AI) ≈ **£0.86/hour** of meeting time

**Acceptance criteria:**
- [ ] Zoom recording auto-downloaded after meeting
- [ ] Audio transcribed with 95%+ accuracy
- [ ] AI draft minutes follow template format
- [ ] Admin can edit draft in browser
- [ ] Published minutes emailed to members within 3 days

---

## Implementation Plan

### Phase 1: Core Platform (Months 1-2, 40-50 hours)

**Week 1-2: Foundation (15-20 hours)**
- Set up Supabase project (database, auth, storage)
- Create database schema (members, meetings, decisions, votes, applications, invoices)
- Set up Next.js project on Vercel
- Implement authentication (login, signup, password reset)
- Create basic member/admin dashboards (layout only)

**Week 3-4: Member Portal (12-15 hours)**
- Profile view/edit page
- Conflicts declaration form
- Meetings list (upcoming/past)
- Voting page (view resolutions, submit votes)
- Payment page (view invoices, Stripe Checkout integration)

**Week 5-6: Admin Dashboard (15-20 hours)**
- Member management (view, edit, activate/deactivate)
- Application approval workflow
- Meeting scheduler (create meetings, send notices)
- Resolution creator (create votes, view results)
- Basic reports (members list, conflicts register)

**Phase 1 deliverables:**
- [ ] Member portal functional (login, profile, view meetings, vote, pay)
- [ ] Admin dashboard functional (manage members, approve applications, create meetings/votes)
- [ ] Supabase database live with RLS policies
- [ ] Stripe payment integration working

---

### Phase 2: Automation (Months 2-3, 25-35 hours)

**Week 7-8: Automated Billing (12-15 hours)**
- Cron job: Generate invoices on last working day
- Email reminders (7 days before, 0, 7, 30, 90 days overdue)
- Stripe webhook: Mark invoices paid when payment received
- Waiver approval workflow
- Payment dashboard (overdue members, monthly revenue)

**Week 9-10: Meeting Automation (15-20 hours)**
- Zoom API integration (create meetings, get cloud recordings)
- Audio transcription (OpenAI Whisper API)
- AI minutes generation (Claude API)
- Minutes editor (Markdown WYSIWYG)
- Publish workflow (email members when published)

**Phase 2 deliverables:**
- [ ] Monthly invoices auto-generated and emailed
- [ ] Payment reminders sent automatically
- [ ] Meeting recordings auto-downloaded and transcribed
- [ ] AI draft minutes generated within 24 hours
- [ ] Admin can review/edit/publish minutes via dashboard

---

### Phase 3: Polish & Alerts (Month 3, 10-15 hours)

**Week 11: Deadline Alerts (5-8 hours)**
- Cron job: Check upcoming deadlines (board meetings, AGM, AR30)
- Email admin 6 weeks, 2 weeks, 14 days before meetings
- AGM/AR30 deadline alerts
- Dashboard: "Upcoming deadlines" widget

**Week 12: Testing & Launch (5-7 hours)**
- Import 9 founding members (migrate from CBS registration data)
- Import 17 conflicts of interest
- Test full workflows (application, approval, payment, meeting, voting)
- Train board on using portal
- Launch announcement

**Phase 3 deliverables:**
- [ ] Deadline alerts working (admin receives emails)
- [ ] All 9 founding members migrated with data
- [ ] Conflicts register imported
- [ ] Platform tested end-to-end
- [ ] Board trained, platform live

---

## Budget Breakdown

### Monthly Costs (Phase 1)

**Free tier (target £0-5/month):**
- Supabase: Free (500MB database, 2GB storage, 100K Edge Function invocations)
- Vercel: Free (hobby plan, unlimited projects)
- Resend: Free (100 emails/day = 3,000/month)
- Zoom: £11.99/month (paid plan for unlimited meeting length) **OR** Free (40-minute limit, use multiple calls)

**Per-use costs:**
- Stripe: 1.4% + 20p per transaction (£10 fee = 20p, net £9.80)
- OpenAI Whisper: £0.006/minute (1-hour meeting = £0.36)
- Claude API: ~£0.50/hour of transcript
- **Total per meeting**: £0.86/hour (4 quarterly meetings × 1 hour = £3.44/year)
- **Total per member/year**: £10 fee × 9 members = £90 revenue, minus £0.20 Stripe fee × 9 = £88.20 net

**Estimated monthly cost:**
- **£0-12/month** (free tier + Zoom if needed)
- **£3.44/year** (meeting transcription/AI for 4 quarterly meetings)
- **Revenue**: £90/year (9 members × £10 annual fee)
- **Net**: £90 - £3.44 - (£11.99 × 12 if paid Zoom) ≈ **-£57.32/year** (cost) OR **+£86.56/year** (profit if free Zoom)

**Recommendation**: Use free Zoom tier (40-minute meetings, schedule 2 back-to-back calls if needed) → **Net profit: £86.56/year**

### One-Time Costs

**Development:**
- 75-100 hours total (Phases 1-3)
- If outsourced: £30-50/hour UK freelancer = £2,250-5,000
- If volunteer time: £0 (but opportunity cost)

**Initial setup:**
- Domain (blkout.uk.coop): Already owned
- SSL certificate: Free (Vercel auto-provisions Let's Encrypt)

**Data migration:**
- Import 9 founding members: 1 hour
- Import 17 conflicts: 1 hour

---

## Risks & Mitigations

### Risk 1: AI minutes not accurate enough
**Likelihood**: Medium
**Impact**: Medium (admin spends 30+ min editing each draft)

**Mitigation:**
- Test with sample meeting recordings before launch
- Provide clear template and detailed prompt
- Use Claude Opus (most capable model) for minutes generation
- Admin always reviews before publishing (safety net)

### Risk 2: Low member portal adoption
**Likelihood**: Medium
**Impact**: High (defeats purpose of self-service)

**Mitigation:**
- Train board on portal usage at launch
- Make portal required for meeting access (Zoom link only in portal)
- Make voting only via portal (not email)
- Send regular reminders "Update your profile/conflicts in portal"

### Risk 3: Payment collection rate <90%
**Likelihood**: Medium
**Impact**: Medium (cash flow issues, manual follow-up needed)

**Mitigation:**
- Auto-reminders at 7/30/90 days overdue
- Make Direct Debit easy (GoCardless integration Phase 2)
- Board approves waivers for genuine hardship
- Inactive members after 90 days (CBS rules allow termination at 12 months)

### Risk 4: Free tier limits exceeded
**Likelihood**: Low (only 9 members currently)
**Impact**: Low (upgrade costs minimal)

**Mitigation:**
- Monitor Supabase usage monthly
- If approaching limits, upgrade to Pro (£20/month)
- Resend limit (100 emails/day) unlikely to hit with 9 members
- If hit, upgrade to Grow (£16/month for 50K emails)

---

## Success Criteria

### Must-Have (Launch Requirements)
- [ ] 9 founding members have portal accounts
- [ ] Members can log in, view profile, update conflicts
- [ ] Members can access meeting links and vote on resolutions
- [ ] Members can pay annual fees via Stripe
- [ ] Admin can approve member applications
- [ ] Admin can schedule meetings and send automated notices
- [ ] AI draft minutes generated from meeting recordings
- [ ] Deadline alerts working (admin receives emails)

### Should-Have (3 months post-launch)
- [ ] 80%+ members log into portal at least quarterly
- [ ] 90%+ annual fees collected within 30 days of due date
- [ ] AI draft minutes require <15 min admin editing per meeting
- [ ] Zero missed deadlines (board meetings, AGM, AR30)
- [ ] Admin time <2 hours/month

### Could-Have (6 months post-launch)
- [ ] Direct Debit integration (GoCardless)
- [ ] Mobile app (React Native) or PWA
- [ ] Automated conflict of interest reminders (annual declaration)
- [ ] Public member directory on website
- [ ] Integration with accounting software (Xero/QuickBooks)

---

## Open Questions

1. **Zoom account**: Do you have a paid Zoom account (£11.99/month) or use free tier?
   - Free tier: 40-minute meeting limit (can schedule back-to-back)
   - Paid tier: Unlimited meeting length + cloud recording storage

2. **Financial year end**: When is BLKOUT's financial year end? (Needed for AGM/AR30 deadline calculations)

3. **First board meeting**: When is the next board meeting? (Want to test meeting automation before then)

4. **Member data**: Do you have the 9 founding members' contact details ready to import?
   - Name, email, phone, join date (CBS registration date)

5. **Conflicts data**: Can we import the 17 conflicts from CBS registration work?
   - Already documented in `CBS_REGISTRATION_WORK/MASTER_AFFILIATIONS_SPREADSHEET.md`

6. **Branding**: Any specific colors/logo for the portal? Or use BLKOUT brand guidelines?

---

## Next Steps (Immediate Actions)

### This week:
1. **User approval**: Review this PRD, confirm requirements match vision
2. **Decide**: Start building now or refine PRD further?

### If approved, Week 1:
3. **Set up Supabase project** (database + auth)
4. **Set up Next.js project** on Vercel
5. **Create database schema** (members, meetings, decisions, votes)
6. **Implement authentication** (login/signup)

### Week 2:
7. **Build member portal** (profile, meetings, voting pages)
8. **Build admin dashboard** (members, applications, meetings)

---

## Conclusion

This Member Management Platform replaces the passive database PRD (#01) with an **active, automated system** that:

- **Members maintain their own data** (profile, conflicts, payments) via portal
- **Automated billing** (£10 annual fees, reminders, payment tracking)
- **Automated meetings** (audio → transcript → AI draft minutes)
- **Automated alerts** (deadlines, fee reminders, meeting notices)
- **Minimal admin time** (<2 hours/month vs. 10+ hours manual database upkeep)

**Budget:** £0-12/month (free tier stack + optional paid Zoom)
**Timeline:** 3 months to launch
**Effort:** 75-100 hours development

**Expected outcome:**
- 80% member self-service (minimal admin data entry)
- 90% fee collection rate (automated reminders)
- AI draft minutes within 24 hours (90% accuracy)
- Zero missed deadlines (automated alerts)
- Platform scales from 9 → 100+ members with same effort

Ready to proceed?

---

**Document Control:**
- **Version**: 1.0
- **Last Updated**: 2024-11-15
- **Next Review**: After user approval
- **Owner**: BLKOUT Infrastructure Team
- **Replaces**: PRD #01 (Member Relationship Management - passive database)
