# otroshi.github.io

Personal academic page of Hatef Otroshi Shahreza — <https://otroshi.github.io/>

## Layout

| Path                | Purpose                                                        |
| ------------------- | -------------------------------------------------------------- |
| `index.html`        | The entire page: markup, styles and scripts are all inline.      |
| `assets/portrait.jpg` | Hero portrait.                                                 |
| `robots.txt`        | Points crawlers at the sitemap.                                  |
| `sitemap.xml`       | Single-URL sitemap; bump `<lastmod>` after a substantive edit.   |
| `.nojekyll`         | Serves the files as-is, skipping GitHub's Jekyll build.          |

There is no build step and no dependencies. Open `index.html` in a browser to
preview, or serve the folder with `python3 -m http.server 8000`.

## Publishing

GitHub Pages serves whatever is on `main`:

```bash
git add -A
git commit -m "Update page"
git push
```

The live site refreshes within a minute or so. Deployment status is under
the repository's **Actions** tab.

## Updating the content

Everything is plain HTML, edited in place.

**Add a news item** — newest first, inside the `<ul class="news">` for that year
(create a new `<div class="news__year">` when the year rolls over). The optional
`chip` link is the small `pdf` / `link` badge:

```html
<li><span class="news__date">Oct 2026</span><span class="news__body">Short description of the news <a class="chip" href="URL">pdf</a></span></li>
```

Older years live inside `<div id="older-news" hidden>`, collapsed behind the
"Show earlier news" button. When you move a year in there, update the button
label in both the `<span id="news-toggle-label">` and the `label.textContent`
fallback in the script at the bottom of the file.

**Add a publication** — inside `<ul class="pubs">`. The `title` attribute is the
tooltip that spells out the venue abbreviation:

```html
<li>
  <div class="pubs__venue" title="Full Venue Name">ABBR<span>2026</span></div>
  <div>
    <a class="pubs__title" href="URL">Paper title</a>
    <p class="pubs__authors"><strong>Hatef Otroshi Shahreza</strong>, Co-author</p>
  </div>
</li>
```

**Change the portrait** — replace `assets/portrait.jpg`. It renders at 104×138
CSS pixels, so roughly 320×420 or larger keeps it sharp on high-DPI screens.

**Colours and spacing** — the CSS custom properties under `:root` near the top of
the file, with dark-mode overrides in the `@media (prefers-color-scheme: dark)`
block directly below. Change a value in both places to keep the themes in step.

## Notes

- **Analytics.** The `gtag` snippet in `<head>` still uses the Idiap page's
  property (`G-0JRKDG7V0G`), so both sites report into one stream. Replace both
  occurrences of that ID to split them out.
- **Canonical URL.** This page declares itself canonical. If the Idiap page at
  <https://www.idiap.ch/~hotroshi/> stays online with the same content, adding
  `<link rel="canonical" href="https://otroshi.github.io/">` to it will point
  search engines here rather than letting the two compete.
