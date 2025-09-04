# BLKOUT Phase 1 Platform - Deployment Guide

## 🚀 Production Deployment Configuration

### Current Live Deployment
- **URL**: https://platform-blkout.vercel.app
- **Status**: ✅ Production Active
- **Last Deployed**: January 2025
- **Version**: Phase 1 Final

## 📋 Deployment Checklist

### ✅ Completed Phase 1 Components
1. **Core Platform** - Homepage with face-cycling GIF integration
2. **Admin Dashboard** - Secure authentication with BLKOUT2025! system  
3. **Unified Moderation** - Option 3 webhook bridge for cross-platform sync
4. **Community Features** - Governance, movement pages, newsroom
5. **Mobile Responsive** - Optimized for all device sizes
6. **Static Assets** - Properly configured Vercel routing
7. **Database Integration** - Supabase with real-time listeners
8. **Chrome Extension** - Content submission pipeline active

## 🔧 Environment Configuration

### Required Environment Variables (.env)
```bash
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your_anon_key_here
VITE_ADMIN_PASSWORD_BASE=BLKOUT2025!
VITE_GOOGLE_SHEET_ID=your_sheet_id_here
```

### Vercel Configuration (vercel.json)
```json
{
  "version": 2,
  "buildCommand": "npm run build",
  "outputDirectory": "dist",
  "framework": null,
  "installCommand": "npm ci --prefer-offline --no-audit",
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        {"key": "X-Content-Type-Options", "value": "nosniff"},
        {"key": "X-Frame-Options", "value": "DENY"},
        {"key": "X-XSS-Protection", "value": "1; mode=block"}
      ]
    }
  ],
  "rewrites": [
    {"source": "/downloads/(.*)", "destination": "/downloads/$1"},
    {"source": "/extension-download.html", "destination": "/extension-download.html"},
    {"source": "/(.*)", "destination": "/index.html"}
  ]
}
```

## 🗄️ Database Schema

### Supabase Tables
- **events**: Community events with moderation workflow
- **newsroom_articles**: News and community stories
- **contacts**: Organizer and contributor information
- **governance_docs**: Community governance documents

### Moderation Status Workflow
```
pending -> published (approved)
pending -> archived (rejected)
```

## 🔌 API Endpoints

### Webhook System (Option 3)
- `POST /api/webhook/moderation` - Cross-platform moderation sync
- `GET /api/webhook/moderation` - Health check endpoint

### Authentication Routes
- `/admin` - Main admin dashboard (requires BLKOUT2025!)
- `/admin/moderation` - Content moderation queue
- `/admin/events` - Events management
- `/admin/newsroom` - News management

## 🚀 Deployment Commands

### Local Development
```bash
npm install
npm run dev
```

### Production Build
```bash
npm run build
npm run preview  # Test production build locally
```

### Deploy to Vercel
```bash
vercel --prod
vercel alias platform-blkout.vercel.app  # Set custom alias
```

## 🔒 Security Features

### Authentication System
- **Password-only authentication** using BLKOUT2025!
- **Role differentiation** (admin vs moderator)
- **24-hour sessions** with 90-day temporary access period
- **Secure headers** for XSS and clickjacking protection

### Webhook Security
- **Signature verification** for cross-platform sync
- **User-Agent validation** for webhook requests
- **Payload validation** to prevent malicious data

## 📊 Performance Optimization

### Build Optimization
- **Code splitting** with Vite
- **Tree shaking** for minimal bundle size
- **Static asset optimization** with proper caching headers
- **Responsive image loading** with lazy loading

### Runtime Performance  
- **React 18 Concurrent Features** for smooth UX
- **Framer Motion** optimized animations
- **Supabase real-time subscriptions** for live data
- **Service worker** for offline functionality

## 🔄 Cross-Platform Integration

### Events Calendar Sync
- **Webhook endpoint**: `https://events-blkout.vercel.app/api/webhook/moderation`
- **Real-time sync** between platform-blkout and events-blkout
- **Unified moderation queue** across both systems

### Chrome Extension Integration
- **Content submission pipeline** directly to Supabase
- **Automatic moderation workflow** with admin approval
- **Status tracking** from submission to publication

## 📱 Mobile Accessibility

### Responsive Design
- **Mobile-first approach** with TailwindCSS
- **Touch-friendly buttons** (minimum 44px tap targets)
- **Readable typography** with proper contrast ratios
- **Hamburger navigation** for mobile devices
- **Optimized loading** with progressive enhancement

### Accessibility Features
- **Screen reader support** with ARIA labels
- **Keyboard navigation** for all interactive elements
- **Skip navigation links** for keyboard users
- **Focus indicators** with proper contrast

## 🚨 Critical Notes

### Code Organization Achievement
- **✅ CONSOLIDATED CODEBASE**: Single repository contains complete Phase 1 platform
- **✅ ELIMINATED SPRAWL**: No more scattered files across multiple directories  
- **✅ PRODUCTION READY**: Clean, documented, deployable codebase
- **✅ UNIFIED ARCHITECTURE**: All components work together seamlessly

### Breaking Changes from Scattered Codebase
- **Centralized configuration** - All settings in single .env file
- **Unified build process** - Single package.json with all dependencies
- **Consolidated assets** - All images and static files in organized structure
- **Single deployment target** - One Vercel project, one production URL

## 🎯 Phase 2 Preparation

### Architectural Foundation Ready
- **Modular component structure** for easy extension
- **Service layer abstraction** for additional integrations
- **Database schema** designed for scalability
- **API architecture** ready for additional endpoints
- **Authentication system** ready for user registration

---

**BLKOUT Phase 1 Platform** • *Deployment Complete* • **January 2025**