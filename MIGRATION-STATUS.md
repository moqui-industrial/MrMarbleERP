# MrMarbleERP migration — 2026-10-17

MR-Moqui port of `moqui/MarbleERP` at `dfbea90`. Repository: https://github.com/moqui/MrMarbleERP (master); upstream remains https://github.com/moqui/MarbleERP. The component name stays **MarbleERP**, preserving component locations, authorization artifacts and `/apps/marble` mounting. `/qapps/marble` also works.

## Work performed

1. Cloned upstream unchanged and pushed that history first. `MIGRATION-INVENTORY.md` freezes the original component lint: 3 XML files, 47 expression sites, 30 parse failures, 28 flagged sites. Whole-runtime screen lint initially had 29 parse failures. `linkCondition` data attributes are not covered by that lint, so they were inspected and tested separately.
2. Used a disposable runtime under `/tmp` with base-component, mr-mantle-udm, mr-mantle-usl, MrSimpleScreens and this component. Built the current framework with `cargo build -p moqui`.
3. The pristine load stopped at the Java-only `moqui-fop` dependency. Removing that dependency was necessary before the pre-conversion load could pass. Print content now comes from MrSimpleScreens' HTML-print replacements and MR-Moqui's Chromium PDF path, not FOP.
4. Mechanical conversion rewrote 26 parameter maps and one data-link Elvis expression in two files. Parse failures fell from 30 to 3. Converter output is committed separately from the hand port.
5. Hand ported `orgPartyRoles*.partyId` to `map`, the inline FreeMarker organization chooser to the fancy dialect, and the two stored party-link role conditions to JavaScript `some`. Replaced the chooser's jQuery/Bootstrap dropdown/tooltip with native `details` and DOM relocation. Organization names are HTML-escaped and IDs URL-encoded.
6. Added `test/MarbleScreens.spec.js` and the dependency-free Chromium smoke `test/browser-smoke.mjs`.

Marble owns only its shell and dashboard; most ERP screens are mounted from SimpleScreens. No Mantle business services were copied into this component. Authorization data and the `MANTLE_ACTIVE_ORG` filters are retained unchanged; no global bypass or new user grant was added.

## Validation

- Component lint: **0 parse failures, 0 flagged sites**; one inline fancy body compiled.
- Whole-runtime screen lint: **0 parse failures**; 31 existing flagged sites in base-component/SimpleScreens, plus eight legacy print-location compatibility adapters. These are not Marble findings.
- `screen-port-scan.py` for Marble: no candidates. All component XML passes `xmllint --noout`.
- Fresh all-data load with entity ECAs enabled: **8,359 records, 571 tables created, zero table/data errors, exit 0**. Marble's setup file loads 26 records. Reloading all demo data onto an already populated database is not an idempotency test: upstream's immutable AssetDetail records can fail on the second load, while the loader continues to other files.
- Final full run: **429 features passed, 0 failed/ignored/skipped, 46 specs** (344 Mantle, 67 SimpleScreens, 18 Marble). Marble includes discovery of parameter-free mounted pages, populated customer/supplier/order/invoice/payment/report pages, order/invoice printing, chooser states, stored role conditions for null/empty/mixed roles, and wiki-link expansion.
- Core unit suite: **940 passed, 0 failed, 1 ignored**.
- Real authenticated Chromium: HTML dashboard/customer/supplier/order/invoice/payment, organization select/clear through the existing preference transition, QVT dashboard/order, SVG barcode and actual order PDF. **Zero uncaught exceptions and zero HTTP failures.** Extracted PDF text contains Ziziwork Retail, Demo Product One-One and `$23,795.00`. Dashboard screenshot inspected.

Evidence from this run (local, not portable fixtures): `/tmp/mrmarble-final-tests.log`, `/tmp/mrmarble-final-junit`, `/tmp/mrmarble-clean-load.log`, `/tmp/mrmarble-core-tests.log`, `/tmp/mrmarble-browser-results.json`, `/tmp/mrmarble-dashboard.png`, `/tmp/mrmarble-order.pdf` and `/tmp/mrmarble-order.txt`.

## Required framework support

Use the current MR-Moqui source and the ported MrSimpleScreens, not an older release binary or upstream SimpleScreens. This was validated with mantle-usl `14d327b`, mantle-udm `50be8e3`, and the in-progress MrSimpleScreens migration based on `2c1ba93` (its migration and supporting framework edits were already present locally).

Chromium found a framework gap that socketless/main-thread tests did not: an OrderDetail shipment include under the full Marble app shell exceeded a nested engine's 256 KiB script budget. Merely increasing the outer script budget did not fix it. Request workers now reserve an 8 MiB native stack, with a shared 4 MiB script budget that nested request engines may use from the remaining allowance. Non-request/service worker budgets are unchanged; minimum remaining stack and script-depth guards remain. A unit regression verifies that request script recursion fails with a script error rather than overflowing the worker. The full suite and authenticated browser smoke were rerun after this fix. See `plans/MarbleERPMigration.md` in MR-Moqui.

## Reproduce

See `test/README.md` for the isolated-runtime setup and commands. Test specs disable authz only around their features and restore it afterward; Chromium used the existing demo administrator with normal authorization enabled. The server is stopped after the smoke; this migration does not leave an app server running.

## Acceptance limits

Passing is not exhaustive role/organization isolation, CSRF, every business transition or every browser interaction. QVT was exercised on dashboard and order, not every mounted screen; organization select/clear was exercised in HTML. Wiki discovery exclusions still require page/space fixtures. Search-link expressions are tested against stored records, not a new exhaustive search-index/browser fixture. The upstream Marketing dashboard item has no mounted screen and remains unavailable. Physical check alignment, all external templates, FOP pagination parity, scanner hardware and production data upgrade behavior are not certified. Existing SimpleScreens acceptance limits still apply.
