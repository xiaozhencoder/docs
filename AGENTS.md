# AGENTS.md

## Cursor Cloud specific instructions

This is a **Docsify** static documentation site with no build system, no package manager, no tests, and no linter.

### Running the dev server

```sh
docsify serve . --port 3000
```

`docsify-cli` is installed globally via npm as part of the VM update script. The server serves the workspace root and renders Markdown files via client-side Docsify JS loaded from CDN.

### Key files

- `index.html` — Docsify config and script/style imports (CDN-based)
- `_config/_sidebar.md` — sidebar navigation structure
- `_config/_coverpage.md` — cover page content
- `_config/css/styles.css` — custom styles
- Markdown content lives at the repo root and in `java/`, `mall/`, `web/` directories

### Notes

- There are **no automated tests, linters, or build steps** in this repository.
- The site loads JS/CSS from `cdn.jsdelivr.net`; internet access is needed for full rendering.
- Opening `index.html` directly as a `file://` URL will not work because Docsify fetches `.md` files via AJAX.
