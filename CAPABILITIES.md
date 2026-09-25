# CanvasXpress Capabilities

A machine-readable summary of what CanvasXpress can do today, for LLMs and site search.
Every entry below describes a **shipped, publicly available** capability. This file is a
curated source — it is published to `/data/md/CAPABILITIES.md`, linked from `llms.txt`, and
indexed by the site search. Keep it product-accurate; do not add internal, planned, or
deferred work here.

> Extend this file by distilling shipped work: `tools/kb/distill-plan.py <plan> --kind web`
> produces a leak-checked product-narrative draft you can curate into a section below.

## Charting

- **40+ native graph types** — bar, line, area, scatter, boxplot, violin, dotplot, heatmap,
  correlation, network, genome, circular, oncoprint, Venn, chord, tree, treemap, sankey,
  alluvial, contour, map, 3D scatter/surface, and more — all from a single unified config.
- **Grammar-of-graphics rendering** — layered geoms, stats, scales, coordinate systems and
  faceting, so complex multi-panel figures come from a declarative specification.
- **ggplot2 import and visual parity** — R ggplot2 plots convert to CanvasXpress and render
  with close visual fidelity (element and legend order, colour/fill/size/shape/linetype/alpha).
- **Time-series forecasting** — `showForecast` projects a regularly spaced series forward with a
  prediction interval using exponential smoothing (SES, Holt, Holt-Winters; matches R
  `stats::HoltWinters`), per group or on date axes, extending the axis over the horizon. R
  `forecast` plots (`autoplot(forecast(...))`, `geom_forecast()`) are drawn from R's own forecast.
- **Live streaming** — `pushData(message)` appends new samples to a chart and keeps a rolling
  window (`streamWindow`, oldest dropped), recomputing fits and filters over the window; about
  2 ms per update. In dashboards, a `kind: "live"` source subscribes a panel to a
  Server-Sent-Events stream from canvasxpress-connectors (no credential in the browser), built
  without code. Dashboard-live cadence (seconds); no stream analytics or event processing.

## Interactivity

- **Built-in interactivity** — hover tooltips, click/double-click events, zoom, pan, brushing,
  selection, filtering, and drill-down without extra code.
- **Live customizer** — an in-chart UI for restyling, reconfiguring, and reshaping data,
  including shelf-style authoring and calculated fields.
- **Dashboards** — multiple linked charts with shared filters, joins/relationships between
  data sources, and saved page-level states across every chart on a page.

## Data & performance

- **Tidy and matrix data** — accepts long/tidy and wide/matrix inputs, with grouping,
  transforms, and aggregation handled by the engine.
- **Large datasets** — decimation and bounded measurement keep large scatter and dense charts
  responsive.

## Ecosystem & APIs

- **JavaScript, R, and Python** — the same chart specification works across a browser
  `new CanvasXpress(...)` call, the R htmlwidget, and the Python package.
- **Notebook and framework support** — Jupyter, Dash, Shiny, Streamlit, Flask, Quarto, and
  Observable.
- **Export** — charts export to PNG, SVG, and reproducible JSON/config.

## Reproducibility

- **Round-trip save and load** — a chart's full state serialises to config and reloads to the
  identical view, so figures are reproducible and shareable.
