# Presay_DOCS

User guide for [Presay](https://presay.hyver.app/), published at <https://docs.presay.hyver.app/>.

A [Docsify](https://docsify.js.org/) site: no build step. GitHub Pages serves `main:/docs`.

## Preview locally

```bash
cd docs && npx serve
```

## Edit

Pages are Markdown under `docs/`; the navigation is `docs/_sidebar.md`. Link between pages with root-absolute paths (`/reports/reading.md`), not relative ones. Merging to `main` publishes.
