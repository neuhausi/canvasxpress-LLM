# CanvasXpress Parameter Compatibility Matrix

This matrix shows which parameters are compatible with different CanvasXpress graph types, helping to ensure valid configurations.

## Matrix Legend

- ✓ : Parameter is fully compatible and commonly used with this graph type
- ○ : Parameter is compatible but less commonly used or has limited functionality
- ✗ : Parameter is incompatible or not applicable to this graph type

## Core Parameters by Graph Type Category

| Parameter | One-Dimensional<br>(Bar, Boxplot, Pie) | Combined<br>(BarLine, AreaLine) | Multi-Dimensional<br>(Scatter2D, Scatter3D) | Distribution<br>(Histogram, Density) | Network<br>(Network, Tree) | Map<br>(Map) |
|-----------|---------------------------------------|--------------------------------|-------------------------------------------|-------------------------------------|----------------------------|--------------|
| **xAxis** | ✓ | ✓ | ✓ | ✓ | ✗ | ✗ |
| **yAxis** | ✗ | ✓ | ✓ | ○ | ✗ | ✗ |
| **zAxis** | ✗ | ✗ | ○ (Scatter3D only) | ✗ | ✗ | ✗ |
| **xAxis2** | ✗ | ✓ | ✗ | ✗ | ✗ | ✗ |
| **groupingFactors** | ✓ | ✓ | ✓ | ✓ | ✗ | ✗ |
| **colorBy** | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| **shapeBy** | ✗ | ✗ | ✓ | ✗ | ○ | ✗ |
| **sizeBy** | ✗ | ✗ | ✓ | ✗ | ○ | ○ |
| **stackBy** | ○ (Bar, Stacked only) | ○ | ✗ | ✗ | ✗ | ✗ |
| **ridgeBy** | ✗ | ✗ | ○ (Ridgeline only) | ✓ (Ridgeline only) | ✗ | ✗ |
| **segregateSamplesBy** | ✓ | ✓ | ✓ | ✓ | ✗ | ✗ |
| **segregateVariablesBy** | ✓ | ✓ | ✓ | ✓ | ✗ | ✗ |
| **showRegressionFit** | ✗ | ✗ | ✓ (Scatter2D only) | ✗ | ✗ | ✗ |
| **showLoessFit** | ✗ | ✗ | ✓ (Scatter2D only) | ✗ | ✗ | ✗ |
| **transformData** | ✓ | ✓ | ✓ | ✓ | ✗ | ✗ |
| **transposeData** | ✓ | ✓ | ○ | ○ | ✗ | ✗ |
| **samplesClustered** | ✓ | ✓ | ○ | ○ | ✗ | ✗ |
| **variablesClustered** | ✓ | ✓ | ○ | ○ | ✗ | ✗ |
| **showHistogram** | ✗ | ✗ | ✓ | ✓ | ✗ | ✗ |
| **mapId** | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ |

## Detailed Parameter Compatibility by Specific Graph Types

### One-Dimensional Graph Types

| Parameter | Bar | Boxplot | Violin | Pie | Donut | Heatmap | Line |
|-----------|-----|---------|--------|-----|-------|---------|------|
| **graphOrientation** | ✓ | ✓ | ✓ | ✗ | ✗ | ✓ | ✓ |
| **barType** | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| **barZero** | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| **boxplotNotched** | ✗ | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ |
| **boxplotType** | ✗ | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ |
| **boxplotWhiskersType** | ✗ | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ |
| **showBoxplotOriginalData** | ✗ | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ |
| **showViolinBoxplot** | ✗ | ✗ | ✓ | ✗ | ✗ | ✗ | ✗ |
| **violinScale** | ✗ | ✗ | ✓ | ✗ | ✗ | ✗ | ✗ |
| **lineType** | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ |
| **lineErrorType** | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ |
| **circularType** | ✗ | ✗ | ✗ | ✓ | ✓ | ✗ | ✗ |

### Multi-Dimensional Graph Types

| Parameter | Scatter2D | Scatter3D | ScatterBubble2D | Contour | Spaghetti | Streamgraph |
|-----------|-----------|-----------|-----------------|---------|-----------|-------------|
| **scatterType** | ✓ | ✗ | ✓ | ✗ | ✗ | ✗ |
| **showContourDataPoints** | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ |
| **contourFilled** | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ |
| **isContour** | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ |
| **showConfidenceIntervals** | ✓ | ✗ | ✓ | ✗ | ✓ | ✗ |
| **showQuantileRegressionFit** | ✓ | ✗ | ✓ | ✗ | ✗ | ✗ |
| **binplotBinWidth** | ○ | ✗ | ○ | ✗ | ✗ | ✗ |
| **binplotBins** | ○ | ✗ | ○ | ✗ | ✗ | ✗ |
| **binplotShape** | ○ | ✗ | ○ | ✗ | ✗ | ✗ |
| **jitter** | ✓ | ✗ | ✓ | ✗ | ✗ | ✗ |

### Distribution Graph Types

| Parameter | Histogram | Density | Ridgeline | CDF | QQ | Quantile |
|-----------|-----------|---------|-----------|-----|----|----|
| **histogramType** | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ |
| **showFilledHistogramDensity** | ✓ | ✓ | ✓ | ✗ | ✗ | ✗ |
| **showHistogramBars** | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ |
| **showHistogramDensity** | ✓ | ✓ | ✓ | ✗ | ✗ | ✗ |
| **showHistogramMedian** | ✓ | ✓ | ✓ | ✗ | ✗ | ✗ |
| **showHistogramQuantiles** | ✓ | ✓ | ✓ | ✗ | ✗ | ✗ |
| **densityPosition** | ✗ | ✓ | ✓ | ✗ | ✗ | ✗ |

### Network and Hierarchical Graph Types

| Parameter | Network | Tree | Treemap | Sunburst | Chord | Sankey | Alluvial |
|-----------|---------|------|---------|----------|-------|--------|----------|
| **connections** | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| **hierarchy** | ✗ | ✓ | ✓ | ✓ | ✗ | ✗ | ✗ |
| **sankeyAxes** | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✓ |
| **sankeyTextShow** | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✓ |
| **sankeyTitleShow** | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✓ |

### Universal Parameters (Compatible with Most Graph Types)

| Parameter | Compatibility |
|-----------|---------------|
| **title** | ✓ All graph types |
| **subtitle** | ✓ All graph types |
| **colorScheme** | ✓ All graph types |
| **theme** | ✓ All graph types |
| **background** | ✓ All graph types |
| **legendPosition** | ✓ All graph types |
| **legendInside** | ✓ All graph types |
| **showLegend** | ✓ All graph types |
| **legendColumns** | ✓ All graph types |
| **citation** | ✓ All graph types |
| **dataPointSize** | ✓ Most graph types |
| **sortData** | ✓ Most graph types except: Bin, Binplot, CDF, Contour, Density, Hex, Hexplot, Histogram, KaplanMeier, QQ, Quantile, Ridgeline, Scatter2D, ScatterBubble2D, Streamgraph |
| **filterData** | ✓ All data-driven graph types |

## How to Use This Matrix

1. Identify the graph type you're working with
2. Check which parameters are compatible (✓ or ○) with that graph type
3. Avoid using incompatible parameters (✗) in your configuration
4. For parameters marked with ○, use with caution and test the result

This matrix helps ensure that your CanvasXpress configurations use only compatible parameters for the selected graph type, reducing errors and improving visualization quality.
