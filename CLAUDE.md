# workflow_nav

A single-file prototype of a **Trace Explorer** — a UI for inspecting a finished workflow execution trace.

`index.html` is fully self-contained: React 18 + Babel are loaded from CDNs and the whole app (data model, logic, and UI) lives in one inline script. Open it directly or serve it statically; no build step.

It was ported from a Claude Design project (`Trace Explorer.dc.html` + `TraceDetail`), reimplemented in plain React to drop the proprietary `DCLogic` template runtime.

## What it shows
- A workflow trace tree (`extLawParalel2`): nodes, parallel gateways, conditions, datasource ops, and subworkflow "tool" nodes.
- **Drill-down** into subworkflow instances, with breadcrumb navigation, a "called as a tool by" marker, an instance switcher, and an "Up" button.
- A **scope summary** bar and a **detail panel** (Logs tab) with per-node metadata and a synthesized execution log.

## Deploy
Served via GitHub Pages from `main` at root → https://bogdandraghici.github.io/workflow_nav/. Any push to `main` rebuilds the site. Requires internet at runtime (CDN dependencies).
