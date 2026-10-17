# Marble migration tests

Use MR-Moqui, mr-mantle-udm, mr-mantle-usl and the migrated MrSimpleScreens. Names in `component.xml`, not checkout directory names, select components for `moqui test`.

From the MR-Moqui root:

```sh
cargo build -p moqui
R=$(mktemp -d /tmp/mrmarble-XXXXXX)
mkdir -p "$R/component"
cp -r runtime/conf "$R/conf"
ln -s "$PWD/runtime/base-component" "$R/base-component"
for c in mantle-udm mantle-usl MrSimpleScreens MrMarbleERP; do
    ln -s "$PWD/runtime/component/$c" "$R/component/$c"
done

# Independent fresh load, with entity ECAs enabled:
MOQUI_RUNTIME="$R" target/debug/moqui load types=all

# Tests create their own fresh disposable database, not the load database above.
MOQUI_RUNTIME="$R" target/debug/moqui test mantle-usl SimpleScreens MarbleERP \
    --keep --junit /tmp/mrmarble-junit

# Faster: Marble and its eight prerequisite Mantle flow specs:
MOQUI_RUNTIME="$R" target/debug/moqui test mantle-usl MarbleERP \
    --spec MarbleScreens --keep --junit /tmp/mrmarble-screen-junit

MOQUI_RUNTIME="$R" target/debug/moqui lint --groovy runtime/component/MrMarbleERP
MOQUI_RUNTIME="$R" target/debug/moqui lint --screens /tmp/mrmarble-screen-lint.txt
python3 -I scripts/screen-port-scan.py runtime/component/MrMarbleERP/screen
find runtime/component/MrMarbleERP -name '*.xml' -print0 | xargs -0 xmllint --noout
cargo test -p moqui-core --lib
```

Both `mantle-usl` and `MarbleERP` must be selected for cross-component test dependencies. The fixture flows create orders 55400/55401, invoice/payment 55400 and other data asserted by the screens. Tests restore the user's original active-organization preference. Discovery excludes wiki-specific pages and SalesSummary, which has its own populated date-bounded check.

## Authenticated browser smoke

Use **disposable** data; this smoke changes and clears the demo user's active organization. Start a server against the retained `/tmp/mt-...` runtime printed at the beginning of the test run, with a free HTTP and cluster port. Marble's normal component config provides the app mount and its setup data provides administrator authorization; no extra authz grant is needed.

```sh
# In a separate terminal, after the test process finishes:
MOQUI_RUNTIME=/tmp/mt-... target/debug/moqui --port 18082 --https-port off \
    --no-run-es -D cluster_https_port=18446

# Once the server reports it is listening (Node 22+ and Chromium):
MRMARBLE_BASE_URL=http://127.0.0.1:18082 \
MRMARBLE_CHROMIUM=/usr/bin/chromium MRMARBLE_OUTPUT_DIR=/tmp \
    node runtime/component/MrMarbleERP/test/browser-smoke.mjs
pdftotext /tmp/mrmarble-order.pdf -
```

The default credentials are the **local demo** `john.doe` / `moqui`; override `MRMARBLE_USERNAME` and `MRMARBLE_PASSWORD` if using a different disposable fixture. Never enable demo credentials in production. Stop the server when done.

The smoke waits for browser load events and QVT DOM mutations, not sleeps. It checks the real mounted HTML and QVT pages, the native organization menu, select/clear preference transitions, barcode SVG and PDF generation, uncaught exceptions and HTTP failures. Outputs: `mrmarble-browser-results.json`, `mrmarble-dashboard.png`, `mrmarble-order.pdf`. See `../MIGRATION-STATUS.md` for results and precise acceptance limits.
