## 1.0.7 (20 May 2026)

- Pre-render no longer overwrites an existing `.gitignore`. Projects can now add their own patterns alongside the inspect-docs defaults without having them stomped on every render. A `.gitignore` is still written when the file is missing.

## 1.0.6 (20 May 2026)

- Emit `<link rel="alternate" type="text/markdown">` head tags pointing to `/llms.txt`, `/llms-full.txt`, and `/llms-guide.txt` on every page so coding agents can discover the LLM-readable docs from any URL.
- `llms.txt`, `llms-full.txt`, and `llms-guide.txt` now also include top-level pages reachable from `website.navbar` (e.g. listing pages on a separate tab) that aren't already covered by `inspect-docs.navigation` or `reference/`.

## 1.0.5 (05 May 2026)

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

