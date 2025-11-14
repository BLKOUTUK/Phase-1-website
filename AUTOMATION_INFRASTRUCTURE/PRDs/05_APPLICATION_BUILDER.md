# Product Requirement Document
## Grant Funding Platform - Application Builder & Content Library

**Version**: 1.0
**Date**: 14 November 2025
**Owner**: BLKOUT Fundraising Team
**Status**: Proposed
**Part of**: Grant Funding Platform Core Architecture

---

## Executive Summary

Transform grant application creation from 8-12 hours of copy-paste and rewriting to 4-6 hours of focused, funder-specific writing by providing reusable content blocks, templates, and intelligent auto-population.

**Value Proposition**: Write each piece of content once (org description, team bios, beneficiary demographics), reuse across all applications. Focus writing time on what's unique to each funder.

---

## Problem Statement

### Current Application Process

**What takes 8-12 hours per application:**
1. **Setup** (30 min): Create new Google Doc, find funder's application template
2. **Org description** (45 min): Rewrite BLKOUT's mission/background for this funder's tone
3. **Team bios** (30 min): Copy-paste from previous apps, update, reformat
4. **Beneficiary demographics** (20 min): Find data from last report, rewrite
5. **Project description** (2 hours): Adapt project for this funder's priorities
6. **Budget** (1 hour): Rebuild budget spreadsheet, write narrative
7. **Supporting documents** (30 min): Find policies, letters, case studies
8. **Funder-specific questions** (3-4 hours): The unique part (can't automate)
9. **Formatting** (30 min): Match funder's template style
10. **Proofread** (30 min): Check for copy-paste errors (wrong funder name!)

**Key insight**: Steps 1-7 (50-60% of time) are **repetitive** - same content, different words each time.

### Pain Points

- ❌ **Reinventing the wheel**: Rewrite org description 15x/year
- ❌ **Copy-paste errors**: Accidentally leave previous funder's name in doc
- ❌ **Version drift**: Team bios in Application A don't match Application B (inconsistent)
- ❌ **Can't find content**: "Where did we write that case study?" (search 10 old apps)
- ❌ **No templates**: Start from blank page every time (unless funder provides template)
- ❌ **Duplicate effort**: Two people writing similar content for different grants

**From Grant-funding repo:**
- ✅ Application template exists (structure)
- ✅ Content library folder (but empty - no actual content blocks)
- ❌ No way to pull content into applications efficiently

---

## Goals & Success Metrics

### Primary Goals

1. **Reduce application drafting time by 40%** (from 8-12 hours → 4-6 hours)
2. **Eliminate copy-paste errors** (wrong funder name, outdated data)
3. **Content reuse >70%** (70%+ of each application uses existing content blocks)
4. **Consistent messaging** (BLKOUT described same way across all applications)
5. **Knowledge retention** (content library survives volunteer turnover)

### Success Metrics

| Metric | Current | Phase 1 Target | Phase 2 Target |
|--------|---------|----------------|----------------|
| Time per application | 8-12 hours | 5-7 hours | 4-6 hours |
| Copy-paste errors | 1-2 per batch | 0 | 0 |
| Content reuse | ~30% (manual copy) | 60% | 75%+ |
| Content blocks in library | 0 | 20 | 40+ |
| Applications completed/month | 1-2 | 3-4 | 5+ |

---

## Functional Requirements

### Phase 1: Content Library & Basic Templates (Month 1)

**FR1: Content Library (Airtable Table)**

**Purpose**: Central repository of reusable content blocks

**Content Block Structure:**
- Block ID (auto)
- Block name (e.g., "Org Description - 200 words", "Team Bio - Robert")
- Type (single-select: Org Description, Team, Beneficiaries, Project, Budget, Policy, Case Study, Letter of Support, Other)
- Content (long text, rich formatting)
- Word count (formula: length of content)
- Keywords/tags (multi-select: LGBTQ+, Black-led, Arts, Infrastructure)
- Versions (1.0, 1.1, 1.2 - track changes)
- Last updated (date, auto)
- Last updated by (user, auto)
- Used in applications (linked field → Applications table)

**Initial Content Blocks (20 to create):**

**Org Description:**
- Full (500 words) - comprehensive history, mission, activities
- Medium (200 words) - standard for most applications
- Short (100 words) - for character-limited forms
- One-sentence (50 words) - elevator pitch

**Team:**
- Robert Berkeley bio (200w, 100w, 50w versions)
- [Each founding member] bio (3 versions each)
- Collective team description (who we are as a group)

**Beneficiaries:**
- LGBTQ+ Black people demographics (who we serve)
- Geographic reach (UK-wide, focus areas)
- Impact numbers (if data available: X people reached, Y events, etc.)

**Projects:**
- [Specific project 1] description (e.g., "Cultural Infrastructure Hub")
- [Specific project 2] description
- Generic "community-led cultural space" description

**Budget:**
- Standard budget narrative template
- Cost categories explanation (why these costs)

**Policies:**
- Safeguarding policy (summary)
- Equality & diversity statement
- Environmental policy (if applicable)

**Case Studies:**
- Success story 1 (testimonial, outcome)
- Success story 2

**Letters of Support:**
- Template request letter
- Boilerplate for partners to use

**Effort**: 8-12 hours to write initial 20 blocks

**FR2: Application Template Library**

**Purpose**: Standard structures for common funder types

**Templates to Create:**

**1. Arts Council England Template**
- Sections: Project description, Artistic excellence, Public engagement, Resilience, Budget
- Guidance for each section
- Word limits noted
- Links to Arts Council criteria

**2. National Lottery Community Fund Template**
- Sections: What will you do?, Who will benefit?, How much will it cost?
- Max characters per section
- Links to Lottery guidance

**3. Trust/Foundation Template (Generic)**
- Sections: Cover letter, Org background, Project description, Budget, Supporting docs
- Adaptable to most trusts

**4. Government Grant Template**
- Sections: Executive summary, Need, Approach, Deliverables, Budget, Evidence of impact
- Formal tone guidance

**5. Custom Template (Blank)**
- Sections: Customizable
- For one-off funders

**Each template includes:**
- Section headers
- Guidance notes (what to include)
- Word/character limits (if applicable)
- Links to funder requirements
- Placeholder for content blocks (drag-drop zones)

**Effort**: 4-6 hours to create 5 templates

**FR3: Application Workspace (Airtable Record)**

**When**: Created after opportunity prioritized as "Apply"

**Application Record Structure:**
- Application ID (auto)
- Opportunity (linked to Opportunities table - pulls funder, grant, amount, deadline)
- Template used (linked to Templates table)
- Status (single-select: Draft, Review, Final, Submitted)
- Assigned to (user - lead writer)
- Reviewer (user - who checks before submit)
- Progress (formula: % of sections completed)
- Draft version (number: 1.0, 1.1, etc.)
- Sections (long text fields, one per template section):
  - Section 1: [Template section name]
  - Section 2: [Template section name]
  - etc.
- Attachments (file upload: supporting docs, final submission)
- Notes (long text: internal comments, questions)
- Submission date (date)
- Decision date (date)
- Word count (formula: total across all sections)

**Effort**: 2-3 hours (Airtable setup)

**FR4: Content Block Insertion (Manual)**

**Phase 1 = Copy-Paste Workflow:**
1. Writer opens Application record
2. Opens Content Library (separate Airtable view)
3. Finds relevant block (e.g., "Org Description - 200w")
4. Copies content
5. Pastes into Application section
6. Edits to customize for this funder (if needed)

**Tracking:**
- Mark which content blocks were used (linked field)
- Track reuse rate (analytics)

**Effort**: 0 hours (manual process, no dev)

### Phase 2: Smart Templates & Automation (Months 2-3)

**FR5: Auto-Populate from Opportunity Data**

**What auto-fills when Application created:**
- Funder name (from Opportunity.funder)
- Grant program name (from Opportunity.grant_name)
- Amount requesting (from Opportunity.amount)
- Deadline (from Opportunity.deadline)
- Cover letter header (auto-generate: "Dear [Funder], we are writing to apply for [Grant] for £[Amount]...")

**Technology**: Airtable automation or Zapier

**Effort**: 2-3 hours

**FR6: Content Block Suggestions**

**AI-Powered (Phase 2b):**
- Analyze funder's focus areas (e.g., "Arts, LGBTQ+, Community")
- Suggest relevant content blocks from library
- Example: Arts Council application → Suggests "Artistic Excellence" case study

**Manual (Phase 2a):**
- Template pre-selects default blocks
- Example: Arts Council template always includes "Org Description - 200w", "Team - Collective", "Beneficiaries - LGBTQ+ Black"

**Effort**: 3-4 hours (manual), 10-15 hours (AI)

**FR7: Version Control & Collaboration**

**Features:**
- Draft versions (1.0, 1.1, 1.2) - track changes
- Comments (reviewer leaves feedback on sections)
- Change history (who edited what when)
- Approval workflow: Writer → Reviewer → Approved → Submit

**Technology**: Airtable native (comments, version via draft number) OR Google Docs integration

**Effort**: 1-2 hours (Airtable) OR 4-6 hours (Google Docs integration)

### Phase 3: AI Writing Assistant (Months 6+)

**FR8: AI-Powered Drafting**

**Features:**
- Generate first draft from project description + funder criteria
- Tone matching (formal for government, warm for community trusts)
- Compliance checking (flag if doesn't meet eligibility)
- Similarity detection (warn if too similar to rejected application)

**Technology**: OpenAI API, fine-tuned on successful BLKOUT applications

**Effort**: 25-35 hours

**FR9: Budget Generator**

**Features:**
- Template budget line items
- Auto-calculate totals, percentages
- Generate budget narrative from line items
- Export to Excel (funder-required format)

**Technology**: Airtable formula + scripting OR separate tool

**Effort**: 10-15 hours

---

## Data Model

### Content Library Table

```
content_blocks
├── id (auto)
├── name (text: "Org Description - 200w")
├── type (single-select: Org, Team, Beneficiaries, Project, Budget, Policy, Case Study, Letter, Other)
├── content (long text, rich formatting)
├── word_count (formula)
├── tags (multi-select: LGBTQ+, Black-led, Arts, etc.)
├── version (text: "1.0", "1.1")
├── is_current (checkbox: latest version)
├── supersedes (link to older version, if applicable)
├── last_updated (date, auto)
├── last_updated_by (user)
├── used_in_applications (linked field → applications)
└── usage_count (rollup: count of linked applications)
```

### Applications Table

```
applications (extends core architecture)
├── opportunity_id (link to opportunities)
├── funder (rollup from opportunity)
├── grant_name (rollup from opportunity)
├── amount_requesting (rollup from opportunity)
├── deadline (rollup from opportunity)
├── template_used (link to templates)
├── status (Draft, Review, Final, Submitted)
├── assigned_to (user)
├── reviewer (user)
├── progress (formula: % sections completed)
├── draft_version (number)
├── sections (long text fields):
│   ├── section_1_name, section_1_content
│   ├── section_2_name, section_2_content
│   └── section_N_name, section_N_content
├── content_blocks_used (linked field → content_blocks)
├── attachments (file upload)
├── notes (long text)
├── word_count_total (formula)
├── submitted_date (date)
├── decision_date (date)
└── outcome (link to decisions table - separate PRD)
```

### Templates Table

```
application_templates
├── id (auto)
├── name (text: "Arts Council NPO", "Lottery Awards for All")
├── funder_type (Foundation, Government, Lottery, Trust, Generic)
├── sections (long text, JSON):
│   [
│     {name: "Project Description", guidance: "...", word_limit: 500},
│     {name: "Budget", guidance: "...", word_limit: null}
│   ]
├── default_content_blocks (linked field → content_blocks)
├── guidance_notes (long text)
├── example_application (file upload: previous successful app)
└── last_used (date)
```

---

## User Stories

### As a Grant Writer
> "I'm drafting an Arts Council application. I need to describe BLKOUT in 200 words. I've written this 10 times before. I want to reuse what I wrote last time (it was approved!)."

**Acceptance Criteria:**
- Open Content Library
- Search "org description 200"
- Find block, copy content
- Paste into Arts Council application section
- Edit 2-3 sentences to customize for Arts Council tone
- Done in 5 minutes (vs. 45 minutes rewriting from scratch)

### As a Fundraising Lead
> "We're applying to 3 grants this month (Arts Council, Lottery, Local Authority). They all ask for team bios. I want to write Robert's bio once, use it in all 3 applications."

**Acceptance Criteria:**
- Write Robert's bio (200w) in Content Library
- Create 3 applications (Arts Council, Lottery, Local Authority)
- Insert Robert's bio into all 3 (copy-paste or drag-drop)
- Each application pulls same content
- If Robert's bio updated (new accomplishment), update in library → all applications reflect change

### As a Reviewer
> "I'm reviewing a draft application before submission. I need to leave feedback on specific sections without editing the writer's work directly."

**Acceptance Criteria:**
- Open application in Review status
- Read each section
- Add comments: "Section 2: Great description, but shorten by 50 words to meet limit"
- Writer receives notification
- Writer edits based on feedback
- Reviewer approves → Status changes to Final

---

## Integration Points

### Input (What This Module Needs)

**From Opportunity Discovery:**
- Opportunity record (funder, grant name, amount, deadline, URL)
- Trigger: When opportunity prioritized as "Apply"

**From Core Architecture:**
- Access to `applications` table (write new application records)
- Access to `content_blocks` table (read content for insertion)
- Access to `templates` table (read template structure)

### Output (What This Module Provides)

**To Pipeline Manager:**
- Application status (Draft, Review, Final, Submitted)
- Progress % (for dashboard visualization)
- Deadline (inherited from opportunity)

**To Analytics:**
- Content block usage data (which blocks used most? Reuse rate?)
- Application success data (which templates → awards? Which content → success?)

**To Document Generation:**
- Final application content (for cover letter generation, if integrated)

---

## Workflow

### Application Creation to Submission Flow

```
1. [Opportunity prioritized as "Apply"]
   └─ User clicks "Create Application"

2. [Application Workspace Created]
   ├─ Pull from Opportunity: funder, grant, amount, deadline
   ├─ User selects template (or "Custom")
   ├─ Template sections auto-populate as empty fields
   ├─ Status = "Draft"
   └─ Assigned to = Current user

3. [Writer Drafts Application]
   ├─ Open Content Library (side panel or separate view)
   ├─ Find relevant blocks:
   │   ├─ "Org Description - 200w" → Copy → Paste into Section 1
   │   ├─ "Team Bio - Robert" → Copy → Paste into Section 2
   │   └─ "Beneficiaries" → Copy → Paste into Section 3
   ├─ Write custom content for funder-specific sections (unique part)
   ├─ Upload supporting docs (attachments)
   └─ Progress updates automatically (% of sections completed)

4. [Mark for Review]
   ├─ Writer sets Status = "Review"
   ├─ Assigns Reviewer
   └─ Reviewer notified (Slack/email)

5. [Reviewer Provides Feedback]
   ├─ Reviewer reads all sections
   ├─ Adds comments/notes
   └─ Options:
       ├─ Approve → Status = "Final"
       └─ Request changes → Status back to "Draft"

6. [Finalize & Submit]
   ├─ Writer addresses feedback (if any)
   ├─ Status = "Final"
   ├─ Export to PDF/Word (if needed)
   ├─ Submit to funder (external process)
   ├─ Record submission:
   │   ├─ Status = "Submitted"
   │   ├─ Submitted_date = Today
   │   └─ Upload submission confirmation (if received)
   └─ Pipeline Manager triggers decision reminder

7. [Post-Submission]
   ├─ Application archived (visible in history)
   ├─ Content blocks marked as "used in [Application X]"
   └─ Await decision (tracked in Pipeline Manager)
```

---

## Technical Implementation

### Phase 1: Airtable

**Tables:**
- Content Library (content_blocks)
- Applications
- Templates

**Views:**
- Content Library: Grid view (all blocks), Gallery view (by type), Search view
- Applications: Kanban by status, Calendar by deadline, List by assigned

**Forms:**
- None needed (use Airtable interface)

**Integrations:**
- None yet (manual copy-paste workflow)

**Cost**: Free (or £20/month if >1,200 records)

**Effort**: 15-20 hours (setup + populate initial content)

### Phase 2: Airtable + Zapier (If Automation Needed)

**Automations:**
- Opportunity prioritized → Auto-create Application record
- Application submitted → Notify Pipeline Manager
- Reviewer assigned → Send email/Slack

**Integrations:**
- Google Docs (optional): Link to Docs for collaborative editing
- Slack: Notifications

**Cost**: £0-40/month (Zapier)

**Effort**: 6-10 hours

### Phase 3: Custom Build (If Outgrow Airtable)

**Stack:**
- Frontend: Next.js (rich text editor, drag-drop content blocks)
- Backend: Next.js API
- Database: Supabase
- Rich text: Tiptap or Quill
- File storage: Supabase Storage

**Effort**: 40-60 hours

---

## Quality & Validation

### Content Accuracy

**Challenge**: Ensuring content blocks stay current

**Solution:**
- Annual review (January): Review all blocks, update if needed
- Version control: Keep old versions, mark which is current
- Ownership: Assign each block to a team member (responsible for keeping updated)

### Consistency

**Challenge**: Applications use different versions of same content

**Solution:**
- Always use latest version (marked `is_current = true`)
- Alert if using old version

### Completeness

**Challenge**: Applications submitted with missing sections

**Solution:**
- Progress tracker (can't mark "Final" until 100% complete)
- Required fields (template specifies which sections mandatory)
- Checklist before submit

---

## Success Criteria

### Phase 1 is "Done" when:

- [ ] Content Library has 20+ blocks
- [ ] 5 templates created (Arts Council, Lottery, Trust, Government, Custom)
- [ ] First application drafted using content library (50%+ content reused)
- [ ] Application time reduced from 8-12 hours to 5-7 hours
- [ ] Zero copy-paste errors (funder name, outdated data)

### Overall Success (6 months):

- [ ] 40+ content blocks in library
- [ ] 10+ applications completed using content library
- [ ] Content reuse rate >70%
- [ ] Application drafting time consistently 4-6 hours
- [ ] Team reports confidence in content quality/consistency

---

## Risks & Mitigation

### Risk 1: Content Library Neglect (Blocks Get Stale)

**Likelihood**: Medium
**Impact**: High (applications use outdated info)

**Mitigation:**
- Annual review calendar reminder
- Flag blocks not updated in 12 months (alert owner)
- Versioning (always know which is current)

### Risk 2: Over-Reliance on Templates (Lose Funder-Specific Nuance)

**Likelihood**: Medium
**Impact**: Medium (applications feel generic)

**Mitigation:**
- Guidance: "Content blocks are starting points, always customize"
- Training: Emphasize funder research, not just template filling
- Review process: Reviewer checks for funder-specific language

### Risk 3: Knowledge Hoarding (Writer Doesn't Add to Library)

**Likelihood**: Low (if incentivized)
**Impact**: Medium (library stays small, less reusable)

**Mitigation:**
- Policy: All applications must add at least 1 new content block (e.g., funder-specific case study)
- Recognize contributions (monthly "Content Block Champion")
- Make it easy (add block button in Application view)

---

## Next Steps

1. **Populate Content Library** (8-12 hours):
   - Write 20 initial content blocks
   - Organize by type
   - Set is_current = true for latest versions

2. **Create Templates** (4-6 hours):
   - Arts Council, Lottery, Trust/Foundation, Government, Custom
   - Document section structure, guidance, word limits

3. **Set up Applications table** (2-3 hours):
   - Configure fields
   - Link to Opportunities, Content Blocks, Templates

4. **Pilot test** (Week 1):
   - Draft 1 application using content library
   - Time the process (did it save time?)
   - Gather feedback (what's missing? What's clunky?)

5. **Iterate** (Week 2):
   - Add missing content blocks
   - Fix workflow issues
   - Train team

6. **Scale** (Month 2+):
   - Use for all applications
   - Track reuse rate, time savings
   - Continuous improvement

---

**Document Control:**
- **Version**: 1.0
- **Last Updated**: 14 November 2025
- **Next Review**: After Phase 1 pilot
- **Owner**: BLKOUT Fundraising Team
- **Dependencies**: Core Architecture, Opportunity Discovery (must have opportunities to apply to)
- **Priority**: HIGH - Core workflow for grant applications
