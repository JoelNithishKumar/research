# joelnithishkumar.github.io

Personal academic site. Jekyll, hosted on GitHub Pages.

## Local development

```bash
# Install Ruby dependencies (first time)
bundle install

# Serve locally with live reload
bundle exec jekyll serve --livereload
```

Visit `http://localhost:4000`.

## Deployment

Push to the `main` branch of `JoelNithishKumar/JoelNithishKumar.github.io`. GitHub Pages builds automatically. Build usually completes in under 60 seconds.

If the build fails, go to **Settings → Pages** on the repo and check the build log. Common issues: unsupported plugin, YAML syntax error in front matter, bad Liquid tag.

## Adding a post (article / writing sample)

Create a file in `_posts/` named `YYYY-MM-DD-slug.md`. Minimal front matter:

```yaml
---
layout: post
title: "Your title here"
date: YYYY-MM-DD
tags: [tag1, tag2]
repo: https://github.com/JoelNithishKumar/your-repo   # optional — shows "Code and data" link
---
```

Tags appear on the writing index and on the post page. Use lowercase, no spaces.
Suggested tags: `snap`, `housing`, `congestion-pricing`, `methods`, `meta`.

## Site structure

```
_config.yml          Jekyll config (title, email, social handles, plugins)
Gemfile              Ruby deps (github-pages gem)
_includes/
  head.html          <head> tag, SEO plugin, stylesheet
  header.html        Site name + nav links
  footer.html        Email + GitHub + LinkedIn
_layouts/
  default.html       Wraps all pages (includes head/header/footer)
  page.html          Generic page (title + content)
  post.html          Article page (title, date, tags, optional repo link)
_posts/              All writing — one file per article
assets/css/main.css  All styles (single file — edit here for visual changes)
index.md             Home
research.md          Research projects
writing.md           Writing index (auto-generated from _posts/)
cv.md                Inline CV
about.md             Bio + contact
404.md               Custom 404
```

## Adding a CV PDF

1. Compile your LaTeX CV to `joel_nithish_cv.pdf`.
2. Drop it in `assets/cv/`.
3. Uncomment the download link in `cv.md`.

## Custom domain (when ready)

1. Buy `joelnithishkumar.com` (Namecheap or Porkbun — ~$12/yr).
2. In the repo, create a file named `CNAME` at the root containing exactly: `joelnithishkumar.com`
3. At your DNS registrar, add four A records pointing to GitHub Pages IPs:
   ```
   185.199.108.153
   185.199.109.153
   185.199.110.153
   185.199.111.153
   ```
   And a CNAME record: `www  →  joelnithishkumar.github.io`
4. In **Settings → Pages**, set the custom domain and enable "Enforce HTTPS."
5. DNS propagation takes up to 24 hours; HTTPS cert provisions automatically after DNS resolves.
