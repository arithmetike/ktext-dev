# ktext-dev

Public website for ktext.dev. Astro 5 + Tailwind CSS 4 + Cloudflare Workers.

## Quick reference

```bash
npm run dev           # dev server at localhost:4321
npm run build         # production build → dist/
npm run preview       # preview production build locally
wrangler deploy --config dist/server/wrangler.json   # deploy (after build)
```

**Always `npm run build` before reviewing CSS or component changes.** The dev server can lag on Tailwind 4 class generation.

**Never deploy from `wrangler.jsonc`** — always use the build-generated `dist/server/wrangler.json`.

## Structure

- `src/styles/global.css` — Tailwind `@theme` block (all design tokens) + `@layer components` utility classes
- `src/layouts/Base.astro` — HTML shell, fonts, OG tags
- `src/layouts/DocsLayout.astro` — sidebar nav + `.prose-docs` scoped styles for all docs pages
- `src/components/` — Nav, Footer, CodeBlock (copy button), ScoreCard
- `src/pages/index.astro` — landing page
- `src/pages/docs/` — index (getting started), schema, scoring, faq

## Tailwind 4 rules

Design tokens are defined in the `@theme` block in `global.css` and become canonical utility class names. **Never use `var()` syntax in class names** — use canonical names only:

```
bg-accent       ✓    bg-[var(--color-accent)]   ✗
text-muted      ✓    text-[var(--color-muted)]  ✗
```

Common patterns are extracted to `@layer components` in `global.css`:
`.text-body`, `.code-inline`, `.card`, `.link-accent`, `.section`, `.section-inner`, `.block-header`, `.label-eyebrow`

Use those before adding long inline class chains.

## Docs pages

All docs pages use `DocsLayout` — it handles sidebar, nav highlighting, and `.prose-docs` scoped styles for `h2`, `h3`, `p`, `a`, `ul`, `code`, `table`, `strong`. No Tailwind classes needed on individual prose elements inside docs pages.

## Copy buttons

Only on the install command and CI snippet. Not on every code block.

## Writing style

No emdashes. Write like a human, not a marketing robot.

## Deployment

CI deploys to Cloudflare Workers on push to main via `.github/workflows/deploy.yml`. The `CLOUDFLARE_API_TOKEN` secret must be set in GitHub Actions. Custom domains `ktext.dev` and `www.ktext.dev` are configured in `wrangler.jsonc`.

## Relationship to ktext

This site documents the [ktext CLI](https://github.com/arithmetike/ktext). All content — commands, flags, schema fields, scoring — must stay in sync with the binary. When ktext ships a change, update the docs here before or alongside the release.
