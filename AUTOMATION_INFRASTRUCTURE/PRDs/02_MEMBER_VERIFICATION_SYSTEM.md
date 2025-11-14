# Product Requirement Document
## Member Verification System

**Version**: 1.0
**Date**: 14 November 2025
**Owner**: BLKOUT Infrastructure Team
**Status**: Prototype Exists (blkout-verification) → Formalize & Expand

---

## Executive Summary

Formalize and expand the member verification system (currently https://blkoutuk.github.io/blkout-verification/) into a reusable infrastructure component for ongoing member onboarding, annual confirmations, and compliance workflows.

**Value Proposition**: The affiliations verification you just built got 6/9 responses within an hour. This validates the approach - now make it reusable for all member verification needs.

---

## Problem Statement

### What You Just Experienced

**CBS Affiliations Verification (Nov 2025):**
- ✅ **Success**: 67% response rate within 1 hour using WhatsApp + GitHub Pages
- ✅ **What worked**: Ultra-short message, simple web form, mobile-friendly
- ✅ **Learning**: Members respond fast when it's genuinely quick and easy

**But this was a one-off build:**
- Custom-coded for one specific use case (affiliations disclosure)
- Not reusable for next verification need
- No tracking/audit trail built in
- Hard to update if member data changes

### Upcoming Verification Needs

You'll need similar verification workflows for:

1. **Annual member confirmations** (CBS requirement - every year)
   - Confirm still want to be a member
   - Confirm contact details
   - Confirm affiliations (annually)
   - Confirm conflict of interest disclosures

2. **New member onboarding**
   - Background information collection
   - Initial affiliations disclosure
   - Sign member agreement
   - Accept code of conduct

3. **Event/project participation**
   - RSVP to events
   - Confirm availability for projects
   - Collect specific information (dietary requirements, access needs, etc.)

4. **Policy acknowledgments**
   - New safeguarding policy → all members must acknowledge
   - Updated conflict of interest policy → re-sign
   - GDPR consent updates

5. **Board elections/votes**
   - Confirm eligibility to vote
   - Cast votes
   - Board nominations

### Current Pain Points

- **No reusable system**: Each verification = rebuild from scratch
- **No progress tracking**: Can't see who's responded, who hasn't
- **No reminders**: Manual WhatsApp follow-up
- **No audit trail**: No record of when/what members confirmed
- **No flexibility**: Hard to adapt for different verification types

---

## Goals & Success Metrics

### Primary Goals

1. **Reusable verification framework** - Build once, use for all future verifications
2. **Fast member responses** - Maintain the 1-hour response rate you achieved
3. **Progress tracking** - Always know who's responded, who needs follow-up
4. **Audit compliance** - Full record of all verifications for FCA/compliance

### Success Metrics

| Metric | Current (Manual) | Target (Automated) | Timeline |
|--------|------------------|-------------------|----------|
| Setup time per verification | 2-4 hours (custom build) | <15 min (template) | Phase 1 |
| Member response time | 1 hour (your WhatsApp approach) | <2 hours (maintain) | Phase 1 |
| Response rate | 67% in 1 hour, 100% in 1 day | 80% in 2 hours, 100% in 1 day | Phase 1 |
| Tracking visibility | Manual checklist | Real-time dashboard | Phase 1 |
| Audit trail completeness | None (no records) | 100% (all responses logged) | Phase 1 |
| Reminder automation | Manual WhatsApp | Automated after 24h | Phase 2 |

### Key Performance Indicators

- **Verification completion rate**: 100% within deadline (currently achieved, maintain)
- **Setup efficiency**: Launch new verification in <15 min
- **Member satisfaction**: "Easy to complete" rating >90%
- **Compliance readiness**: Full audit trail for all verifications
- **System uptime**: 99.5% (critical during verification windows)

---

## User Stories

### As a CBS Administrator
> "I need to collect annual member confirmations every year for FCA. Last time I built a custom form and spent hours tracking responses. I want a template I can launch in 10 minutes."

**Acceptance Criteria:**
- Select "Annual Member Confirmation" template
- Auto-populates with current member list
- Customize questions (if needed)
- Launch → get shareable link
- Real-time dashboard showing responses
- Auto-reminders after 24h

### As a BLKOUT Member
> "When I get a verification request, I want to complete it on my phone in under 2 minutes without creating an account or remembering a password."

**Acceptance Criteria:**
- Click link → personalized page (my name pre-filled)
- See exactly what needs confirming
- Tick boxes / enter data
- Submit → confirmation message
- Works perfectly on mobile
- No login required (magic link approach)

### As a Compliance Officer
> "For FCA audit, I need to prove all members confirmed their affiliations on [date]. I need exportable records with timestamps and digital signatures."

**Acceptance Criteria:**
- Export all responses to CSV/PDF
- Includes timestamp, IP address (for audit)
- Digital trail (who confirmed what when)
- Downloadable for 7 years
- Filterable by date/member/verification type

### As a Partnerships Lead
> "When onboarding a new partner organization, I need their staff to confirm they've read our safeguarding policy. I want to track completion and send reminders to non-responders."

**Acceptance Criteria:**
- Upload list of partner staff (name, email)
- Select "Policy Acknowledgment" template
- Auto-send personalized links
- Track completion
- Auto-reminder after 48h
- Export completion report

---

## Functional Requirements

### Core Features (Phase 1)

**FR1: Verification Templates**

Pre-built templates for common use cases:
- **Annual Member Confirmation** (affiliations, contact details, membership status)
- **New Member Onboarding** (background info, initial disclosures)
- **Policy Acknowledgment** (simple yes/no + timestamp)
- **Event RSVP** (yes/no + additional info)
- **Custom** (build your own)

Each template includes:
- Pre-defined questions
- Customizable fields
- Appropriate validation rules
- Mobile-optimized layout

**FR2: Member List Management**

- Upload CSV of members (name, email, DOB, role)
- Or pull from existing member database (if integrated)
- Support for groups (e.g., "Founding Members", "General Members", "Partners")
- Deduplication (prevent duplicate sends)

**FR3: Personalized Verification Pages**

- Each member gets unique URL (e.g., `/verify/abc123xyz`)
- Page shows their name, role (pre-filled)
- Shows what needs confirming (pre-filled with known data)
- Member confirms/updates/adds information
- Mobile-first design (like your blkout-verification site)

**FR4: Real-Time Progress Dashboard**

- See all members and their response status:
  - ✅ Completed (green)
  - ⏳ In Progress (yellow)
  - ❌ Not Started (red)
- Completion percentage
- Last activity timestamp
- Filter by status, role, date
- Export to CSV

**FR5: Response Collection & Storage**

- Store all responses in database
- Timestamp each submission
- Log IP address (for audit)
- Support attachments (e.g., signed documents)
- Immutable audit trail (can't delete/edit responses)

**FR6: Export & Reporting**

- Export all responses to CSV
- Generate PDF summary report
- FCA-ready format (if applicable)
- Include audit metadata (timestamps, IPs)
- Downloadable for 7 years

**FR7: Link Generation & Sharing**

- Auto-generate unique links for each member
- Copy all links to clipboard (for WhatsApp bulk send)
- Email send option (if SMTP configured)
- QR codes (for in-person events)

### Enhanced Features (Phase 2)

**FR8: Automated Reminders**

- Send reminder after configurable time (default: 24h)
- Escalation reminders (48h, 72h)
- Different reminder channels:
  - Email (if configured)
  - SMS (via Twilio/similar)
  - WhatsApp (manual or via Business API)
- Stop reminders once submitted

**FR9: Email Integration (Optional)**

- Integrate with SendGrid/Mailgun/Postmark
- Auto-send verification links via email
- Branded email templates
- Track email opens/clicks
- Fallback to manual link sharing if email fails

**FR10: Conditional Logic**

- Show/hide questions based on previous answers
- Example: "If member says YES to new affiliation → show affiliation details form"
- Branching workflows
- Skip logic

**FR11: Digital Signatures**

- Capture typed signature
- Timestamp and IP logging
- Legally binding (if configured correctly)
- Export with signature image

**FR12: Integration with Member Database**

- Auto-pull current member list
- Auto-update member records with confirmations
- Two-way sync
- Conflict resolution (if data differs)

### Advanced Features (Phase 3)

**FR13: Multi-Language Support**

- Templates in multiple languages
- Auto-detect member's preferred language
- Easy translation workflow

**FR14: Accessibility Features**

- Screen reader compatible
- Keyboard navigation
- High contrast mode
- Text resizing

**FR15: API for Integrations**

- Programmatic creation of verifications
- Webhook notifications on completion
- Integration with other BLKOUT systems

**FR16: Advanced Analytics**

- Response time distribution
- Completion rate trends
- Member engagement metrics
- Identify "slow responders" for targeted outreach

---

## Technical Requirements

### Technology Stack

**Frontend (GitHub Pages Approach - What You've Used):**
- **Framework**: HTML/CSS/JavaScript (simple) OR Next.js/React (scalable)
- **Styling**: Tailwind CSS (fast, mobile-first)
- **Hosting**: GitHub Pages (free, fast, reliable)
- **Forms**: Custom JS OR Formspree/Basin (form backend)

**Backend (For Phase 2+):**
- **Framework**: Next.js API routes OR Supabase (BaaS)
- **Database**: Supabase (PostgreSQL) OR Firebase
- **Authentication**: Magic links (email-based, no password)
- **File Storage**: Supabase Storage OR AWS S3

**Recommended Stack (Balanced):**
- **Next.js** (frontend + API routes in one codebase)
- **Supabase** (database + auth + storage, generous free tier)
- **Vercel** (hosting, free tier, great Next.js integration)
- **Resend** or **SendGrid** (email, free tier available)

### Data Model

**Verifications Table:**
```sql
verifications (
  id: uuid PRIMARY KEY,
  title: text, -- "Annual Confirmation 2025"
  type: text, -- "annual_confirmation", "policy_acknowledgment", etc.
  template_id: uuid, -- reference to template used
  created_by: uuid, -- admin who created it
  created_at: timestamp,
  deadline: timestamp,
  status: text, -- "draft", "active", "closed"
  settings: jsonb -- reminder config, etc.
)
```

**Verification Invitations Table:**
```sql
verification_invitations (
  id: uuid PRIMARY KEY,
  verification_id: uuid FOREIGN KEY,
  member_id: uuid FOREIGN KEY, -- or null if external person
  member_name: text,
  member_email: text,
  unique_token: text UNIQUE, -- for personalized URL
  sent_at: timestamp,
  reminded_at: timestamp,
  completed_at: timestamp NULL,
  status: text -- "pending", "completed", "expired"
)
```

**Verification Responses Table:**
```sql
verification_responses (
  id: uuid PRIMARY KEY,
  invitation_id: uuid FOREIGN KEY,
  verification_id: uuid FOREIGN KEY,
  member_id: uuid FOREIGN KEY,
  responses: jsonb, -- flexible structure for different templates
  submitted_at: timestamp,
  ip_address: text, -- for audit
  user_agent: text -- for audit
)
```

**Templates Table:**
```sql
verification_templates (
  id: uuid PRIMARY KEY,
  name: text,
  type: text,
  questions: jsonb, -- array of question objects
  created_at: timestamp,
  is_default: boolean
)
```

### Security & Privacy

**Data Protection:**
- Personal data (email, DOB, responses) → encrypted at rest
- Unique tokens (URLs) → cryptographically secure (not guessable)
- Rate limiting on submission endpoint (prevent spam)
- HTTPS only (no unencrypted traffic)

**Access Control:**
- Admin access (can create verifications, see all responses)
- Member access (can only see their own verification, via unique token)
- Read-only access (for compliance officer - can export, can't edit)

**Audit Trail:**
- Log all admin actions (who created what when)
- Log all member submissions (timestamp, IP)
- Immutable responses (can't delete or edit after submission)
- 7-year retention for compliance

**GDPR Compliance:**
- Clear purpose statement on verification pages
- Member consent recorded
- Right to access (members can download their data)
- Right to rectification (members can update within window)
- Data minimization (only collect what's needed)

### Performance Requirements

- **Page load time**: <2 seconds (critical for mobile users)
- **Form submission**: <1 second response
- **Dashboard load**: <3 seconds (even with 100+ members)
- **Uptime**: 99.5% during verification windows
- **Mobile performance**: 90+ Lighthouse score

---

## Implementation Phases

### Phase 1: Core System (Month 1) - Based on Your Prototype

**Deliverables:**
- [ ] Formalize your blkout-verification prototype into reusable template
- [ ] Member list upload (CSV)
- [ ] Generate unique links for each member
- [ ] Personalized verification pages
- [ ] Response collection (store in Supabase or similar)
- [ ] Real-time progress dashboard
- [ ] Export to CSV
- [ ] 3 templates: Annual Confirmation, New Member Onboarding, Policy Acknowledgment

**Effort**: 20-30 hours
**Priority**: HIGH (makes verification repeatable)

**Success Criteria:**
- Can launch annual confirmation in <15 min
- Member experience identical to your successful prototype
- Dashboard shows real-time progress
- Export works for compliance

### Phase 2: Automation (Month 2-3)

**Deliverables:**
- [ ] Automated reminders (24h, 48h)
- [ ] Email integration (SendGrid/Resend)
- [ ] Conditional logic in forms
- [ ] Integration with member database (if exists)
- [ ] Digital signatures

**Effort**: 25-35 hours
**Priority**: MEDIUM (reduces manual follow-up work)

### Phase 3: Advanced Features (Month 4-6)

**Deliverables:**
- [ ] Multi-language support
- [ ] Advanced analytics
- [ ] API for integrations
- [ ] Accessibility enhancements

**Effort**: 30-40 hours
**Priority**: LOW (nice-to-have)

---

## Dependencies

### External Dependencies

- **Hosting**: GitHub Pages (free) OR Vercel (free tier)
- **Database**: Supabase (free tier: 500MB, 50K requests/month)
- **Email** (Phase 2): SendGrid (free tier: 100 emails/day) OR Resend (free tier: 3K emails/month)
- **Domain**: blkoutuk.github.io (already have) OR custom domain

### Internal Dependencies

- **Member database**: Need canonical list of members (CSV OK for Phase 1)
- **Email addresses**: Need current emails for all members
- **Admin access**: Who can create/manage verifications?

---

## Risks & Mitigation

### Risk 1: Members Don't Respond (Despite Success This Time)

**Likelihood**: Low (you just achieved 67% in 1 hour)
**Impact**: High (can't meet compliance deadlines)

**Mitigation:**
- Maintain the winning formula: WhatsApp + ultra-short message + simple form
- Automated reminders (Phase 2)
- Escalate to phone calls for stragglers (proven effective)
- Deadline pressure (clear cutoff date/time)

### Risk 2: Data Loss

**Likelihood**: Low (using hosted services with backups)
**Impact**: Critical (lose compliance records)

**Mitigation:**
- Daily automated backups (Supabase provides this)
- Export to CSV after each verification (manual backup)
- Multi-region storage (if using cloud provider)
- Test restore process quarterly

### Risk 3: Privacy Breach

**Likelihood**: Low (unique tokens, encryption)
**Impact**: High (reputational damage, GDPR fines)

**Mitigation:**
- Secure token generation (cryptographic random)
- HTTPS only
- Rate limiting (prevent brute force)
- Regular security audits
- Penetration testing before launch

---

## Alternatives Considered

### Alternative 1: Google Forms

**Pros:**
- Free
- Easy to set up (5 minutes)
- Familiar to users
- Built-in response collection

**Cons:**
- Not personalized (can't pre-fill member data)
- Generic branding (not BLKOUT-branded)
- Limited customization
- No audit trail features
- Responses stored in Google (data sovereignty concerns)

**Decision**: Reject - your custom solution performed better (67% in 1 hour). Google Forms would likely get slower responses due to lack of personalization.

### Alternative 2: Typeform / JotForm

**Pros:**
- Beautiful UI
- Good UX
- Conditional logic built-in
- Analytics

**Cons:**
- **Cost**: £25-70/month
- Still not personalized (can't pre-fill)
- Vendor lock-in
- Limited control over data

**Decision**: Reject - your GitHub Pages approach is free and performed excellently. Save budget for other tools.

### Alternative 3: Off-the-Shelf Member Management System

**Pros:**
- All-in-one (verification + member database + comms)
- Professional support
- Proven at scale

**Cons:**
- **Cost**: £500-2000/year
- Overkill for current size (9 members)
- Learning curve
- Less flexibility

**Decision**: Reject for now - revisit when BLKOUT grows to 50+ members

---

## Success Criteria & Definition of Done

### Phase 1 MVP is "Done" when:

- [ ] Can create new verification in <15 min
- [ ] Member experience matches your successful prototype (simple, fast, mobile-friendly)
- [ ] Dashboard shows real-time progress (who's responded, who hasn't)
- [ ] Export works (CSV with all responses)
- [ ] Successfully used for next verification (e.g., annual confirmation)
- [ ] Achieves 80%+ response rate within 2 hours (maintain your success)
- [ ] Documentation complete (how to create, send, track)

### Overall Project is "Successful" when:

- [ ] Used for 3+ different verification types
- [ ] Saves 2+ hours per verification (vs. custom build each time)
- [ ] Maintains 100% response rate within deadline
- [ ] Zero compliance issues related to missing verifications
- [ ] Full audit trail for all verifications (FCA-ready)

---

## Future Enhancements

- **WhatsApp Business API integration** (auto-send links, auto-reminders)
- **SMS reminders** (for members who don't use WhatsApp)
- **Verification history for members** (self-service portal - see all past confirmations)
- **Blockchain verification** (immutable, tamper-proof record)
- **Integration with voting system** (reuse for board elections)
- **Video confirmation option** (for high-stakes verifications)

---

## Open Questions

1. **Should members be able to edit responses after submission?** (Within 24h window? Or immutable?)
2. **What happens if a member reports their verification link was used by someone else?** (Security protocol?)
3. **Should we send email by default or stick with WhatsApp?** (Email = more formal, WhatsApp = faster response)
4. **What's the retention policy for old verifications?** (Keep forever? Archive after 7 years?)
5. **Who should have admin access?** (Robert only? All board members? Compliance officer?)

---

## Appendix: Your Successful Approach (Document for Replication)

### What Worked in CBS Affiliations Verification

**Message Format:**
- Ultra-short (4 lines)
- Clear action (click link)
- Clear deadline (Monday 17th, 10am)
- Friendly tone ("cross the registration line 🏛️")
- Personal sender (Rob, not "BLKOUT Admin")

**Delivery Method:**
- WhatsApp (where members already are)
- Not email (less immediate, might go to spam)

**Verification Page:**
- Clean, branded (blkoutuk.github.io)
- Mobile-optimized
- Personalized (showed each member their specific findings)
- Quick (2 minutes promise, actually delivered)
- Clear purpose (FCA requirement explained)

**Results:**
- 67% (6/9) in 1 hour
- Expect 100% (9/9) by end of day

**Key Insight**: Speed + Simplicity + Personal Touch = High Response Rate

This should be the template for all future verifications.

---

**Document Control:**
- **Version**: 1.0
- **Last Updated**: 14 November 2025
- **Next Review**: After Phase 1 completion
- **Owner**: BLKOUT Infrastructure Team
- **Reference**: Based on successful blkout-verification prototype (Nov 2025)
