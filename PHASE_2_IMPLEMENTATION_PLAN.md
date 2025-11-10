# BLKOUT Phase 2: Complete Implementation Plan
**Community-Owned Automation Infrastructure for Liberation Technology**

**Version**: 2.0
**Date**: November 2025
**Philosophy**: "Move at the speed of trust" - Incremental, community-reviewed automation

---

## Executive Summary

Phase 2 transforms BLKOUT from a manually-managed platform into a **self-sustaining, community-powered automation hub** while maintaining cooperative ownership and digital sovereignty values.

### Key Decisions

✅ **CHOSEN**: Open source stack (n8n, FreshRSS, Formbricks)
❌ **REJECTED**: Paid SaaS tools (Marblism, Pyxa, Content360, Formflow)
⚠️ **OPTIONAL**: PaddyPost ($47 lifetime) as simplified backup only

### Financial Impact

| Approach | Year 1 Cost | 5-Year Cost | Sovereignty |
|----------|-------------|-------------|-------------|
| **Paid Tools Stack** | $1,220 | $4,388 | ❌ Vendor-owned |
| **Phase 2 Plan (Open Source)** | $360-480 | $1,800-2,400 | ✅ Community-owned |
| **Savings** | **$860** | **$1,988-2,588** | **Full control** |

---

## Phase 2 Core Objectives

### 1. Content Automation
- **Goal**: Reduce manual content discovery from 10+ hours/week to <1 hour/week
- **Method**: Automated RSS + Event scraping + Community Chrome extension
- **Target**: 100-200 items/week automatically curated

### 2. Social Media Automation
- **Goal**: Auto-post approved content to all platforms
- **Method**: n8n workflows + platform APIs
- **Target**: 0 hours/week manual social media posting

### 3. Community Management
- **Goal**: Automated moderation workflows + health monitoring
- **Method**: Supabase triggers + n8n + AI classification
- **Target**: 50% reduction in moderation time

### 4. Analytics & Reporting
- **Goal**: Liberation-focused metrics (not extraction-based)
- **Method**: Automated dashboards + weekly digests
- **Target**: Real-time community health visibility

### 5. Newsletter Automation
- **Goal**: Weekly community digest without manual curation
- **Method**: AI-powered content summarization + email distribution
- **Target**: Automated weekly newsletter

---

## Technology Stack

### Core Infrastructure (Required)

| Component | Purpose | Cost | Sovereignty |
|-----------|---------|------|-------------|
| **n8n (self-hosted)** | Workflow automation hub | $10-20/mo VPS | ✅ Full control |
| **FreshRSS** | RSS feed aggregation | $0 (same VPS) | ✅ Self-hosted |
| **Supabase** | Database + real-time | $0 (current) | ⚠️ Managed |
| **Formbricks** | Form builder (optional) | $0 (self-hosted) | ✅ Full control |
| **Postiz** | Social media UI (optional) | $0 (self-hosted) | ✅ Full control |

**Total Infrastructure**: $10-20/month

### API Usage (Pay-per-use)

| Service | Purpose | Est. Monthly Cost |
|---------|---------|-------------------|
| **OpenAI API** | Content classification | $5-10 |
| **Claude API** | Content generation | $5-10 |
| **Social Media APIs** | Auto-posting | $0 (free tier) |
| **Event Platform APIs** | Event discovery | $0 (free tier) |

**Total API Usage**: $10-20/month

### **Total Phase 2 Monthly Cost**: $20-40/month

---

## Implementation Roadmap

### Month 1: Foundation & Core Automation

#### **Week 1: n8n Deployment & Configuration**
**Focus**: Get automation infrastructure running

**Tasks:**
- [ ] Deploy n8n instance (self-hosted on Hetzner/DigitalOcean)
- [ ] Configure environment variables for all services
- [ ] Set up webhook endpoints for platform communication
- [ ] Test basic workflow execution
- [ ] Configure error handling and monitoring

**Deliverables:**
- ✅ n8n instance accessible and secure
- ✅ Basic health monitoring in place
- ✅ Test workflow running successfully

**Time**: 4-6 hours
**Cost**: $10-20/month VPS setup
**Responsible**: Technical lead

---

#### **Week 2: RSS Feed Automation (Tier 1 Scraping)**
**Focus**: Automated news/article discovery

**Tasks:**
- [ ] Deploy FreshRSS (Docker on same VPS as n8n)
- [ ] Curate and add 15-20 RSS feeds:
  - **Black UK Media**: The Voice, Black Ballad, gal-dem
  - **LGBTQ+ News**: PinkNews, Attitude, Gay Times
  - **Activism**: Novara Media, Sisters Uncut, Gal-Dem
  - **Mainstream (filtered)**: Guardian, BBC, Independent
  - **Community**: Local Black-led organizations
- [ ] Build n8n workflow: **"Daily News Scraper"**
  ```
  Schedule (9am daily) →
  FreshRSS API (fetch new items) →
  OpenAI Classification (filter for relevance) →
  Supabase Insert (moderation queue) →
  Telegram Notification (moderators)
  ```
- [ ] Test with real feeds for 3 days
- [ ] Refine AI classification prompts based on results

**Deliverables:**
- ✅ FreshRSS deployed with 15-20 feeds
- ✅ n8n workflow auto-curating 50-100 articles/week
- ✅ Moderation queue receiving relevant content

**Time**: 6-8 hours
**Cost**: $0 (infrastructure already paid)
**Responsible**: Content team + technical lead

---

#### **Week 3: Event Platform API Integration (Tier 2 Scraping)**
**Focus**: Automated event discovery

**Tasks:**
- [ ] Set up Eventbrite API credentials
  - Create developer account
  - Generate API key
  - Test authentication
- [ ] Build n8n workflow: **"Eventbrite Auto-Discovery"**
  ```
  Schedule (6am daily) →
  Eventbrite Trigger Node (search: UK + Black QTIPOC keywords) →
  Filter (location, date range) →
  Deduplicate (check existing events) →
  Supabase Insert (events table) →
  Telegram Notification
  ```
- [ ] Set up Facebook Graph API for Events
  - Create Facebook App
  - Get access token
  - Configure permissions
- [ ] Build n8n workflow: **"Facebook Events Discovery"**
- [ ] Add Meetup integration via HTTP Request node
- [ ] Test event ingestion with real data

**Deliverables:**
- ✅ Eventbrite API integrated and running daily
- ✅ Facebook Events API discovering relevant events
- ✅ 20-50 events/week automatically curated
- ✅ Events appearing in moderation queue

**Time**: 8-10 hours
**Cost**: $0 (free tier APIs)
**Responsible**: Technical lead

---

#### **Week 4: Chrome Extension Distribution (Tier 3 Scraping)**
**Focus**: Community-powered content discovery

**Tasks:**
- [ ] Package existing Chrome extension for distribution
- [ ] Create visual installation guide with screenshots
- [ ] Record 2-minute tutorial video
- [ ] Set up dedicated landing page: `/extension/install`
- [ ] Test with 5 beta users from community
- [ ] Address any installation issues
- [ ] Distribute to 15-20 active community members
- [ ] Configure webhook handler for extension submissions

**Deliverables:**
- ✅ Chrome extension installation package
- ✅ Installation guide and video tutorial
- ✅ 15-20 community members trained and using extension
- ✅ Extension submissions flowing to moderation queue

**Time**: 5-6 hours
**Cost**: $0 (extension already built)
**Responsible**: Community coordinator + technical lead

**Files Involved:**
- `/blkout-extension/` (existing)
- `/blkout-extension/content-scripts/detector.js` (existing - lines 1-418)

---

### Month 2: Social Media Automation & Content Distribution

#### **Week 5: Social Media API Configuration**
**Focus**: Connect all social media platforms to n8n

**Tasks:**
- [ ] LinkedIn API setup
  - Create LinkedIn Developer App
  - Generate access tokens
  - Test posting capability
- [ ] Facebook/Instagram Graph API setup
  - Configure Facebook Business account
  - Link Instagram Business account
  - Generate page access tokens
- [ ] Twitter/X API setup
  - Apply for Twitter Developer account
  - Get API keys and bearer token
  - Test posting
- [ ] YouTube API setup (for video announcements)
  - Create Google Cloud project
  - Enable YouTube Data API
  - Generate credentials
- [ ] Update environment variables in n8n
- [ ] Test each platform API with sample posts

**Deliverables:**
- ✅ All social media APIs authenticated and working
- ✅ Environment variables configured
- ✅ Test posts successful on each platform

**Time**: 6-8 hours
**Cost**: $0 (free tier APIs)
**Responsible**: Technical lead + social media coordinator

---

#### **Week 6: Social Media Auto-Posting Workflows**
**Focus**: Automated content distribution

**Tasks:**
- [ ] Build n8n workflow: **"Event Approved → Auto-Post"**
  ```
  Supabase Trigger (event status = published) →
  OpenAI (generate platform-specific captions) →
  Branch:
    → LinkedIn (professional tone)
    → Instagram (visual/community tone)
    → Facebook (detailed/community)
    → Twitter/X (concise/hashtags)
  → Log success/failures
  → Update analytics
  ```
- [ ] Build n8n workflow: **"Article Approved → Auto-Post"**
  ```
  Supabase Trigger (article status = published) →
  Claude (generate engaging summaries) →
  Format for each platform →
  Multi-platform posting →
  Track engagement
  ```
- [ ] Add AI caption optimization
  - Platform-specific tone
  - Optimal hashtag generation
  - Character limit compliance
- [ ] Test with real approved content
- [ ] Monitor for 48 hours and refine

**Deliverables:**
- ✅ Automated social media posting on all platforms
- ✅ Platform-optimized captions via AI
- ✅ 0 hours/week manual social posting required
- ✅ Engagement tracking in place

**Time**: 10-12 hours
**Cost**: $5-10/month (AI API usage)
**Responsible**: Technical lead

**n8n Templates Reference:**
- [AI Social Media Content Generator](https://n8n.io/workflows/4637)
- [Multi-Platform Publishing](https://n8n.io/workflows/3086)

---

#### **Week 7: Moderation Automation Enhancement**
**Focus**: Streamline moderation workflows

**Tasks:**
- [ ] Build n8n workflow: **"AI-Assisted Moderation"**
  ```
  Supabase Trigger (new submission) →
  OpenAI Classification:
    - Relevance score (0-100)
    - Community fit assessment
    - Suggested category
    - Safety check
  → Auto-approve if score > 90 →
  → Manual review if 70-90 →
  → Auto-reject if < 70 with reason
  ```
- [ ] Activate unified moderation bridge (existing code)
- [ ] Set up cross-platform sync
  - Events calendar ↔ Platform admin
  - Chrome extension → Moderation queue
  - Social media feedback → Analytics
- [ ] Configure moderation priority levels
- [ ] Add Telegram alerts for high-priority items

**Deliverables:**
- ✅ AI-assisted moderation reducing manual work by 50%
- ✅ Unified moderation across all platforms
- ✅ Priority-based queue management
- ✅ Real-time moderator notifications

**Time**: 6-8 hours
**Cost**: $2-5/month (AI classification)
**Responsible**: Technical lead + moderation team

**Files Involved:**
- `/src/services/unifiedModerationBridge.ts` (existing - lines 1-303)
- `/src/api/webhook/moderation.ts` (existing - lines 1-105)

---

#### **Week 8: Newsletter Automation**
**Focus**: Automated weekly community digest

**Tasks:**
- [ ] Build n8n workflow: **"Weekly Newsletter Generator"**
  ```
  Schedule (Monday 8am) →
  Query Supabase:
    - Events from last 7 days
    - Articles from last 7 days
    - Community highlights
  → OpenAI Summarization:
    - Generate engaging intro
    - Summarize top stories
    - Highlight upcoming events
  → HTML Template Generation →
  → SendGrid/Mailchimp API →
  → Log sent newsletter
  ```
- [ ] Design newsletter HTML template
- [ ] Set up email distribution list management
- [ ] Test with small group (10-20 subscribers)
- [ ] Refine based on feedback
- [ ] Schedule for production

**Deliverables:**
- ✅ Automated weekly newsletter
- ✅ Professional HTML template
- ✅ No manual curation required
- ✅ Subscriber management system

**Time**: 8-10 hours
**Cost**: $0-15/month (SendGrid free tier → paid if >100 emails/day)
**Responsible**: Content team + technical lead

---

### Month 3: Analytics, Community Tools & Optimization

#### **Week 9: Analytics Automation**
**Focus**: Liberation-focused metrics and dashboards

**Tasks:**
- [ ] Build n8n workflow: **"Community Health Monitoring"**
  ```
  Schedule (Every 2 hours) →
  Fetch from Supabase:
    - Event attendance trends
    - Article engagement
    - Community growth metrics
    - Content approval rates
  → Calculate health scores →
  → Update dashboard (via API) →
  → Alert if scores drop below threshold
  ```
- [ ] Connect Google Analytics API
- [ ] Build n8n workflow: **"Weekly Analytics Report"**
  ```
  Schedule (Sunday 8pm) →
  Gather all metrics →
  OpenAI Analysis (trends, insights) →
  Generate HTML report →
  Email to admin team →
  Post summary to Telegram
  ```
- [ ] Set up custom liberation-focused metrics:
  - Community self-sufficiency score
  - Content diversity index
  - Geographic reach
  - Engagement quality (not just quantity)
  - Member empowerment indicators

**Deliverables:**
- ✅ Automated community health monitoring
- ✅ Weekly analytics reports
- ✅ Liberation-focused metrics dashboard
- ✅ Real-time alerts for concerning trends

**Time**: 8-10 hours
**Cost**: $0 (Google Analytics free tier)
**Responsible**: Technical lead + community coordinator

**n8n Templates Reference:**
- [Google Analytics Reporting](https://n8n.io/workflows/2549)
- [Analytics Dashboard Integration](https://n8n.io/integrations/google-analytics/)

---

#### **Week 10: Community Forms & Submissions**
**Focus**: Easy community contribution pathways

**Tasks:**
- [ ] Deploy Formbricks (self-hosted form builder)
  ```bash
  docker run -d --name formbricks \
    -p 3000:3000 \
    -e DATABASE_URL=postgresql://... \
    formbricks/formbricks
  ```
- [ ] Create forms:
  - Event submission form
  - Article suggestion form
  - Community feedback form
  - Partnership inquiry form
  - Volunteer signup form
- [ ] Build n8n workflows for each form:
  ```
  Formbricks Webhook (form submission) →
  Validate data →
  Enrich with metadata →
  Insert to Supabase →
  Send confirmation email →
  Notify relevant team
  ```
- [ ] Embed forms on platform pages
- [ ] Test submission → moderation → publication flow

**Deliverables:**
- ✅ Professional form builder deployed
- ✅ 5+ community contribution forms live
- ✅ Automated form processing
- ✅ Seamless integration with moderation queue

**Time**: 6-8 hours
**Cost**: $0 (self-hosted)
**Responsible**: Technical lead + UX designer

**Alternative**: Use existing Supabase forms if Formbricks unnecessary

---

#### **Week 11: Advanced Scraping Automation**
**Focus**: Custom scraping for sources without RSS/APIs

**Tasks:**
- [ ] Deploy existing backend scraper as API endpoint
  - Package `/api-backup/rag/scrape.ts` as serverless function
  - Deploy to Vercel/Netlify
  - Configure CORS and authentication
- [ ] Build n8n workflow: **"Custom Site Scraper"**
  ```
  Schedule (daily/weekly based on source) →
  HTTP Request to scraper API →
  Process returned JSON →
  AI Classification →
  Deduplicate →
  Submit to moderation queue
  ```
- [ ] Add scraping targets (sites without RSS):
  - Local Black community organizations
  - Smaller activism groups
  - Regional event platforms
  - Community newsletters (web archives)
- [ ] Implement respectful scraping:
  - User-Agent identification
  - Rate limiting (1 request/second)
  - robots.txt compliance
  - Caching to reduce requests
- [ ] Monitor for scraping errors and adjust

**Deliverables:**
- ✅ Custom scraper API deployed and functional
- ✅ 5-10 additional sources monitored
- ✅ Ethical, sustainable scraping practices
- ✅ Increased content diversity

**Time**: 8-10 hours
**Cost**: $0 (serverless free tier)
**Responsible**: Technical lead

**Files Involved:**
- `/api-backup/rag/scrape.ts` (existing - lines 1-451)
- Refactor and deploy as standalone API

---

#### **Week 12: Testing, Documentation & Training**
**Focus**: Production readiness and community handoff

**Tasks:**
- [ ] Comprehensive testing:
  - Load test all workflows (simulate 1000 items/day)
  - Test error handling and recovery
  - Verify all notifications working
  - Check data integrity across systems
  - Security audit of API endpoints
- [ ] Documentation:
  - Create workflow documentation for each n8n workflow
  - Write troubleshooting guides
  - Document all API credentials and storage locations
  - Create emergency contact procedures
- [ ] Community training:
  - Train 3-5 community members on workflow management
  - Create video tutorials for common tasks
  - Hold 2 training sessions for moderators
  - Establish rotation schedule for system monitoring
- [ ] Backup and disaster recovery:
  - Set up automated n8n workflow backups
  - Document restoration procedures
  - Test failover scenarios
  - Create runbooks for common issues

**Deliverables:**
- ✅ All workflows tested and production-ready
- ✅ Comprehensive documentation for community
- ✅ 3-5 community members trained on system
- ✅ Disaster recovery plan in place

**Time**: 10-12 hours
**Cost**: $0
**Responsible**: Full team

---

## Complete n8n Workflow Inventory

### Content Discovery Workflows (5)

1. **Daily News Scraper**
   - Trigger: Schedule (9am daily)
   - Sources: FreshRSS API (15-20 feeds)
   - Processing: OpenAI classification → Supabase
   - Output: 50-100 articles/week to moderation queue

2. **Eventbrite Auto-Discovery**
   - Trigger: Schedule (6am daily)
   - Sources: Eventbrite API
   - Processing: Filter + Deduplicate → Supabase
   - Output: 10-30 events/week

3. **Facebook Events Discovery**
   - Trigger: Schedule (6am daily)
   - Sources: Facebook Graph API
   - Processing: Filter + Enrich → Supabase
   - Output: 5-20 events/week

4. **Custom Site Scraper**
   - Trigger: Schedule (daily/weekly)
   - Sources: Custom scraper API
   - Processing: Parse + Classify → Supabase
   - Output: 10-20 items/week from non-RSS sources

5. **Chrome Extension Handler**
   - Trigger: Webhook (real-time)
   - Sources: Community member submissions
   - Processing: Validate → Supabase
   - Output: 10-20 community submissions/week

---

### Content Distribution Workflows (3)

6. **Event Approved → Auto-Post**
   - Trigger: Supabase (event status = published)
   - Processing: AI caption generation → Multi-platform APIs
   - Platforms: LinkedIn, Instagram, Facebook, Twitter/X
   - Output: Automatic social media posting

7. **Article Approved → Auto-Post**
   - Trigger: Supabase (article status = published)
   - Processing: Claude summarization → Platform APIs
   - Platforms: LinkedIn, Facebook, Twitter/X
   - Output: Optimized posts with engagement tracking

8. **Weekly Newsletter Generator**
   - Trigger: Schedule (Monday 8am)
   - Processing: Query Supabase → AI summarization → HTML template
   - Output: Automated weekly digest to subscriber list

---

### Moderation & Management Workflows (3)

9. **AI-Assisted Moderation**
   - Trigger: Supabase (new content submission)
   - Processing: OpenAI classification + safety check
   - Output: Auto-approve, queue for review, or reject with reason

10. **Cross-Platform Moderation Sync**
    - Trigger: Supabase (moderation action)
    - Processing: Webhook to all connected platforms
    - Output: Synchronized moderation across systems

11. **Priority Alert System**
    - Trigger: Supabase (high-priority content)
    - Processing: Evaluate urgency → Telegram notification
    - Output: Real-time alerts to moderators

---

### Analytics & Monitoring Workflows (4)

12. **Community Health Monitoring**
    - Trigger: Schedule (every 2 hours)
    - Processing: Fetch metrics → Calculate scores → Update dashboard
    - Output: Real-time health indicators

13. **Weekly Analytics Report**
    - Trigger: Schedule (Sunday 8pm)
    - Processing: Aggregate data → AI analysis → HTML report
    - Output: Comprehensive weekly insights

14. **Social Media Engagement Tracker**
    - Trigger: Schedule (daily)
    - Processing: Platform APIs → Aggregate metrics → Store trends
    - Output: Engagement analytics dashboard

15. **n8n Workflow Monitoring**
    - Trigger: Each workflow completion
    - Processing: Log execution → Check for errors → Alert if failures
    - Output: System health dashboard

---

### Community Engagement Workflows (3)

16. **Form Submission Handler** (5 forms)
    - Trigger: Formbricks webhook
    - Processing: Validate → Enrich → Route to appropriate queue
    - Output: Processed submissions with confirmations

17. **Community Response System** (existing)
    - Trigger: Webhook (community questions)
    - Processing: IVOR AI query → Format response
    - Output: Real-time community support

18. **Partnership Amplification**
    - Trigger: Supabase (high-engagement content)
    - Processing: Identify partnership opportunities → Maven network outreach
    - Output: Automated partnership suggestions

---

## Total Workflow Count: **18 Active Workflows**

---

## Infrastructure Specifications

### VPS Requirements (n8n + FreshRSS)

**Recommended Provider**: Hetzner Cloud (best price/performance)

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| **CPU** | 2 vCPU | 4 vCPU |
| **RAM** | 4GB | 8GB |
| **Storage** | 40GB SSD | 80GB SSD |
| **Bandwidth** | 20TB/month | Unlimited |
| **Cost** | €4.51/month (~$5) | €8.21/month (~$9) |

**Setup**: Ubuntu 22.04 LTS + Docker + Docker Compose

---

### n8n Configuration

```yaml
# docker-compose.yml
version: '3.8'

services:
  n8n:
    image: n8nio/n8n:latest
    container_name: n8n
    restart: always
    ports:
      - "5678:5678"
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=blkout_admin
      - N8N_BASIC_AUTH_PASSWORD=${N8N_PASSWORD}
      - N8N_HOST=${N8N_HOST}
      - N8N_PORT=5678
      - N8N_PROTOCOL=https
      - NODE_ENV=production
      - WEBHOOK_URL=https://n8n.blkoutuk.com
      - GENERIC_TIMEZONE=Europe/London
    volumes:
      - n8n_data:/home/node/.n8n
      - /var/run/docker.sock:/var/run/docker.sock

  freshrss:
    image: freshrss/freshrss:latest
    container_name: freshrss
    restart: always
    ports:
      - "8080:80"
    environment:
      - CRON_MIN=*/15  # Update feeds every 15 minutes
      - TZ=Europe/London
    volumes:
      - freshrss_data:/var/www/FreshRSS/data

  postgres:
    image: postgres:15
    container_name: postgres
    restart: always
    environment:
      - POSTGRES_USER=blkout
      - POSTGRES_PASSWORD=${POSTGRES_PASSWORD}
      - POSTGRES_DB=n8n
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  n8n_data:
  freshrss_data:
  postgres_data:
```

---

## Environment Variables Inventory

### Core Services

```bash
# n8n Configuration
N8N_PASSWORD=<secure_password>
N8N_HOST=n8n.blkoutuk.com
WEBHOOK_URL=https://n8n.blkoutuk.com

# Database
POSTGRES_PASSWORD=<secure_password>
DATABASE_URL=postgresql://blkout:${POSTGRES_PASSWORD}@postgres:5432/n8n

# Supabase (existing)
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=<your_key>
SUPABASE_SERVICE_KEY=<service_key>
```

---

### Social Media APIs

```bash
# LinkedIn
LINKEDIN_CLIENT_ID=<linkedin_client_id>
LINKEDIN_CLIENT_SECRET=<linkedin_secret>
LINKEDIN_ACCESS_TOKEN=<access_token>
LINKEDIN_ORGANIZATION_ID=<org_id>

# Facebook/Instagram
FACEBOOK_ACCESS_TOKEN=<facebook_token>
FACEBOOK_PAGE_ID=<page_id>
INSTAGRAM_BUSINESS_ACCOUNT_ID=<account_id>

# Twitter/X
TWITTER_API_KEY=<twitter_key>
TWITTER_API_SECRET=<twitter_secret>
TWITTER_ACCESS_TOKEN=<access_token>
TWITTER_ACCESS_SECRET=<access_secret>
TWITTER_BEARER_TOKEN=<bearer_token>

# YouTube
YOUTUBE_CLIENT_ID=<youtube_client_id>
YOUTUBE_CLIENT_SECRET=<youtube_secret>
YOUTUBE_ACCESS_TOKEN=<access_token>
YOUTUBE_REFRESH_TOKEN=<refresh_token>
```

---

### Event & Content APIs

```bash
# Eventbrite
EVENTBRITE_API_KEY=<eventbrite_key>
EVENTBRITE_ORGANIZATION_ID=<org_id>

# Meetup (if using)
MEETUP_API_KEY=<meetup_key>

# FreshRSS
FRESHRSS_API_URL=http://freshrss:80/api
FRESHRSS_API_TOKEN=<freshrss_token>
```

---

### AI Services

```bash
# OpenAI
OPENAI_API_KEY=<openai_key>
OPENAI_ORG_ID=<org_id>

# Anthropic Claude
ANTHROPIC_API_KEY=<claude_key>

# Google AI (optional)
GOOGLE_AI_KEY=<google_key>
```

---

### Communication & Notifications

```bash
# Telegram
TELEGRAM_BOT_TOKEN=<telegram_token>
TELEGRAM_CHAT_ID=<chat_id>  # For moderation alerts

# SendGrid (newsletter)
SENDGRID_API_KEY=<sendgrid_key>
SENDGRID_FROM_EMAIL=newsletter@blkoutuk.com

# BLKOUTHUB Integration (existing)
BLKOUTHUB_API_URL=https://api.heartbeat.chat/v1
BLKOUTHUB_ACCESS_TOKEN=<hub_token>
BLKOUTHUB_COMMUNITY_ID=<community_id>
```

---

## Security Considerations

### Access Control

1. **n8n Admin Access**
   - Basic auth for n8n interface
   - Rotate password quarterly
   - 2FA via Cloudflare Access (optional)

2. **API Key Management**
   - Store in environment variables (never in code)
   - Use least-privilege permissions
   - Rotate annually or on suspected compromise

3. **Webhook Security**
   - Signature verification on all incoming webhooks
   - Rate limiting (100 requests/minute per IP)
   - HTTPS only, no HTTP fallback

4. **Database Access**
   - Supabase RLS policies enforced
   - Service keys only in backend, never frontend
   - Regular access audits

---

### Monitoring & Alerts

```yaml
# Monitoring Stack (optional but recommended)
services:
  uptime-kuma:
    image: louislam/uptime-kuma:latest
    ports:
      - "3001:3001"
    volumes:
      - uptime_data:/app/data
    # Monitor:
    # - n8n availability
    # - FreshRSS health
    # - Critical workflows
    # - API endpoint uptime
```

**Alerts sent to**:
- Telegram (immediate)
- Email (daily digest)
- Slack (optional team channel)

---

## Testing Strategy

### Pre-Production Testing (Week 12)

1. **Unit Testing**
   - Each n8n workflow tested in isolation
   - Mock data for reproducibility
   - Edge case handling verified

2. **Integration Testing**
   - Full content pipeline: Discovery → Moderation → Publication
   - Cross-platform sync verification
   - API rate limit handling

3. **Load Testing**
   - Simulate 1,000 items/day processing
   - Verify queue management under load
   - Check database performance

4. **Security Testing**
   - Webhook signature verification
   - API key exposure scan
   - SQL injection attempts (none should succeed)
   - XSS vulnerability check

5. **User Acceptance Testing**
   - 5 community members test full workflows
   - Moderators test moderation interface
   - Content creators test submission process

---

## Success Metrics

### Month 1 Targets

- ✅ **100+ articles/week** automatically curated
- ✅ **30+ events/week** automatically discovered
- ✅ **15+ community members** using Chrome extension
- ✅ **n8n availability** > 99.5%
- ✅ **0 hours/week** manual content discovery

---

### Month 3 Targets

- ✅ **200+ content items/week** processed automatically
- ✅ **0 hours/week** manual social media posting
- ✅ **50% reduction** in moderation time
- ✅ **Weekly newsletter** sent automatically
- ✅ **Real-time analytics** dashboard operational
- ✅ **5+ trained community members** managing system

---

### Month 6 Targets

- ✅ **Self-sustaining content pipeline** requiring <2 hours/week oversight
- ✅ **50+ active community contributors** via Chrome extension
- ✅ **Custom workflows** created by cooperative members
- ✅ **Zero vendor dependencies** for core automation
- ✅ **Complete data sovereignty** maintained
- ✅ **Measurable community growth** from automation efficiency

---

## Risk Mitigation

### Technical Risks

| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|
| **API rate limits exceeded** | Medium | High | Implement queueing, caching, and fallback sources |
| **VPS downtime** | Low | High | Automated backups, documented restore process |
| **Workflow errors** | Medium | Medium | Error handling, retry logic, alerting |
| **Data loss** | Low | Critical | Daily backups to S3, version control for workflows |
| **Security breach** | Low | Critical | Regular audits, key rotation, access logs |

---

### Community Risks

| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|
| **Technical knowledge gap** | High | Medium | Comprehensive documentation, training sessions |
| **Automation over-reliance** | Medium | Medium | Manual override capabilities, regular reviews |
| **Quality degradation** | Medium | High | AI quality thresholds, human moderation required |
| **Community disengagement** | Low | High | Keep humans in loop, transparent processes |

---

## Rollback Procedures

### If Phase 2 Encounters Critical Issues

1. **Immediate Actions** (within 1 hour)
   - Pause all automated workflows
   - Switch to manual content posting
   - Alert community of temporary service interruption

2. **Diagnosis** (within 4 hours)
   - Review error logs
   - Identify root cause
   - Assess whether fixable quickly

3. **Decision Point**
   - **If fixable**: Implement fix, test, resume
   - **If not fixable**: Rollback to Phase 1 operations

4. **Phase 1 Rollback** (if needed)
   - Disable n8n workflows
   - Resume manual admin dashboard usage
   - Keep data collected during Phase 2
   - Plan Phase 2.1 with fixes

---

## Post-Implementation Review

### After Month 3

**Review Questions:**
1. Are we achieving target automation levels?
2. Is content quality maintained or improved?
3. Are community members engaged with system?
4. What manual processes still remain?
5. What unexpected challenges emerged?
6. What worked better than expected?

**Output**: Phase 3 Planning Document

---

## Budget Summary

### One-Time Costs

| Item | Cost | When |
|------|------|------|
| **VPS Setup** | $10-20 | Month 1, Week 1 |
| **Domain** (if new) | $15/year | Month 1, Week 1 |
| **SSL Certificate** | $0 (Let's Encrypt) | Month 1, Week 1 |
| **Initial Development Time** | Community volunteer | Ongoing |
| **Total One-Time** | **$25-35** | - |

---

### Recurring Monthly Costs

| Category | Service | Cost/Month |
|----------|---------|------------|
| **Infrastructure** | Hetzner VPS (4 vCPU, 8GB) | $9 |
| | FreshRSS (same VPS) | $0 |
| | Supabase (current plan) | $0 |
| **APIs - Social** | LinkedIn/Facebook/Twitter | $0 (free tier) |
| | YouTube | $0 (free tier) |
| **APIs - Content** | Eventbrite | $0 (free tier) |
| | Facebook Events | $0 (free tier) |
| **APIs - AI** | OpenAI (classification) | $5-10 |
| | Claude (content generation) | $5-10 |
| **Email** | SendGrid (0-100 emails/day) | $0 |
| | SendGrid (100-40k emails/month) | $15 (if needed) |
| **Monitoring** | Uptime Kuma (self-hosted) | $0 |
| **Total Monthly** | - | **$19-44** |

**Average Monthly Cost**: ~$30/month

---

### Cost Comparison

| Approach | Monthly | Annual | 5-Year |
|----------|---------|--------|--------|
| **Phase 2 Plan** | $30 | $360 | $1,800 |
| **Paid Tools** (Marblism + Formflow + etc) | $102 | $1,220 | $6,100 |
| **Enterprise SaaS** (Bright Data + etc) | $600+ | $7,200+ | $36,000+ |
| **Savings** | **$72-570** | **$860-6,840** | **$4,300-34,200** |

---

## Community Governance Integration

### Decision-Making Process

1. **Technical decisions** (infrastructure, tools)
   - Technical team proposes
   - Community review period (7 days)
   - Cooperative vote if contentious

2. **Content policies** (moderation, classification)
   - Community-led discussions
   - Consensus-based decisions
   - Documented in shared wiki

3. **Resource allocation** (budget, priorities)
   - Quarterly budget review
   - Transparent cost reporting
   - Democratic prioritization

### Transparency Requirements

- **Monthly reports** on automation metrics
- **Open access** to all workflow code
- **Public changelog** for system updates
- **Community training** sessions quarterly

---

## Next Steps After Plan Approval

1. **Community Review** (Week 0)
   - Share plan with cooperative members
   - Gather feedback and concerns
   - Refine based on input
   - Vote on approval

2. **Resource Allocation** (Week 0)
   - Assign technical lead
   - Identify community volunteers
   - Secure VPS and accounts
   - Set up project tracking

3. **Kickoff Meeting** (Week 1, Day 1)
   - Review timeline with team
   - Assign responsibilities
   - Set communication channels
   - Begin implementation

---

## Appendices

### A. RSS Feed Recommendations (15-20 sources)

#### Black UK Media
1. **The Voice** - https://www.voice-online.co.uk/feed/
2. **Black Ballad** - https://blackballad.co.uk/feed/
3. **gal-dem** - https://gal-dem.com/feed/

#### LGBTQ+ News
4. **PinkNews** - https://www.thepinknews.com/feed/
5. **Attitude** - https://attitude.co.uk/feed/
6. **Gay Times** - https://www.gaytimes.co.uk/feed/

#### Activism & Politics
7. **Novara Media** - https://novaramedia.com/feed/
8. **The Canary** - https://www.thecanary.co/feed/
9. **OpenDemocracy** - https://www.opendemocracy.net/en/feed/

#### Mainstream (Filtered)
10. **The Guardian (UK News)** - https://www.theguardian.com/uk-news/rss
11. **BBC News** - http://feeds.bbci.co.uk/news/rss.xml
12. **The Independent** - https://www.independent.co.uk/rss

#### Community & Local
13. **Local organization feeds** (add as discovered)
14. **Black-led initiatives** (add as discovered)
15. **QTIPOC groups** (add as discovered)

---

### B. AI Classification Prompts

#### Content Relevance Classifier

```
You are a content curator for BLKOUT, a platform serving Black queer communities in the UK.

Analyze this article and provide:
1. Relevance Score (0-100): How relevant is this to Black QTIPOC communities?
2. Category: original / curated / community-response
3. Reasoning: Brief explanation of scoring
4. Suggested Action: auto-approve / review / reject

Article:
Title: {title}
Content: {content}
Source: {source}

Criteria for high relevance:
- Directly discusses Black queer experiences
- Covers UK-specific Black community issues
- Addresses liberation, justice, activism
- QTIPOC-led initiatives or voices
- Systemic racism, discrimination, resistance

Criteria for rejection:
- Harmful stereotypes or misrepresentation
- Not UK-relevant
- Clickbait without substance
- Irrelevant to community focus

Output as JSON:
{
  "score": 0-100,
  "category": "original|curated|community-response",
  "reasoning": "explanation",
  "action": "approve|review|reject",
  "tags": ["suggested", "tags"]
}
```

---

#### Social Media Caption Generator

```
You are a social media manager for BLKOUT, a Black queer liberation platform.

Generate a {platform}-optimized post for this content:

Content Type: {event|article}
Title: {title}
Description: {description}
URL: {url}

Platform Guidelines:
- LinkedIn: Professional, informative, 100-150 words
- Instagram: Visual, community-focused, emotional, use emojis, max 125 chars first line
- Facebook: Detailed, conversational, call-to-action, 150-200 words
- Twitter/X: Concise, engaging, hashtags, max 280 chars

Tone: Empowering, authentic, community-centered
Include: Relevant hashtags, call-to-action, accessibility considerations

Output:
{
  "caption": "platform-optimized text",
  "hashtags": ["relevant", "hashtags"],
  "alt_text": "image description if applicable"
}
```

---

### C. Emergency Contacts & Runbooks

#### System Administrators
- **Primary Technical Lead**: [contact]
- **Backup Admin**: [contact]
- **Community Coordinator**: [contact]

#### Critical Runbooks

**1. n8n Down**
```bash
# Check status
docker ps | grep n8n

# Restart
docker restart n8n

# Check logs
docker logs n8n --tail 100

# If still down, contact tech lead
```

**2. Workflow Errors**
```
1. Check n8n UI → Executions → Filter by "error"
2. Review error message
3. Check if API keys expired
4. Verify external service availability
5. Manually retry if transient error
6. Disable workflow if persistent issues
```

**3. API Rate Limits Exceeded**
```
1. Identify which API (check error logs)
2. Pause associated workflows
3. Implement delay (increase interval)
4. Consider upgrading API tier or adding alternative source
5. Resume workflows with new limits
```

---

### D. Training Resources

#### For Community Members

1. **n8n Basics** (1 hour video)
   - Understanding workflows
   - Reading execution logs
   - Basic troubleshooting
   - When to escalate

2. **Content Moderation** (30 min video)
   - Using AI recommendations
   - Override capabilities
   - Quality standards
   - Community guidelines

3. **System Health Monitoring** (20 min doc)
   - Key metrics to watch
   - Normal vs concerning trends
   - Alert response procedures

#### For Technical Team

1. **n8n Advanced** (2 hour workshop)
   - Building workflows from scratch
   - Error handling best practices
   - Performance optimization
   - Security considerations

2. **API Integration** (1 hour doc)
   - OAuth 2.0 flows
   - Rate limiting strategies
   - Webhook security
   - Testing integrations

3. **Incident Response** (1 hour workshop)
   - Diagnosis procedures
   - Rollback protocols
   - Communication during incidents
   - Post-incident reviews

---

## Conclusion

This Phase 2 implementation plan transforms BLKOUT from a manually-managed platform into a **self-sustaining, community-powered automation hub** while maintaining strict adherence to cooperative ownership and digital sovereignty values.

**Key Achievements:**
- ✅ **$860-6,840/year saved** vs commercial alternatives
- ✅ **90%+ reduction** in manual content management
- ✅ **Complete data sovereignty** maintained
- ✅ **Community-owned infrastructure** from day one
- ✅ **Scalable foundation** for future growth

**Timeline**: 12 weeks to full production deployment
**Budget**: $30/month average ongoing cost
**Team**: Technical lead + 3-5 community volunteers

**Next Action**: Community review and approval vote

---

*"Building the world we want to live in, one workflow at a time."*

**Document Version**: 2.0
**Last Updated**: November 2025
**Maintained By**: BLKOUT Technical Cooperative
