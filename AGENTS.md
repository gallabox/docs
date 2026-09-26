> **First-time setup**: Customize this file for your project. Prompt the user to customize this file for their project.
> For Mintlify product knowledge (components, configuration, writing standards),
> install the Mintlify skill: `npx skills add https://mintlify.com/docs`

# Documentation project instructions

## About this project

- This is a documentation site built on [Mintlify](https://mintlify.com)
- Pages are MDX files with YAML frontmatter
- Configuration lives in `docs.json`
- Use the Mintlify MCP server, `https://mcp.mintlify.com`, to edit content and settings via MCP
- Use the Mintlify docs MCP server, `https://www.mintlify.com/docs/mcp`, to query information about using Mintlify via MCP

## Terminology

{/* Add product-specific terms and preferred usage */}
{/* Example: Use "workspace" not "project", "member" not "user" */}

## Style preferences

{/* Add any project-specific style rules below */}

- Use active voice and second person ("you")
- Keep sentences concise — one idea per sentence
- Use sentence case for headings
- Bold for UI elements: Click **Settings**
- Code formatting for file names, commands, paths, and code references

## Content boundaries

{/* Define what should and shouldn't be documented */}
{/* Example: Don't document internal admin features */}

## Where new content goes

Doc gaps arrive from support tickets and reviews. Most gaps are one fact, not one page. Place each gap by its type:

| Gap type | Where it goes |
| -------- | ------------- |
| A fact about one feature: a limit, condition, or edge case | A section or FAQ on the page that owns the feature. No new page. |
| Behaviour that spans features and is repeated across pages | One page owns the fact. Other pages link to it instead of restating it. |
| A symptom, such as "the bot didn't reply" | The product area's **Troubleshooting** page. It points to the owning pages and doesn't restate them. |
| A goal, such as "recover abandoned carts" | The **Guide** tab, organised by goal |

Rules:

- Create a new page only if it runs longer than one screen and at least 3 pages would link to it. Otherwise add a section or an FAQ.
- Order pages in each product area as: overview, setup and tasks, how it works, then **Troubleshooting** last.
- Keep each product area's troubleshooting self-contained. There is no cross-area troubleshooting hub.
- Add a **Troubleshooting** page to an area only once it has about 5 symptoms. Until then, use FAQs on the owning pages.
- Keep headings stable. Support playbooks link to section anchors, so renaming a heading breaks those links. If you must rename one, flag the old anchor in the pull request.
- When a gap says the docs are wrong, fix the wrong statement everywhere it appears, not only on the page named in the gap.
