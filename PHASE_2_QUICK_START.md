# BLKOUT Phase 2: Quick Start Guide

**Read this first, then refer to `PHASE_2_IMPLEMENTATION_PLAN.md` for details**

---

## TL;DR

**Goal**: Automate 90% of content management while maintaining community control
**Timeline**: 12 weeks
**Cost**: $30/month (saves $860-6,840/year vs paid alternatives)
**Approach**: Open source stack (n8n + FreshRSS + existing tools)

---

## What We're Building

### 1. Automated Content Discovery
- **RSS feeds** → 50-100 articles/week (auto-curated)
- **Event APIs** → 30-70 events/week (auto-discovered)
- **Chrome extension** → Community submissions (10-20/week)

### 2. Social Media Automation
- **Zero manual posting** required
- **AI-optimized captions** for each platform
- **Multi-platform distribution** (LinkedIn, Instagram, Facebook, Twitter/X)

### 3. Streamlined Moderation
- **AI-assisted classification** (50% time reduction)
- **Unified queue** across all platforms
- **Priority-based** alerts

### 4. Analytics & Reporting
- **Liberation-focused metrics** (not extraction-based)
- **Automated weekly reports**
- **Real-time community health monitoring**

### 5. Newsletter Automation
- **Weekly digest** auto-generated
- **No manual curation** needed
- **Professional templates**

---

## Technology Decisions

### ✅ CHOSEN: Open Source Stack

| Tool | Purpose | Cost |
|------|---------|------|
| **n8n** (self-hosted) | Workflow automation | $10-20/mo VPS |
| **FreshRSS** | RSS aggregation | $0 (same VPS) |
| **Formbricks** | Form builder | $0 (self-hosted) |
| **Postiz** | Social media UI | $0 (optional) |
| **OpenAI/Claude** | AI processing | $10-20/mo pay-per-use |

**Total**: $20-40/month

---

### ❌ REJECTED: Paid SaaS Tools

| Tool | Cost/Year | Why Rejected |
|------|-----------|--------------|
| **Marblism** | $468 | n8n does this better + free |
| **Formflow** | $348 | Formbricks is free + open source |
| **Content360** | $67 lifetime | n8n has same features |
| **Pyxa** | $50 lifetime | Direct AI APIs cheaper |
| **Total Avoided** | **$933+** | **Vendor lock-in, no sovereignty** |

---

## 12-Week Implementation Timeline

### Month 1: Content Automation Foundation

**Week 1**: Deploy n8n + infrastructure (4-6 hours)
**Week 2**: RSS automation via FreshRSS (6-8 hours)
**Week 3**: Event platform APIs (Eventbrite, Facebook) (8-10 hours)
**Week 4**: Chrome extension distribution (5-6 hours)

**Outcome**: 100-150 content items/week auto-curated

---

### Month 2: Distribution & Moderation

**Week 5**: Social media API setup (6-8 hours)
**Week 6**: Auto-posting workflows (10-12 hours)
**Week 7**: AI-assisted moderation (6-8 hours)
**Week 8**: Newsletter automation (8-10 hours)

**Outcome**: Zero manual social posting + automated weekly newsletter

---

### Month 3: Analytics & Polish

**Week 9**: Analytics automation (8-10 hours)
**Week 10**: Community forms deployment (6-8 hours)
**Week 11**: Advanced scraping (8-10 hours)
**Week 12**: Testing, docs, training (10-12 hours)

**Outcome**: Self-sustaining system requiring <2 hours/week oversight

---

## 18 Automated Workflows

### Content Discovery (5 workflows)
1. Daily News Scraper (RSS feeds)
2. Eventbrite Auto-Discovery
3. Facebook Events Discovery
4. Custom Site Scraper
5. Chrome Extension Handler

### Content Distribution (3 workflows)
6. Event → Social Media Auto-Post
7. Article → Social Media Auto-Post
8. Weekly Newsletter Generator

### Moderation (3 workflows)
9. AI-Assisted Classification
10. Cross-Platform Sync
11. Priority Alert System

### Analytics (4 workflows)
12. Community Health Monitoring
13. Weekly Analytics Report
14. Social Media Engagement Tracker
15. Workflow Monitoring

### Community Engagement (3 workflows)
16. Form Submission Handler
17. Community Response System (IVOR)
18. Partnership Amplification

---

## Infrastructure Requirements

### VPS Specs (Hetzner Cloud Recommended)

```
CPU: 4 vCPU
RAM: 8GB
Storage: 80GB SSD
Cost: €8.21/month (~$9/month)
```

### What Runs on VPS
- n8n (automation engine)
- FreshRSS (RSS aggregator)
- PostgreSQL (database)
- Uptime Kuma (monitoring - optional)

---

## APIs Needed

### Social Media (All Free Tier)
- [ ] LinkedIn Developer App
- [ ] Facebook/Instagram Graph API
- [ ] Twitter/X Developer Account
- [ ] YouTube Data API

### Content Discovery (All Free Tier)
- [ ] Eventbrite API
- [ ] Facebook Events (via Graph API)
- [ ] Meetup API (optional)

### AI Services (Pay-per-use)
- [ ] OpenAI API (~$5-10/month)
- [ ] Anthropic Claude (~$5-10/month)

### Communication (Free Tier)
- [ ] Telegram Bot (for alerts)
- [ ] SendGrid (0-100 emails/day free)

---

## Success Metrics

### After Month 1
- ✅ 100+ articles/week auto-curated
- ✅ 30+ events/week auto-discovered
- ✅ 15+ community members using extension
- ✅ 0 hours/week manual content discovery

### After Month 3
- ✅ 200+ items/week processed automatically
- ✅ 0 hours/week manual social posting
- ✅ 50% reduction in moderation time
- ✅ Weekly newsletter automated
- ✅ <2 hours/week system oversight needed

### After Month 6
- ✅ Self-sustaining content pipeline
- ✅ 50+ active community contributors
- ✅ Custom workflows by cooperative members
- ✅ Complete data sovereignty maintained

---

## Quick Commands Reference

### Deploy Infrastructure (Week 1)

```bash
# Clone docker-compose from plan
cd /home/user/Phase-1-website
# Copy docker-compose.yml from PHASE_2_IMPLEMENTATION_PLAN.md

# Start services
docker-compose up -d

# Access services
# n8n: https://your-domain.com:5678
# FreshRSS: https://your-domain.com:8080
```

### Add RSS Feeds (Week 2)

```bash
# Login to FreshRSS: http://your-server:8080
# Add feeds from Appendix A in implementation plan
# Configure auto-refresh: every 15 minutes
```

### Import n8n Workflows (Weeks 2-11)

```bash
# In n8n UI:
# 1. Go to Workflows
# 2. Click "Import from URL" or "Import from File"
# 3. Use templates from n8n.io or build from plan
```

---

## Critical Files Reference

### Your Existing Assets (Already Built!)

```
/blkout-extension/
├── content-scripts/detector.js       # Chrome extension scraper
├── popup/popup.js                    # Extension UI
└── manifest.json                     # Extension config

/src/services/
├── unifiedModerationBridge.ts        # Cross-platform moderation
└── moderationService.ts              # Moderation logic

/src/api/webhook/
└── moderation.ts                     # Moderation webhook

/api-backup/rag/
└── scrape.ts                         # Backend scraper (RSS + web)
```

### New Files to Create

```
/docker-compose.yml                   # Infrastructure setup
/.env                                 # Environment variables
/n8n-workflows/                       # Exported workflow JSON files
/docs/training/                       # Community training materials
```

---

## Week 1 Checklist (Start Here!)

### Day 1-2: VPS Setup
- [ ] Choose VPS provider (Hetzner recommended)
- [ ] Provision server (4 vCPU, 8GB RAM)
- [ ] Point domain to server IP
- [ ] Install Docker & Docker Compose
- [ ] Set up SSL certificate (Let's Encrypt)

### Day 3-4: Deploy Services
- [ ] Create docker-compose.yml
- [ ] Set environment variables
- [ ] Deploy n8n + FreshRSS + PostgreSQL
- [ ] Verify services are running
- [ ] Configure basic auth for n8n

### Day 5-7: Initial Configuration
- [ ] Create first n8n workflow (test)
- [ ] Add 3-5 RSS feeds to FreshRSS (test)
- [ ] Connect Supabase to n8n
- [ ] Test Telegram notifications
- [ ] Document credentials securely

**Time**: 4-6 hours total
**Outcome**: Working n8n instance ready for workflows

---

## Common Questions

### Q: Do we need all 18 workflows immediately?
**A**: No. Start with:
1. Daily News Scraper (Week 2)
2. Eventbrite Discovery (Week 3)
3. Event Auto-Post (Week 6)

Add others as needed.

---

### Q: What if we don't want to self-host?
**A**: Use n8n Cloud (€20/month, 2.5k executions)
- Pros: No server management
- Cons: Higher cost, less control
- Still way cheaper than Marblism + Formflow ($102/month)

---

### Q: Can we add back paid tools later?
**A**: Yes, but only if truly needed:
- **PaddyPost** ($47 lifetime): Simplified UI for non-technical team
- **Apify Event Scraper** ($49/month): If free APIs insufficient
- Avoid Marblism, Pyxa, Formflow - n8n does their jobs better

---

### Q: What if something breaks?
**A**: See PHASE_2_IMPLEMENTATION_PLAN.md → Appendix C: Emergency Runbooks
- Restart services: `docker restart n8n`
- Check logs: `docker logs n8n --tail 100`
- Contact: Technical lead (see contacts in plan)
- Worst case: Rollback to Phase 1 (manual operations)

---

### Q: Who maintains this after implementation?
**A**:
- **Technical team**: 1-2 hours/week monitoring + updates
- **Community moderators**: Use system as normal
- **Quarterly reviews**: Check metrics, adjust workflows
- **Training**: 3-5 community members can manage system

---

## Next Steps

1. **Review full plan**: Read `PHASE_2_IMPLEMENTATION_PLAN.md`
2. **Community discussion**: Share with cooperative members
3. **Get approval**: Vote on proceeding
4. **Assign roles**: Technical lead + volunteers
5. **Week 1 kickoff**: Deploy infrastructure
6. **Start building**: Follow 12-week timeline

---

## Support Resources

### Documentation
- Full Plan: `PHASE_2_IMPLEMENTATION_PLAN.md` (1,348 lines)
- n8n Docs: https://docs.n8n.io
- FreshRSS Docs: https://freshrss.github.io/FreshRSS/

### Community Templates
- n8n Workflows: https://n8n.io/workflows
- RSS Automation: https://n8n.io/workflows/categories/rss
- Social Media: https://n8n.io/workflows/categories/social-media

### Emergency Contacts
- Technical Lead: [Add contact]
- Backup Admin: [Add contact]
- Community Coordinator: [Add contact]

---

## Cost Summary (Quick Reference)

| Category | Monthly | Annual | 5-Year |
|----------|---------|--------|--------|
| **Phase 2 (Open Source)** | $30 | $360 | $1,800 |
| **Paid Tools Alternative** | $102 | $1,220 | $6,100 |
| **Enterprise SaaS** | $600+ | $7,200+ | $36,000+ |
| **YOU SAVE** | **$72-570** | **$860-6,840** | **$4,300-34,200** |

---

*"Move at the speed of trust. Build at the scale of liberation."*

**Ready to start? Go to Week 1, Day 1 in the full implementation plan.**
