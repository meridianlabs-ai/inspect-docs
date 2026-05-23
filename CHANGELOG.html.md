# changelog – Inspect Docs

## 1.0.8 (23 May 2026)

- New `llms-script` frontmatter field lets a page generate its own `.html.md` instead of going through pandoc. The script is resolved relative to the `.qmd`, receives the rendered main content on stdin, and writes the full `.html.md` body to stdout. `.py` scripts run via `python`; anything else is invoked directly.
- Auto-detected “simple reference” mode: when `reference/` contains exactly one user-authored `index.qmd` (with a `reference:` frontmatter field), the extension skips index auto-generation and the Python API / CLI wrapper sections, folding a flat Reference link into the main sidebar.
- Never overwrite a user-authored `reference/index.qmd` (one with a `reference:` field) with the auto-generated landing page.

## 1.0.7 (20 May 2026)

- Pre-render no longer overwrites an existing `.gitignore`. Projects can now add their own patterns alongside the inspect-docs defaults without having them stomped on every render. A `.gitignore` is still written when the file is missing.
- Auto-discover the project module name in `post-render.py` (matching `pre-render.py`) so the llms.txt Reference section appears without requiring an explicit `inspect-docs.module` setting.

## 1.0.6 (20 May 2026)

- Emit `<link rel="alternate" type="text/markdown">` head tags pointing to `/llms.txt`, `/llms-full.txt`, and `/llms-guide.txt` on every page so coding agents can discover the LLM-readable docs from any URL.
- `llms.txt`, `llms-full.txt`, and `llms-guide.txt` now also include top-level pages reachable from `website.navbar` (e.g. listing pages on a separate tab) that aren’t already covered by `inspect-docs.navigation` or `reference/`.

## 1.0.5 (05 May 2026)

- Auto-detected “simple reference” mode: when `reference/` contains exactly one user-authored `index.qmd` (with a `reference:` frontmatter field), the extension skips index auto-generation and the Python API / CLI wrapper sections, folding a flat Reference link into the main sidebar.
- Never overwrite a user-authored `reference/index.qmd` (one with a `reference:` field) with the auto-generated landing page.
- Auto-discover the project module name in `post-render.py` (matching `pre-render.py`) so the llms.txt Reference section appears without requiring an explicit `inspect-docs.module` setting.
- Skip griffe step if there is no reference generation in play.
- Cache HTML→Markdown conversion in post-render to skip the per-page `quarto pandoc` subprocess when content is unchanged.  
- Cache reference frontmatter and symbol scan in pre-render so unchanged `reference/*.qmd` files are not re-read on every render.  
- Skip the external-refs network download when the local `refs-{pkg}.json` cache was written within the last 24 hours (delete the file to force a refresh).  
- Correct copy page as markdown behavior for index page (/).

## 1.0.4 (14 April 2026)

- Interlinking for pages in sub-directories.

## 1.0.3 (12 April 2026)

- Various improvements.

## 1.0.2 (10 April 2026)

- Only write files that have changed in pre-render.py.

## 1.0.1 (07 April 2026)

- Changes required for Inspect Scout docs migration.

## 1.0.0 (07 April 2026)

- Initial release.
