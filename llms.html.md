# llms.txt – Inspect Docs

## Index Page

Inspect Docs produces an [`llms.txt`](https://llmstxt.org) index page at the root of your site, built from your site’s `title`, `description`, `navigation`, and reference pages:

``` markdown
# My Package

> Description of what the package does.

## Docs

- [Getting Started](https://docs.example.com/index.html): Install the package and render your first site.
- [Guides](https://docs.example.com/guides/index.html): Task-oriented walkthroughs.

## API Reference

- [my_package](https://docs.example.com/reference/my_package.html): Core tasks and utilities.
- [my_package.utils](https://docs.example.com/reference/my_package.utils.html): Helper functions.

## CLI Reference

- [my_package run](https://docs.example.com/reference/my_package_run.html): Run a task.
```

### Descriptions

Each entry in `llms.txt` uses the page’s frontmatter `description` field as its summary.

To use a different summary for `llms.txt` than the one shown on the page, set `llms-description`:

``` yaml
---
title: Getting Started
description: Get up and running in five minutes!
llms-description: Installation, first render, and project layout.
---
```

If `llms-description` is absent, `description` is used.

## Full Documentation

Alongside `llms.txt`, Inspect Docs also publishes two concatenated files at the site root for LLMs that want to ingest the entire site in a single request:

| File             | Contents                                          |
|------------------|---------------------------------------------------|
| `llms-full.txt`  | Every page in the site, including reference docs. |
| `llms-guide.txt` | Every page *except* anything under `reference/`.  |

Both files are built by concatenating the per-page Markdown sources in navigation order, with the site title and description as a header.

## Markdown Pages

Inspect Docs publishes a plain-Markdown version of each page at the same URL with `.html.md` appended. A page rendered at `https://docs.example.com/guides/install.html` is also available at `https://docs.example.com/guides/install.html.md`.

Inspect Docs also injects a **Copy page** button into every page header. The button lets readers:

- **Copy as Markdown** — copy the page’s Markdown source to the clipboard.
- **Open as Markdown** — open the `.html.md` version in a new tab.

### Custom Generation

By default the `.html.md` for each page is produced by running pandoc on the rendered HTML. A page can override this by declaring an `llms-script` in its frontmatter — useful when the default conversion misses something, or when the Markdown should be generated from a source other than the rendered HTML (e.g. introspecting code or assembling a digest from data files):

``` yaml
---
title: API Reference
llms-script: scripts/render_api_md.py
---
```

The script path is resolved relative to the `.qmd` file. `.py` scripts are run via `python`; anything else is invoked directly and must be executable. The rendered page’s main content is piped in on stdin, and the script’s stdout becomes the full body of the `.html.md` file (no title is prepended — the script is in full control of the output):

``` python
#!/usr/bin/env python
import sys

html = sys.stdin.read()
sys.stdout.write(my_html_to_md(html))
```

If the declared script can’t be found, a warning is printed and the page falls back to pandoc.
