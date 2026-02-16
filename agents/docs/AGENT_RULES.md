# AI Agent Rules — Ta9in Voting Board

> These rules govern how AI agents (including Antigravity) should behave when contributing to this codebase.

---

## 1. General Agent Rules

### 1.1 Context Awareness

- **Always read** `agents/context/PROJECT.md` and `agents/docs/SPECIFICATIONS.md` before making any code changes.
- **Check** `CHANGELOG.md` to understand the current state of the project.
- **Never assume** — if something is ambiguous, ask the user rather than guessing.

### 1.2 Code Style & Conventions

- **Language**: TypeScript everywhere. No `any` types unless absolutely unavoidable (and document why).
- **Vue**: Use `<script setup lang="ts">` for all components. Composition API only.
- **Naming**: 
  - Components: `PascalCase` (e.g., `IdeaCard.vue`).
  - Composables: `camelCase` prefixed with `use` (e.g., `useVote.ts`).
  - Convex functions: `camelCase` (e.g., `ideas.listTop`).
  - Files: `kebab-case` for pages/layouts, `PascalCase` for components.
- **Imports**: Use Nuxt auto-imports. Do not manually import Vue composables (`ref`, `computed`, etc.) or Nuxt utilities (`useRoute`, `navigateTo`, etc.).
- **Comments**: Only when the "why" isn't obvious. Never explain what the code does — make the code self-explanatory.

### 1.3 UI & Styling

- **shadcn-vue is mandatory**. Always use shadcn-vue components before creating custom ones.
- **Tailwind CSS** for all styling. No `<style>` blocks unless truly necessary for complex animations.
- **RTL-first**: Always test in both RTL (Arabic) and LTR (English). Use logical properties (`ms-`, `me-`, `ps-`, `pe-`, `start`, `end`) instead of physical ones (`ml-`, `mr-`, `pl-`, `pr-`, `left`, `right`).
- **Responsive-first**: Mobile layout first, then enhance for larger screens.
- **Dark mode**: Every component must work in both light and dark modes.
- **Accessibility**: All interactive elements must have ARIA labels. Keyboard navigation must work.

### 1.4 Data Layer (Convex)

- **Schema changes** must be proposed in the implementation plan before execution.
- **Validation**: Always validate inputs in Convex mutations using `v` validators.
- **Authorization**: Always check `authorId` matches for mutations that modify a user's own data.
- **Denormalized counts**: When updating `voteCount`, always do so inside the same mutation as the vote insert/delete to maintain consistency.
- **Queries must be efficient**: Use indexes, avoid full table scans for sorted/filtered data.

### 1.5 i18n

- **All user-facing strings** must come from locale files (`locales/en.json`, `locales/ar.json`). Never hardcode text in templates.
- **Keys**: Use dot-notation namespacing (e.g., `ideas.submitButton`, `suggestions.pending`).
- **Dates**: Use locale-aware formatting via `useI18n` or `Intl.DateTimeFormat`.
- **Direction**: Use `useI18n().locale` to determine direction, apply `dir="rtl"` or `dir="ltr"` at the layout level.

### 1.6 Testing

- Write unit tests for Convex functions (queries, mutations) covering happy path and edge cases.
- Write component tests for critical UI flows (vote toggle, submit flow, suggestion review).
- Mock Convex client in component tests.
- Test both RTL and LTR rendering for layout-sensitive components.

### 1.7 File Organization

```
voting_board/
├── agents/
│   ├── context/          # Project context files
│   ├── docs/             # Documentation
│   ├── reports/          # Reports & analysis
│   └── guides/           # How-to guides
├── app/
│   ├── components/       # Vue components
│   │   ├── idea/         # Idea-related components
│   │   ├── suggestion/   # Suggestion components
│   │   ├── layout/       # Layout components (Header, Footer)
│   │   └── shared/       # Reusable shared components
│   ├── composables/      # Vue composables
│   ├── layouts/          # Nuxt layouts
│   ├── pages/            # Nuxt pages (file-based routing)
│   └── assets/           # Static assets, global CSS
├── convex/               # Convex backend
│   ├── schema.ts         # Database schema
│   ├── ideas.ts          # Idea queries & mutations
│   ├── votes.ts          # Vote queries & mutations
│   └── suggestions.ts    # Suggestion queries & mutations
├── locales/              # i18n translation files
│   ├── en.json
│   └── ar.json
├── public/               # Public static files
├── nuxt.config.ts        # Nuxt configuration
├── tailwind.config.ts    # Tailwind configuration
└── CHANGELOG.md          # Change log
```

### 1.8 Commits & PRs

- **Conventional commits**: `feat:`, `fix:`, `refactor:`, `docs:`, `chore:`, `test:`.
- **Atomic commits**: One logical change per commit.
- **CHANGELOG.md**: Update with every meaningful change.
- **Never push breaking changes** without updating documentation.

---

## 2. Antigravity-Specific Rules

### 2.1 Planning Phase

- **Always create an implementation plan** before writing code for any feature that touches more than 2 files.
- **Research before implementing**: Query Context7 docs for Nuxt, Convex, and shadcn-vue before proposing solutions.
- **Check existing patterns**: Before creating a new component or composable, verify no existing one serves the purpose.

### 2.2 Execution Phase

- **Build incrementally**: Implement one feature at a time. Verify it works before moving to the next.
- **Run the dev server** after changes to verify no build errors.
- **Test RTL**: After any layout or UI change, verify in both Arabic and English.
- **Use browser tools**: Take screenshots or snapshots to verify visual output.

### 2.3 Verification Phase

- **Always verify builds**: Run `npm run dev` and check for errors.
- **Visual verification**: Use browser tools to verify the UI looks correct.
- **Test data flows**: Submit an idea, vote, add a suggestion — verify the full cycle.
- **Create a walkthrough**: Document what was done, with screenshots when possible.

### 2.4 Communication

- **Be concise**: Don't explain obvious changes. Focus on non-obvious decisions.
- **Ask first**: If a spec decision feels wrong, explain why and suggest alternatives — don't silently deviate.
- **Flag scope creep**: If a task grows beyond what was planned, notify the user before proceeding.

### 2.5 Performance Awareness

- **Lazy load** components that aren't above the fold.
- **Minimize bundle size**: Use tree-shaking, avoid importing entire libraries.
- **Optimize images**: Compress and use modern formats (WebP/AVIF).
- **Cache**: Leverage Cloudflare's edge caching for static assets and SSR responses.

### 2.6 What NOT to Do

- ❌ Do not install unnecessary dependencies. Justify every `npm install`.
- ❌ Do not create custom components when shadcn-vue provides one.
- ❌ Do not hardcode strings in templates — always use i18n.
- ❌ Do not use physical CSS properties (`left`, `right`, `ml-`, `mr-`) — use logical ones.
- ❌ Do not skip error handling in Convex mutations.
- ❌ Do not commit `console.log` statements.
- ❌ Do not write `<style>` blocks in Vue components unless absolutely necessary.
- ❌ Do not ignore TypeScript errors — fix them properly.
