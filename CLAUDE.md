# workflow_nav

A single-file prototype of a **Trace Explorer** — a UI for inspecting a finished workflow execution trace.

`index.html` is fully self-contained: React 18 + Babel are loaded from CDNs and the whole app (data model, logic, and UI) lives in one inline script. Open it directly or serve it statically; no build step.

It was ported from a Claude Design project (`Trace Explorer.dc.html` + `TraceDetail`), reimplemented in plain React to drop the proprietary `DCLogic` template runtime.

## What it shows
- A workflow trace tree (`extLawParalel2`): start/end, parallel gateways, conditions, datasource ops, subworkflow nodes, and a **Custom Agent** node whose tool-call workflows are nested under it inline.
- **Drill-down** across three levels — root → `extProcessLawOne` instances → their child subworkflows — with breadcrumb navigation, an instance switcher, and an "Up" button.
- A "called as a tool by" breadcrumb marker shown **only** for genuine agent tool calls (nodes flagged `calledAsToolBy`), not for ordinary subworkflow drill-downs.
- A **scope summary** bar and a **detail panel** (Logs tab) with per-node metadata and a synthesized execution log.

## Data
The tree is hand-authored in `build()` but audited against the real trace: the top level and the four `extProcessLawOne` instances mirror `extLawParalel2_instance.json` exactly (durations, UUIDs, datasource filters, conditions). The deepest child subworkflows and the Custom Agent's tools are synthesized (weighted durations that sum to the real parent duration; reused instance UUIDs/resource IDs where available), since the run doesn't capture them.

## Deploy
Served via GitHub Pages from `main` at root → https://bogdandraghici.github.io/workflow_nav/. Any push to `main` rebuilds the site. Requires internet at runtime (CDN dependencies).
