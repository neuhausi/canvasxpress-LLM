# Handling Contradictory Requirements in CanvasXpress Configurations

When generating CanvasXpress configurations from English descriptions, you may encounter contradictory or incompatible requirements. This document provides guidelines to resolve such conflicts while maintaining visualization integrity.

## Types of Contradictions

### 1. Graph Type vs. Data Structure Contradictions
When the requested graph type is incompatible with the described data structure.

**Examples:**
- Requesting a pie chart to show correlation between variables
- Asking for a line chart with categorical data on both axes

### 2. Dimensional Contradictions
When the number of variables exceeds what the requested graph type can effectively visualize.

**Examples:**
- Requesting a 2D scatter plot for 4+ variables
- Asking for a bar chart to display 3D data

### 3. Parameter Incompatibilities
When requested parameters cannot be used together or with the specified graph type.

**Examples:**
- Using both `stackBy` and `ridgeBy` in the same visualization
- Requesting `showRegressionFit` with a bar chart

## Resolution Hierarchy

When faced with contradictory requirements, follow this prioritization:

1. **Data integrity** - Ensure the visualization accurately represents the underlying data
2. **Primary visualization goal** - Identify and preserve the main analytical purpose
3. **Graph type preference** - Honor the requested graph type when possible
4. **Parameter preferences** - Include requested parameters when compatible

## Resolution Strategies

### For Graph Type vs. Data Structure Contradictions:
- Prioritize data structure over requested graph type
- Use substitution mapping (e.g., if correlation analysis is requested with incompatible graph type → Use Scatter2D)

### For Dimensional Contradictions:
- Reduce dimensions by focusing on primary variables
- Map additional variables to visual attributes (color, size, shape) when possible

### For Parameter Incompatibilities:
- Prioritize essential parameters and discard incompatible ones
- Use parameter substitution when appropriate

## Example Resolution

**Request:** "Create a pie chart showing the correlation between temperature and pressure"

**Resolution:**
1. Identify primary goal: showing correlation between two variables
2. Substitute appropriate graph type: Scatter2D
3. Configuration:
   ```json
   {
     "graphType": "Scatter2D",
     "xAxis": ["temperature"],
     "yAxis": ["pressure"],
     "showRegressionFit": true,
     "title": "Correlation between Temperature and Pressure"
   }
