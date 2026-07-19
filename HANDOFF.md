# HANDOFF

## Latest state

Initial commit (`3f734d6`) pushed to `main` on `origin`
(https://github.com/devgenix/fastcac_internal_docs.git). This is the first content in the repo —
previously empty.

What was added: a full Mintlify site consolidating VAS (Oasis Product)'s scattered API docs —
Business Name Registration, LLC (Company) Registration, and Validation Services — into one
internal reference, plus pricing sourced from production.

- `docs.json` — site config, nav grouped into Getting Started / Business Name Registration / LLC
  (Company) Registration / Validation Services / Pricing, sandbox+production dashboard anchors
- `index.mdx`, `quickstart.mdx` (auth walkthrough, including the VAS-key/bash-`$`-expansion
  gotcha), `known-issues.mdx`, `pricing.mdx`
- `business-name/` — overview, endpoints, compliance codes, naming rules
- `llc/` — overview, endpoints
- `validation/` — overview, endpoints
- `logo/`, `favicon.svg`, `AGENTS.md`, `README.md`, `LICENSE`, `.mintignore`

`known-issues.mdx` documents the specific gaps/inconsistencies found in VAS's own material while
writing this — worth reading before trusting a pricing or endpoint detail that looks off:
- Sandbox pricing is confirmed stale (production is source of truth); Business Name was
  undercounted by ₦10,500 (₦16,500 sandbox vs. ₦27,000 production, confirmed by VAS/Oasis
  2026-07-18). LLC pricing separately flagged as wrong, no corrected figures yet.
- VAS's own Postman collection leaks a live-looking bcrypt API key in several LLC curl examples —
  never use it.
- Validation Services pricing catalog lists 33 priced line items but only 15 have documented
  endpoints — several cheaper non-VRC-gated equivalents and undocumented-but-priced items exist
  with no confirmed URL.

## What's still open / next steps

- LLC pricing figures are known-wrong but not yet corrected — no confirmed replacement numbers
  from VAS yet.
- The undocumented-but-priced Validation Services endpoints (see `known-issues.mdx`) need their
  actual URLs confirmed with VAS before anyone integrates against them.
- LLC "Forward Flow" is missing the POST endpoints that create `shares` and
  `registration.address` — needs confirming with VAS.
- Mintlify's GitHub app needs to be installed (from the Mintlify dashboard) against this repo for
  pushes to `main` to auto-deploy — not yet confirmed done.
- Per root workspace `CONTEXT.md`, this repo is the seed content for a future
  `developers.fastcac.com` once FastCAC has its own B2B API worth documenting — kept private for
  now, don't confuse with that future site.
