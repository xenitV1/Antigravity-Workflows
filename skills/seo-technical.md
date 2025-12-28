---
name: seo-technical
description: Technical SEO, Core Web Vitals, site structure and performance optimization. Mobile-first and voice search strategies.
metadata:
  skillport:
    category: marketing
    tags:
      - technical-seo
      - core-web-vitals
      - site-structure
      - mobile-first
      - voice-search
---

# SEO Technical - Technical SEO & Core Web Vitals

> Core Web Vitals, site structure, mobile-first indexing and voice search optimization.
> 2025 technical SEO standards and performance metrics.

---

# 📋 Table of Contents

1. [Core Web Vitals & Technical SEO](#1-core-web-vitals--technical-seo)
2. [Mobile-First Optimization](#2-mobile-first-optimization)
3. [Checklist](#3-checklist)

---

# 1. Core Web Vitals & Technical SEO

## 1.1 Core Web Vitals Metrics (2025)

| Metric | Target | Description |
|--------|--------|-------------|
| **LCP (Largest Contentful Paint)** | < 2.5 seconds | Main content loading time |
| **INP (Interaction to Next Paint)** | < 200 ms | Response speed to user interactions (replaced FID) |
| **CLS (Cumulative Layout Shift)** | < 0.1 | Visual stability (page shift) |

## 1.2 Technical SEO Checklist

### Site Structure and Indexing
```markdown
☐ XML Sitemap created and submitted to Google Search Console
☐ robots.txt properly configured
☐ Canonical tags correctly used
☐ Hreflang tags (for multilingual sites)
☐ 301 redirects properly configured
☐ 404 errors fixed
☐ Broken link check completed
```

### Page Speed Optimization
```markdown
☐ Image optimization (WebP/AVIF format)
☐ Lazy loading implemented
☐ Minification (CSS, JS, HTML)
☐ GZIP/Brotli compression active
☐ Browser caching configured
☐ CDN usage
☐ Critical CSS inlined
```

### Mobile-First Optimization
```markdown
☐ Responsive design
☐ Mobile-friendly test passed
☐ Touch-friendly UI elements
☐ Viewport meta tag correct
☐ Font sizes readable (min 16px)
```

### Structured Data (Schema Markup)
```markdown
☐ Article schema
☐ Product schema (for e-commerce)
☐ LocalBusiness schema (for local SEO)
☐ FAQ schema
☐ Breadcrumb schema
☐ Review/Rating schema
☐ Organization schema
```

## 1.3 Core Web Vitals Measurement Tools

1. **Google PageSpeed Insights**: https://pagespeed.web.dev/
2. **Google Search Console**: Core Web Vitals report
3. **Lighthouse**: Chrome DevTools integration
4. **WebPageTest**: Detailed performance analysis
5. **GTmetrix**: Comprehensive speed test

## 1.4 Improvement Recommendations

```javascript
// Image optimization example
<img
  src="hero.webp"
  srcset="hero-320w.webp 320w, hero-640w.webp 640w, hero-1024w.webp 1024w"
  sizes="(max-width: 600px) 100vw, 50vw"
  alt="Descriptive alt text"
  loading="lazy"
  width="1024"
  height="768"
/>

// Critical CSS inline
<style>
  /* Above-the-fold critical styles */
  .hero { display: flex; min-height: 100vh; }
</style>

// Defer non-critical JS
<script src="analytics.js" defer></script>
<script src="chatwidget.js" async></script>
```

---

# 2. Mobile-First Optimization

## 2.1 Mobile-First Indexing

Google now primarily indexes the mobile version of your site.

### Mobile Optimization Checklist

```markdown
☐ Responsive design (not adaptive)
☐ Mobile-friendly test passed (Google)
☐ Font size minimum 16px
☐ Touch targets minimum 48x48 px
☐ No horizontal scrolling
☐ Viewport meta tag correct:
  <meta name="viewport" content="width=device-width, initial-scale=1">
☐ Pop-ups not intrusive
☐ Mobile page speed < 3 seconds
☐ Thumb-friendly navigation
☐ Forms mobile-optimized (large input, autofill)
```

### Mobile UX Best Practices

```markdown
✅ Hamburger menu (three lines)
✅ Sticky header/navigation
✅ Large, tappable buttons
✅ Minimal text input
✅ Auto-fill and auto-suggest
✅ Click-to-call buttons
✅ Google Maps integration
✅ Accelerated Mobile Pages (AMP) - optional

❌ Flash usage
❌ Small fonts
❌ Close buttons (accidental clicks)
❌ Interstitial pop-ups
```

---

# 3. Checklist

## Technical SEO Audit

```markdown
### Site Structure
☐ XML Sitemap current
☐ robots.txt correct
☐ Canonical tags proper
☐ Hreflang tags (multilingual)
☐ 301 redirects configured
☐ 404 errors fixed

### Performance
☐ Core Web Vitals targets met
☐ Image optimization done
☐ Lazy loading active
☐ Minification applied
☐ Compression active
☐ CDN in use

### Mobile
☐ Mobile-friendly test passed
☐ Responsive design working
☐ Touch targets adequate size
☐ Font sizes readable

### Schema & Structured Data
☐ Relevant schema markups added
☐ Google Rich Results Test passed
☐ Structured data error-free
```

## Voice Search Readiness

```markdown
☐ Natural language content used
☐ Question-format headings added
☐ Featured snippet optimization done
☐ FAQ schema added
☐ Local SEO strengthened
☐ Page speed < 2.5 seconds
```

---

**Last Updated:** December 2025
**Version:** 1.0

## Sources

- [A Comprehensive Technical SEO Checklist for 2025](https://dashthis.com/blog/technical-seo-checklist/)
- [Webflow technical SEO guide for fixing Core Web Vitals in 2025](https://www.broworks.net/blog/webflow-technical-seo-guide-for-fixing-core-web-vitals-in-2025)
- [Full Technical SEO Checklist (from Start to Finish)](https://www.semrush.com/blog/technical-seo-checklist/)
