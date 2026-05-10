# Personal website

Personal website built with Jekyll and styled from the `charlieoneill11.github.io` source.

## Edit your content

- Change your name, bio, email, and profile image path in `_data/profile.yml`.
- Add research or project entries in `_data/research.yml`.
- Update deployment settings such as `url` and `baseurl` in `_config.yml`.
- Replace `images/profile-placeholder.svg` with your own profile photo and update the image path in `_data/profile.yml`.
- Add posts as Markdown files under `_posts/` using names like `2026-05-08-my-post.md`.

See `EDITING.md` for the full editing workflow.

## Local Development

```bash
bundle install
bundle exec jekyll serve --livereload
```

Site will be at http://127.0.0.1:4000.
