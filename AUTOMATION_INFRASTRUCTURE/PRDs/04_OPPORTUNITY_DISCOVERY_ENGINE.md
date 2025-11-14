# Product Requirement Document
## Grant Funding Platform - Opportunity Discovery Engine

**Version**: 1.0
**Date**: 14 November 2025
**Owner**: BLKOUT Fundraising Team
**Status**: Proposed
**Part of**: Grant Funding Platform Core Architecture

---

## Executive Summary

Automate the discovery and intake of grant funding opportunities through RSS monitoring, email forwarding, web scraping, and manual entry - ensuring BLKOUT never misses a relevant opportunity.

**Value Proposition**: Transform monthly manual landscape scanning into continuous automated discovery, finding 3-5x more opportunities with less effort.

---

## Problem Statement

### Current Manual Process

**Grant-funding repo** includes monthly scanning plan:
- First Monday of each month
- Manual website checks (Arts Council, Lottery, local authorities, etc.)
- Google Alerts (inconsistent, misses opportunities)
- Word of mouth (unreliable, late notification)

**Pain points:**
- ❌ **Monthly = Gaps**: Grants announced mid-month might be missed
- ❌ **Manual = Time-consuming**: 2-3 hours every first Monday
- ❌ **Reactive**: Only find what we actively search for
- ❌ **No tracking**: Discovered opportunities written in notes, forgotten
- ❌ **Inconsistent**: Depends on who does scan, what mood they're in

**Example miss:**
- Grant opens June 5th, deadline July 15th (6 weeks)
- Monthly scan is first Monday (June 3rd - miss it, or June 30th - only 2 weeks left)
- Discover too late to write quality application

---

## Goals & Success Metrics

### Primary Goals

1. **Find 3-5x more opportunities** (from ~20/year to 60-100/year discovered)
2. **Reduce manual scanning time** (from 2-3 hours/month to 30 min/month review)
3. **Early discovery** (find grants average 8+ weeks before deadline vs. 4 weeks currently)
4. **Comprehensive coverage** (monitor 30+ funder sources vs. 10 currently)
5. **Zero missed opportunities** (in monitored categories)

### Success Metrics

| Metric | Current (Manual) | Phase 1 Target | Phase 2 Target |
|--------|------------------|----------------|----------------|
| Opportunities discovered | ~20/year | 50/year | 100+/year |
| Time spent scanning | 2-3 hours/month | 30 min/month (review) | 15 min/month (AI-filtered) |
| Average notice period | 4 weeks | 6 weeks | 8+ weeks |
| Funder sources monitored | ~10 | 20 | 30+ |
| False positives | N/A | <20% | <10% |
| Discovery completeness | ~60% (estimate) | 80% | 95% |

---

## Functional Requirements

### Phase 1: Semi-Automated Discovery (Month 1)

**FR1: Manual Opportunity Intake Form**

**Purpose**: Easy way to add opportunities found manually or via word-of-mouth

**Fields:**
- Funder name (text, required)
- Grant program name (text, required)
- Amount (currency, required) - can be range
- Deadline (date, required)
- URL (link, required)
- Eligibility criteria (long text)
- Description (long text)
- Keywords (multi-select: LGBTQ+, Black communities, Arts, Cultural infrastructure, etc.)
- Source (single select: Web search, Email alert, Word of mouth, RSS feed, Other)
- Discovered by (user, auto-filled)
- Discovered date (date, auto-filled)

**Integration**: Form submission creates record in `opportunities` table, triggers priority scoring

**Access**: Public form (team members can submit from anywhere) OR internal-only

**Effort**: 1-2 hours (Airtable form creation)

**FR2: Email Forwarding Integration**

**How it works:**
1. Team receives grant alert email (from funder, Google Alert, etc.)
2. Forward to special email address (e.g., grants@blkout.uk.coop)
3. System parses email, extracts:
   - Funder name (from sender or subject)
   - Grant program (from subject line)
   - URL (first link in body)
   - Deadline (date recognition in body)
4. Auto-creates opportunity record (status: "Needs Review" - human confirms details)

**Technology**:
- Zapier: Email Parser trigger → Airtable create record action
- Or: Custom email parser (if budget for development)

**Effort**: 3-4 hours (Zapier setup + testing)

**FR3: Funder Database (Monitor List)**

**Purpose**: Track which funders to monitor, their typical grant cycles

**Fields**:
- Funder name
- Type (Foundation, Government, Lottery, Trust, Corporate)
- Website URL
- RSS feed URL (if available)
- Typical grant cycle (annual, quarterly, rolling)
- Focus areas (multi-select: Arts, LGBTQ+, etc.)
- Last checked date
- Monitor status (Active, Paused, Inactive)
- Notes

**Use**: Feed into automated scanners (Phase 2)

**Effort**: 2-3 hours (create table, populate with 20 initial funders)

### Phase 2: Automated Discovery (Months 2-3)

**FR4: RSS Feed Monitoring**

**Funder websites with RSS:**
- Arts Council England grant announcements
- National Lottery Community Fund
- Local authority grant pages (if RSS available)
- Grant portals (Grants Online, Funding Central, etc.)

**How it works:**
1. Zapier/Make.com monitors RSS feeds (check every 6-24 hours)
2. New item detected → Extract title, link, publication date
3. Create opportunity record (status: "Auto-discovered - Needs Review")
4. Notify team (Slack, email digest)

**Effort**: 4-6 hours (RSS feed research, Zapier setup for 10 feeds)

**FR5: Web Scraping (Selective)**

**Target websites without RSS:**
- Trust Foundation websites (check "Latest Grants" page)
- Regional arts councils
- Local authority grant pages

**Approach:**
- Use Apify, Scrapy, or custom scraper
- Run weekly (Saturday night, results reviewed Monday)
- Look for changes (new grant announcements)
- Extract: Title, link, deadline (if available)

**Legal/Ethical:**
- Only scrape publicly available info
- Respect robots.txt
- Don't overload servers (rate limiting)
- Check terms of service

**Effort**: 8-12 hours (scraper development + maintenance)

**Note**: May not be necessary if RSS + email forwarding cover 80% of sources

**FR6: Google Alerts Integration**

**Setup:**
- Create Google Alerts for keywords: "LGBTQ+ grant UK", "Black-led grant", "Arts funding 2025", etc.
- Alerts sent to grants@blkout.uk.coop
- Email parser (FR2) extracts and creates opportunities

**Effort**: 1 hour (set up alerts) + included in FR2

### Phase 3: AI-Powered Discovery (Months 6+)

**FR7: Intelligent Opportunity Matching**

**AI Features:**
- Natural language processing: Read funder criteria, auto-tag if BLKOUT is eligible
- Semantic search: Find grants even if keywords don't exactly match
- Predictive discovery: "Grants similar to those BLKOUT won before"
- False positive filtering: AI learns to ignore irrelevant opportunities

**Technology:**
- OpenAI API or similar
- Train on historical data (grants applied to, won, rejected)

**Effort**: 20-30 hours (AI integration, training)

---

## Data Model

### Opportunities Table (Extended)

```
opportunities (extends core architecture)
├── discovery_source (text: "RSS", "Email", "Manual", "Scraper", "AI")
├── discovery_confidence (1-10: how confident auto-discovery is accurate)
├── auto_populated (boolean: was this auto-discovered or manual?)
├── needs_review (boolean: human hasn't verified details yet)
├── reviewed_by (user)
├── reviewed_date (date)
```

### Discovery Sources Table (New)

```
discovery_sources
├── id
├── name (text: "Arts Council RSS", "Local Authority Email Alerts", etc.)
├── type (RSS, Email, Scraper, Manual)
├── url (if applicable)
├── status (Active, Paused, Broken)
├── last_check (timestamp)
├── opportunities_found (rollup count)
├── false_positive_rate (%)
```

---

## User Stories

### As a Fundraising Lead
> "Every Monday I spend 3 hours manually checking 10 funder websites. Most weeks I find 1-2 new grants. I want the system to check these websites for me and just show me what's new."

**Acceptance Criteria:**
- RSS feeds monitor Arts Council, Lottery, key funders
- New grants auto-added to "Needs Review" queue
- Monday morning: Review queue shows 3-5 new grants
- Click "Confirm" or "Reject" for each
- Confirmed grants move to Assessment module

### As a Grant Writer
> "I hear about a grant from a colleague via WhatsApp. I want to quickly add it to the system without filling out 20 fields."

**Acceptance Criteria:**
- Simple intake form (5 required fields: funder, grant name, amount, deadline, URL)
- Submit form from mobile phone
- Opportunity appears in system within 1 minute
- Can add more details later

### As a Team Member
> "I subscribe to several grant alert newsletters. I want to forward these emails and have them automatically logged, not manually re-enter details."

**Acceptance Criteria:**
- Forward email to grants@blkout.uk.coop
- System extracts funder, grant name, URL, deadline
- Creates opportunity record (status: "Needs Review")
- Notify me if parsing failed (need manual entry)

---

## Integration Points

### Input (What This Module Needs)

**From Core Architecture:**
- Access to `opportunities` table (write new records)
- Access to `funders` table (lookup funder details, check if already exists)
- Access to `discovery_sources` table (track what's being monitored)

**From External:**
- RSS feeds (URLs)
- Email forwarding address
- Web scraping targets (if Phase 2)

### Output (What This Module Provides)

**To Assessment Module:**
- New opportunity records (with funder, amount, deadline, URL populated)
- Discovery metadata (source, confidence, needs review status)

**To Pipeline Manager:**
- Count of new opportunities discovered (for dashboard stats)

**To Team:**
- Notifications (new grant found, needs review)
- Weekly digest (all discoveries this week)

---

## Workflow

### Discovery to Assessment Flow

```
1. [Discovery Source]
   ├─ RSS feed finds new grant OR
   ├─ Email forwarded OR
   └─ Manual form submitted

2. [Parse & Extract]
   ├─ Extract: funder, grant, amount, deadline, URL
   ├─ Auto-tag keywords (if AI available)
   └─ Set needs_review = true

3. [Create Opportunity Record]
   ├─ Insert into opportunities table
   ├─ Link to funder (or create funder if new)
   └─ Set stage = "discovered"

4. [Notify Team]
   ├─ Slack: "New grant found: [Grant Name] - £[Amount] - Deadline [Date]"
   ├─ Email digest (if daily/weekly batch)
   └─ In-app notification (red dot on Dashboard)

5. [Human Review]
   ├─ Team member reviews details
   ├─ Confirms or edits auto-populated fields
   ├─ Sets needs_review = false
   └─ Opportunity moves to Assessment module

6. [Assessment Module] (separate PRD)
   ├─ Reads confirmed opportunities
   └─ Calculates priority score
```

---

## Technical Implementation

### Phase 1: Airtable + Zapier

**Airtable:**
- Opportunities table (with discovery fields)
- Discovery Sources table
- Intake form (Airtable form)

**Zapier:**
- RSS feed monitors (10 feeds = 10 Zaps)
  - Trigger: RSS by Zapier - New Item in Feed
  - Action: Airtable - Create Record
  - Map: title → grant_name, link → url, etc.
- Email parser (1 Zap)
  - Trigger: Email Parser by Zapier
  - Extract: Funder, Grant, URL, Deadline
  - Action: Airtable - Create Record

**Notifications:**
- Zapier: Airtable - New Record → Slack - Send Message
- Or: Airtable automation (built-in, no Zapier needed)

**Cost:**
- Airtable: Free (or £20/month Plus if >1,200 records)
- Zapier: Free tier (100 tasks/month) may suffice, or £20/month (750 tasks)
- **Total**: £0-40/month

**Effort**: 15-20 hours setup + 2-3 hours/month maintenance

### Phase 2: Custom Build (If Needed)

**Stack:**
- Backend: Python script (cron job, runs daily)
- RSS parsing: `feedparser` library
- Email parsing: IMAP + regex
- Web scraping: `BeautifulSoup` or `Scrapy`
- Database: Supabase (write to opportunities table)
- Notifications: Slack API, email (SendGrid)

**Hosted:**
- GitHub Actions (free, cron schedule)
- Or: Railway/Fly.io (£5-10/month)

**Effort**: 20-30 hours development + ongoing maintenance

---

## Quality & Validation

### False Positive Filtering

**Problem**: Auto-discovery may find irrelevant grants

**Solution:**
1. **Keyword filtering** (Phase 1):
   - Only create opportunity if description contains: "LGBTQ+", "Black", "arts", "culture", "community", "infrastructure"
   - Skip if contains: "medical research", "animal welfare", "international development" (not BLKOUT focus)

2. **Human review** (Phase 1):
   - All auto-discovered grants flagged "Needs Review"
   - Team confirms before it moves to Assessment

3. **AI learning** (Phase 3):
   - Track which auto-discovered grants were confirmed vs. rejected
   - Train AI to improve precision over time
   - Target: <10% false positive rate

### Data Quality Checks

**Required field validation:**
- Deadline must be future date
- Amount must be positive number
- URL must be valid link (http/https)

**Duplicate detection:**
- Check if opportunity with same funder + grant name already exists
- If yes: Update existing record (refresh deadline/amount if changed)
- If no: Create new record

**Data completeness:**
- Flag opportunities missing eligibility criteria (human should research)
- Flag opportunities missing description (extract from funder website)

---

## Success Criteria

### Phase 1 is "Done" when:

- [ ] Intake form working (can manually add opportunities in <2 min)
- [ ] Email forwarding working (forward email → opportunity created)
- [ ] 10+ RSS feeds monitored (Arts Council, Lottery, key funders)
- [ ] 20+ funders in database (monitor list)
- [ ] New opportunities auto-tagged with keywords
- [ ] Team receives notifications (Slack or email)
- [ ] First month: Discover 10+ opportunities (vs. 2-3 manual)

### Overall Success (6 months):

- [ ] 50+ opportunities discovered (vs. 20 manual)
- [ ] <20% false positive rate (80%+ of auto-discoveries are relevant)
- [ ] Manual scanning time reduced from 2-3 hours/month to 30 min/month
- [ ] Zero "surprise" grants (find everything in monitored categories)
- [ ] Team reports confidence that no opportunities are missed

---

## Risks & Mitigation

### Risk 1: RSS Feeds Break / Change

**Likelihood**: Medium (websites change, feeds deprecated)
**Impact**: Medium (miss opportunities from that source)

**Mitigation:**
- Monitor feed health (track last successful check)
- Alert if feed hasn't updated in 30 days
- Monthly audit of all feeds (test each one)
- Backup: Email alerts + manual checks

### Risk 2: Email Parser Fails (Poor Extraction)

**Likelihood**: High (emails vary in format)
**Impact**: Low (falls back to manual entry)

**Mitigation:**
- Test parser with 10 sample emails before launch
- Graceful fallback: If parsing fails, forward to human with "Please enter manually"
- Improve parser iteratively (learn from failures)
- Phase 2: AI-powered email parsing (better than regex)

### Risk 3: Information Overload (Too Many Opportunities)

**Likelihood**: Medium (if successful, may find 100+ opportunities/year)
**Impact**: Medium (team overwhelmed, can't review all)

**Mitigation:**
- Prioritization from Day 1 (Assessment module auto-scores)
- Only notify team of HIGH priority opportunities (rest in dashboard)
- Weekly digest format (not real-time alerts for every discovery)
- Phase 2: AI filters out low-fit opportunities before human review

---

## Next Steps

1. **Research funder RSS feeds** (1-2 hours)
   - Identify 20 funders to monitor
   - Check if RSS feed available
   - Document feed URLs

2. **Set up Airtable base** (2-3 hours)
   - Opportunities table (with discovery fields)
   - Discovery Sources table
   - Intake form

3. **Configure Zapier** (4-6 hours)
   - RSS monitors (10 feeds)
   - Email parser
   - Slack notifications

4. **Test with real data** (2-3 hours)
   - Add 5 sample opportunities (manual)
   - Test email forwarding
   - Trigger RSS feeds (if possible, or wait for real updates)

5. **Launch pilot** (1 month)
   - Monitor daily
   - Track: How many opportunities found? False positive rate?
   - Iterate: Fix broken feeds, improve parser

6. **Evaluate** (end of Month 1)
   - Did it save time? Find more opportunities?
   - Go/No-Go: Continue to Phase 2 or stick with Phase 1?

---

**Document Control:**
- **Version**: 1.0
- **Last Updated**: 14 November 2025
- **Next Review**: After Phase 1 pilot (Month 1)
- **Owner**: BLKOUT Fundraising Team
- **Dependencies**: Core Architecture PRD (must read first)
- **Priority**: HIGH - Foundation of grant pipeline
