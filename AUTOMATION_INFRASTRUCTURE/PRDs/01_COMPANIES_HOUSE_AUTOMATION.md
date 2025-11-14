# Product Requirement Document
## Companies House Registry Automation System

**Version**: 1.0
**Date**: 14 November 2025
**Owner**: BLKOUT Infrastructure Team
**Status**: Proposed

---

## Executive Summary

Automate Companies House officer searches for BLKOUT members, partners, and grant applicants using the Companies House API. Reduce manual registry searches from 15+ minutes per person to instant lookup, with automatic monitoring for changes.

**Value Proposition**: What took us hours of manual Perplexity searches could be automated into a 30-second API query with ongoing monitoring.

---

## Problem Statement

### Current Pain Points

**From CBS Registration Experience:**
- Manual registry searches took hours for 9 founding members
- Had to use Perplexity AI because our tools couldn't access interactive registries
- Missed Robert's CIC directorship initially (only found via external search)
- No way to monitor for future changes to member affiliations
- Process will need to be repeated for every new member, partner, or grant recipient

**Broader Impact:**
- Due diligence on collaboration partners (manual process)
- Grant recipient verification (no current system)
- Ongoing compliance monitoring (currently reactive, not proactive)
- Board recruitment (need background checks on new trustees)

### Why This Matters

1. **Compliance**: CBS regulations require ongoing disclosure of member affiliations
2. **Due Diligence**: Partnerships and grants require conflict of interest checks
3. **Risk Management**: Early detection of conflicts or disqualifying appointments
4. **Efficiency**: 10+ hours/year of manual searches → automated

---

## Goals & Success Metrics

### Primary Goals

1. **Automate officer searches** for any UK individual (name + DOB)
2. **Monitor existing members** for affiliation changes
3. **Generate reports** in FCA-ready format
4. **Integrate with member onboarding** workflow

### Success Metrics

| Metric | Current State | Target State | Timeline |
|--------|--------------|--------------|----------|
| Time per person search | 15-20 min (manual) | <30 seconds (automated) | Phase 1 (Month 1) |
| Search accuracy | ~90% (missed Robert's CIC) | 100% (API is authoritative) | Phase 1 |
| Monitoring cadence | Never (manual only) | Weekly automated checks | Phase 2 (Month 2) |
| Report generation time | 2+ hours (manual compilation) | <5 min (automated) | Phase 1 |
| Cost per search | £0 (staff time ~£5) | <£0.10 (API costs) | Phase 1 |

### Key Performance Indicators (KPIs)

- **Searches performed**: Target 50+ in first 6 months (9 current members + partners + new members)
- **Changes detected**: Baseline unknown → track all affiliation changes
- **Compliance incidents avoided**: Target 100% (catch all conflicts before they become issues)
- **User adoption**: 100% of member onboarding uses automated search

---

## User Stories

### As a CBS Administrator
> "When a new founding member joins, I need to verify their affiliations within 24 hours for FCA disclosure. Currently this takes manual Perplexity searches and I might miss directorships."

**Acceptance Criteria:**
- Enter name + DOB → get complete list of directorships/secretaryships
- Results include: company name, number, role, appointment date, status
- Export to FCA-ready format (table/PDF)
- Flagged conflicts with existing members

### As a Partnerships Lead
> "Before signing an MOU with another organization, I need to check if any of their directors have conflicts with BLKOUT board. Currently I have no systematic way to do this."

**Acceptance Criteria:**
- Upload list of names + DOBs (CSV)
- Bulk search all individuals
- Cross-reference against BLKOUT member affiliations
- Generate conflict report

### As a Compliance Officer
> "I need to know immediately if a board member takes on a new directorship that conflicts with BLKOUT activities. Currently I only find out when they tell me (if they remember)."

**Acceptance Criteria:**
- Automated weekly checks on all members
- Email alert if new appointment detected
- Dashboard showing all current affiliations
- Change history log

### As a Grant Manager
> "When evaluating grant applications, I need to verify applicant organizations aren't connected to BLKOUT board members. Manual searches take too long and might miss connections."

**Acceptance Criteria:**
- Search by company number or name
- See all directors/secretaries
- Highlight any matches with BLKOUT database
- One-click conflict check

---

## Functional Requirements

### Core Features (Phase 1)

**FR1: Individual Officer Search**
- Input: Name (first, last), Date of Birth (month/year or full)
- Output: List of all current and historical appointments
- Data returned: Company name, number, role, appointed date, resigned date, company status
- Response time: <5 seconds
- UI: Simple form (web interface)

**FR2: Company Officer Lookup**
- Input: Company name OR company number
- Output: List of all current officers (directors, secretaries)
- Cross-reference with BLKOUT member database
- Flag conflicts automatically

**FR3: Bulk Search**
- Input: CSV file (name, DOB columns)
- Output: Combined report for all individuals
- Max: 50 individuals per batch (API rate limits)
- Progress indicator for long searches

**FR4: Export Formats**
- FCA-ready table (Markdown/Word/PDF)
- CSV for data processing
- JSON for integrations
- Conflict report (highlighted issues)

**FR5: Basic Dashboard**
- View all BLKOUT members' current affiliations
- Summary statistics (total affiliations, conflicts, etc.)
- Last updated timestamp
- Manual refresh button

### Enhanced Features (Phase 2)

**FR6: Automated Monitoring**
- Weekly automated re-check of all BLKOUT members
- Email alerts for new appointments/resignations
- Configurable alert recipients
- Change history log (who changed what when)

**FR7: Conflict Detection Engine**
- Define conflict rules (e.g., "any director of funder organization")
- Automatic flagging when conflicts detected
- Severity levels (High/Medium/Low)
- Suggested actions (recusal, disclosure, etc.)

**FR8: Member Onboarding Integration**
- New member form includes automated search
- Pre-populates affiliations for member confirmation
- Tracks verification status
- Integrates with member verification workflow

**FR9: Historical Tracking**
- Store snapshots of all searches
- Track affiliation changes over time
- Audit trail for compliance
- "Changes since last FCA submission" report

### Advanced Features (Phase 3)

**FR10: Charity Commission Integration**
- Search charity trusteeships (API if available, web scraping if not)
- Combined Companies House + Charity Commission report
- One search, both registries

**FR11: Network Visualization**
- Graph view of connections (who's connected to whom via shared directorships)
- Interactive exploration
- Export to visualization tools

**FR12: API for Other Systems**
- RESTful API for integrations
- Webhook notifications for changes
- Integration with grant management system
- Integration with member database

---

## Technical Requirements

### API & Data Sources

**Primary: Companies House API**
- Endpoint: https://api.company-information.service.gov.uk/
- Authentication: API key (free, register at https://developer.company-information.service.gov.uk/)
- Rate Limits: 600 requests/5 minutes (should be sufficient)
- Cost: Free for non-commercial use
- Data Coverage: All UK companies, CICs, LLPs

**Officer Search Endpoint:**
```
GET /search/officers?q={name}&items_per_page=100
```

**Company Officers Endpoint:**
```
GET /company/{company_number}/officers
```

**Officer Appointments Endpoint:**
```
GET /officers/{officer_id}/appointments
```

### Technology Stack

**Backend (Recommended):**
- **Language**: Python 3.11+
- **Framework**: FastAPI (for API) or Flask (simpler)
- **Database**: PostgreSQL (for storing search history, member records)
- **Task Queue**: Celery + Redis (for bulk searches, monitoring jobs)
- **Caching**: Redis (cache API responses, reduce duplicate calls)

**Frontend (Recommended):**
- **Framework**: Next.js (React) - already familiar from verification site
- **Styling**: Tailwind CSS (rapid development)
- **Deployment**: GitHub Pages (static) + Vercel (API routes)
- **Alternative**: Simple HTML/JS if minimal UI needed

**Infrastructure:**
- **Hosting**: Vercel (free tier sufficient for Phase 1)
- **Database**: Supabase (free tier: 500MB, sufficient) or Railway
- **Monitoring**: Sentry (error tracking), Uptime Robot (uptime monitoring)
- **Storage**: GitHub (code) + database (search results)

### Data Model

**Members Table:**
```sql
members (
  id: uuid PRIMARY KEY,
  first_name: text,
  last_name: text,
  date_of_birth: date,
  role: text (founding_member, trustee, advisor, etc.),
  added_date: timestamp,
  status: text (active, resigned, etc.)
)
```

**Affiliations Table:**
```sql
affiliations (
  id: uuid PRIMARY KEY,
  member_id: uuid FOREIGN KEY,
  company_number: text,
  company_name: text,
  officer_role: text (director, secretary),
  appointed_date: date,
  resigned_date: date NULL,
  company_status: text,
  discovered_date: timestamp,
  last_verified: timestamp,
  source: text (companies_house, member_declared)
)
```

**Searches Table (Audit):**
```sql
searches (
  id: uuid PRIMARY KEY,
  search_type: text (individual, company, bulk),
  searched_by: text,
  search_params: jsonb,
  results_count: integer,
  timestamp: timestamp
)
```

**Conflicts Table:**
```sql
conflicts (
  id: uuid PRIMARY KEY,
  member_id: uuid FOREIGN KEY,
  conflict_type: text,
  description: text,
  severity: text (high, medium, low),
  status: text (active, resolved, disclosed),
  detected_date: timestamp,
  resolved_date: timestamp NULL
)
```

### Security & Compliance

**Data Protection:**
- Date of birth is personal data (GDPR/UK GDPR)
- Store only what's necessary (name, DOB, affiliations)
- Encrypt at rest (database encryption)
- Secure API keys (environment variables, not in code)
- Access controls (who can search, who can see results)

**API Key Management:**
- Store Companies House API key in environment variables
- Rotate keys periodically
- Monitor usage (Companies House provides dashboard)
- Rate limit internal API to prevent abuse

**Retention Policy:**
- Keep search history for 7 years (CBS compliance requirement)
- Anonymize/delete departed member data after 2 years
- Regular backups of database

### Performance Requirements

- **Search response time**: <5 seconds for individual search
- **Bulk search**: <2 minutes for 50 people
- **Dashboard load**: <2 seconds
- **Uptime**: 99% (not mission-critical, but should be reliable)
- **Concurrent users**: 5-10 (internal tool, low traffic)

---

## Implementation Phases

### Phase 1: MVP (Month 1) - Manual Search Tool

**Deliverables:**
- [ ] Companies House API integration (officer search)
- [ ] Simple web form (name + DOB input)
- [ ] Individual search results display
- [ ] Export to CSV/Markdown
- [ ] Basic member database (manual entry of 9 founding members)

**Effort**: 20-30 hours
**Priority**: HIGH (immediate value, replaces manual Perplexity searches)

**Success Criteria:**
- Can search any individual in <30 seconds
- Results match Companies House exactly
- Export works in FCA-ready format

### Phase 2: Automation & Monitoring (Month 2-3)

**Deliverables:**
- [ ] Bulk search (CSV upload)
- [ ] Automated weekly monitoring of members
- [ ] Email alerts for changes
- [ ] Dashboard with all member affiliations
- [ ] Conflict detection (basic rules)

**Effort**: 30-40 hours
**Priority**: MEDIUM (improves efficiency, enables proactive monitoring)

**Success Criteria:**
- Monitors all 9 founding members weekly
- Detects and alerts on new appointments within 7 days
- Bulk search handles 50+ people

### Phase 3: Integration & Advanced Features (Month 4-6)

**Deliverables:**
- [ ] Member onboarding integration
- [ ] Charity Commission search (if feasible)
- [ ] Network visualization
- [ ] API for other systems
- [ ] Historical tracking and audit trail

**Effort**: 40-50 hours
**Priority**: LOW (nice-to-have, not urgent)

**Success Criteria:**
- New member onboarding includes automated search
- Can visualize connection networks
- Full audit trail for compliance

### Phase 4: Maintenance & Optimization (Ongoing)

**Deliverables:**
- [ ] Bug fixes and performance improvements
- [ ] UI/UX refinements based on user feedback
- [ ] Documentation updates
- [ ] API monitoring and optimization

**Effort**: 5-10 hours/month
**Priority**: MEDIUM (ongoing)

---

## Dependencies

### External Dependencies

- **Companies House API**: Must remain available and free (high confidence)
- **API key approval**: Typically instant, but allow 1-2 days
- **Rate limits**: 600 requests/5 min sufficient for our needs
- **API stability**: Companies House API is stable, breaking changes rare

### Internal Dependencies

- **Member database**: Need to establish source of truth for member list
- **Email system**: For alerts (can use existing email, or SendGrid/Mailgun)
- **Hosting infrastructure**: Need to decide on Vercel vs. self-hosted
- **Access controls**: Who should have access to search system?

### Skills/Resources Required

- **Python developer**: 20-30 hours (Phase 1), ongoing maintenance
- **Frontend developer** (optional): 10-15 hours for better UI
- **DevOps** (minimal): 5 hours for deployment setup
- **Product owner**: 5-10 hours for requirements refinement, testing

---

## Risks & Mitigation

### Risk 1: Companies House API Changes/Deprecation

**Likelihood**: Low (API has been stable for years)
**Impact**: High (entire system breaks)

**Mitigation:**
- Monitor Companies House developer announcements
- Build abstraction layer (easy to swap data source)
- Cache all results (even if API fails, have historical data)
- Fallback to manual Perplexity search if needed

### Risk 2: API Rate Limits Exceeded

**Likelihood**: Low (600 req/5min is generous for our volume)
**Impact**: Medium (searches fail temporarily)

**Mitigation:**
- Implement rate limiting in our code (stay under 600/5min)
- Cache repeated searches (don't re-query same person)
- Queue bulk searches (spread out over time)
- Monitor API usage dashboard

### Risk 3: Data Privacy / GDPR Compliance

**Likelihood**: Medium (handling personal data)
**Impact**: High (legal/reputational risk)

**Mitigation:**
- Minimize data collection (only what's needed)
- Encrypt sensitive data
- Clear retention policy
- Access controls (who can search)
- Privacy policy and user consent (for members)
- Regular GDPR audits

### Risk 4: Incomplete Data (Missing Directorships)

**Likelihood**: Low (Companies House is authoritative register)
**Impact**: Medium (missed conflicts)

**Mitigation:**
- Always include disclaimer: "Based on Companies House data only"
- Encourage member self-declaration as backup
- Add Charity Commission search in Phase 3
- Annual manual verification with members

### Risk 5: Development Resource Unavailable

**Likelihood**: Medium (relying on volunteer/contractor time)
**Impact**: Medium (delays, incomplete features)

**Mitigation:**
- Phase approach (MVP first, can stop after Phase 1 if needed)
- Clear documentation (enable handover to new developer)
- Consider low-code solutions (n8n, Zapier) as alternative
- Outsource to freelancer if budget available

---

## Alternatives Considered

### Alternative 1: Continue Manual Searches (Status Quo)

**Pros:**
- No development cost
- No ongoing maintenance
- Flexibility (can use Perplexity, web search, etc.)

**Cons:**
- Time-consuming (15-20 min per person)
- Error-prone (missed Robert's CIC)
- Not scalable (10+ members = hours of work)
- No monitoring capability

**Decision**: Reject - automation provides clear ROI

### Alternative 2: Third-Party Service (e.g., DueDil, Creditsafe)

**Pros:**
- No development needed
- Professional support
- Additional features (credit checks, etc.)

**Cons:**
- **Cost**: £500-2000/year for small org plan
- **Overkill**: We only need basic officer search
- **Data retention**: May not meet our compliance needs
- **Vendor lock-in**: Hard to switch later

**Decision**: Reject for Phase 1 - build in-house using free API. Reconsider if needs expand beyond Companies House.

### Alternative 3: Low-Code Automation (n8n, Zapier)

**Pros:**
- Faster development (visual workflow builder)
- No/low code required
- Easy integrations

**Cons:**
- Monthly cost (~£20-50/month for sufficient workflows)
- Limited customization
- May not handle bulk searches well
- Less control over data

**Decision**: Consider as fallback if development resource unavailable. Python API integration preferred for flexibility.

---

## Success Criteria & Definition of Done

### Phase 1 MVP is "Done" when:

- [ ] Can search any individual by name + DOB
- [ ] Returns all Companies House appointments (current + historical)
- [ ] Results display company name, number, role, dates, status
- [ ] Export works (CSV, Markdown, PDF)
- [ ] 9 founding members loaded into system
- [ ] Search completes in <30 seconds
- [ ] Tested with 10+ real searches (accuracy verified)
- [ ] Documentation written (how to use, how to maintain)

### Overall Project is "Successful" when:

- [ ] Replaces 90%+ of manual registry searches
- [ ] Used by all team members for due diligence
- [ ] Catches at least 1 conflict that would have been missed manually
- [ ] Saves 10+ hours/year of manual work
- [ ] Zero compliance incidents related to undisclosed affiliations

---

## Future Enhancements (Beyond Phase 3)

- **Charity Commission full integration** (when/if API becomes available)
- **Scottish/NI equivalents** (if BLKOUT expands beyond England/Wales)
- **International registers** (if working with international partners)
- **AI-powered conflict analysis** (LLM reviews affiliations and suggests potential conflicts)
- **Member self-service portal** (members can log in, see their affiliations, update)
- **Integration with grant management system** (auto-check all grant applicants)
- **Slack/Discord notifications** (real-time alerts in team chat)

---

## Open Questions

1. **Who should have access to search system?** (All staff? Just compliance officer? Board only?)
2. **Should members be able to see their own records?** (Self-service portal?)
3. **What email system to use for alerts?** (Personal email? Shared inbox? Slack?)
4. **Should we store partial DOBs or full DOBs?** (Privacy vs. accuracy trade-off)
5. **What constitutes a "conflict of interest" for automatic flagging?** (Need clear rules)

---

## Appendix: API Examples

### Example 1: Search for "Robert Berkeley"

**Request:**
```
GET https://api.company-information.service.gov.uk/search/officers?q=robert+berkeley
Authorization: Basic [BASE64_ENCODED_API_KEY]
```

**Response (truncated):**
```json
{
  "items": [
    {
      "title": "Robert BERKELEY",
      "date_of_birth": { "month": 3, "year": 1974 },
      "address_snippet": "...",
      "appointments": { "total_count": 11 },
      "links": { "self": "/officers/abc123" }
    }
  ]
}
```

### Example 2: Get all appointments for an officer

**Request:**
```
GET https://api.company-information.service.gov.uk/officers/abc123/appointments
```

**Response:**
```json
{
  "items": [
    {
      "company_name": "THE BLACK BOY JOY CLUB CIC",
      "company_number": "11794996",
      "officer_role": "director",
      "appointed_on": "2025-03-07",
      "resigned_on": null,
      "company_status": "active"
    }
  ]
}
```

---

**Document Control:**
- **Version**: 1.0
- **Last Updated**: 14 November 2025
- **Next Review**: After Phase 1 completion
- **Owner**: BLKOUT Infrastructure Team
- **Stakeholders**: CBS compliance officer, board, partnerships team
