# fastcac-docs

A [Mintlify](https://mintlify.com) documentation site — **FastCAC's internal, consolidated
reference for the VAS API**, the third-party vendor (Oasis Product) that
[`fastcac_api`](../fastcac_api) integrates with to submit Business Name and LLC registrations to
Nigeria's Corporate Affairs Commission (CAC).

**This is not FastCAC's own public developer documentation** — there is no FastCAC-facing
developer product yet. VAS's own documentation is scattered across an in-app interactive
explorer, a public FAQ site, and an externally-hosted Postman collection (for LLC only), with real
gaps and inconsistencies between them. This site merges all of that into one place, with pricing
attached. See [`known-issues.mdx`](known-issues.mdx) for the specific discrepancies found along the
way (e.g. a stale sandbox pricing page that undercounted Business Name registration by ₦10,500).

Kept private for now. Per the root workspace [`CONTEXT.md`](../CONTEXT.md), the plan is for this
to become the seed content for a real `developers.fastcac.com` once FastCAC has its own B2B API
contract worth documenting — don't confuse this (FastCAC's reference for someone *else's* API)
with that future site (FastCAC's own API, documented for third parties).

## What's covered

- **Business Name Registration** — compliance check, submission, status, query/update, certificate
  download. Production-live today.
- **LLC (Company) Registration** — affiliates, PSC (Persons with Significant Control), share
  allocation, stamp duty via Remita. Beta, but vendor-confirmed production-ready.
- **Validation Services** — KYB lookups for an existing company (VRC consent mechanism).
- **Pricing** — all priced line items across BN, LLC, Validation, and Annual Return Services, in
  one table, sourced from the *production* dashboard (the sandbox pricing page is confirmed stale
  — see [`pricing.mdx`](pricing.mdx)).

## Prerequisites

- **Node.js ≥ 20.3 (20.3+ or 21+)** — Mintlify's CLI (`mint`) depends on `sharp`, which fails to
  install on older Node versions. If you hit an install error here, run `nvm install --lts` (or
  otherwise upgrade Node) before retrying.
- The [Mintlify CLI](https://www.npmjs.com/package/mint):

  ```bash
  npm i -g mint
  ```

## Running the docs locally

From this directory (where `docs.json` lives):

```bash
mint dev
```

Open [http://localhost:3000](http://localhost:3000) for a live local preview. If a page loads as
a 404, confirm you're running the command from this directory (Mintlify needs to find `docs.json`
at the working directory root).

If your local dev environment stops working correctly, update the CLI first:

```bash
mint update
```

## Publishing

Mintlify's GitHub app propagates changes from this repo to the deployed site. Once installed
(from the [Mintlify dashboard](https://dashboard.mintlify.com/settings/organization/github-app)),
pushes to the default branch deploy to production automatically — there's no separate build step
to run manually.

## Project structure

```
docs.json               # site config: nav structure, theme, colors, logo, footer links
index.mdx                # landing page — why this site exists, what's covered, environments table
quickstart.mdx            # auth: getting an API key, the X_API_KEY header, a real bash `$`-expansion gotcha
known-issues.mdx           # documented gaps/inconsistencies found across VAS's own scattered docs
pricing.mdx                 # all priced line items, sourced from production (not sandbox)
business-name/                # BN registration: overview, endpoints, compliance codes, naming rules
llc/                            # LLC registration: overview, endpoints
validation/                       # KYB validation services: overview, endpoints
logo/, favicon.svg                 # branding assets
```

## Content conventions

Set by `AGENTS.md` in this repo — worth reading before adding pages:

- Active voice, second person ("you")
- One idea per sentence, sentence-case headings
- Bold for UI elements (e.g. **Settings**), code formatting for file names/commands/paths
- Pages are MDX with YAML frontmatter (`title`, `description`); navigation structure lives
  entirely in `docs.json`, not inferred from the file tree

## Environments reference

| Environment | Dashboard (login, pricing, wallet, API keys) | API base URL |
|---|---|---|
| Sandbox | `https://vas.oasisproducts.ng` | `https://vasapp.oasisproducts.ng` |
| Production | `https://vas.cac.gov.ng` | `https://vasapp.cac.gov.ng` |

The dashboard and API hosts are different domains for both environments — see
[`quickstart.mdx`](quickstart.mdx) for the full authentication walkthrough, including why loading
a VAS API key via `bash source .env` silently corrupts it (VAS keys are bcrypt-hash-shaped and
start with `$`, which bash interprets as variable expansion).

## Further reading

- [`AGENTS.md`](AGENTS.md) — writing style and content conventions for this repo, plus Mintlify
  MCP server references for AI-assisted editing.
- [`known-issues.mdx`](known-issues.mdx) — the specific gaps and contradictions found while
  consolidating VAS's scattered documentation.
- Root workspace [`CONTEXT.md`](../CONTEXT.md) — how this site fits into the rest of FastCAC.
