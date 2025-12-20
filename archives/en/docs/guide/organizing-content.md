---
title: "Organizing Content"
weight: 3
bookToc: true
---

# Organizing Content

Learn how to effectively organize your blog content.

## Directory Structure

hugo-book theme uses a hierarchical directory structure:

```
content.en/
├── docs/
│   ├── _index.md          # Section main page
│   ├── getting-started.md
│   ├── tutorials/          # Sub-section
│   │   ├── _index.md
│   │   ├── tutorial-1.md
│   │   └── tutorial-2.md
│   └── guides/
│       ├── _index.md
│       └── guide-1.md
└── posts/                  # Blog posts
    ├── _index.md
    └── 2025-01-01-my-post.md
```

## Categories and Tags

Hugo supports categories and tags through the Taxonomy system.

### Adding to Front Matter

```yaml
---
title: "Post Title"
categories: ["Tutorial", "Development"]
tags: ["hugo", "go", "web-development"]
---
```

### hugo.toml Configuration

To enable categories and tags:

```toml
# hugo.toml
[taxonomies]
  category = 'categories'
  tag = 'tags'
```

Note: hugo-book theme disables taxonomies by default, so you need to enable them in configuration.

### Taxonomy Pages

Hugo automatically generates these pages:

- `/categories/` - List of all categories
- `/categories/tutorial/` - Posts in "Tutorial" category
- `/tags/` - List of all tags
- `/tags/hugo/` - Posts with "hugo" tag

## Menu Configuration

### Auto Menu (File Tree)

hugo-book automatically generates sidebar menu from `content.en/docs/` directory structure.

Adjust menu order with `weight`:

```yaml
---
title: "First Document"
weight: 1  # Lower value appears higher
---
```

### Section Configuration

Control section behavior in `_index.md`:

```yaml
---
title: "Tutorials"
weight: 10
bookFlatSection: false      # Display sub-items flat
bookCollapseSection: true   # Collapsed by default
---
```

### Custom Menu

Define menu manually in hugo.toml:

```toml
[[menu.before]]
  name = "Home"
  url = "/"
  weight = 1

[[menu.after]]
  name = "GitHub"
  url = "https://github.com/yourusername"
  weight = 10
```

## Hiding Pages

Hide specific pages from menu:

```yaml
---
title: "Hidden Page"
bookHidden: true
---
```

## Exclude from Search

Exclude pages from search results:

```yaml
---
title: "Search Excluded Page"
bookSearchExclude: true
---
```

## Multi-language Content Organization

### Separation by Directory (Current Setup)

```
content.ko/      # Korean content
  docs/
    getting-started.md

content.en/      # English content
  docs/
    getting-started.md
```

### Separation by Filename (Alternative)

```
content/
  docs/
    getting-started.ko.md
    getting-started.en.md
```

### Translation Linking

To link multi-language versions of the same content, maintain identical file structure:

```
content.ko/docs/tutorial.md
content.en/docs/tutorial.md
```

Hugo automatically generates language switcher links.

## Static Files Organization

### Images

```
static/
  images/
    2025/
      01/
        photo.jpg
```

Usage:
```markdown
![Description](/images/2025/01/photo.jpg)
```

### Download Files

```
static/
  downloads/
    document.pdf
```

Link:
```markdown
[Download PDF](/downloads/document.pdf)
```

### Language-specific Static Files

```
static/
  ko/
    images/
      banner.jpg
  en/
    images/
      banner.jpg
```

## Archive Organization

### By Date

```
content.en/
  posts/
    2025/
      01/
        post-1.md
        post-2.md
```

### By Topic

```
content.en/
  docs/
    backend/
      _index.md
      django.md
      fastapi.md
    frontend/
      _index.md
      react.md
      vue.md
```

## Front Matter Templates

Use `archetypes` for consistent metadata:

### archetypes/docs.md

```yaml
---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
weight: 10
bookToc: true
categories: []
tags: []
---
```

Create new post:
```bash
hugo new --kind docs content.en/docs/my-post.md
```

## Organization Tips

1. **Maintain Consistent Structure**: Use identical directory structure across all languages
2. **Weight System**: Use increments like 10, 20, 30... for easy insertion later
3. **Naming Convention**: Use lowercase and hyphens for filenames (e.g., `my-post.md`)
4. **Use Sections**: Group related documents into sections
5. **Optimize for Search**: Include important keywords in titles and descriptions
6. **Use ToC**: Enable `bookToc: true` for long documents to improve readability
