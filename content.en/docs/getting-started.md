---
title: "Getting Started with Hugo"
weight: 1
bookToc: true
---

# Getting Started with Hugo

This is the first post using Hugo and hugo-book theme.

## What is Hugo?

Hugo is a Static Site Generator written in Go. It's known for its fast build speed and simple usage.

### Key Features

- **Fast Speed**: Extremely fast build times thanks to Go
- **Easy to Use**: Get started without complex configuration
- **Multi-language Support**: Built-in support for multilingual sites
- **Rich Themes**: Wide variety of free themes available

## hugo-book Theme

This site uses the hugo-book theme. hugo-book is a clean theme optimized for documentation.

### Main Features

- Clean and simple design
- Mobile-friendly
- Dark mode support
- Built-in search functionality
- Automatic table of contents generation

## Multi-language Configuration

This site supports Korean and English. You can switch languages from the top menu.

```toml
# hugo.toml
defaultContentLanguage = 'ko'

[languages]
  [languages.ko]
    languageName = '한국어'
    contentDir = 'content.ko'
    weight = 1

  [languages.en]
    languageName = 'English'
    contentDir = 'content.en'
    weight = 2
```

## Blog Management Guides

Guides to effectively manage your blog:

- [Writing Posts]({{< relref "guide/writing-posts" >}}) - How to create new posts and configure Front Matter
- [Organizing Content]({{< relref "guide/organizing-content" >}}) - Categories, tags, and menu organization
- [SEO Optimization]({{< relref "guide/seo-optimization" >}}) - Search engine optimization settings

## Next Steps

- Customize the theme
- Configure deployment (GitHub Pages, Netlify, etc.)
