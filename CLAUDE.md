# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Gallabox's customer-facing product documentation, published with [Mintlify](https://mintlify.com). No application code — 155 MDX pages, one `docs.json` config, and a flat `images/` asset folder. The audience is Gallabox customers (business owners, marketers, support agents), not developers. Developer API reference lives in a separate site (`api-docs.gallabox.com`), linked as an anchor from `docs.json`.

See also `AGENTS.md` for the shared writing-style baseline.

## Commands

```bash
npm i -g mint          # one-time: install the Mintlify CLI
mint dev               # local preview at http://localhost:3000 (run from repo root)
mint broken-links      # run when a change adds, moves, or renames links or pages
mint update            # upgrade the CLI if dev server misbehaves
```

There is no `package.json`, build step, test suite, or linter. `mint broken-links` is the only check worth running, and only when a change touches links, page paths, or redirects.

Two MCP servers are configured for this project: `https://mcp.mintlify.com` (edit content/settings) and `https://www.mintlify.com/docs/mcp` (query Mintlify's own docs).

## Workflow

- **Every change goes through a pull request.** Pushing to `main` deploys straight to production via the Mintlify GitHub app, so never commit there directly — branch, commit, open a PR.
- **When something isn't clear enough to state to a customer, ask before deciding.** These pages are external and customer-facing; a plausible-sounding guess ships as fact. If the product behaviour, plan availability, role permission, price, or effective date can't be verified, raise the question instead of writing around it.

## Structure and navigation

Top-level directories map to product areas: `concepts/`, `conversations/` (surfaced in the sidebar as **Inbox**), `contacts/`, `ai-agents-and-bots/`, `whatsapp/`, `instagram/`, `web-chat/`, `integrations/`, `reports-and-analytics/`, `settings/`, `privacy-and-security/`, `pricing-and-billing/`, plus a separate `guide/` tab for how-to guides.

`docs.json` is the single source of truth for what appears on the site and in what order:

- **A new `.mdx` file is invisible until it is added to a `navigation.tabs[].groups[].pages` array.** Page entries are paths without the `.mdx` extension (`whatsapp/broadcasts/create-broadcast`).
- Every directory that is a sidebar group has an `overview.mdx` (43 of them) plus a `redirects` entry mapping the bare directory path to it (`/whatsapp` → `/whatsapp/overview`).
- `redirects` holds ~385 entries preserving URLs from the pre-Mintlify site and past restructures. **Never delete or repoint an existing redirect casually, and when you move or rename a page, add a redirect from the old path to the new one.** Redirect destinations may include anchors (`/settings/security#allowed-ips`).
- Group nesting is arbitrary depth — `integrations/` nests category → vendor → pages (e.g. CRM → HubSpot → its pages).

## Page conventions

Frontmatter: `title` always; `description` on most pages (used for SEO and search); `sidebarTitle` on overview/hub pages so the sidebar reads "Overview" while the page title names the product area. No `icon` frontmatter — group icons are set in `docs.json`.

Recurring page shape, in this order:

1. A `> **Who can use this?**` blockquote (present on 76 pages) listing plan availability and which roles can use the feature.
2. An `<Info>` callout giving the one-paragraph "what this is".
3. A `## Plan Availability` markdown table (64 pages) — capability rows against Basic / Essential / Advanced columns, `✓` and `—` as cell values, centre-aligned (`:-:`).
4. `## Before You Start` prerequisites on long task pages.
5. `## Steps` with `### Step N: <imperative>` subsections separated by `---`, or a `<Steps>`/`<Step>` component.
6. `## FAQs` as an `<AccordionGroup>` of `<Accordion>` items — the dominant pattern for reference detail (388 accordions repo-wide).

Components in use, roughly by frequency: `Frame`, `Accordion`/`AccordionGroup`, `Steps`/`Step`, `Info`, `Warning`, `Card`, `Columns`, `Check`, `Note`, `Tabs`/`Tab`, `Tip`. Hub pages are built from `<Columns cols="2">` of `<Card title=... href=...>`.

Media: all assets live flat in `/images/` (no subfolders) and are referenced as `/images/<name>`. Screen recordings (`.mp4`, ~300 of them) outnumber screenshots (`.png`) and are always wrapped like this:

```mdx
<Frame>
  <video src="/images/authorize-hubspot.mp4" autoPlay loop muted playsInline controls className="w-full aspect-video" />
</Frame>
```

Links between pages are always root-relative and extensionless (`/whatsapp/templates/custom-marketing`), never relative paths or `.mdx`.

## Writing

Follow the style rules in `AGENTS.md`: active voice, second person, one idea per sentence, sentence case headings, **bold** for UI labels, backticks for file names and paths.

Beyond that:

- Write for a non-technical reader. Recent commits exist specifically to strip jargon and internal markup language from pages — don't reintroduce it.
- Describe what the product actually does today. Accuracy against the shipped UI is the recurring theme of this repo's history; never infer a behaviour from the docs' own prior wording.
- One page owns each fact. FAQ and overview pages link to the detailed page as the source of truth instead of restating it; duplicated rate cards and pricing tables have been deliberately removed.
- Pricing pages carry dated policy changes (e.g. the Oct 1, 2026 WhatsApp pricing changes) — keep effective dates explicit rather than writing "new" or "soon".
- Commit messages use a `docs:` prefix and say what changed for the reader.
