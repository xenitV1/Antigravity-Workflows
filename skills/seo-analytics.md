---
name: seo-analytics
description: SEO analytics, measurement and reporting. Google Analytics, Search Console and SEO tools usage.
metadata:
  skillport:
    category: marketing
    tags:
      - seo-analytics
      - google-analytics
      - search-console
      - seo-tools
      - reporting
---

# SEO Analytics - Measurement & Reporting

> Performance measurement with Google Analytics 4, Search Console and SEO tools.
> KPI tracking, reporting and data-driven SEO strategies.

---

# 📋 Table of Contents

1. [Key Performance Indicators](#1-key-performance-indicators)
2. [Google Search Console](#2-google-search-console)
3. [Google Analytics 4](#3-google-analytics-4)
4. [SEO Tools](#4-seo-tools)
5. [Reporting Framework](#5-reporting-framework)
6. [Checklist](#6-checklist)

---

# 1. Key Performance Indicators

## 1.1 Essential KPIs

| KPI | Description | Tool |
|-----|-------------|------|
| **Organic Traffic** | Visitors from search engines | Google Analytics 4 |
| **Keyword Rankings** | Target keyword positions | Ahrefs, SEMrush, GSC |
| **Click-Through Rate (CTR)** | Click rate relative to impressions | Google Search Console |
| **Bounce Rate** | Single-page exit rate | GA4 |
| **Avg. Session Duration** | Average session time | GA4 |
| **Pages per Session** | Page views per session | GA4 |
| **Conversion Rate** | Goal conversion rate | GA4 |
| **Backlink Profile** | Total backlinks, referring domains | Ahrefs, Majestic |
| **Domain Authority (DA)** | Site authority (Moz metric) | Moz, Ahrefs |
| **Core Web Vitals** | LCP, INP, CLS | GSC, PageSpeed Insights |

---

# 2. Google Search Console

## 2.1 Important Reports

### Performance Report

```markdown
Metrics:
- Total clicks
- Total impressions
- Average CTR
- Average position

Analysis:
- Query-based (which keywords bring traffic)
- Page-based (which pages perform well)
- Country-based (which countries)
- Device-based (mobile vs desktop)
```

### Coverage Report

```markdown
☐ Check indexed pages
☐ Fix errors
☐ Review warnings
☐ Analyze excluded pages
☐ Optimize valid pages
```

### Core Web Vitals

```markdown
☐ Mobile performance
☐ Desktop performance
☐ Poor URLs - fix urgently
☐ Needs improvement - optimize
☐ Good URLs - maintain
```

### Links Report

```markdown
Review:
- Top linking sites (who's linking)
- Top linked pages (which pages get links)
- Internal linking (internal link structure)
```

## 2.2 GSC Insights & Actions

```markdown
Which keywords get impressions but no clicks?
→ Action: Title/description optimization

Which pages are dropping in rank?
→ Action: Content refresh, add backlinks

Which pages aren't indexed at all?
→ Action: Check robots.txt, canonical, noindex

Which sites are giving backlinks?
→ Action: Strengthen relationship, request more links
```

---

# 3. Google Analytics 4

## 3.1 Important Metrics for SEO

### Organic Traffic

```markdown
Reports > Acquisition > Traffic acquisition
Filter: session_source/medium = google / organic

Review:
- Traffic trend (increasing or decreasing)
- New vs returning users
- Device breakdown (mobile, desktop, tablet)
```

### Landing Pages Performance

```markdown
Reports > Engagement > Landing page
+ Secondary dimension: Session source/medium = google/organic

Metrics:
- Sessions
- Bounce rate
- Average engagement time
- Conversions
```

### User Behavior Flow

```markdown
Explore > Path exploration
Starting point: Landing page

Analysis:
- Where users go next
- Where drop-off occurs
- What's the conversion path
```

### Conversions

```markdown
Reports > Monetization > Conversions
Filter by: First user default channel grouping = Organic Search

Measure:
- Lead form submissions
- Purchases
- Newsletter signups
- Custom events
```

## 3.2 Custom SEO Dashboard

```markdown
Dashboard Components:

1. Traffic Overview
   - Organic sessions (trend chart)
   - New vs returning users
   - Device breakdown (pie chart)

2. Top Landing Pages
   - Sessions, bounce rate, conversion rate (table)

3. Top Organic Keywords (GSC integration)
   - Clicks, impressions, CTR, position (table)

4. Goal Completions
   - Lead forms, purchases, signups (bar chart)

5. Site Speed
   - Avg page load time
   - Core Web Vitals (gauge)
```

---

# 4. SEO Tools

## 4.1 All-in-One Platforms

| Tool | Strengths | Price |
|------|-----------|-------|
| **Ahrefs** | Backlink analysis, competitor research, keyword research | $99/mo |
| **SEMrush** | Comprehensive SEO suite, PPC integration, position tracking | $119/mo |
| **Moz Pro** | DA/PA metrics, site audit, rank tracking | $99/mo |

## 4.2 Specialized Tools

### Keyword Research

```markdown
- Google Keyword Planner (free)
- Ubersuggest ($29/mo)
- AnswerThePublic ($99/mo)
- KeywordTool.io ($89/mo)
```

### Technical SEO

```markdown
- Screaming Frog (£149/year)
- Sitebulb ($35/mo)
- DeepCrawl ($300+/mo)
```

### Rank Tracking

```markdown
- AccuRanker ($116/mo)
- SERPWatcher (Mangools) ($49/mo)
- Rank Tracker (SEO PowerSuite) ($299/year)
```

### Backlink Analysis

```markdown
- Majestic ($49/mo)
- Monitor Backlinks ($25/mo)
- LinkMiner (Mangools) ($49/mo included)
```

### Content Optimization

```markdown
- Clearscope ($170/mo)
- Surfer SEO ($99/mo)
- Frase ($45/mo)
- MarketMuse ($149/mo)
```

### Local SEO

```markdown
- BrightLocal ($29/mo)
- Whitespark ($25/mo)
- LocalFalcon ($25/mo)
```

### Free Tools

```markdown
✅ Free and Powerful:
- Google Search Console
- Google Analytics 4
- Google Business Profile
- Google PageSpeed Insights
- Google Mobile-Friendly Test
- Google Rich Results Test
- Bing Webmaster Tools
```

---

# 5. Reporting Framework

## 5.1 Monthly SEO Report Template

```markdown
# SEO Performance Report - [Month, Year]

## Executive Summary
- 🎯 Key wins
- ⚠️ Points to note
- 💡 Recommendations

## Traffic Overview
| Metric | This Month | Last Month | Change |
|--------|------------|------------|--------|
| Organic Sessions | 12,450 | 10,800 | ↑ +15.3% |
| Organic Users | 9,320 | 8,100 | ↑ +15.1% |
| Avg. Session Duration | 2:45 | 2:30 | ↑ +10% |
| Bounce Rate | 58% | 62% | ↓ -6.5% |
| Conversion Rate | 3.2% | 2.8% | ↑ +14.3% |

## Keyword Rankings
| Keyword | Position | Change | Search Volume | Est. Traffic |
|---------|----------|--------|---------------|--------------|
| what is seo | 3 | ↑ +2 | 12,000 | 1,800 |
| how to do seo | 8 | ↑ +5 | 8,000 | 640 |

## Top Landing Pages
| Page | Sessions | Conv. Rate | Avg. Position |
|------|----------|------------|---------------|
| /blog/seo-guide | 1,250 | 4.2% | 5.3 |

## Backlink Growth
| Metric | This Month | Last Month | Change |
|--------|------------|------------|--------|
| Total Backlinks | 1,250 | 1,120 | ↑ +11.6% |
| Referring Domains | 340 | 315 | ↑ +7.9% |
| Lost Backlinks | 25 | 18 | - |

## Technical Health
☐ Core Web Vitals: 85% Good URLs
☐ Crawl errors: 3 (fixed)
☐ Index coverage: 1,245 indexed

## Content Published
- [SEO Beginner Guide 2025] - /blog/seo-beginner
- [Local SEO Tips] - /blog/local-seo

## Completed Tasks
- ✅ 10 broken links fixed
- ✅ 5 new backlinks acquired
- ✅ Schema markup added to 20 pages

## Next Month Priorities
1. Content refresh: Top 10 old articles
2. Backlink outreach: 50 target sites
3. Technical audit: Site speed optimization
```

## 5.2 Weekly Quick Report

```markdown
# Weekly SEO Snapshot - Week [#]

📊 Traffic: [Number] sessions (↑/↓ [%] vs last week)
🎯 Rank Improvements: [X] keywords moved up
🔗 New Backlinks: [X] new referring domains
⚡ Page Speed: Avg [X]s (LCP)
✅ Tasks Completed: [X]/[Y]
```

---

# 6. Checklist

## Daily Monitoring

```markdown
☐ New errors in GSC
☐ Ranking changes (top 10 keywords)
☐ Organic traffic spike/drop
☐ Google algorithm update news
```

## Weekly Analysis

```markdown
☐ Traffic trend analysis
☐ Top landing pages performance
☐ New backlinks check
☐ Disavow toxic links if present
☐ Competitor ranking changes
```

## Monthly Reporting

```markdown
☐ Full traffic report (GA4)
☐ Keyword ranking report (Ahrefs/SEMrush)
☐ Backlink profile analysis
☐ Content performance review
☐ Technical SEO audit
☐ Core Web Vitals check
☐ Conversion rate analysis
☐ ROI calculation
```

---

**Last Updated:** December 2025
**Version:** 1.0
