---
layout: post
title: Template Post
description: A dummy post showing the front matter and Markdown patterns this site supports.
date: 2026-05-10
tag: other
math: true
hidden: true
---

This is a dummy template post. It is hidden from the posts index because the front matter has:

```yaml
hidden: true
```

Delete that line, or set it to `false`, when you want the post to appear on the posts page.

# Section Heading

Use normal Markdown for prose, links, lists, and emphasis.

- Add bullets when they help.
- Use **bold** for emphasis.
- Link to references like [this](https://example.com).

# Math

Set `math: true` in the front matter to enable MathJax for the post.

Inline math works like $E = mc^2$.

Display math works like:

$$
\mathcal{L}(\theta) = \mathbb{E}_{x \sim D}[-\log p_\theta(x)]
$$

# Code

Use fenced code blocks:

```python
def hello(name: str) -> str:
    return f"hello, {name}"
```

# Metadata

Common front matter fields:

```yaml
layout: post
title: My Post Title
description: One-line preview shown on the posts page.
date: 2026-05-10
tag: ai
math: false
hidden: false
```

The posts page currently recognizes:

- `tag: ai`
- `tag: other`
