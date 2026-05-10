# Editing Guide

This repo has two concerns:

- **Template code:** layout, styling, reusable structure.
- **Personal content:** name, bio, research, posts, images, deployment target.

Keep those separate so the original template stays useful.

## Branch Workflow

Use a clean branch for the reusable scaffold and a separate branch for the personal site.

Suggested setup:

```bash
git branch
```

Keep something like:

```text
template-base   clean reusable template
main            deployed/personal version
```

Before editing personal content, make sure you are not on the template branch:

```bash
git status --short --branch
```

If you are on `template-base`, switch away before adding personal content:

```bash
git checkout main
```

## What To Edit For Personal Content

These files are expected to change for your actual site:

```text
_data/profile.yml
_data/research.yml
_config.yml
_posts/
images/
```

Typical edits:

- `_data/profile.yml`: name, homepage bio, email, profile image path.
- `_data/research.yml`: research/project entries.
- `_config.yml`: site description, `url`, and `baseurl`.
- `_posts/`: blog posts as Markdown files.
- `images/`: profile photo and post images.

Supported post categories:

```yaml
tag: ai
tag: technical
tag: other
```

For the current GitHub Pages test deploy at `https://rosikand.github.io/newpw/`, `_config.yml` should keep:

```yml
url: "https://rosikand.github.io"
baseurl: "/newpw"
```

For a future root site like `https://rosikand.github.io/`, use:

```yml
url: "https://rosikand.github.io"
baseurl: ""
```

## What To Avoid Editing For Content Changes

These are mostly template files:

```text
_layouts/
_includes/
_sass/
assets/css/
posts/index.html
```

Edit them when changing the design or behavior. Avoid editing them just to add personal facts.

## Local Preview

Use the working local command from `LOCAL_DEV.md`:

```bash
GEM_HOME=vendor/ruby GEM_PATH=vendor/ruby JEKYLL_NO_BUNDLER_REQUIRE=true /usr/bin/ruby vendor/bin/jekyll serve --host 127.0.0.1 --port 4000
```

Then open:

```text
http://127.0.0.1:4000/newpw/
```

## Structured Content In `_data`

Jekyll has a special `_data/` directory. YAML files in `_data/` become structured data available to templates. This repo uses `_data/` for profile and research content.

Edit:

```text
_data/profile.yml
_data/research.yml
```

`_data/profile.yml` holds homepage/profile content:

```yml
name: Your Name
email: you@example.com
photo: /images/profile-placeholder.svg
bio: |
  Short homepage bio goes here. Markdown works, so **bold text** and
  [links](https://example.com) are supported.

  Add a blank line to create another paragraph.
```

`_data/research.yml` holds research/project entries:

```yml
- title: Project, paper, or research direction
  authors: Your Name
  meta: Add venue, status, collaborators, or a one-line note
  links:
    - label: Link
      url: "#"
```

`index.html` and `research.html` render this data using Liquid instead of hardcoding content directly in HTML.

## Why Use `_data`?

The point is to separate personal facts from template structure. It helps because:

- you want to keep the template almost completely generic;
- you expect to reuse this scaffold across multiple personal sites;
- you want future content edits to avoid HTML;
- you want cleaner diffs between template changes and personal content changes;
- you expect research entries to grow into a longer structured list.

For normal content edits, start in `_data/profile.yml` and `_data/research.yml`. Edit `index.html` or `research.html` only when changing page structure.

For multi-paragraph bios, use `bio: |` and separate paragraphs with blank lines. Use normal Markdown inside the bio. Do not prefix normal paragraphs with `>` unless you intentionally want a blockquote.

## Edit Cycle

1. Check the branch:

   ```bash
   git status --short --branch
   ```

2. Edit personal content files.

3. Preview locally:

   ```bash
   GEM_HOME=vendor/ruby GEM_PATH=vendor/ruby JEKYLL_NO_BUNDLER_REQUIRE=true /usr/bin/ruby vendor/bin/jekyll build
   ```

4. Review changes:

   ```bash
   git diff
   ```

5. Commit a focused change:

   ```bash
   git add _data _config.yml _posts images
   git commit -m "Add personal site content"
   ```

Adjust the `git add` list to match the files actually edited.
