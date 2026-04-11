# ktext.dev

The public website for [ktext](https://github.com/arithmetike/ktext) — a CLI tool that generates, validates, and exports `CONTEXT.yaml`, a machine-readable project context file for AI coding agents and developer tools.

Live at **[ktext.dev](https://ktext.dev)**.

## What's on the site

- **Landing page** — explains the problem ktext solves, how it works, and what the schema looks like in practice
- **Getting Started** — install instructions, `ktext init`, `ktext validate`, `ktext export`, and CI integration
- **Schema Reference** — complete field reference for all `CONTEXT.yaml` sections
- **Scoring** — how `ktext validate` scores files across eight sections, section weights, quality checks, and JSON output
- **Common Questions** — answers to "why not just use a README", "why not CLAUDE.md", and other common questions

## Stack

- [Astro 5](https://astro.build) — static site, all pages prerendered
- [Tailwind CSS 4](https://tailwindcss.com) — utility-first styling with `@theme` design tokens
- [Cloudflare Workers](https://developers.cloudflare.com/workers/) — hosting via `@astrojs/cloudflare` adapter

## Development

```bash
npm install
npm run dev        # dev server at localhost:4321
npm run build      # production build → dist/
npm run preview    # preview the production build locally
```

## Deployment

The site deploys automatically to Cloudflare Workers on push to `main` via `.github/workflows/deploy.yml`.

To deploy manually after a build:

```bash
npm run build
wrangler deploy --config dist/server/wrangler.json
```

The build generates the authoritative `wrangler.json` at `dist/server/` — don't deploy from `wrangler.jsonc` directly.

## About ktext

Every codebase has context that lives in engineers' heads: why Postgres instead of MySQL, what you must never log, which layer owns what. When a new engineer joins, or an AI agent opens a PR, that context is missing. They guess. They get it wrong.

`CONTEXT.yaml` is a single file that captures that knowledge in a structured, machine-readable format. `ktext` generates it from your existing repo, scores it, and exports it to XML or JSON for efficient injection into any LLM context window.

The CLI is at [github.com/arithmetike/ktext](https://github.com/arithmetike/ktext). MIT licensed, no accounts, no strings attached.

## License

MIT
