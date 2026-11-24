# AGENTS.md — woocommerceconnector

Entry file for any AI agent or person working in this repository. It is tool-neutral. `CLAUDE.md` imports it, so
edit this file, not that one.

## What this repository is
Frappe app: libracore's ERPNext WooCommerce Connector (publisher `libracore` in `hooks.py`, AGPL), which syncs
items, stock, customers, addresses, sales orders, sales invoices and payment entries with a WooCommerce shop. It
is an upstream app uploaded here as files.

**Legacy.** Two commits, both on 5 Feb 2024 ("Add files via upload"); nothing since. Where it runs, if anywhere, is
not recorded in this repo (unverified).

## Read first
The estate's rules live in `AL2018/littlecocoa-docs`. Read them in this order before working here:
1. `docs/cc-briefs/METHOD-02-how-we-work.md`: how Alan, the architect and the coder work. Always first.
2. `docs/cc-briefs/PRODUCTION-INTEGRITY-RULE.md`: what may touch production, and how.
3. `docs/cc-briefs/ACCEPTANCE-CRITERIA-RULE.md` and `docs/cc-briefs/OPERATING-STANDARDS-v1.0.md`.
4. `docs/cc-briefs/CC_STANDING_RULES_v0.9.md` (v0.9 governs; earlier versions are superseded).
5. `docs/architecture/GOTCHAS.md`: the single register of known traps.
Then this file, then the repo's own docs.

## Rules that bite here
A short digest; the documents above are the source, and this list is a cache.
- Production is changed only through the application or its API, never by direct SQL. Staging first.
- The default branch is protected: feature branch, then PR. Deploys name both the branch and the commit.
- No secrets in the repo. AI never sends a message to anyone outside the team.
- Australian English in copy and comments.
- Never declare `frappe` (or `erpnext`) as a pip dependency. uv cannot resolve it, because frappe's own metadata carries `PyPika @ git+https://...` and uv rejects transitive URL dependencies (fixed in dieline and Silent-Print-ERPNext, 28–29 Jul 2026). Bench provides frappe. `requirements.txt` here still lists `frappe` (and `woocommerce`) and `setup.py` reads it.
- `test_sites/test_site/site_config.json` is upstream's committed test-site config and carries password keys. Never copy it into a real site, and never treat its values as estate credentials.
- Legacy code: don't build on it without a brief. The estate's web-order work is recorded in littlecocoa-docs.

## Structure
- `woocommerceconnector/sync_products.py`, `sync_customers.py`, `sync_orders.py`: the sync jobs.
- `woocommerceconnector/woocommerce_requests.py`, `webhooks.py`, `api.py`: the WooCommerce API side.
- `woocommerceconnector/woocommerceconnector/doctype/`: WooCommerce Config and Item Product Category.
- `woocommerceconnector/patches/V1_0/`: upstream patches. `test_sites/`: upstream test-site files.

## Conventions
- Default branch `main`. No CI.
- Whether this app is installed on any site is not recorded in this repo (unverified). Any deploy is Alan's, on Frappe Cloud, by branch and SHA, after staging.

## Current state
Not kept here: entry files describe the repo, not the week. See `AL2018/littlecocoa-docs`
`docs/handoffs/STATUS-LEDGER.md` and the workstream folder under `docs/` for this repo.
