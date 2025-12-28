---
name: geo-analytics
description: GEO analytics and measurement. AI engine citation tracking, generative appearance monitoring, and GEO performance reporting.
metadata:
  skillport:
    category: marketing
    tags:
      - geo-analytics
      - ai-citation-tracking
      - generative-appearance
      - geo-metrics
      - ai-performance
---

# GEO Analytics - Measurement & Reporting for Generative Engines

> AI citation tracking, generative appearance monitoring, and GEO performance metrics.
> Measuring visibility across ChatGPT, Claude, Perplexity, and Google Gemini.

---

# Table of Contents

1. [GEO Metrics Framework](#1-geo-metrics-framework)
2. [AI Citation Tracking](#2-ai-citation-tracking)
3. [Competitive Analysis](#3-competitive-analysis)
4. [GEO Reporting](#4-geo-reporting)
5. [Tools and Implementation](#5-tools-and-implementation)
6. [Checklist](#6-checklist)

---

# 1. GEO Metrics Framework

## 1.1 Primary GEO Metrics

| Metric | Definition | Calculation | Target |
|--------|------------|-------------|--------|
| **Generative Appearance Score (GAS)** | % of AI responses citing your brand | (Brand Citations / Total AI Responses) × 100 | >10% for brand terms |
| **AI Citation Rate** | Total citations across AI platforms | Monthly citation count | 10-20% MoM growth |
| **Share of AI Voice** | Your citations vs competitors | Your Citations / Total Citations | >25% in your niche |
| **Citation Quality Score** | Weighted citation value | Query Volume × Citation Position × Prominence | Increasing trend |
| **Brand Mention in AI** | Brand mentions without links | Monthly mention count | Increasing trend |

## 1.2 Secondary Metrics

| Metric | Definition | Relevance |
|--------|------------|-----------|
| **AI-Referred Traffic** | Traffic from AI response clicks | UTM tracking |
| **Query Coverage** | % of target queries where you're cited | Citation breadth |
| **Entity Recognition Rate** | AI correctly identifies your entity | Brand accuracy |
| **Citation Recency** | Fresh citations vs old content | Content freshness |
| **Platform Distribution** | Citations per AI platform | Platform presence |

## 1.3 Metric Hierarchy

```markdown
Priority Levels for GEO:

Tier 1 (Critical):
☐ AI Citation Rate - Primary success indicator
☐ Share of AI Voice - Competitive position
☐ Generative Appearance Score - Visibility level

Tier 2 (Important):
☐ Citation Quality Score - Impact measurement
☐ AI-Referred Traffic - Business value
☐ Brand Mention Trends - Awareness growth

Tier 3 (Nice to Have):
☐ Query Coverage - Breadth measurement
☐ Entity Recognition - Accuracy check
☐ Platform Distribution - Multi-platform presence
```

---

# 2. AI Citation Tracking

## 2.1 Manual Tracking Process

```markdown
Step-by-Step Manual Citation Monitoring:

1. Query Selection
   - Identify top 50 target queries
   - Include brand terms
   - Include industry topics
   - Include product-specific queries

2. Platform Testing
   For each query, test across:
   ☐ ChatGPT (GPT-4)
   ☐ Claude (Claude 3.5)
   ☐ Perplexity AI
   ☐ Google Gemini (SGE)
   ☐ Microsoft Copilot

3. Citation Recording
   Track:
   - Citation or not
   - Citation position (first, middle, last)
   - Citation context (direct quote, general reference)
   - Competitor citations
   - Date recorded

4. Data Organization
   Use spreadsheet:
   | Query | Platform | Cited? | Position | Competitors | Date |
   |-------|----------|--------|----------|------------|------|
```

## 2.2 Automated Tracking Approaches

```markdown
Semi-Automated Monitoring:

1. Browser Extensions (Emerging)
   - AI citation trackers (2025+)
   - Brand mention monitors
   - Search result analyzers

2. Custom Scripts
   Python example (concept):
   ```python
   # Track brand mentions in AI responses
   queries = ["what is geo", "geo vs seo", "best geo strategies"]
   platforms = ["chatgpt", "claude", "perplexity"]

   for query in queries:
       for platform in platforms:
           response = ai_search(platform, query)
           if brand_mentioned(response, "Your Brand"):
               citations.append({
                   "query": query,
                   "platform": platform,
                   "cited": True,
                   "context": extract_context(response)
               })
   ```

3. API-Based Tracking (Enterprise)
   - OpenAI API for analysis
   - Perplexity API for search
   - Custom web scraping (where allowed)

Note: Automated GEO tracking is an emerging field.
Many tools are in development as of 2025.
```

## 2.3 UTM Tracking for AI-Referred Traffic

```markdown
AI-Referred Traffic Measurement:

Since AI engines don't always pass referrer data,
use brand monitoring + UTM parameters:

Strategy 1: Trackable Links
If AI engines cite your content:
- Monitor traffic spikes
- Check direct traffic increases
- Analyze new visitor patterns

Strategy 2: Brand-Only CTAs
Encourage AI users to search for your brand:
"Cited by Your Brand - search for more insights"

Strategy 3: AI-Specific Landing Pages
Create pages specifically mentioned in content:
"Learn more at example.com/ai-guide"
Track visits to these specific URLs
```

## 2.4 Citation Quality Scoring

```markdown
Citation Quality Framework:

For each citation, calculate score:

Position Score:
- First citation: 100 points
- Middle citation: 75 points
- Last citation: 50 points
- General mention: 25 points

Query Volume Score:
- High volume (>10K searches): 100 points
- Medium volume (1K-10K): 75 points
- Low volume (<1K): 50 points

Citation Context Score:
- Direct quote: 100 points
- Specific reference: 75 points
- General mention: 50 points

Overall Quality Score:
= (Position × 0.4) + (Volume × 0.3) + (Context × 0.3)
```

---

# 3. Competitive Analysis

## 3.1 Competitor Identification

```markdown
Finding Your GEO Competitors:

1. Direct Competitors
   - Brands in your industry
   - Similar service offerings
   - Target same keywords

2. Citation Competitors
   - Check AI responses for your queries
   - Note who gets cited
   - May differ from SEO competitors

3. Identify Top 5 Competitors
   - Most frequently cited
   - Highest authority
   - Best positioned in AI responses
```

## 3.2 Competitive Citation Tracking

```markdown
Competitive Monitoring Template:

Query: [Target query]
Platform: [AI engine]
Date: [Date]

Citations Found:
☐ Your Brand (Position: X)
☐ Competitor A (Position: Y)
☐ Competitor B (Position: Z)
☐ Competitor C (Position: W)

Citation Analysis:
- Total sources cited: 5-10
- Your position: 1st / 2nd / 3rd
- Citation gap vs leader

Repeat for:
- Top 20 target queries
- All 5 major AI platforms
- Monthly tracking cycle
```

## 3.3 Share of AI Voice Calculation

```markdown
Share of AI Voice (SAV) Formula:

For a specific query set:
SAV = Your Citations / (Your Citations + Competitor Citations)

Example:
Query: "what is geo"
- Your Brand: 8 citations
- Competitor A: 12 citations
- Competitor B: 5 citations
- Competitor C: 3 citations

Total citations: 28
Your SAV = 8 / 28 = 28.6%

Target SAV by market position:
- Market leader: >40%
- Strong competitor: 25-40%
- Growing presence: 10-25%
- Emerging: <10%
```

## 3.4 Gap Analysis

```markdown
Competitive Gap Analysis:

For each competitor, analyze:

Content Gaps:
- What topics do they cover that you don't?
- What formats do they use?
- How do they structure content?

Entity Gaps:
- What entities do they rank for?
- What relationships do they establish?
- How do they define concepts?

Authority Gaps:
- What sources cite them?
- What's their domain authority?
- What's their brand recognition?

Strategy:
- Identify gaps to close
- Prioritize by impact
- Create action plan
```

---

# 4. GEO Reporting

## 4.1 Monthly GEO Report Template

```markdown
# GEO Performance Report - [Month, Year]

## Executive Summary
- 🎯 Key wins
- ⚠️ Points to note
- 💡 Recommendations

## Citation Overview

### Citation Growth
| Metric | This Month | Last Month | Change |
|--------|------------|------------|--------|
| Total Citations | 156 | 128 | ↑ +21.9% |
| ChatGPT Citations | 45 | 38 | ↑ +18.4% |
| Claude Citations | 32 | 28 | ↑ +14.3% |
| Perplexity Citations | 48 | 38 | ↑ +26.3% |
| Gemini Citations | 31 | 24 | ↑ +29.2% |

### Share of AI Voice
| Query Set | Your SAV | Leader SAV | Gap |
|-----------|----------|------------|-----|
| Brand Terms | 42% | 42% | ✅ Leader |
| Industry Topics | 28% | 35% | -7% |
| Product Queries | 18% | 45% | -27% |

## Top Cited Content

| Content | Citations | Platform | Query Volume |
|---------|-----------|----------|--------------|
| GEO vs SEO Guide | 23 | Perplexity | High |
| 2025 GEO Statistics | 18 | ChatGPT | Medium |
| What is GEO? | 15 | Gemini | High |

## Competitive Position

| Competitor | Their Citations | Your Citations | Gap |
|------------|-----------------|----------------|-----|
| Competitor A | 198 | 156 | -42 |
| Competitor B | 134 | 156 | +22 |
| Competitor C | 89 | 156 | +67 |

## Citation Quality Analysis

| Metric | Score | Change |
|--------|-------|--------|
| Avg. Citation Position | 2.3 | ↑ +0.4 |
| High-Value Citations | 68% | ↑ +8% |
| Direct Quotes | 45% | ↑ +3% |

## Content Performance

### Top Performing
- ✅ GEO Statistics 2025 - 23 citations
- ✅ Entity Optimization Guide - 19 citations
- ✅ RAG Explained - 15 citations

### Underperforming (High potential, low citations)
- ⚠️ Local GEO Strategies - 3 citations
- ⚠️ GEO Tools Comparison - 5 citations
- ⚠️ Enterprise GEO - 2 citations

## Action Items

### Completed
- ✅ Published original GEO survey
- ✅ Added FAQ sections to top 10 pages
- ✅ Updated schema markup

### Next Month Priorities
1. Create "Local GEO" comprehensive guide
2. Update "GEO Tools" with 2025 data
3. Build 5 more entity-defining pages
4. Outreach for 10 industry expert quotes
```

## 4.2 Weekly Quick Report

```markdown
# Weekly GEO Snapshot - Week [#]

📊 Citation Count: [Number] (↑/↓ [%] vs last week)
🎯 Share of AI Voice: [%] (↑/↓ [%])
🏆 Competitive Position: [#X] position
📈 Top Content: [Page name] - [X] new citations

### Weekly Highlights
- [Key win 1]
- [Key win 2]

### Areas for Improvement
- [Gap identified]
- [Action item]

### Next Week Focus
1. [Priority 1]
2. [Priority 2]
```

## 4.3 Quarterly Strategic Report

```markdown
# Quarterly GEO Strategy Review - Q[X] [Year]

## Q-Quarter Performance

### Citation Growth Trend
| Month | Citations | Growth |
|-------|-----------|--------|
| Month 1 | 128 | - |
| Month 2 | 156 | +21.9% |
| Month 3 | 198 | +26.9% |

### Platform Performance
- ChatGPT: [Trend]
- Claude: [Trend]
- Perplexity: [Trend]
- Gemini: [Trend]

## Strategic Analysis

### What Worked
1. [Successful tactic 1]
2. [Successful tactic 2]

### What Didn't Work
1. [Failed tactic 1]
2. [Failed tactic 2]

### Competitive Shifts
- [New competitor emerged?]
- [Competitor lost ground?]
- [Market changes?]

## Next Quarter Strategy

### Focus Areas
1. [Strategic priority 1]
2. [Strategic priority 2]
3. [Strategic priority 3]

### Investment Allocation
- Content creation: [%]
- Technical optimization: [%]
- Outreach/PR: [%]
- Tools/automation: [%]

### Goals
- Citation target: [Number]
- SAV target: [%]
- New content pieces: [Number]
```

---

# 5. Tools and Implementation

## 5.1 Spreadsheet Template

```markdown
GEO Tracking Spreadsheet Structure:

Sheet 1: Citation Log
| Date | Query | Platform | Your Brand | Position | Competitor Citations | Notes |

Sheet 2: Competitor Matrix
| Competitor | Domain | Monthly Citations | SAV | Strengths | Gaps |

Sheet 3: Content Performance
| Content URL | Title | Total Citations | Last Citation | Quality Score | Status |

Sheet 4: Platform Summary
| Platform | Total Citations | Your Share | Trend | Notes |

Sheet 5: Action Items
| Priority | Task | Owner | Due Date | Status |
```

## 5.2 Dashboard Metrics

```markdown
GEO Dashboard Components:

1. Overview Panel
   - Total citations (all-time, this month)
   - Citation growth rate
   - Share of AI Voice
   - Competitive position

2. Trend Charts
   - Citations over time (line chart)
   - Platform distribution (pie chart)
   - Competitor comparison (bar chart)
   - Quality score trend (line chart)

3. Content Performance
   - Top cited content table
   - Underperforming content list
   - Content gap analysis

4. Competitive Intelligence
   - Competitor citation trends
   - SAV comparison
   - Gap analysis

5. Action Center
   - Outstanding tasks
   - Optimization opportunities
   - Content recommendations
```

## 5.3 Alert Configuration

```markdown
GEO Alerts to Set Up:

Daily/Weekly:
- New citations detected
- Competitor surge (unusual increase)
- Position drop in key queries

Monthly:
- Citation trends vs targets
- SAV changes
- New competitors identified

Quarterly:
- Strategic performance review
- Market position shifts
- Tool/technology updates
```

---

# 6. Checklist

## Tracking Setup

```markdown
☐ Query list defined (top 50)
☐ Competitor list identified (top 5)
☐ Spreadsheet template created
☐ Baseline citation count documented
☐ Monthly monitoring schedule set
☐ Alert configuration defined
☐ UTM tracking parameters set
```

## Monthly Tasks

```markdown
☐ Manual citation search completed
☐ All 5 platforms tested
☐ Spreadsheet updated
☐ SAV calculated
☐ Competitive analysis updated
☐ Quality scores calculated
☐ Monthly report generated
☐ Action items reviewed
```

## Quarterly Tasks

```markdown
☐ Strategic performance review
☐ Competitive landscape analysis
☐ Tool/technology assessment
☐ Goal setting for next quarter
☐ Strategy adjustment
☐ Resource allocation review
```

## Ongoing Monitoring

```markdown
☐ Citation trends tracked
☐ Competitor movements monitored
☐ Content performance analyzed
☐ Platform changes noted
☐ New AI engines tested
☐ Industry developments tracked
```

---

**Last Updated:** December 2025
**Version:** 1.0

## Sources

- [GEO: Generative Engine Optimization](https://arxiv.org/abs/2311.09735) - Aggarwal et al., KDD 2024
- [AI Citation Tracking Methods](https://www.searchenginejournal.com/ai-search-analytics/)
- [Generative Engine Metrics Framework](https://www.marketingprofs.com/ai-search-metrics/)
