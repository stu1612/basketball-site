# Club Site — Project Overview

## What this is

A full rebuild of the existing website for a basketball club based in Helsingborg, Sweden. The existing site is built on an outdated, non-responsive drag-and-drop platform and is being replaced entirely with a modern, architecturally considered stack.

## Who it's for

**The club** — a real basketball club with three active teams (men's, women's, youth/juniors), competing in the Helsingborg/Skåne region. The site needs to serve real visitors: parents checking training times, fans checking fixtures, sponsors expecting visibility, and the club itself needing an easy way to publish news without technical help.

**The developer** — this project is also a deliberate portfolio piece, built to demonstrate hireable skill to the Skåne/Copenhagen tech job market. That context matters for how it's built, not just what it does: architectural decisions are made with the same rigor a professional team would expect, not just "whatever ships fastest." Where a shortcut and a correct-but-slower approach conflict, prefer the approach that's defensible in a technical interview.

## Design intent

Editorial, content-first, not visually chaotic — closer to a professional football club's site (Manchester United, Juventus) translated into basketball, at a scale appropriate for a small regional club rather than a global one. Activity (news, fixtures) is surfaced before static "about" content. Hero sections are emotive, not informational. Brand colours are black, white, and a club red — used deliberately and restrictively, not applied everywhere just because it's the brand colour (see `/accessibility` skill for the exact contrast rules governing this).

Full design reference material — screenshots, extracted patterns, locked and open decisions — lives in `design-brief.md` and `design-patterns.md`.

## Tech stack

- **Framework:** Astro 7, TypeScript (strict mode)
- **CMS:** Hygraph (GraphQL headless CMS) — schema fully built and reconciled against the actual live config. Switched off by default: `CONTENT_SOURCE="demo"` serves every model from local data about a fictional club, Sundets Basketförening (see `/graphql`). The rendered site never names the real club.
- **Styling:** Tailwind CSS 4 via the Vite plugin — no `tailwind.config.js`, design tokens live in an `@theme` block
- **Data layer:** `graphql-request` (chosen over Apollo — Astro is server-rendered/static, Apollo's client-side caching is dead weight here) + `graphql-codegen` (schema-generated types feed every RD type — never hand-written)
- **Hosting:** Vercel, connected to GitHub, environment variables configured
- **Contact:** `mailto:` only — no contact form or email service (`/kontakt` + Resend dropped 2026-10-01)
- **Package manager:** pnpm

## How this project is built

Skills define outcomes and structural constraints, not implementation steps. Where a skill is silent, use your own judgment. Load the skill that matches the task:

- **`/data-mapping`**: the RD → mapper → VM → UI pattern and per-field fallbacks
- **`/graphql`**: all Hygraph access through `hygraphClient.ts` and each model's failure strategy
- **`/seo`**: SEO and JSON-LD rules
- **`/accessibility`**: WCAG 2.1 AA rules and the Definition of Done

Schema facts (models, enums, the field-by-field Required/Flag/Default table) live in `.claude/skills/data-mapping/fallback-reference.md`.

## Working relationship

- **Claude Code** works in plan mode by default.
- **The developer** keeps authority at every decision and review point. Plans get reviewed and locked before more work is built on them.

## Status

Live at https://sundet-basket.vercel.app/. `src/docs/progress-tracker.md` is the historical build log. Don't read it unless the developer asks.

## What's explicitly out of scope for v1

Membership signup with payment, live scores, dark mode. Do not build toward these unless the brief changes.

## What's deferred but planned

League standings table, ICS calendar export, GDPR/cookie consent, club history/trophy timeline, Swedish/English i18n toggle, photo galleries, player season stats, downloads section, FAQ page. Don't build these speculatively — they're not in scope until explicitly requested.

---

## Development

When starting the dev server, use background mode:

```
astro dev --background
```

Manage the background server with `astro dev stop`, `astro dev status`, and `astro dev logs`.

## Documentation

Full documentation: https://docs.astro.build

Consult these guides before working on related tasks:

- [Adding pages, dynamic routes, or middleware](https://docs.astro.build/en/guides/routing/)
- [Working with Astro components](https://docs.astro.build/en/basics/astro-components/)
- [Using React, Vue, Svelte, or other framework components](https://docs.astro.build/en/guides/framework-components/)
- [Adding or managing content](https://docs.astro.build/en/guides/content-collections/)
- [Adding styles or using Tailwind](https://docs.astro.build/en/guides/styling/)
- [Supporting multiple languages](https://docs.astro.build/en/guides/internationalization/)
