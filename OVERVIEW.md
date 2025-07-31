# CanvasXpress Overview

CanvasXpress was designed as a powerful visualization tool for bioinformatics and systems biology analysis. It offers extensive support for a wide range of visualizations, making it ideal for presenting both scientific and non-scientific data with clarity and precision. The library delivers exceptional performance, capable of effortlessly plotting millions of data points with ease.

# Creating a CanvasXpress Visualization

To integrate CanvasXpress into a webpage, simply include the required CSS and JavaScript files. These can be found at the following URLs: https://www.canvasxpress.org/dist/canvasXpress.css for the CSS file and https://www.canvasxpress.org/dist/canvasXpress.min.js for the JavaScript file. To create the display area for your visualization, insert a `<canvas>` element within the `<body>` section of your HTML. Be sure to specify clear width and height dimensions for the canvas to ensure proper rendering. Finally, include the necessary script to initialize the CanvasXpress visualization.

Here is an example:

```html
<html>
  <head>
    <!-- 1. Include the CanvasXpress library -->
    <link rel="stylesheet" href="https://www.canvasxpress.org/dist/canvasXpress.css" type="text/css"/>
    <script type="text/javascript" src="https://www.canvasxpress.org/dist/canvasXpress.min.js"></script>
  </head>
  <body>
    <!-- 2. DOM element where the visualization will be displayed -->
    <canvas  id="canvasId" width="540" height="540"></canvas>
    <!-- 3. Include script to initialize object -->
    <script>
      // Data as 2-dimensional array
      // The first row contains the column names, and the first column contains the row names.
      // The rest of the data is numerical / categorical values.
      var data = [
        ["Id", "Smp1", "Smp2", "Smp3"],
        ["Gene1", 10, 35, 88]
      ];
      // Configuration
      var conf = {
        "graphType": "Bar"
      };
      // Initialize object
      var cX = new CanvasXpress("canvasId", data, conf);
    </script>
  </body>
</html>
```

The canvasXpress object is created using the new constructor function. This function can be called in one of two ways: by passing four separate arguments—targetId, data, configuration, and events—or by providing a single JSON object that encapsulates these four parameters.

```javascript
var cX = new CanvasXpress(targetId, data, config, events);
//  or:
var cX = new CanvasXpress({
  "renderTo": targetId,
  "data": data,
  "config": config,
  "events": events
});
```

- *targetId*:
specifies the DOM ID of the `<canvas>` element within the `<body>` of the webpage where the graph will be rendered.

- *data*:
can be either a JSON object or a URL linking to a file (JSON or text-delimited) containing the necessary data for the graph.

- *config*:
is a JSON object that allows you to customize the graph with a wide range of properties, enabling you to tailor the visualization to your specific requirements. Not all parameters are applicable to every graph type, so it is essential to refer to the documentation for the specific graph type you are using.

- *events*:
is an optional JSON object that allows users to define custom mouse event behaviors, enabling enhanced interactivity. However, this topic will not be discussed further here.

## Data Format:

In CanvasXpress, the most straightforward data format for plotting is a dataframe, organized by columns. This structure arranges cases (rows or variables), each containing a series of observations or measurements (columns or samples). In plain JavaScript, this format is represented as a two-dimensional array and serves as the preferred method for passing data to CanvasXpress. The data should be structured as follows:

```javascript
[
  ["Variable", "Sample1", "Sample2", "Sample3", "Pathway" ],
  ["Variable1", 10, 20, 30, "P1"],
  ["Variable2", 35, 25, 15, "P2"],
  ["Variable3", 13, 10, 42, "P1"]
]
```

To enhance performance and organization, the data can be structured into three distinct dataframes. The first, named "y", contains numerical data formatted as a two-dimensional array, accompanied by two vectors that define the row and column names. The second dataframe, "x", stores column or sample metadata. This metadata is arranged as key-value pairs, where each key represents a metadata field, and the corresponding value is a vector containing the related data. The third dataframe, "z", functions similarly but holds metadata for rows or variables instead. This streamlined approach improves efficiency, clarity, and overall data management.
Here is an example: of such data:

```javascript
{
  "y": {
    "vars": [ "Variable1", "Variable2" ],
    "smps": [ "Sample1", "Sample2", "Sample3" ],
    "data": [ [ 10, 20, 30 ],
              [ 35, 25, 15 ] ]
  },
  "x": {
    "Tissue": [ "Kidney", "Lung", "Heart" ],
    "Donor": [ "D1", "D1", "D2" ]
  },
  "z": {
    "Symbol": [ "AAA", "BBB" ],
    "Pathway": [ "P1", "P2" ]
  }
}
```

## Graph Types:

The graph type to be plotted is defined in the configuration using the graphType parameter.

CanvasXpress graphs are organized by their dimensions, each serving a specific purpose. One-dimensional graphs pair a categorical variable with a numerical one, while two-dimensional graphs illustrate the relationship between two numerical variables. Three-dimensional graphs take it further, showcasing interactions among three numerical variables.

Beyond these core types, CanvasXpress offers specialized graphs, including heatmaps, correlation plots, maps, networks, oncoprints, SPLOM, tag clouds, and Venn diagrams. Additionally, hierarchical visualizations, such as packing bubbles, Sankey plots, tree maps, trees, and sunburst charts, which provide unique insights into complex data structures are also available in CanvasXpress.

One-dimensional graphs come in many styles, each designed to suit specific visualization needs. Common types include area charts, bar graphs, boxplots, bullet charts, donut plots, dot plots, dumbbell plots, line graphs, lollipop charts, parallel coordinate plots, pie charts, radar plots, stacked charts, violin plots, waterfall charts, and even hybrid combinations of these styles. When creating violin plots or boxplots, it is essential to include a groupingFactors parameter with categorical variable(s) to ensure accurate grouping and representation.

Two-dimensional plots, commonly beginning as scatter plots, can transform into various visual formats depending on the data and purpose. Examples include line graphs, area charts, ribbon visuals, and stream plots—ideal for showcasing time series data. Additionally, variations like bin plots or hex plots are effective for analyzing relationships between two numerical values. Likewise, a single column from a dataset can be transformed into various visualizations, including histograms, density plots, contour plots, or ridgeline charts. These versatile tools offer dynamic ways to analyze and present data effectively. Similarly, three-dimensional plots begin as scatter plots but can also be adapted into contour diagrams.

## Axes:

CanvasXpress simplifies data visualization by automatically identifying the data to be plotted. However, you have complete control to customize your charts.

- For one-dimensional plots, which lack a y-axis regardless of orientation, you can use the xAxis parameter to define the data to be plotted.

- For combined graphs, you can take customization further by specifying both a primary x-axis and a secondary x-axis (xAxis2), allowing for greater flexibility and precision in your visualizations.

- In two-dimensional plots, you can define both axes by using the xAxis and yAxis parameters.

- For three-dimensional plots, the xAxis, yAxis, and zAxis parameters let you specify data for all three axes, providing a comprehensive framework for intricate data representation.

## Maps:

CanvasXpress provides comprehensive mapping capabilities, supporting a wide variety of maps, including world maps, continent maps, country maps, U.S. state maps, and even custom maps. To create a map, you can either upload a topoJSON file or use a valid map identifier string. Examples of map identifiers include: "World," "Africa," "Asia," "Europe," "NorthAmerica," "SouthAmerica," "Oceania," "USACounties," "USAStates," and "WorldContinents," among others. You can also use a three-letter country code (e.g., "USA," "CAN," "MEX," "ARG") or a two-letter U.S. state code, or simply provide the name of a country or U.S. state.

To get started, assign your selected identifier to the mapId parameter. If you'd like to enrich your map with additional data, you can supply the relevant details using the data parameter. CanvasXpress automatically maps your provided IDs to the corresponding geographic elements, making the process efficient and hassle-free.

## Data Filtering:

Data filtering is an important aspect of data visualization, allowing you to focus on specific subsets of your data. CanvasXpress provides a single parameter, filterData, to enable data filtering. The parameter accepts an array that specifies the filtering criteria. This array should contain four elements:

- The first element is a string that indentify the location of the data to be filtered, such as "var" for the variables, "smp" for the samples, "x" for sample metadata, or "z" for variable metadata, etc. It can also be "guess" to automatically determine the data type based on the provided data structure.

- The second element is a string that specifies the column / row name to be used for filtering.

- The third element is a string that defines the filter condition, such as "=", ">=", "<=", "like", "different", etc.

- The fourth element is the value to be used in the filter condition.

For example, to filter the data to include only rows where the value in the "Pathway" column equals "P1", you would use the following configuration:

```javascript

  "filterData": [
    [
      "guess",
      "Pathway",
      "equals",
      "P1"
    ]
  ]

```
## Data Sorting:

Data sorting is a crucial step in data visualization, allowing you to organize your data in a meaningful way. CanvasXpress provides a single parameter, sortData, to enable data sorting. The sortData parameter accepts an array that specifies the sorting criteria. Each element in the array defines how the data should be sorted.

- The first element is a string that indicates the location of the data to be sorted, such as "var" for variables, "smp" for samples, or "cat" for categories of either samples or variables.

- The second element is a string that specifies the index to be sorted by, such as "smp" for sample names or "var" for variable names.

- The third element is a string that identifies the specific column or row name to be used for sorting.

For example, to sort the data by the "Factor1" column, and then by the "Factor2" column, you would use the following configuration:

```javascript

  "sortData": [
    [
      "cat",
      "smp",
      "Factor1"
    ],
    [
      "cat",
      "smp",
      "Factor2"
    ]
  ]
```

## Data Wrangling:

Data wrangling is a crucial step in preparing your data for visualization. CanvasXpress offers a range of functions that are mapped to parameters to help you manipulate and transform your data effectively. These functions include:

- Grouping: Combine data based on specific criteria to create meaningful categories. The groupingFactors parameter allows you to specify the variables used for grouping.

- Faceting: Create multiple subplots based on a categorical variable, enabling you to visualize data across different groups. Use the parameter segregateSamplesBy to create subplot by columns in the data or/and segregateVariablesBy to create subplot by rows in the data.

- Transformation: Apply mathematical transformations to your data, such as logarithmic or square root transformations, to enhance visualization. The transformData parameter allows you to specify the type of transformation.

- Transposition: Rearrange your data by swapping rows and columns to better suit your visualization needs. The transposeData parameter enables you to transpose the data.

- Pivoting: Reshape your data by converting rows into columns or vice versa, allowing for more flexible data representation. The pivotBy parameter accept a column name to pivot the data.

- Clustering: Create a side dendrogram to visualize the hierarchical relationships between variables or samples. Use the samplesClustered and variablesClustered parameters to enable clustering for samples and variables, respectively.

- Histogramming: Generate histograms to visualize the distribution of numerical data. The showHistogram parameter allows you to create histograms for your data.

## Line Fitting:

Line fitting is an essential technique for identifying trends and patterns in your data. CanvasXpress provides several parameters to facilitate line fitting, including:

- showRegressionFit: This parameter enables the display of a regression line on your scatter plot, helping to visualize the relationship between variables.

- showLoessFit: Use this parameter to display a lowess fit line, which is particularly useful for capturing non-linear relationships in your data.

## Decorations:

CanvasXpress offers a decoration parameter to enhance the visual appeal and clarity of your graphs. These include: lines, shapes, text annotations, etc. Each decoration type can be customized with various properties such as color, size, and position, etc. The parameter takes an object with the following structure:

```javascript
  "decorations": {
    "type1": [
      {
        "property1": "value1",
        "property2": "value2"
      }
    ],
    "type2": [
      {
        "property1": "value1",
        "property2": "value2"
      }
    ]
  }
```

The "type1" and "type2" can be any of the supported decoration types, such as "line", "shape", "text", etc. Each decoration type can have multiple instances, each defined by an object with its specific properties. The properties of each decoration type vary based on the type itself. Of the supported decoration types, the "line" type is commonly used to draw horizontal or vertical lines across the graph. There is an important distiction when specifying the positions in one dimensional graphs and multi-dimensional graphs. In one-dimensional graphs, the position is specified using the parameter "value" independently of the orientation of the graph, while in multi-dimensional graphs, the position is specified using an "x" parameter and a "y" parameter.

Here is an example of how to use the decorations parameter to add a horizontal line at 20 in a one-dimensional graph:

```javascript
  "decorations": {
    "line": [
      {
        "color": "black",
        "value": 20
      }
    ]
  }
```

Here is an example of how to use the decorations parameter to add a horizontal line at y = 20 in a two-dimensional graph:

```javascript
  "decorations": {
    "line": [
      {
        "color": "black",
        "y": 20
      }
    ]
  }
```

## Data Sets

This dataset contains 17 rows and 30 columns, arranged in a clear, structured format. The first row serves as the column header, while the first column functions as the row identifier. The remaining columns include a mix of numerical values and categorical data. Presented as a two-dimensional array, each inner array represents an individual row of the dataset. Throughout the examples below, we will refer to this dataset using the variable name "data".

```javascript
[
  ["Id", "Col1", "Col2", "Col3", "Col4", "CI-Lower", "CI-Higher", "YearFact", "NumFact", "SeqD", "R50", "R75", "R100", "Neg", "Diff", "FC", "LOD", "Year", "Time", "Survival", "Start", "End", "Set", "Group", "Type", "Category", "Final", "8th", "4th", "Semifinal"],
  ["Row00",  5, 80, 30,  2,  4,  7, 2019, 4,  0.5, 50, 75, 100, -10, 120,  1.5, 1.2, 1980,  5, 1, 20140221, 20140520, "Set1", "GroupA", "TypeX", "Cat1", "I", "A", "A", "A"],
  ["Row01", 10, 25, 32,  4,  7, 12, 2020, 1,  1.5, 50, 75, 100,  -5, -20,  0.1, 0.5, 1981,  5, 1, 20140521, 20140820, "Set2", "GroupA", "TypeX", "Cat1", "I", "A", "A", "A"],
  ["Row02", 85, 67, 55,  1, 81, 89, 2021, 2,  2.5, 50, 75, 100, -30,  40,  1.0, 1.0, 1982,  8, 1, 20140821, 20141120, "Set1", "GroupB", "TypeY", "Cat1", "I", "C", "A", "A"],
  ["Row03", 22, 45, 65,  5, 19, 24, 2022, 3,  3.5, 50, 75, 100, -20,  60,  0.6, 0.8, 1983,  8, 1, 20141121, 20150220, "Set1", "GroupA", "TypeZ", "Cat1", "I", "C", "A", "A"],
  ["Row04", 45, 30, 38, 10, 40, 47, 2019, 3,  4.5, 50, 75, 100, -15, -30,  1.8, 2.3, 1984, 12, 1, 20150221, 20150520, "Set2", "GroupC", "TypeX", "Cat2", "I", "E", "G", "A"],
  ["Row05", 60, 15, 12,  3, 58, 63, 2020, 2,  5.5, 50, 75, 100, -25, -30,  4.1, 1.9, 1985, 16, 0, 20150521, 20150820, "Set1", "GroupB", "TypeY", "Cat2", "I", "E", "G", "A"],
  ["Row06", 75, 80, 90,  3, 73, 77, 2021, 1,  6.5, 50, 75, 100, -35,  20,  1.6, 3.1, 1986, 23, 1, 20150821, 20151120, "Set1", "GroupA", "TypeZ", "Cat2", "I", "G", "G", "A"],
  ["Row07", 33, 28, 15, 12, 30, 36, 2022, 4,  7.5, 50, 75, 100, -40,  15,  2.0, 1.5, 1987, 27, 1, 20151121, 20160220, "Set2", "GroupC", "TypeY", "Cat2", "I", "G", "G", "A"],
  ["Row08", 58, 44, 22,  6, 52, 62, 2019, 3,  8.5, 50, 75, 100, -50,  20, -2.1, 2.1, 1988, 30, 1, 20160221, 20160520, "Set1", "GroupB", "TypeX", "Cat3", "I", "I", "I", "I"],
  ["Row09", 92, 76, 55,  6, 89, 95, 2020, 4,  9.5, 50, 75, 100, -60, -20, -0.3, 0.8, 1989, 33, 1, 20160521, 20160820, "Set2", "GroupA", "TypeZ", "Cat3", "I", "I", "I", "I"],
  ["Row10", 17, 39, 61, 14, 13, 22, 2021, 1, 10.5, 50, 75, 100, -22,  40, -0.1, 0.2, 1990, 43, 1, 20160821, 20161120, "Set2", "GroupC", "TypeX", "Cat3", "I", "K", "I", "I"],
  ["Row11", 41, 53, 77,  9, 39, 55, 2022, 2, 11.5, 50, 75, 100, -12,  50,  0.0, 0.0, 1991, 45, 1, 20171121, 20180220, "Set2", "GroupB", "TypeY", "Cat3", "I", "K", "I", "I"],
  ["Row12", 66, 79, 93,  5, 61, 70, 2019, 1, 12.5, 50, 75, 100,  -8, -20, -0.2, 0.0, 1992, 46, 1, 20180221, 20180520, "Set1", "GroupA", "TypeX", "Cat4", "I", "N", "N", "I"],
  ["Row13", 81, 94, 29,  8, 75, 82, 2020, 3, 13.5, 50, 75, 100, -18,  30, -3.5, 2.1, 1993, 47, 0, 20180521, 20180820, "Set1", "GroupC", "TypeZ", "Cat4", "I", "N", "N", "I"],
  ["Row14", 96, 81, 46, 11, 91, 98, 2021, 4, 14.5, 50, 75, 100, -28, -40, -2.1, 2.5, 1994, 48, 1, 20180821, 20181120, "Set2", "GroupB", "TypeY", "Cat4", "I", "O", "N", "I"],
  ["Row15", 12, 27, 55, 12, 10, 15, 2022, 2, 15.5, 50, 75, 100, -38,   0, -0.6, 1.1, 1995, 49, 1, 20190221, 20190220, "Set2", "GroupA", "TypeZ", "Cat4", "I", "O", "N", "I"]
]
```

This is a dataset with 5 rows and 5 columns, arranged in a clear, structured format. The first row serves as the column header, while the first column functions as the row identifier. The remaining columns are numerical values to produce chord diagrams. This dataset will be refrered with the variable name "chord" in the examples below.

```javascript
[
  ["Id", "A", "B", "C", "D"],
  ["A", 11975,  5871, 8916, 2868],
  ["B",  1951, 10048, 2060, 6171],
  ["C",  8010, 16145, 8090, 8045],
  ["D",  1013,   990,  940, 6907]
]
```

This is a dataset with 16 rows and 2 columns, arranged in a clear, structured format. The first row serves as the column header, while the first column functions as the row identifier and the second columns are numerical values to produce venn diagrams. This dataset will be refrered with the variable name "venn" in the examples below.

```javascript
[
  ["Id", "Value"],
  ["A",    340],
  ["AB",   639],
  ["ABC",  552],
  ["ABCD", 148],
  ["ABD",  578],
  ["AC",   456],
  ["ACD",  298],
  ["AD",   257],
  ["B",    562],
  ["BC",   915],
  ["BCD",  613],
  ["BD",   354],
  ["C",    620],
  ["CD",   143],
  ["D",    592]
]
```

This is a dataset with 34 nodes and 78 edges. This dataset will be refrered with the variable name "network" in the examples below.

```javascript
{
  "edges": [
    { "id1": "n2", "id2": "n1" },
    { "id1": "n3", "id2": "n1" },
    { "id1": "n3", "id2": "n2" },
    { "id1": "n4", "id2": "n1" },
    { "id1": "n4", "id2": "n2" },
    { "id1": "n4", "id2": "n3" },
    { "id1": "n5", "id2": "n1" },
    { "id1": "n6", "id2": "n1" },
    { "id1": "n7", "id2": "n1" },
    { "id1": "n7", "id2": "n5" },
    { "id1": "n7", "id2": "n6" },
    { "id1": "n8", "id2": "n1" },
    { "id1": "n8", "id2": "n2" },
    { "id1": "n8", "id2": "n3" },
    { "id1": "n8", "id2": "n4" },
    { "id1": "n9", "id2": "n1" },
    { "id1": "n9", "id2": "n3" },
    { "id1": "n10", "id2": "n3" },
    { "id1": "n11", "id2": "n1" },
    { "id1": "n11", "id2": "n5" },
    { "id1": "n11", "id2": "n6" },
    { "id1": "n12", "id2": "n1" },
    { "id1": "n13", "id2": "n1" },
    { "id1": "n13", "id2": "n4" },
    { "id1": "n14", "id2": "n1" },
    { "id1": "n14", "id2": "n2" },
    { "id1": "n14", "id2": "n3" },
    { "id1": "n14", "id2": "n4" },
    { "id1": "n17", "id2": "n6" },
    { "id1": "n17", "id2": "n7" },
    { "id1": "n18", "id2": "n1" },
    { "id1": "n18", "id2": "n2" },
    { "id1": "n20", "id2": "n1" },
    { "id1": "n20", "id2": "n2" },
    { "id1": "n22", "id2": "n1" },
    { "id1": "n22", "id2": "n2" },
    { "id1": "n26", "id2": "n24" },
    { "id1": "n26", "id2": "n25" },
    { "id1": "n28", "id2": "n3" },
    { "id1": "n28", "id2": "n24" },
    { "id1": "n28", "id2": "n25" },
    { "id1": "n29", "id2": "n3" },
    { "id1": "n30", "id2": "n24" },
    { "id1": "n30", "id2": "n27" },
    { "id1": "n31", "id2": "n2" },
    { "id1": "n31", "id2": "n9" },
    { "id1": "n32", "id2": "n1" },
    { "id1": "n32", "id2": "n25" },
    { "id1": "n32", "id2": "n26" },
    { "id1": "n32", "id2": "n29" },
    { "id1": "n33", "id2": "n3" },
    { "id1": "n33", "id2": "n9" },
    { "id1": "n33", "id2": "n15" },
    { "id1": "n33", "id2": "n16" },
    { "id1": "n33", "id2": "n19" },
    { "id1": "n33", "id2": "n21" },
    { "id1": "n33", "id2": "n23" },
    { "id1": "n33", "id2": "n24" },
    { "id1": "n33", "id2": "n30" },
    { "id1": "n33", "id2": "n31" },
    { "id1": "n33", "id2": "n32" },
    { "id1": "n34", "id2": "n9" },
    { "id1": "n34", "id2": "n10" },
    { "id1": "n34", "id2": "n14" },
    { "id1": "n34", "id2": "n15" },
    { "id1": "n34", "id2": "n16" },
    { "id1": "n34", "id2": "n19" },
    { "id1": "n34", "id2": "n20" },
    { "id1": "n34", "id2": "n21" },
    { "id1": "n34", "id2": "n23" },
    { "id1": "n34", "id2": "n24" },
    { "id1": "n34", "id2": "n27" },
    { "id1": "n34", "id2": "n28" },
    { "id1": "n34", "id2": "n29" },
    { "id1": "n34", "id2": "n30" },
    { "id1": "n34", "id2": "n31" },
    { "id1": "n34", "id2": "n32" },
    { "id1": "n34", "id2": "n33" }
  ],
  "nodes": [
    { "color": "#0ab0db", "id": "n1" },
    { "color": "#0ab0db", "id": "n2" },
    { "color": "#0ab0db", "id": "n3" },
    { "color": "#0ab0db", "id": "n4" },
    { "color": "#0ab0db", "id": "n5" },
    { "color": "#0ab0db", "id": "n6" },
    { "color": "#0ab0db", "id": "n7" },
    { "color": "#0ab0db", "id": "n8" },
    { "color": "#0ab0db", "id": "n9" },
    { "color": "#0ab0db", "id": "n10" },
    { "color": "#0ab0db", "id": "n11" },
    { "color": "#0ab0db", "id": "n12" },
    { "color": "#0ab0db", "id": "n13" },
    { "color": "#0ab0db", "id": "n14" },
    { "color": "#0ab0db", "id": "n15" },
    { "color": "#0ab0db", "id": "n16" },
    { "color": "#0ab0db", "id": "n17" },
    { "color": "#0ab0db", "id": "n18" },
    { "color": "#0ab0db", "id": "n19" },
    { "color": "#0ab0db", "id": "n20" },
    { "color": "#0ab0db", "id": "n21" },
    { "color": "#0ab0db", "id": "n22" },
    { "color": "#0ab0db", "id": "n23" },
    { "color": "#0ab0db", "id": "n24" },
    { "color": "#0ab0db", "id": "n25" },
    { "color": "#0ab0db", "id": "n26" },
    { "color": "#0ab0db", "id": "n27" },
    { "color": "#0ab0db", "id": "n28" },
    { "color": "#0ab0db", "id": "n29" },
    { "color": "#0ab0db", "id": "n30" },
    { "color": "#0ab0db", "id": "n31" },
    { "color": "#0ab0db", "id": "n32" },
    { "color": "#0ab0db", "id": "n33" },
    { "color": "#0ab0db", "id": "n34" }
  ]
}
```

## Examples

This are minimal examples of how to use CanvasXpress with the datase above. You can see these examples [here](https://www.canvasxpress.org/minimalExamples.html). You can find more examples in the [CanvasXpress Website](https://www.canvasxpress.org/). You can add additional parameters to the configuration object to customize the graphs further.

# Alluvial

```javascript
new CanvasXpress("Alluvial", data, {
  "graphType": "Alluvial",
  "xAxis": ["Col1"],
  "sankeyAxes": ["Type", "Group", "Category"]
});
```

# Area

```javascript
new CanvasXpress("Area", data, {
  "graphType": "Area",
  "xAxis": ["Col1", "Col2", "Col3"]
});
```

# Area Stacked

```javascript
new CanvasXpress("AreaS", data, {
  "graphType": "Area",
  "xAxis": ["Col1", "Col2", "Col3"],
  "areaType": "stacked"
});
```

# Area Percent

```javascript
new CanvasXpress("AreaP", data, {
  "graphType": "Area",
  "xAxis": ["Col1", "Col2", "Col3"],
  "areaType": "percent"
});
```

# AreaLine

```javascript
new CanvasXpress("AreaLine", data, {
  "graphType": "AreaLine",
  "xAxis": ["Col1"],
  "xAxis2": ["Col2"]
});
```

# Bar

```javascript
new CanvasXpress("Bar", data, {
  "graphType": "Bar",
  "xAxis": ["Col1"]
});
```

# BarLine

```javascript
new CanvasXpress("BarLine", data, {
  "graphType": "BarLine",
  "xAxis": ["Col1"],
  "xAxis2": ["Col2"]
});
```

# Boxplot

```javascript
new CanvasXpress("Boxplot", data, {
  "graphType": "Boxplot",
  "xAxis": ["Col4"],
  "groupingFactors": ["Group"]
});
```

# Bin

```javascript
new CanvasXpress("Bin", data, {
  "graphType": "Bin",
  "xAxis": ["Col3"],
});
```

# Binplot

```javascript
new CanvasXpress("Binplot", data, {
  "graphType": "Bin",
  "xAxis": ["Col3"],
});
```

# Bubble

```javascript
new CanvasXpress("Bubble", data, {
  "graphType": "Bubble",
  "xAxis": ["Col1"],
  "hierarchy": ["Group", "Type"],
});
```

# Bullet

```javascript
new CanvasXpress("Bullet", data, {
  "graphType": "Bullet",
  "xAxis": ["Col1"],
  "bulletTargetVarName": "Col2",
  "rangeStack": ["R50", "R75", "R100"]
});
```

# Bump

```javascript
new CanvasXpress("Bump", data, {
  "graphType": "Bump",
  "xAxis": ["YearFact"],
  "yAxis": ["NumFact"],
  "lineBy": "Category",
});
```

# CDF

```javascript
new CanvasXpress("CDF", data, {
  "graphType": "CDF",
  "xAxis": ["Col2"]
});
```

# Chord

```javascript
new CanvasXpress("Chord", chord, {
  "graphType": "Chord",
  "xAxis": ["A", "B", "C", "D"]
});
```

# Circular

```javascript
new CanvasXpress("Circular", data, {
  "graphType": "Circular",
  "xAxis": ["Col1", "Col2", "Col3"]
});
```

# Circular2D

```javascript
new CanvasXpress("Circular2D", data, {
  "graphType": "Circular",
  "rAxis" : "SeqD",
  "ringTracks": ["", "A", "B", "B"],
  "xAxis": ["SeqD", "Col1", "Col2", "Col3"]
});
```

# Circular Connected

```javascript
new CanvasXpress("CircularConn", data, {
  "graphType": "Circular",
  "xAxis": ["Col1", "Col2", "Col3"],
  "connections": [["rgb(0,0,255)", "Row01", "Row06"], ["rgb(0,255,0)", "Row03", "Row14"], ["rgb(255,0,0)", "Row05", "Row10"]]
});
```

# Cleveland

```javascript
new CanvasXpress("Cleveland", data, {
  "graphType": "Cleveland",
  "xAxis": ["Col1", "Col2"]
});
```

# Contour

```javascript
new CanvasXpress("Contour", data, {
  "graphType": "Contour",
  "xAxis": ["Col1"],
  "yAxis": ["Col2"]
});
```

# Correlation

```javascript
new CanvasXpress("Correlation", data, {
  "graphType": "Correlation",
  "xAxis": ["Col1", "Col2", "Col3", "YearFact", "NumFact"]
});
```

# Density

```javascript
new CanvasXpress("Density", data, {
  "graphType": "Density",
  "xAxis": ["Col2"]
});
```

# Distribution

```javascript
new CanvasXpress("Distribution", data, {
  "graphType": "Distribution",
  "xAxis": ["Col1"]
});
```

# Dumbbell

```javascript
new CanvasXpress("Dumbbell", data, {
  "graphType": "Dumbbell",
  "xAxis": ["Col1", "Col2"]
});
```

# Donut

```javascript
new CanvasXpress("Donut", data, {
  "graphType": "Donut",
  "xAxis": ["Col1"]
});
```

# DotLine

```javascript
new CanvasXpress("DotLine", data, {
  "graphType": "DotLine",
  "xAxis": ["Col1"],
  "xAxis2": ["Col2"]
});
```

# Dotplot

```javascript
new CanvasXpress("Dotplot", data, {
  "graphType": "Dotplot",
  "xAxis": ["Col1"]
});
```

# Gantt

```javascript
new CanvasXpress("Gantt", data, {
  "graphType": "Gantt",
  "xAxis": ["Start", "End"]
});
```

# Heatmap

```javascript
new CanvasXpress("Heatmap", data, {
  "graphType": "Heatmap",
  "xAxis": ["Col1", "Col2", "Col3"],
});
```

# Hex

```javascript
new CanvasXpress("Hex", data, {
  "graphType": "Hex",
  "xAxis": ["Col1"]
});
```

# Hexplot

```javascript
new CanvasXpress("Hexplot", data, {
  "graphType": "Hexplot",
  "xAxis": ["Col1"]
});
```

# Histogram

```javascript
new CanvasXpress("Histogram", data, {
  "graphType": "Histogram",
  "xAxis": ["Col1"]
});
```

# KaplanMeier

```javascript
new CanvasXpress("KaplanMeier", data, {
  "graphType": "KaplanMeier",
  "xAxis": ["Time"],
  "yAxis": ["Survival"]
});
```

# Line

```javascript
new CanvasXpress("Line", data, {
  "graphType": "Line",
  "xAxis": ["Col1"]
});
```

# Lollipop

```javascript
new CanvasXpress("Lollipop", data, {
  "graphType": "Lollipop",
  "xAxis": ["Col1"]
});
```

# Map

```javascript
new CanvasXpress("Map", false, {
  "graphType": "Map",
  "mapId": "World",
});
```

# Meter

```javascript
new CanvasXpress("Meter", data, {
  "graphType": "Meter",
  "xAxis": ["Col1"]
});
```

# Network

```javascript
new CanvasXpress("Network", network, {
  "graphType": "Network"
});
```

# ParallelCoordinates

```javascript
new CanvasXpress("ParallelCoordinates", data, {
  "graphType": "ParallelCoordinates",
  "xAxis": ["Col1", "Col2", "Col3"],
});
```

# Pareto

```javascript
new CanvasXpress("Pareto", data, {
  "graphType": "Pareto",
  "xAxis": ["Col1"],
  "xAxis2": ["Col2"]
});
```

# Pie

```javascript
new CanvasXpress("Pie", data, {
  "graphType": "Pie",
  "xAxis": ["Group"]
});
```

# QQ

```javascript
new CanvasXpress("QQ", data, {
  "graphType": "QQ",
  "xAxis": ["Col1"]
});
```

# Quantile

```javascript
new CanvasXpress("Quantile", data, {
  "graphType": "Quantile",
  "xAxis": ["Col1"]
});
```

# Radar

```javascript
new CanvasXpress("Radar", data, {
  "graphType": "Radar",
  "xAxis": ["Col1"]
});
```

# Ribbon

```javascript
new CanvasXpress("Ribbon", data, {
  "graphType": "Ribbon",
  "xAxis": ["Col1"],
  "sankeyAxes": ["Group", "Type", "Category"]
});
```

# Ridgeline

```javascript
new CanvasXpress("Ridgeline", data, {
  "graphType": "Ridgeline",
  "xAxis": ["Col2"],
  "ridgeBy": ["Category"],
});
```

# Sankey

```javascript
new CanvasXpress("Sankey", data, {
  "graphType": "Sankey",
  "xAxis": ["Col1"],
  "sankeyAxes": ["Group", "Type"]
});
```

# Scatter2D

```javascript
new CanvasXpress("Scatter2D", data, {
  "graphType": "Scatter2D",
  "xAxis": ["Col1"],
  "yAxis": ["Col2"]
});
```

# Scatter3D

```javascript
new CanvasXpress("Scatter3D", data, {
  "graphType": "Scatter3D",
  "xAxis": ["Col1"],
  "yAxis": ["Col2"],
  "zAxis": ["Col3"]
});
```

# ScatterBubble2D

```javascript
new CanvasXpress("ScatterBubble2D", data, {
  "graphType": "ScatterBubble2D",
  "xAxis": ["Col1"],
  "yAxis": ["Col2"],
  "zAxis": ["Col3"]
});
```

# Spaghetti

```javascript
new CanvasXpress("Spaghetti", data, {
  "graphType": "Spaghetti",
  "xAxis": ["Col1"],
  "yAxis": ["Col2"],
  "colorBy": ["Group"],
});
```

# SPLOM

```javascript
new CanvasXpress("SPLOM", data, {
  "graphType": "SPLOM",
  "xAxis": ["Col1", "Col2", "Col3"],
  "yAxis": ["Col1", "Col2", "Col3"]
});
```

# Stacked

```javascript
new CanvasXpress("Stacked", data, {
  "graphType": "Stacked",
  "xAxis": ["Col1", "Col2", "Col3"]
});
```

# StackedLine

```javascript
new CanvasXpress("StackedLine", data, {
  "graphType": "StackedLine",
  "xAxis": ["Col1", "Col2"],
  "xAxis2": ["Col3"]
});
```

# StackedPercent

```javascript
new CanvasXpress("StackedPercent", data, {
  "graphType": "StackedPercent",
  "xAxis": ["Col1", "Col2", "Col3"]
});
```

# StackedPercentLine

```javascript
new CanvasXpress("StackedPercentLine", data, {
  "graphType": "StackedPercentLine",
  "xAxis": ["Col1", "Col2"],
  "xAxis2": ["Col3"]
});
```

# Streamgraph

```javascript
new CanvasXpress("Streamgraph", data, {
  "graphType": "Streamgraph",
  "xAxis": ["Year"],
  "yAxis": ["Col1", "Col2", "Col3"]
});
```

# Sunburst

```javascript
new CanvasXpress("Sunburst", data, {
  "graphType": "Sunburst",
  "hierarchy": ["Type", "Group"]
});
```

# TagCloud

```javascript
new CanvasXpress("TagCloud", data, {
  "graphType": "TagCloud",
  "xAxis": ["Col1"],
  "colorBy": ["Group"]
});
```

# TimeSeries

```javascript
new CanvasXpress("TimeSeries", data, {
  "graphType": "TimeSeries",
  "xAxis": ["Year"],
  "yAxis": ["Col1", "Col2", "Col3"]
});
```

# Tornado

```javascript
new CanvasXpress("Tornado", data, {
  "graphType": "Tornado",
  "xAxis": ["Col1", "Neg"]
});
```

# Tree

```javascript
new CanvasXpress("Tree", data, {
  "graphType": "Tree",
  "xAxis": ["Col1"],
  "hierarchy": ["Group", "Type"]
});
```

# TreeBracket

```javascript
new CanvasXpress("TreeBracket", data, {
  "graphType": "Tree",
  "xAxis": ["Col1"],
  "hierarchy": ["Final", "Semifinal", "4th", "8th"],
  "treeType": "bracket",
  "treeNodeSizeScaleFactor": 2,
  "treeInverted": true
});
```


# TreeMap

```javascript
new CanvasXpress("Treemap", data, {
  "graphType": "Treemap",
  "xAxis": ["Col1"],
  "groupingFactors": ["Group"]
});
```

# Venn

```javascript
new CanvasXpress("Venn", venn, {
  "graphType": "Venn",
  "xAxis": ["A", "AB", "ABC", "ABCD", "ABD", "AC", "ACD", "AD", "B", "BC", "BCD", "BD", "C", "CD", "D"],
  "vennGroups": 4
});
```

# Violin

```javascript
new CanvasXpress("Violin", data, {
  "graphType": "Violin",
  "xAxis": ["Col1"],
  "groupingFactors": ["Group"]
});
```

# Volcano

```javascript
new CanvasXpress("Volcano", data, {
  "graphType": "Volcano",
  "xAxis": ["FC"],
  "yAxis": ["LOD"]
});
```

# Waterfall

```javascript
new CanvasXpress("Waterfall", data, {
  "graphType": "Waterfall",
  "xAxis": ["Diff"]
});
```

# WordCloud

```javascript
new CanvasXpress("WordCloud", data, {
  "graphType": "WordCloud",
  "xAxis": ["Col2"],
  "colorBy": ["Type"]
});
```
