---
title: "Writing Posts"
weight: 2
bookToc: true
---

# Writing Posts

Learn how to create new posts in Hugo.

## Creating a New Post

Use the Hugo CLI to generate a new post:

```bash
# Create Korean post
hugo new content.ko/docs/my-first-post.md

# Create English post
hugo new content.en/docs/my-first-post.md
```

## Front Matter Configuration

Each post has Front Matter at the top defining metadata.

### Basic Configuration

```yaml
---
title: "Post Title"
date: 2025-12-19T20:00:00+09:00
weight: 10
bookToc: true
---
```

### Main Front Matter Options

| Option | Description | Example |
|--------|-------------|---------|
| `title` | Post title | "Getting Started with Hugo" |
| `date` | Publication date | 2025-12-19T20:00:00+09:00 |
| `weight` | Menu order (lower = higher) | 10 |
| `bookToc` | Show table of contents | true/false |
| `bookHidden` | Hide from menu | true/false |
| `bookFlatSection` | Display section flat | true/false |
| `bookCollapseSection` | Collapse section | true/false |

### Custom Metadata

Additional metadata for search and SEO:

```yaml
---
title: "Post Title"
description: "Brief description of the post"
tags: ["hugo", "blog", "web-development"]
categories: ["Tutorial"]
author: "Author Name"
---
```

## Writing Markdown

Hugo supports standard Markdown and extended features.

### Headings

```markdown
# H1 Heading
## H2 Heading
### H3 Heading
```

### Text Styles

```markdown
**Bold**
*Italic*
~~Strikethrough~~
`Inline code`
```

### Links and Images

```markdown
[Link text](https://example.com)
![Image description](/images/photo.jpg)
```

### Code Blocks

````markdown
```python
def hello():
    print("Hello, Hugo!")
```
````

### Lists

```markdown
- Item 1
- Item 2
  - Sub-item

1. Ordered item 1
2. Ordered item 2
```

### Blockquotes

```markdown
> Quote content
```

### Tables

```markdown
| Column1 | Column2 |
|---------|---------|
| Content1 | Content2 |
```

## hugo-book Shortcodes

hugo-book theme provides useful shortcodes.

### Hints (Notice Boxes)

```markdown
{{</* hint info */>}}
Info message
{{</* /hint */>}}

{{</* hint warning */>}}
Warning message
{{</* /hint */>}}

{{</* hint danger */>}}
Danger message
{{</* /hint */>}}
```

### Buttons

```markdown
{{</* button relref="/" */>}}Home{{</* /button */>}}
{{</* button href="https://example.com" */>}}External Link{{</* /button */>}}
```

### Columns

```markdown
{{</* columns */>}}

## Left Column
Content...

<--->

## Right Column
Content...

{{</* /columns */>}}
```

### Tabs

```markdown
{{</* tabs "unique-id" */>}}
{{</* tab "Tab1" */>}} Tab1 content {{</* /tab */>}}
{{</* tab "Tab2" */>}} Tab2 content {{</* /tab */>}}
{{</* /tabs */>}}
```

### Details (Collapse/Expand)

```markdown
{{</* details "Title" */>}}
Expandable content
{{</* /details */>}}
```

## Image Management

Store images in the `static` directory:

```
static/
  images/
    photo.jpg
    logo.png
```

Reference in markdown:

```markdown
![Description](/images/photo.jpg)
```

## Draft Mode

Mark posts as draft while writing:

```yaml
---
title: "Work in Progress"
draft: true
---
```

Run server with drafts:

```bash
hugo server --buildDrafts
```

## Preview Posts

Preview locally:

```bash
hugo server
```

Visit http://localhost:1313 in your browser

## Tips

1. **Use Weight**: Adjust post order with weight values
2. **Enable ToC**: Use `bookToc: true` for long documents
3. **Use Shortcodes**: Create rich content with hugo-book shortcodes
4. **Optimize Images**: Use appropriately sized images
5. **Internal Links**: Use `relref` shortcode for safe internal linking
