# Project Context — Ideas Board

## Identity

- **Name**: Ideas Board
- **Type**: Collaborative voting board for workshops
- **Status**: Pre-development (specifications phase)

## Tech Stack

| Layer | Technology | Version |
|---|---|---|
| Framework | Nuxt 3 | Latest |
| UI | shadcn-vue + Tailwind CSS | Latest |
| Database | Convex | Latest |
| Hosting | Cloudflare Pages | — |
| i18n | @nuxtjs/i18n | Latest |
| Icons | Lucide (via shadcn-vue) | — |

## Key Architecture Decisions

1. **Convex Auth from day one** — OAuth (Google, GitHub) + anonymous guest sign-in. All write actions require authentication. Browsing is public.
2. **Board is the root page** — No separate home/landing page. Users land directly on the idea list at `/{locale}`.
3. **Convex as sole backend** — No custom API routes. All data flows through Convex queries/mutations with real-time subscriptions.
4. **SSR for SEO** — All public pages server-rendered for social sharing meta tags and SEO.
5. **RTL-first development** — Logical CSS properties everywhere, tested in Arabic and English.
6. **shadcn-vue as component foundation** — Custom components only when no shadcn-vue primitive exists.

## Important Files

| File | Purpose |
|---|---|
| `agents/docs/SPECIFICATIONS.md` | Full application specifications |
| `agents/docs/AGENT_RULES.md` | AI agent behavior rules |
| `agents/context/PROJECT.md` | This file — project context |
| `convex/schema.ts` | Convex database schema |
| `nuxt.config.ts` | Nuxt configuration |
| `CHANGELOG.md` | Change tracking |

## Current Focus

- Specifications review and refinement
- Next: Project scaffolding and initial setup
