+++
title = 'Markdown Style Guide'
date = 2025-06-02T09:00:00Z
description = 'A reference page showing how every Markdown element looks in this theme.'
tags = ['meta', 'markdown']
+++

This post shows how common Markdown elements are rendered, so you can check
the styling at a glance.

## Text

Paragraphs are plain text. You can use **bold**, *italic*, ~~strikethrough~~,
`inline code`, and [links](https://gohugo.io).

## Lists

1. Install Hugo.
2. Create a site with `hugo new site blog`.
3. Write a post:
   - front matter goes at the top
   - content goes below it

- [x] Write the post
- [ ] Proofread it

## Blockquotes

> HINT: Blockquotes work well for notes, hints, and warnings.

## Code

A fenced code block with syntax highlighting:

```go
package main

import "fmt"

func main() {
	for i := 1; i <= 3; i++ {
		fmt.Printf("hello %d\n", i)
	}
}
```

A shell session:

```bash
$ hugo new linux/my-post.md
$ hugo server -D
```

## Tables

| Command        | What it does                     |
| -------------- | -------------------------------- |
| `hugo new`     | Create content from an archetype |
| `hugo server`  | Run a local preview server       |
| `hugo`         | Build the site into `public/`    |

## Images

Images placed next to `index.md` in a page bundle can be referenced directly:

![Bryce Canyon National Park](bryce-canyon.jpg)

---

That's everything. Headings, lists, quotes, code, tables, and images all share
the same calm palette.
