# CanvasXpress Capabilities

A machine-readable summary of what CanvasXpress can do today, for LLMs and site search.
Every entry below describes a **shipped, publicly available** capability. This file is a
curated source — it is published to `/data/md/CAPABILITIES.md`, linked from `llms.txt`, and
indexed by the site search. Keep it product-accurate; do not add internal, planned, or
deferred work here.

> Extend this file by distilling shipped work: `tools/kb/distill-plan.py <plan> --kind web`
> produces a leak-checked product-narrative draft you can curate into a section below.
> Entries name the config parameters (in `code`) and common alternative terms ("also known
> as") so a search in another product's vocabulary still finds the feature.

## Charting

- **60+ native graph types** from one unified config:
  - **Everyday:** bar, stacked / percent-stacked, line, area, pie, donut, scatter, bubble,
    histogram, waterfall, Pareto, lollipop, dumbbell, Cleveland dot, bump, radar, gantt,
    tornado, word/tag cloud.
  - **Distributions:** boxplot, violin, dotplot, density, ridgeline, CDF, QQ, hexbin / 2D bin,
    contour.
  - **Scientific:** heatmap, correlation matrix, scatter-plot matrix (SPLOM), parallel
    coordinates, volcano, Manhattan, Kaplan-Meier survival, oncoprint, UpSet, Venn, genome
    browser, circular (Circos-style) with ideograms, Visium spatial plots, fish plots.
  - **Flows and hierarchies:** network, Sankey, alluvial, chord, tree, tree bracket, treemap,
    sunburst, streamgraph.
  - **3D:** 3D scatter.
  - **KPI and finance:** meter / gauge and bullet graphs sharing one range/target model;
    OptionsWall (candlesticks plus an options chain on a shared price axis).
- **Grammar-of-graphics rendering** — layered geoms, stats, scales, coordinate systems and
  faceting, so complex multi-panel figures come from a declarative specification.
- **Faceting / small multiples / trellis** — `segregateSamplesBy`, `segregateVariablesBy`,
  `layoutType` (wrap / rows / cols); combination plots share axes across panels.
- **Maps (geographic, choropleth, symbol maps)** — `graphType: "Map"` with TopoJSON / GeoJSON
  (`topoJSON`). Built-in basemaps cover continents, countries, US states and US zip codes
  (`mapId`, `mapZipCodeIds`). Mercator, Albers and orthographic projections
  (`mapProjection`), optional Leaflet tile basemaps, markers, connections between locations, and
  pie charts on regions.
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

## Analytics built into the chart

- **Hierarchical clustering with dendrograms** — `samplesClustered` / `variablesClustered`,
  with euclidean, manhattan or max distance (`clusteringDistance`) and single, complete or
  average linkage (`linkage`). Missing values are imputed by mean or median (`imputeMethod`).
- **K-means clustering** — `samplesKmeaned` / `variablesKmeaned` with a set number of clusters.
- **Regression and fit lines** — linear, exponential, logarithmic, power and polynomial
  (`regressionType`), loess smoothing, quantile regression, confidence intervals
  (`confidenceLevel`) and error ellipses (`ellipseBy`).
- **Statistical summaries** — box/violin statistics, kernel density, histograms, CDF, QQ,
  error bars, correlation matrices, Kaplan-Meier survival curves.
- **Network analysis** — force-directed, circular, radial and constraint-based (cola) layouts
  (`networkLayoutType`); community detection (Louvain) with convex hulls.
- **Data transforms** — log2/log10, exponential, square root, percentile, z-score and ratio
  (`transformData`), applied and undone in the chart.
- **Data wrangling** — a declarative dplyr/tidyr-style pipeline (`dataPipeline`), flexible
  group-by aggregation (`aggregations`), and calculated fields from formulas
  (`calculatedFields`, a safe evaluator with no `eval`).

## Styling and annotation

- **Titles, subtitles and citations** — `title`, `subtitle`, `citation`, each with its own font,
  colour and alignment.
- **Annotations (also known as reference lines, range highlights, shaded bands, callouts)** —
  `decorations` with `line`, `range`, `text`, `point` and `marker` entries drawn in data
  coordinates.
- **20+ themes** — `theme`, including ggplot, bw, minimal, classic, Economist, Wall Street
  Journal, Tableau, Excel, Stata, solarized, dark and high-contrast.
- **Colour** — named colour schemes, gradients, transparency, and colourblind simulation
  (deuteranopia, protanopia) from the menu.
- **Highlight / ghost / focus** — `highlightMode` and `selectionMode` emphasise chosen samples
  and grey out the rest (gghighlight-style), declaratively or by selection.
- **Animations and transitions** — animated first render and transitions between states
  (`transitionType`, `transitionStep`).
- **Responsive sizing** — the `data-responsive` and `data-aspectRatio` canvas attributes let the
  chart follow its container.

## Interactivity

- **Built-in interactivity** — hover tooltips, click/double-click events, zoom, pan, brushing,
  lasso selection, filtering and highlighting without extra code.
- **Live customizer** — an in-chart UI for restyling, reconfiguring, and reshaping data,
  including shelf-style authoring and calculated fields.
- **Data filters** — filter by sample, variable, network node/edge or genome feature
  annotations (`filterSmpBy`, `filterVarBy`, `filterNodeBy`, `filterEdgeBy`, `filterFeatureBy`),
  combined with and/or, hiding or greying out filtered data.
- **Data table view** — the chart's data as a table with search, sorting, pagination, pinned
  columns, per-column width/alignment/format (`dataTable*`).
- **Undo / redo and history** — committed actions (data, config, filters, sorting, clustering,
  transforms) form an undo/redo stack; the steps export as a replayable recipe.
- **Saved states** — named authoring states per chart, and page-level states that save and
  restore every chart on a page together.
- **Natural-language charting** — describe a chart in plain English to generate or modify its
  config, using the built-in service or your own (`llmServiceURL`).
- **Dashboards** — multiple linked charts with shared filters, joins/relationships between
  data sources, and saved page-level states across every chart on a page.

## Accessibility

- **Screen-reader support** — each chart gets a generated text summary (graph type, title,
  axes, series counts and value range) and an off-screen data table, kept in sync as the data
  changes, with live-region announcements.
- **Keyboard** — the chart is focusable, arrow keys move between data points, widgets are
  keyboard-operable, and a visible focus outline is shown.
- **High-contrast theme and reduced motion** — transitions are skipped when the operating
  system requests reduced motion.
- **Conformance report** — WCAG 2.1 AA report (VPAT-style) at `/accessibility.html`.

## Data & performance

- **Tidy and matrix data** — accepts long/tidy and wide/matrix inputs, with grouping,
  transforms, and aggregation handled by the engine.
- **File formats** — JSON, CSV/TSV and other delimited text, Apache Parquet, and GML/GPML
  network files (including WikiPathways GPML).
- **Missing data** — configurable missing-value token, colour and handling in transforms.
- **Large datasets** — decimation and bounded measurement keep large scatter and dense charts
  responsive.

## Ecosystem & APIs

- **JavaScript, R, and Python** — the same chart specification works across a browser
  `new CanvasXpress(...)` call, the R htmlwidget, and the Python package.
- **Notebook and framework support** — Jupyter, Dash, Shiny, Streamlit, Flask, Quarto, and
  Observable.
- **Export** — charts export to PNG (high-resolution via `printMagnification`), SVG, and
  reproducible JSON/config.

## Reproducibility

- **Round-trip save and load** — a chart's full state serialises to config and reloads to the
  identical view, so figures are reproducible and shareable.
