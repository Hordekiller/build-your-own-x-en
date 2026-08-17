# Build Your Own X — English Catalog

[![Live site](https://img.shields.io/badge/🌐%20Live%20—%20English%20Catalog-hordekiller.github.io/build-your-own-x-en-blue?logo=githubpages&logoColor=white)](https://hordekiller.github.io/build-your-own-x-en/)
[![Persian version](https://img.shields.io/badge/🇮🇷%20Persian%20version-hordekiller.github.io/build-your-own-x-orange)](https://hordekiller.github.io/build-your-own-x/)
[![Russian version](https://img.shields.io/badge/🇷🇺%20Russian%20version-hordekiller.github.io/build-your-own-x-ru-green)](https://hordekiller.github.io/build-your-own-x-ru/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/Hordekiller/build-your-own-x/blob/main/LICENSE)

> What I cannot create, I do not understand — Richard Feynman

A curated English catalog of **359 step-by-step tutorials** for re-creating your
favorite technologies from scratch — compilers, operating systems, game
engines, databases, neural networks, renderers, and more.

This is the English companion of the
[Persian BYOX catalog](https://github.com/Hordekiller/build-your-own-x),
which in turn is a full-page translation of the famous
[`build-your-own-x`](https://github.com/codecrafters-io/build-your-own-x)
community list. Every tutorial gets its own dedicated landing page with a
summary, learning goals, core ideas, and links to the original source.

---

## Live site

- **English:** <https://hordekiller.github.io/build-your-own-x-en/>
- **Persian:** <https://hordekiller.github.io/build-your-own-x/>
- **Russian:** <https://hordekiller.github.io/build-your-own-x-ru/>

## Features

- **359 tutorial pages** across 30 categories — from
  [3D renderers](https://hordekiller.github.io/build-your-own-x-en/tutorials-en/index.html)
  and [BitTorrent clients](https://hordekiller.github.io/build-your-own-x-en/tutorials-en/index.html)
  to programming languages, neural networks, and operating systems.
- Fast, zero-dependency static site — plain HTML + CSS + vanilla JS, no
  frameworks, no build step, no external requests besides Google Fonts.
- Search-as-you-type and category filtering on the landing page.
- "Done" progress tracking per tutorial with per-category progress bars.
- Cross-language navigation: every page links to its Persian and Russian
  counterparts when available.
- Deployed with GitHub Actions to GitHub Pages (`workflow` build type).

## Repository structure

```
.
├── assets/
│   ├── css/style.css          # Shared styling
│   └── js/
│       ├── tutorials-en.js    # Tutorial index data (id, category, lang, …)
│       └── main.js            # Rendering, search, filters, progress
├── templates/
│   └── page_template.html     # Landing-page template used by the generator
├── tutorials-en/
│   └── *.html                 # 359 tutorial landing pages
├── en-done.json               # Ordered list of tutorial ids (audit artifact)
├── index.html                 # Catalog landing page
└── .github/workflows/
    └── deploy-pages.yml       # Build + deploy to GitHub Pages
```

## Pages

Each tutorial page (`tutorials-en/{id}.html`) contains:

- Language badge and category badge
- Links to the original source and the Persian/Russian versions
- Four sections: **About**, **What you will learn**,
  **Core idea** (with code excerpts), and **Why it matters**
- A copyright callout reminding readers the tutorial belongs to its
  original author

## How the catalog was built

1. Tutorial metadata is curated in `assets/js/tutorials-en.js`
   (359 entries: id, category, language, original URL, video flag).
2. Landing pages are generated from `templates/page_template.html`
   by a Python generator script; the results are committed directly.
3. An audit script verifies every page against the index — titles, badges,
   sections, code blocks, cross-language links, and link hygiene
   (no raw `&`, no dead internal links) — with a guaranteed-clean
   result of `359/359`.

## Deploy

The repository deploys itself on every push to `main`:

```yaml
# .github/workflows/deploy-pages.yml (abridged)
on: push
permissions:
  contents: read
  pages: write
  id-token: write
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/configure-pages@v5
      - uses: actions/upload-pages-artifact@v3
        with: { path: . }
      - uses: actions/deploy-pages@v4
```

## License & credits

- All tutorials belong to their original authors — see each page for the
  original source link.
- Catalog structure and page generation follow the
  [Persian BYOX project](https://github.com/Hordekiller/build-your-own-x).
- The tutorial list itself originates from the community
  [build-your-own-x](https://github.com/codecrafters-io/build-your-own-x)
  repository.
- This repository's own code is MIT licensed.