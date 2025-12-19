---
title: "SEO Optimization"
weight: 4
bookToc: true
---

# SEO Optimization

Learn how to improve your blog's visibility through Search Engine Optimization (SEO).

## Basic SEO Configuration

### hugo.toml Settings

```toml
baseURL = 'https://chiho.me/'
title = 'My Blog'
languageCode = 'en-us'

# Google Analytics (optional)
googleAnalytics = 'G-XXXXXXXXXX'

# Author information
[author]
  name = 'Author Name'
  email = 'email@example.com'

# Social media
[params]
  description = 'Blog description'
  keywords = ['keyword1', 'keyword2', 'keyword3']
  images = ['/images/og-image.jpg']

[params.social]
  twitter = 'username'
  github = 'username'
```

### Robots.txt

Hugo automatically generates robots.txt. To customize:

```toml
# hugo.toml
enableRobotsTXT = true
```

Create `layouts/robots.txt`:

```
User-agent: *
Disallow: /admin/
Disallow: /private/

Sitemap: {{ .Site.BaseURL }}sitemap.xml
```

## Front Matter Optimization

Optimize metadata for each post:

```yaml
---
title: "Clear and Descriptive Title (under 60 chars)"
description: "Summary of page content (under 155 chars)"
date: 2025-12-19T20:00:00+09:00

# SEO metadata
keywords: ["keyword1", "keyword2", "keyword3"]
author: "Author Name"

# Open Graph (social media sharing)
images: ["/images/post-image.jpg"]

# Search engine crawling control
robots: "index, follow"
---
```

### Title Writing Tips

1. **Length**: 50-60 characters
2. **Keywords**: Place important keywords at the beginning
3. **Uniqueness**: Unique title for each page
4. **Meaning**: Clear title that encourages clicks

Examples:
```yaml
# Good
title: "Complete Guide to Hugo Blog SEO Optimization"

# Bad
title: "Blog Post 1"
```

### Description Writing Tips

1. **Length**: 120-155 characters
2. **Summary**: Accurately summarize page content
3. **Call-to-Action**: Include phrases that encourage clicks

```yaml
description: "Detailed guide on SEO configuration methods and best practices for Hugo static sites."
```

## Sitemap Configuration

Hugo automatically generates sitemap.xml.

### Customizing Sitemap

```toml
# hugo.toml
[sitemap]
  changefreq = 'weekly'
  filename = 'sitemap.xml'
  priority = 0.5
```

Per-page configuration in Front Matter:

```yaml
---
title: "Important Page"
sitemap:
  priority: 1.0
  changefreq: daily
---
```

## URL Structure

### Clean URLs

Hugo generates clean URLs by default:

```
/docs/getting-started/  (good)
/docs/getting-started.html  (not recommended)
```

### Permalinks Configuration

```toml
# hugo.toml
[permalinks]
  posts = '/blog/:year/:month/:slug/'
  docs = '/docs/:slug/'
```

Examples:
```
/blog/2025/12/my-post/
/docs/getting-started/
```

## Performance Optimization

### Image Optimization

1. **Appropriate Size**: Resize to needed dimensions
2. **Compression**: Use WebP, JPEG compression
3. **Lazy Loading**: Apply lazy loading

```markdown
![Description](/images/photo.jpg "Title")
```

Using Hugo Page Resources:

```
content.en/
  docs/
    my-post/
      index.md
      featured.jpg
```

### Minification

Automatic compression on build:

```toml
# hugo.toml
[minify]
  disableHTML = false
  disableCSS = false
  disableJS = false
  disableJSON = false
  disableXML = false
```

## Structured Data (Schema.org)

### Article Schema

Create `layouts/_default/single.html` or partial:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "{{ .Title }}",
  "description": "{{ .Description }}",
  "author": {
    "@type": "Person",
    "name": "{{ .Site.Author.name }}"
  },
  "datePublished": "{{ .Date.Format "2006-01-02" }}",
  "dateModified": "{{ .Lastmod.Format "2006-01-02" }}",
  "image": "{{ .Params.images | default .Site.Params.images }}",
  "url": "{{ .Permalink }}"
}
</script>
```

## Open Graph & Twitter Cards

hugo-book theme supports basic Open Graph. Additional configuration:

```yaml
---
title: "Post Title"
description: "Post description"
images: ["/images/og-image.jpg"]

# Twitter Card
twitter:
  card: "summary_large_image"
  site: "@username"
---
```

## Multi-language SEO

### hreflang Tags

Hugo automatically generates hreflang tags:

```html
<link rel="alternate" hreflang="ko" href="https://chiho.me/ko/docs/post/" />
<link rel="alternate" hreflang="en" href="https://chiho.me/en/docs/post/" />
```

### Per-language Sitemap

Separate sitemap for each language:
```
/ko/sitemap.xml
/en/sitemap.xml
/sitemap.xml (combined)
```

## Content Optimization

### Heading Structure

Use proper heading hierarchy:

```markdown
# H1 - Page Title (only one)

## H2 - Main Sections

### H3 - Sub-sections

#### H4 - Detailed Items
```

### Internal Linking

Link related content:

```markdown
For more details, see [Writing Posts]({{</* relref "writing-posts" */>}}).
```

### Keyword Usage

- Include main keywords in title and first paragraph
- Distribute keywords naturally throughout content
- Avoid keyword stuffing

## Analytics and Monitoring

### Google Analytics

```toml
# hugo.toml
googleAnalytics = 'G-XXXXXXXXXX'
```

### Google Search Console

1. Verify site ownership
2. Submit sitemap: `https://chiho.me/sitemap.xml`
3. Monitor crawling errors
4. Analyze search performance

### Performance Measurement Tools

- **Google PageSpeed Insights**: Page speed analysis
- **Lighthouse**: Overall quality assessment
- **GTmetrix**: Performance and optimization suggestions

## Checklist

Before publishing:

- [ ] Clear and descriptive title (under 60 chars)
- [ ] Appropriate description (under 155 chars)
- [ ] Keywords configured
- [ ] Image alt text added
- [ ] Internal links included
- [ ] Proper heading structure
- [ ] Open Graph image set
- [ ] URL structure verified
- [ ] Mobile-friendly tested
- [ ] Page loading speed checked

## Additional Resources

- [Google Search Central](https://developers.google.com/search)
- [Hugo SEO Documentation](https://gohugo.io/templates/embedded/#open-graph)
- [Schema.org](https://schema.org/)
- [Web.dev](https://web.dev/learn-core-web-vitals/)
