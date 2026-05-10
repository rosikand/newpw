# Deployment

This is a static Jekyll site. The two simplest deployment targets are GitHub Pages and Vercel.

## Before Deploying

Make sure the site is ready to publish:

```bash
git status --short
GEM_HOME=vendor/ruby GEM_PATH=vendor/ruby JEKYLL_NO_BUNDLER_REQUIRE=true /usr/bin/ruby vendor/bin/jekyll build
```

Review placeholder content before publishing:

- `_data/profile.yml` still has placeholder name, bio, email, and profile image
- `_data/research.yml` still has a placeholder research entry
- `images/profile-placeholder.svg` is still the profile image

Do not commit `.codex-session/`; it is intentionally ignored because raw Codex logs can contain sensitive context.

## Option 1: GitHub Pages

GitHub Pages is the most direct option for a Jekyll personal site.

### Test Deploy to `rosikand.github.io/newpw`

To test without touching `rosikand.github.io`, deploy this as a GitHub Pages project site from a repository named:

```text
newpw
```

GitHub Pages project sites publish at:

```text
https://OWNER.github.io/REPOSITORY/
```

So `rosikand/newpw` publishes at:

```text
https://rosikand.github.io/newpw/
```

This repo is configured for that target:

```yml
url: "https://rosikand.github.io"
baseurl: "/newpw"
```

The repo also includes `.github/workflows/pages.yml`, which uses GitHub's official Pages Actions flow:

- `actions/configure-pages@v5`
- `actions/jekyll-build-pages@v1`
- `actions/upload-pages-artifact@v3`
- `actions/deploy-pages@v4`

To deploy:

1. Create a new GitHub repo named `newpw` under `rosikand`.

2. Point this local repo at that remote:

   ```bash
   git remote set-url origin https://github.com/rosikand/newpw.git
   ```

   Or keep the current `origin` and add a second remote:

   ```bash
   git remote add newpw https://github.com/rosikand/newpw.git
   ```

3. Commit the deployment prep:

   ```bash
   git add _config.yml .github/workflows/pages.yml DEPLOYMENT.md LOCAL_DEV.md
   git commit -m "Prepare GitHub Pages test deploy"
   ```

4. Push to the `newpw` repo:

   ```bash
   git push origin main
   ```

   If using the second remote:

   ```bash
   git push newpw main
   ```

5. In GitHub, open `rosikand/newpw` -> **Settings** -> **Pages**.

6. Set **Build and deployment** source to **GitHub Actions**.

7. Go to the **Actions** tab and wait for the Pages workflow to finish.

8. Visit:

   ```text
   https://rosikand.github.io/newpw/
   ```

GitHub's docs state that project sites publish under `https://<owner>.github.io/<repositoryname>` and that Pages publishing can take several minutes.

### If The Workflow Fails At `Setup Pages`

If the GitHub Actions log shows:

```text
Error: Get Pages site failed. Please verify that the repository has Pages enabled and configured to build using GitHub Actions
Error: HttpError: Not Found
```

the repository has not been enabled for GitHub Pages with the Actions source yet.

Fix it in GitHub:

1. Open `https://github.com/rosikand/newpw`.
2. Go to **Settings** -> **Pages**.
3. Under **Build and deployment**, set **Source** to **GitHub Actions**.
4. Save if GitHub shows a save button.
5. Go back to the failed Actions run.
6. Click **Re-run jobs**.

Do not switch the source to `Deploy from a branch` for this workflow. This repo uses `.github/workflows/pages.yml`, so the Pages source should be **GitHub Actions**.

The `actions/configure-pages` action has an `enablement` option, but GitHub documents that this requires a token other than the default `GITHUB_TOKEN` with extra Pages/admin permissions. Manual setup in **Settings** -> **Pages** is simpler for this test deploy.

### Decide the URL Shape

For a user site:

```text
https://USERNAME.github.io/
```

the repository should usually be named:

```text
USERNAME.github.io
```

and `_config.yml` should use:

```yml
url: "https://USERNAME.github.io"
baseurl: ""
```

For a project site from this current repo, whose remote is currently:

```text
https://github.com/rosikand/con-pw.git
```

the default Pages URL would be:

```text
https://rosikand.github.io/con-pw/
```

and `_config.yml` should use:

```yml
url: "https://rosikand.github.io"
baseurl: "/con-pw"
```

For a custom domain, such as `example.com`, use:

```yml
url: "https://example.com"
baseurl: ""
```

### Publish

1. Commit the site:

   ```bash
   git add .
   git commit -m "Prepare personal site"
   git push origin main
   ```

2. In GitHub, open the repository settings.

3. Go to **Pages**.

4. Configure the publishing source. GitHub currently recommends GitHub Actions for Jekyll-backed Pages sites, but branch-based publishing can also work for simple static/Jekyll sites depending on repository settings.

5. Wait for the Pages build to finish. GitHub says publishing can take several minutes.

6. Visit the Pages URL shown in the repository's Pages settings.

Official docs: https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll

## Option 2: Vercel

Vercel is also a good fit for this repo. It will build the Jekyll site and serve the generated static files.

### Git-Based Deploy

1. Push this repo to GitHub.

2. Go to Vercel and import the GitHub repository.

3. Let Vercel detect Jekyll. If it does not, set:

   ```text
   Framework Preset: Other
   Build Command: bundle exec jekyll build
   Output Directory: _site
   ```

4. Deploy.

5. Vercel will give the site a `.vercel.app` URL. Add a custom domain later if desired.

### Important Vercel Lockfile Step

Because Vercel builds on Linux, Vercel recommends adding the Linux platform to `Gemfile.lock` and committing the result:

```bash
bundle lock --add-platform x86_64-linux
git add Gemfile.lock
git commit -m "Add Linux platform for Vercel build"
```

Do this before importing/deploying to Vercel if the build complains about Bundler platforms.

Official docs:

- https://vercel.com/kb/guide/deploying-jekyll-with-vercel
- https://vercel.com/docs/git

## Recommendation

For a personal Jekyll site:

- Use **GitHub Pages** if you want the simplest static-site hosting tied directly to GitHub.
- Use **Vercel** if you want preview deployments for branches/PRs, easy rollback, and a polished custom-domain workflow.

If using the current repo name `con-pw`, remember that GitHub Pages needs `baseurl: "/con-pw"` unless you rename the repo to `USERNAME.github.io` or use a custom domain.
