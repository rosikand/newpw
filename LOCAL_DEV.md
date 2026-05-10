# Local Development

This site is a Jekyll project.

## Preview Locally

From this repo, use the vendored-gems command:

```bash
cd /Users/vandnamd/dev/new-pw-experiments/charlie
GEM_HOME=vendor/ruby GEM_PATH=vendor/ruby JEKYLL_NO_BUNDLER_REQUIRE=true /usr/bin/ruby vendor/bin/jekyll serve --host 127.0.0.1 --port 4000
```

Open:

```text
http://127.0.0.1:4000/newpw/
```

Leave the terminal running while previewing. Stop the server with `Ctrl-C`.

The `/newpw/` path mirrors the GitHub Pages test deployment target:

```text
https://rosikand.github.io/newpw/
```

## Why Not `bundle exec`

On this machine, the Homebrew Ruby/Bundler path currently fails with:

```text
zsh: killed     bundle exec jekyll serve --livereload
```

That appears to be a local Homebrew Ruby/Bundler issue, not a site build issue. The vendored command above successfully builds and serves the site.

Once Ruby/Bundler is fixed, the normal command should be:

```bash
bundle exec jekyll serve --livereload
```

## First-Time Setup

If dependencies are missing, install them with:

```bash
bundle install
```

The original site README recommends Homebrew Ruby on macOS because system Ruby can be too old for current Jekyll/Bundler combinations.

## Current Site State

The site builds and serves locally, but the top-level content still has placeholders:

- `_data/profile.yml` has placeholder name, bio, email, and profile image
- `_data/research.yml` has a placeholder research entry
- `images/profile-placeholder.svg` is still the profile image
