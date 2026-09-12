# Documentation project instructions

Guidance for AI coding agents and humans editing the plamotrack documentation site.

## About this project

- This is the documentation site for [plamotrack](https://github.com/DeusMaximus/plamotrack), a self-hosted Gunpla and plastic-model collection tracker, built on [Mintlify](https://mintlify.com).
- Pages are MDX files with YAML frontmatter; navigation and site configuration live in `docs.json`.
- The app itself lives in the `plamotrack` repository. These docs describe what that repository ships; they never describe planned work as if it existed.
- Preview locally with `mint dev`; check links with `mint broken-links`.

## Audience

Two readers, one site. The **Get Started** and **Using plamotrack** groups are for a hobbyist who wants to track a collection and may never have opened a terminal before installing this: every step names the button, and the pages carry screenshots. **Deployment**, **Authentication**, **AI & MCP** and **Configuration & Maintenance** are for the same person on a more advanced setup — a VPS, a reverse proxy, an identity provider — and can assume the terminal.

## Terminology

- Use the UI's own words for anything the reader clicks or reads on screen. The source of truth is the app's `en-AU` catalogue, `frontend/src/i18n/catalogues/en-AU.json` in the app repository: **Add kit**, **New order**, **Record order**, **Save changes**, **Already in hand**, **Apply to kit**, **Withdraw…**, **Preview changes**, **Apply import**, **Create token**. If a label changes in the app, the docs are wrong until they change too.
- The six kit statuses are spelled as the UI spells them: **Pre-ordered**, **Ordered**, **In Transit**, **Backlog**, **Building**, **Complete**. In CSV columns and API fields they are `pre_ordered`, `ordered`, `in_transit`, `backlog`, `building`, `complete` — code formatting, never translated.
- A **kit** is one physical model; two copies are two kits. A **catalog** is one of the four inventory tables — **Tools**, **Consumables**, **Upgrades**, **Display** — named as the Inventory tabs name them. A **retailer** is a shop. The **owner** is the one account an instance has. A **personal access token** is the credential for scripts and MCP clients; do not shorten it to "API key".
- Money is stored in minor units with a currency code; the docs say "reference currency" for the instance default, never "base currency".
- Settings, environment keys, file names, commands and URLs are code-formatted: `PUBLIC_BASE_URL`, `.env`, `docker compose up -d --build --wait`.

## Screenshots

- Every screenshot under `images/screenshots/` is generated, not hand-taken, by the app repository's `frontend/e2e/screenshots.spec.ts` against a throwaway database seeded with invented demo data. Re-run that spec after a UI change rather than editing an image; the recipe is in the spec's header comment.
- Each capture comes as a pair, `name.png` (dark) and `name-light.png`, embedded so the reader's theme picks one:

  ```mdx
  <Frame caption="…">
    <img className="block dark:hidden" src="/images/screenshots/name-light.png" alt="…" />
    <img className="hidden dark:block" src="/images/screenshots/name.png" alt="…" />
  </Frame>
  ```

- Never show real shops, real ratings or a real credential. Captions say the data is invented where a reader might wonder.

## Style preferences

- Use active voice and second person ("you").
- Keep sentences concise — one idea per sentence.
- Australian English, matching the app: "recognise", "organised", "catalogue" in prose — except the product term **catalog** for the inventory tables, which follows the API.
- Use sentence case for headings.
- Bold for UI elements: Click **Settings**.
- Code formatting for file names, commands, paths and code references.
- A how-to is a `<Steps>` block with one action per step; a reference is a table.

## Content boundaries

- Document only released behaviour. The four deployment paths in **Deployment** are the ones that have been run through the app repository's deployment gate; do not add a fifth from general knowledge.
- No internal references: no issue numbers, review rounds, milestone names or agent process in reader-facing pages. The changelog may link a GitHub issue that a release note names.
- Nothing that helps an attacker: no example that puts a token in a URL, no advice to disable a security control to make something work.
- The pages are public. A PR body or comment written by an agent opens with a line naming the model and closes with a sign-off, as in the app repository; the pages themselves carry no attribution.
