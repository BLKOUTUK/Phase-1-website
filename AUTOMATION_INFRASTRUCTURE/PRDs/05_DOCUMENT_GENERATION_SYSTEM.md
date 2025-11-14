# Product Requirement Document
## Document Generation System

**Version**: 1.0
**Date**: 14 November 2025
**Owner**: BLKOUT Infrastructure Team
**Status**: Proposed

---

## Executive Summary

Automate the creation of repetitive documents (member emails, FCA letters, reports, meeting minutes, etc.) using templates and data merges. Eliminate copy-paste errors and save hours of formatting time.

**Value Proposition**: What took you 2 hours to create 8 personalized member emails could take 5 minutes with automated document generation.

---

## Problem Statement

### What You Just Experienced

**CBS Affiliations Member Emails (Nov 2025):**

You manually created 8 personalized emails for founding members. Each email required:
- ✅ Personalized greeting (member name)
- ✅ Customized findings (their specific affiliations)
- ✅ Customized confirmation questions (different for members with 0 vs. 1 vs. 3 affiliations)
- ✅ Conflict of interest section (only for Olamide and Cardew)
- ✅ Consistent formatting and tone across all 8

**Time spent**: ~2 hours to draft all 8 emails manually

**With automation**: Could have been 5 minutes
- Load member data (CSV or database)
- Select template ("Member Affiliations Confirmation")
- Click "Generate" → 8 personalized emails ready to send

### Other Documents You'll Need to Generate Repeatedly

**Member Communications:**
- Welcome emails for new members (personalized with their role, date joined, etc.)
- Annual confirmations (affiliations, contact details, membership renewal)
- Event invitations (personalized RSVPs)
- Policy acknowledgment requests

**Compliance Documents:**
- FCA response letters (vary by query type, but structure similar)
- Annual return cover letters
- Member lists (formatted for FCA submission)
- Meeting minutes (consistent format, variable content)

**Funder Communications:**
- Grant application cover letters (personalized to each funder)
- Award acceptance letters
- Progress reports (quarterly/annual)
- Budget narratives (auto-generate from spreadsheet)

**Internal Documents:**
- Board papers (consistent format, variable agenda)
- Committee reports
- Volunteer agreements (personalized to role/dates)
- Reference letters

### Pain Points of Manual Document Creation

1. **Time-consuming**: Repetitive typing/formatting
2. **Error-prone**: Copy-paste mistakes, forgot to change name, etc.
3. **Inconsistent**: Formatting varies between documents
4. **Not scalable**: 8 members = manageable, 50 members = nightmare
5. **Knowledge loss**: If template is in one person's head, hard to handover

---

## Goals & Success Metrics

### Primary Goals

1. **Reduce document creation time by 80%**
2. **Eliminate personalization errors** (wrong name, wrong data)
3. **Ensure consistency** (all docs follow same format/tone)
4. **Enable non-technical users** to generate docs (no coding required)
5. **Maintain quality** (generated docs are professional, accurate)

### Success Metrics

| Metric | Current (Manual) | Target (Automated) | Timeline |
|--------|------------------|-------------------|----------|
| Time to create 8 member emails | 2 hours | 5 min | Phase 1 |
| Personalization errors | 1-2 per batch (estimate) | 0 | Phase 1 |
| Time to create FCA letter | 30-45 min | 5 min | Phase 1 |
| Templates available | 0 (ad-hoc) | 10+ | Phase 1-2 |
| Users who can generate docs | 1 (technical person) | All team (4+) | Phase 1 |
| Document consistency score | 60% (varies by author) | 95%+ (template-driven) | Phase 1 |

### Key Performance Indicators

- **Time saved per month**: Target 5-10 hours
- **Documents generated**: Target 50-100/year (emails, letters, reports)
- **Error rate**: <0.5% (less than 1 error per 200 documents)
- **User adoption**: 80% of team uses system for repetitive docs
- **Template library growth**: 20+ templates by end of Year 1

---

## User Stories

### As a CBS Secretary
> "I need to send an FCA response letter. I've written 5 similar letters before, but I always start from scratch and worry I've forgotten something important. I want a template that ensures I include all required sections."

**Acceptance Criteria:**
- Select "FCA Response Letter" template
- Fill in form: query type, reference number, date, specific details
- Click "Generate" → professional letter ready
- Download as Word/PDF
- Edit if needed before sending

### As a Membership Coordinator
> "10 new members joined this month. I need to send each a welcome email with their name, role, join date, and next steps. Doing this manually for 10 people takes 2 hours."

**Acceptance Criteria:**
- Upload CSV of new members (name, email, role, join date)
- Select "New Member Welcome Email" template
- Click "Generate" → 10 personalized emails created
- Review (quick scan)
- Send via email or export to Gmail/Mailchimp

### As a Fundraising Lead
> "I'm applying to 5 grants this month. Each needs a cover letter with funder name, program officer, grant amount, project name. These are 90% identical except for those variables."

**Acceptance Criteria:**
- Select "Grant Cover Letter" template
- Enter variables (funder, officer, amount, project)
- Click "Generate" → professional cover letter
- Merge with application PDF
- Submit

### As a Board Member
> "I need to write minutes from last night's board meeting. The format is always the same (attendees, apologies, decisions, actions) but I spend 30 min formatting."

**Acceptance Criteria:**
- Select "Board Meeting Minutes" template
- Fill in form: date, attendees, agenda items, decisions, actions
- Click "Generate" → formatted minutes (Markdown or Word)
- Review/edit
- Share with board

### As a Grants Reporting Officer
> "I need to submit quarterly reports to 3 funders. Each has slightly different format, but the data is the same (beneficiary numbers, activities, spend). Currently I manually rewrite for each funder."

**Acceptance Criteria:**
- Enter data once (beneficiaries, activities, spend)
- Select funder templates (Arts Council, Lottery, Local Authority)
- Click "Generate All" → 3 customized reports
- Download/submit

---

## Functional Requirements

### Core Features (Phase 1)

**FR1: Template Library**

**Pre-built templates for common use cases:**
- Member welcome email
- Annual member confirmation email
- FCA response letter
- Grant cover letter
- Meeting minutes (board, AGM)
- Policy acknowledgment request
- Reference letter
- Volunteer agreement

**Each template includes:**
- **Variables** (placeholders: {member_name}, {date}, {amount}, etc.)
- **Conditional sections** (show/hide based on data: "If member has affiliations, show conflict of interest section")
- **Formatting** (consistent styling, fonts, spacing)
- **Guidance** (instructions for filling out template)

**FR2: Data Input Methods**

**Single Record (One Document):**
- Form-based input (fill in variables one by one)
- Quick and simple for one-off documents

**Bulk Generation (Multiple Documents):**
- CSV upload (rows = records, columns = variables)
- Database connection (pull from member database, if integrated)
- Example: Upload 10 members → Generate 10 personalized emails

**FR3: Document Generation Engine**

- **Merge variables** into template
- **Process conditional logic** (if/then, show/hide)
- **Format output** (respect line breaks, lists, tables)
- **Generate preview** (before finalizing)
- **Support multiple formats**: Markdown, Word (.docx), PDF, HTML

**FR4: Preview & Edit**

- **Live preview** (see document before generating)
- **Edit after generation** (make manual tweaks)
- **Save edited version** (don't lose changes)
- **Regenerate** (if data changes, can regenerate without losing edits)

**FR5: Output & Export**

**Download formats:**
- Word (.docx) - for further editing
- PDF - for formal submission
- Markdown - for GitHub/documentation
- HTML - for email (formatted)
- Plain text - for simple emails

**Send options:**
- Download (manual send)
- Copy to clipboard (paste into email client)
- Email integration (Phase 2: auto-send via SendGrid/Mailgun)

**FR6: Template Management**

- **Create new templates** (admin only, or all users depending on config)
- **Edit existing templates** (update wording, add variables)
- **Version control** (track changes to templates)
- **Categorize** (by type: Member Comms, Compliance, Funders, Internal)
- **Search** (find template by name or keyword)

### Enhanced Features (Phase 2)

**FR7: Advanced Conditional Logic**

- **If/else**: "If member_type == 'founding', show Section A, else show Section B"
- **Loops**: "For each affiliation, list organization name and role"
- **Calculations**: "Total budget = sum of line items"
- **Date math**: "Deadline = today + 30 days"

**FR8: Email Integration**

- **Auto-send** via SMTP (SendGrid, Mailgun, Gmail)
- **Bulk send** (generate 10 emails → send all at once)
- **Track opens/clicks** (if using email service provider)
- **Merge with CRM** (if member database integrated)

**FR9: Rich Formatting**

- **Tables** (auto-generate from data)
- **Charts** (embed simple charts in reports)
- **Images** (insert logos, signatures)
- **Headers/footers** (consistent branding)

**FR10: Approval Workflows**

- **Draft → Review → Approve → Send**
- **Assign reviewers** (secretary reviews before member sends)
- **Track status** (who's reviewed, who hasn't)
- **Version history** (compare draft vs. final)

**FR11: Multi-Language Support**

- **Templates in multiple languages** (English, others if needed)
- **Auto-select language** based on member preference
- **Translation memory** (reuse translated phrases)

**FR12: Integration with Other Systems**

- **Pull data from Member Verification System** (auto-populate member details)
- **Pull data from Funding Pipeline** (auto-populate grant details)
- **Pull data from CBS Compliance Dashboard** (auto-populate filing details)
- **Webhook notifications** (alert when document generated)

### Advanced Features (Phase 3)

**FR13: AI-Powered Template Suggestions**

- **Analyze document** (upload existing letter)
- **AI suggests template** (identify structure, variables)
- **One-click convert** to reusable template

**FR14: Natural Language Generation**

- **AI writes first draft** from bullet points
- **Tone adjustment** (formal, casual, urgent)
- **Compliance checking** (flag if missing required info)

**FR15: Collaborative Editing**

- **Real-time co-editing** (Google Docs style)
- **Comments/suggestions** (team feedback on draft)
- **Track changes** (see who changed what)

---

## Technical Requirements

### Technology Stack

**Recommended Approach (Phased):**

**Phase 1: Google Docs + Autocrat (No-Code)**

**Why Google Docs + Autocrat?**
- **Autocrat** is a free Google Sheets add-on for mail merge
- **No coding required** (anyone can set up)
- **Free** (no cost)
- **Familiar** (Google Docs/Sheets interface)
- **Quick setup** (30 min - 1 hour per template)

**How it works:**
1. Create template in Google Docs with {{variable}} placeholders
2. Create data sheet in Google Sheets (rows = records, columns = variables)
3. Install Autocrat add-on
4. Configure merge (link template to data)
5. Run → generates personalized docs

**Limitations:**
- Basic conditional logic only
- No complex loops
- Manual process (not fully automated)
- Clunky for bulk operations >50 docs

**Good for**: Phase 1, validate concept, immediate value

**Phase 2: Pandoc + Markdown Templates (Low-Code)**

**Why Pandoc?**
- **Command-line tool** for document conversion
- **Supports variables** and simple conditionals
- **Markdown → Word/PDF** (beautiful output)
- **Free and open-source**
- **Scriptable** (can automate via GitHub Actions or cron jobs)

**How it works:**
1. Write template in Markdown with {{variable}} syntax
2. Create YAML data file (or CSV)
3. Run command: `pandoc template.md --metadata-file=data.yaml -o output.docx`
4. Output: Professional Word doc

**Limitations:**
- Requires command-line skills (or web wrapper)
- Less user-friendly than Google Docs
- Limited visual preview

**Good for**: Phase 2, more control, better for GitHub-centric workflow

**Phase 3: Custom Web App (Full Control)**

**Stack:**
- **Frontend**: Next.js (React)
- **Backend**: Next.js API routes
- **Template Engine**: Handlebars or Mustache (variable substitution)
- **Document Generation**: Docxtemplater (Word docs), jsPDF (PDFs), Marked (Markdown)
- **Database**: Supabase (store templates, generated docs)
- **Hosting**: Vercel

**Pros:**
- Full customization
- Beautiful UI
- Complex logic supported
- Integration-ready

**Cons:**
- Development time: 30-40 hours
- Requires maintenance

**Good for**: Phase 3, if BLKOUT scales significantly

**Recommended Path**: Start with **Google Docs + Autocrat** (Phase 1), migrate to **Pandoc** (Phase 2) for GitHub integration, consider **custom app** (Phase 3) only if >100 docs/month.

### Data Model (If Building Custom)

**Templates Table:**
```sql
document_templates (
  id: uuid PRIMARY KEY,
  name: text,
  category: text, -- "member_comms", "compliance", "funders", "internal"
  description: text,
  template_content: text, -- Markdown with {{variables}}
  variables: jsonb, -- [{name: "member_name", type: "text", required: true}, ...]
  conditionals: jsonb, -- [{if: "member_type == 'founding'", show: "section_a"}, ...]
  output_formats: text[], -- ["docx", "pdf", "md"]
  created_by: uuid,
  created_at: timestamp,
  version: integer,
  is_active: boolean
)
```

**Generated Documents Table:**
```sql
generated_documents (
  id: uuid PRIMARY KEY,
  template_id: uuid FOREIGN KEY,
  data_source: jsonb, -- variables used {member_name: "Robert", date: "2025-11-14"}
  output_format: text,
  file_url: text, -- S3/Supabase storage URL
  generated_at: timestamp,
  generated_by: uuid,
  status: text, -- "draft", "final", "sent"
)
```

### Security & Privacy

**Data Protection:**
- **Personal data** (names, emails, DOBs) in templates → encrypt at rest
- **Access control** (who can create templates, who can generate docs)
- **Audit trail** (log all document generations: who, when, what data)

**Template Security:**
- **Version control** (track changes, prevent accidental deletion)
- **Approval required** (for sensitive templates like FCA letters)
- **Backup** (daily backup of all templates)

**Data Minimization:**
- Only collect variables needed for template
- Don't store full documents indefinitely (purge after 2 years if not compliance-related)
- Delete member data when they leave (GDPR right to erasure)

---

## Implementation Phases

### Phase 1: Google Docs + Autocrat (Week 1) - IMMEDIATE VALUE

**Deliverables:**
- [ ] Set up Google Workspace (if not already)
- [ ] Install Autocrat add-on
- [ ] Create 5 core templates:
  1. Member welcome email
  2. Annual member confirmation email
  3. FCA response letter
  4. Grant cover letter
  5. Meeting minutes
- [ ] Test each template (generate 3-5 sample docs)
- [ ] Write user guide (how to use Autocrat)
- [ ] Train team (30 min workshop)

**Effort**: 4-6 hours
**Priority**: HIGH (immediate ROI)

**Success Criteria:**
- All 5 templates working
- Team successfully generates docs without assistance
- First "real" doc generated (e.g., next FCA letter uses template)

### Phase 2: Pandoc + GitHub Integration (Month 2-3)

**Deliverables:**
- [ ] Convert Google Docs templates to Markdown
- [ ] Set up Pandoc on GitHub Actions (or local CLI)
- [ ] Create web form for variable input (simple HTML form)
- [ ] Automate generation (form submit → Pandoc runs → doc downloads)
- [ ] Version control templates in GitHub
- [ ] Expand library to 15+ templates

**Effort**: 12-18 hours
**Priority**: MEDIUM

**Success Criteria:**
- Markdown templates in GitHub
- Anyone can generate doc via web form (no command-line needed)
- Output quality matches/exceeds Google Docs

### Phase 3: Custom Web App (Month 6+)

Only pursue if generating >100 docs/month or if complex conditionals needed.

**Deliverables:**
- [ ] Build Next.js app with template editor
- [ ] Beautiful UI for template creation
- [ ] Advanced conditional logic
- [ ] Email integration (auto-send)
- [ ] API for integrations

**Effort**: 30-40 hours
**Priority**: LOW (nice-to-have, not urgent)

---

## Dependencies

### External Dependencies

- **Google Workspace** (if using Phase 1 approach) - Free or £4/user/month
- **Pandoc** (if using Phase 2 approach) - Free, open-source
- **GitHub** (for version control, already have)

### Internal Dependencies

- **Template content** (need to write initial templates)
- **User training** (team needs to learn tool)
- **Data sources** (member list, funder list, etc.)

---

## Risks & Mitigation

### Risk 1: Templates Become Stale (Not Updated)

**Likelihood**: Medium (templates need maintenance)
**Impact**: Medium (generate docs with outdated info)

**Mitigation:**
- **Annual review** (review all templates in January)
- **Version control** (track when last updated)
- **Feedback loop** (team reports issues with templates)
- **Owner per template** (someone responsible for keeping it current)

### Risk 2: Over-Reliance on Templates (Lose Personal Touch)

**Likelihood**: Medium (temptation to use template for everything)
**Impact**: Low (some docs should be personalized)

**Mitigation:**
- **Guideline**: Use templates for repetitive docs, customize for high-stakes (e.g., funder relationship building)
- **Edit after generation** (always review, add personal touches)
- **Not a replacement for judgment** (template is starting point, not final product)

### Risk 3: Data Errors (Wrong Data in Template)

**Likelihood**: Medium (garbage in, garbage out)
**Impact**: High (send email with wrong person's name = embarrassing)

**Mitigation:**
- **Preview before send** (always review generated doc)
- **Data validation** (check member name, email before merge)
- **Test with dummy data** (before bulk send, test with 3-5 records)

---

## Success Criteria & Definition of Done

### Phase 1 is "Done" when:

- [ ] 5 core templates created and tested
- [ ] Team can generate docs without assistance
- [ ] First 10 "real" docs generated (not test data)
- [ ] Time saved: At least 3 hours in first month
- [ ] Zero data errors in first 20 docs

### Overall Project is "Successful" when:

- [ ] 20+ templates available
- [ ] 100+ docs generated in Year 1
- [ ] Document creation time reduced by 80%
- [ ] Zero personalization errors
- [ ] Team reports high satisfaction (docs are professional, consistent)

---

## Immediate Next Steps

1. **Decide on Phase 1 approach** (Google Docs + Autocrat recommended)
2. **Identify first 3 templates to create** (likely: member email, FCA letter, grant cover letter)
3. **Gather sample data** (CSV of members for testing)
4. **Set up Autocrat** (1 hour)
5. **Create first template** (1 hour)
6. **Test with real data** (30 min)
7. **Generate first batch of docs** (e.g., next member communication)

---

## Appendix: Example Template (Member Welcome Email)

**Template (Markdown with variables):**

```markdown
Subject: Welcome to BLKOUT, {{member_name}}!

Hi {{member_name}},

Welcome to BLKOUT Community Benefit Society! We're thrilled to have you join as a {{member_type}}.

Your membership officially started on {{join_date}}.

**What happens next:**

1. **Review our founding Rules**: [link to Rules]
2. **Join our Slack/Discord**: [invite link]
3. **Attend our next event**: {{next_event_name}} on {{next_event_date}}

{% if member_type == "founding" %}
As a founding member, you'll also need to:
- Complete your affiliations disclosure (separate email coming)
- Attend the first AGM on {{agm_date}}
{% endif %}

If you have any questions, reply to this email or reach out to {{contact_person}}.

Looking forward to working with you!

Best,
{{sender_name}}
{{sender_role}}
BLKOUT Community Benefit Society
```

**Data (CSV):**

```csv
member_name,member_type,join_date,next_event_name,next_event_date,contact_person,sender_name,sender_role
Lloyd Young,founding,2025-11-01,Winter Social,2025-12-15,Robert,Robert Berkeley,Secretary
Jane Doe,general,2025-11-10,Winter Social,2025-12-15,Robert,Robert Berkeley,Secretary
```

**Output for Lloyd:**

```
Subject: Welcome to BLKOUT, Lloyd Young!

Hi Lloyd,

Welcome to BLKOUT Community Benefit Society! We're thrilled to have you join as a founding member.

Your membership officially started on 2025-11-01.

**What happens next:**

1. **Review our founding Rules**: [link to Rules]
2. **Join our Slack/Discord**: [invite link]
3. **Attend our next event**: Winter Social on 2025-12-15

As a founding member, you'll also need to:
- Complete your affiliations disclosure (separate email coming)
- Attend the first AGM on 2026-11-01

If you have any questions, reply to this email or reach out to Robert.

Looking forward to working with you!

Best,
Robert Berkeley
Secretary
BLKOUT Community Benefit Society
```

**Time saved**: Manual = 10 min per email. Automated = 30 sec per email (after template created).

---

**Document Control:**
- **Version**: 1.0
- **Last Updated**: 14 November 2025
- **Next Review**: After Phase 1 implementation
- **Owner**: BLKOUT Infrastructure Team
- **Priority**: MEDIUM-HIGH (immediate value, low effort)
