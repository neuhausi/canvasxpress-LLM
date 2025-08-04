# CanvasXpress Parameter Compatibility Matrix

This document reorganizes the parameter information to show which parameters are compatible with each graph type.

## CanvasXpress Key Definitions used in this file
- **All Graphs**: The following are all supported graph types in CanvasXpress: Alluvial, Area, AreaLine, Bar, BarLine, Boxplot, Bin, Binplot, Bubble, Bullet, Bump, CDF, Chord, Circular, Cleveland, Contour, Correlation, Density, Distribution, Donut, DotLine, Dotplot, Dumbbell, Gantt, Heatmap, Hex, Hexplot, Histogram, KaplanMeier, Line, Lollipop, Map, Meter, Network, ParallelCoordinates, Pareto, Pie, QQ, Quantile, Radar, Ribbon, Ridgeline, Sankey, Scatter2D, Scatter3D, ScatterBubble2D, Spaghetti, Stacked, StackedLine, StackedPercent, StackedPercentLine, Streamgraph, Sunburst, TagCloud, TimeSeries, Tornado, Tree, Treemap, Upset, Violin, Volcano, Venn, Waterfall, WordCloud.
- **Single-Dimensional Graphs**: The followings graph types are considered Single-Dimensional because they only need the `xAxis` parameter. No `yAxis` or `zAxis` is allowed: Alluvial, Area, Bar, Boxplot, Bin, Binplot, Bubble, Bullet, CDF, Chord, Circular, Cleveland, Correlation, Density, Distribution, Donut, Dotplot, Dumbbell, Gantt, Heatmap, Hex, Hexplot, Histogram, Line, Lollipop, Meter, ParallelCoordinates, Pie, QQ, Quantile, Radar, Ribbon, Ridgeline, Sankey, Stacked, StackedPercent, TagCloud, Tornado, Tree, Treemap, Violin, Venn, Waterfall, WordCloud.
- **Combined Graphs**: The following graph types are considered Combined because they need both `xAxis` and `xAxis2` parameters. No `yAxis` or `zAxis` is allowed: AreaLine, BarLine, DotLine, Pareto, StackedLine, StackedPercentLine.
- **Multi-Dimensional Graphs**: The following graph types are considered Multi-Dimensional. They need both `xAxis` and `yAxis` parameters. They may have `zAxis`: Bump, Contour, Scatter2D, Scatter3D, ScatterBubble2D, Spaghetti, Streamgraph, Volcano.
- **Three-Dimensional Graphs**: The following graph types are considered Three-Dimensional because they need `xAxis`, `yAxis`, and `zAxis` parameters: ScatterBubble2D, Scatter3D.

## Graph-Specific Parameters
This section lists parameters that are exclusive to or primarily define a particular graph type.

### Area
- areaType

### Bar
- barZero
- stackBy

### Bin, Binplot, Hex, Hexplot
- binplotBinWidth
- binplotBins
- binplotShape

### Boxplot, Violin
- boxplotConnect
- boxplotNotched
- boxplotType
- boxplotWhiskersType
- showBoxplotOriginalData

### Bullet
- bulletTargetVarName

### Circular
- circularType
- rAxis
- rAxisShow
- rAxisTextColor
- rAxisTextFontStyle
- rAxisTextScaleFontFactor
- rAxisTitle
- rAxisTitleColor
- rAxisTitleFontStyle
- rAxisTitleScaleFontFactor
- rAxisTransform
- setMaxR
- setMinR

### Contour
- contourFilled
- showContourDataPoints

### Density
- densityPosition

### Dumbbell
- dumbbellType

### Histogram
- histogramType
- showFilledHistogramDensity
- showHistogram
- showHistogramBars
- showHistogramDensity
- showHistogramMedian
- showHistogramQuantiles

### Line, BarLine, DotLine, StackedLine, StackedPercentLine, Scatter2D
- lineErrorType
- lineType

### Map
- mapColor
- mapConfig
- mapId
- topoJSON
- useLeaflet

### QQ, Quantile, Scatter2D
- showQuantileRegressionFit

### Sankey, Alluvial
- sankeyAxes
- sankeyTextColor
- sankeyTextFontStyle
- sankeyTextScaleFontFactor
- sankeyTextShow
- sankeyTitleColor
- sankeyTitleFontStyle
- sankeyTitleScaleFontFactor
- sankeyTitleShow

### Violin, Boxplot
- showBoxplotIfViolin
- showViolinBoxplot
- showViolinQuantiles
- violinScale
- violinTrim

## General and Shared Parameters
This section lists parameters that are compatible with multiple graph types.

### General
| Parameter Name | Compatible Graph Types |
|----------------|-------------------------|
| dataPointSizeScaleFactor | All Graphs |
| variableSpace | Single-Dimensional Graphs |
| widthFactor | Single-Dimensional Graphs |
| colorScheme | All Graphs |
| background | All Graphs |
| graphType | All Graphs |
| theme | All Graphs |
| graphOrientation | One-dimensional graphs |
| view | All Graphs |
| binned | Dotplot, DotLine, Boxplot, Violin |
| jitter | Dotplot, DotLine, Boxplot, Violin |
| objectBorderColor | One-dimensional graphs |

### Metadata
| Parameter Name | Compatible Graph Types |
|----------------|-------------------------|
| showConfidenceIntervals | Regression, Scatter2D |
| decorations | All Graphs |
| showLoessFit | Scatter2D |
| smpOverlays | Single-Dimensional Graphs |
| varOverlays | Heatmap |
| regressionType | Regression, Scatter2D |
| showRegressionFit | Regression, Scatter2D |

### Data
| Parameter Name | Compatible Graph Types |
|----------------|-------------------------|
| samplesClustered | Single-Dimensional Graphs |
| samplesKmeaned | Single-Dimensional Graphs |
| variablesClustered | Heatmap |
| variablesKmeaned | Heatmap |
| groupingFactors | Single-Dimensional Graphs|
| stringSampleFactors | All Graphs |
| stringVariableFactors | All Graphs |
| segregateSamplesBy | All Graphs |
| segregateVariablesBy | All Graphs |
| splitSamplesBy | All Graphs |
| splitVariablesBy | All Graphs |
| filterData | All Graphs |
| colorBy | All Graphs |
| pieBy | Pie |
| pivotBy | Single-Dimensional Graphs|
| ridgeBy | Ridgeline, Scatter2D |
| shapeBy | All Graphs |
| sizeBy | All Graphs |
| selectedDataPoints | All Graphs |
| sortData | Single-Dimensional Graphs|
| transformData | All Graphs |
| hierarchy | Trees, Bubble |

### Legend, Titles, Samples & Variables
| Parameter Name | Compatible Graph Types |
|----------------|-------------------------|
| legendColumns | All Graphs |
| legendInside | All Graphs |
| legendPosition | All Graphs |
| showLegend | All Graphs |
| subtitle | All Graphs |
| subtitleColor | All Graphs |
| subtitleFontStyle | All Graphs |
| subtitleScaleFontFactor | All Graphs |
| title | All Graphs |
| titleColor | All Graphs |
| titleFontStyle | All Graphs |
| titleScaleFontFactor | All Graphs |
| citation | All Graphs |
| citationColor | All Graphs |
| citationFontStyle | All Graphs |
| citationScaleFontFactor | All Graphs |
| highlightSmp | Single-Dimensional Graphs |
| showSampleNames | Single-Dimensional Graphs |
| smpTextColor | Single-Dimensional Graphs |
| smpTextFontStyle | Single-Dimensional Graphs |
| smpTextRotate | Single-Dimensional Graphs |
| smpTextScaleFontFactor | Single-Dimensional Graphs |
| smpTitle | Single-Dimensional Graphs |
| smpTitleColor | Single-Dimensional Graphs |
| smpTitleFontStyle | Single-Dimensional Graphs |
| smpTitleRotate | Single-Dimensional Graphs |
| smpTitleScaleFontFactor | Single-Dimensional Graphs |
| highlightVar | Heatmap |
| showVariableNames | Heatmap |
| varTextColor | Heatmap |
| varTextFontStyle | Heatmap |
| varTextRotate | Heatmap |
| varTextScaleFontFactor | Heatmap |
| varTitle | Heatmap |
| varTitleColor | Heatmap |
| varTitleFontStyle | Heatmap |
| varTitleScaleFontFactor | Heatmap |

### Axes
| Parameter Name | Compatible Graph Types |
|----------------|-------------------------|
| setMaxX | All Graphs |
| setMinX | All Graphs |
| xAxis | All Graphs |
| xAxis2 | Combined Graphs |
| xAxis2Show | Combined Graphs |
| xAxis2Title | Combined Graphs |
| xAxisShow | All Graphs |
| xAxisTextColor | All Graphs |
| xAxisTextScaleFontFactor | All Graphs |
| xAxisTitle | All Graphs |
| xAxisTitleColor | All Graphs |
| xAxisTitleFontStyle | All Graphs |
| xAxisTitleScaleFontFactor | All Graphs |
| xAxisTransform | All Graphs |
| setMaxY | Multi-Dimensional Graphs |
| setMinY | Multi-Dimensional Graphs |
| yAxis | Multi-Dimensional Graphs |
| yAxisShow | Multi-Dimensional Graphs |
| yAxisTextColor | Multi-Dimensional Graphs |
| yAxisTextFontStyle | Multi-Dimensional Graphs |
| yAxisTextScaleFontFactor | Multi-Dimensional Graphs |
| yAxisTitle | Multi-Dimensional Graphs |
| yAxisTitleColor | Multi-Dimensional Graphs |
| yAxisTitleFontStyle | Multi-Dimensional Graphs |
| yAxisTitleScaleFontFactor | Multi-Dimensional Graphs |
| yAxisTransform | Multi-Dimensional Graphs |
| setMaxZ | Three-Dimensional Graphs |
| setMinZ | Three-Dimensional Graphs |
| zAxis | Three-Dimensional Graphs |
| zAxisShow | Three-Dimensional Graphs |
| zAxisTextColor | Three-Dimensional Graphs |
| zAxisTextFontStyle | Three-Dimensional Graphs |
| zAxisTextScaleFontFactor | Three-Dimensional Graphs |
| zAxisTitle | Three-Dimensional Graphs |
| zAxisTitleColor | Three-Dimensional Graphs |
| zAxisTitleFontStyle | Three-Dimensional Graphs |
| zAxisTitleScaleFontFactor | Three-Dimensional Graphs |
| zAxisTransform | Three-Dimensional Graphs |

