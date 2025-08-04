# CanvasXpress Graph Type Selection Decision Tree

This decision tree is designed to help users select the appropriate graph type for their data visualization needs based on the dimensionality of the data and the specific goals of the visualization. It provides a structured approach to determine the most suitable graph type, ensuring clarity and effectiveness in data representation.

## Ambiguity Handling
When using the [rules](RULES.md) for generating CanvasXpress JSON configurations, it is crucial to handle ambiguity in the English description of the graph type. The decision tree below outlines how to proceed when the description is not clear or does not specify a particular graph type.
If the English description is ambiguous or does not provide enough information to determine a specific graph type or configuration, follow this decision tree:

1. **Clarify Requirements:** Ask clarifying questions to gather more information about the user's intent and the data being visualized.
2. **Default to Common Cases:** If no additional information can be obtained, default to the most common graph type for the given data dimensionality and context.
3. **Document Assumptions:** Clearly document any assumptions made during the decision-making process to ensure transparency.

Start with data dimensionality:

```
ONE-DIMENSIONAL DATA:
├── Goal: Compare categories/values
│   ├── Few categories
│   │   ├── Standard comparison → Bar
│   │   ├── Emphasis on data points → Lollipop
│   │   ├── Horizontal orientation → Cleveland
│   │   ├── Show change/difference → Dumbbell
│   │   └── Cumulative values → Waterfall
│   └── Many categories
│       ├── Standard comparison → Bar
│       └── Text frequency → WordCloud/TagCloud
│
├── Goal: Show distribution
│   ├── Single variable
│   │   ├── Basic frequency → Histogram
│   │   ├── Smooth density → Density
│   │   ├── Cumulative → CDF
│   │   └── Quantile comparison → QQ
│   └── Multiple groups
│       ├── Box-and-whisker → Boxplot
│       ├── Kernel density → Violin
│       ├── Individual points → Dotplot
│       └── Multiple densities → Ridgeline
│
├── Goal: Show part-to-whole
│   ├── Circular preference
│   │   ├── Standard → Pie
│   │   ├── With center hole → Donut
│   │   └── Hierarchical → Sunburst
│   └── Rectangular preference
│       ├── Hierarchical → Treemap
│       ├── Stacked → Stacked
│       └── Percentage → StackedPercent
│
├── Goal: Show ranking
│   ├── Standard → Bar
│   └── With threshold line → Pareto
│
└── Goal: Show time series
    ├── Standard → Line
    ├── Area under curve → Area
    ├── Stacked areas → Streamgraph
    └── Rank changes over time → Bump

TWO-DIMENSIONAL DATA:
├── Goal: Show correlation/relationship
│   ├── Continuous variables
│   │   ├── Basic scatter → Scatter2D
│   │   ├── With size dimension → ScatterBubble2D
│   │   └── Density of points
│   │       ├── Rectangular bins → Bin/Binplot
│   │       ├── Hexagonal bins → Hex/Hexplot
│   │       └── Contour lines → Contour
│   └── Categorical & continuous
│       ├── Points by category → Scatter2D with colorBy
│       ├── Boxplots by category → Boxplot
│       └── Violins by category → Violin
│
├── Goal: Show time series with multiple variables
│   ├── Standard → Line
│   ├── Connected scatter → Spaghetti
│   └── With confidence bands → Ribbon
│
└── Goal: Compare multiple metrics
    ├── Combined bar & line → BarLine
    ├── Combined area & line → AreaLine
    ├── Combined dot & line → DotLine
    ├── Radar/spider → Radar
    └── Parallel coordinates → ParallelCoordinates

THREE-DIMENSIONAL DATA:
└── 3D relationship → Scatter3D

NETWORK/RELATIONSHIP DATA:
├── Hierarchical
│   ├── Node-link diagram → Tree
│   ├── Space-filling → Treemap
│   └── Radial → Sunburst
├── General network → Network
└── Flow diagram
    ├── Directional flow → Sankey
    ├── Circular flow → Chord
    └── Multi-level flow → Alluvial

GEOGRAPHICAL DATA:
└── Map visualization → Map

SET RELATIONSHIPS:
├── Standard → Venn
└── Complex intersections → Upset

SPECIAL PURPOSE:
├── Correlation matrix → Correlation
├── Volcano plot → Volcano
├── Survival analysis → KaplanMeier
├── Project scheduling → Gantt
├── Circular layout → Circular
├── Measurement gauge → Meter
└── Tornado analysis → Tornado
```