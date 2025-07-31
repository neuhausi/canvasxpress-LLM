# Chain-of-Thought Process for CanvasXpress Configuration

STEP 1: ANALYZE DESCRIPTION
Example: "Create a bar chart comparing sales across different product categories."
Thought process:
- This is asking for a comparison between categories (products)
- The comparison is of a single metric (sales)
- No time component is mentioned
- No grouping or faceting is mentioned
- This is a straightforward categorical comparison

STEP 2: IDENTIFY DATA STRUCTURE
Thought process:
- Column headers likely include "Product" and "Sales"
- "Product" is categorical
- "Sales" is numerical
- This is a one-dimensional data structure (category + value)
- No additional metadata appears necessary

STEP 3: SELECT GRAPH TYPE
Thought process:
- For category comparison, consider: Bar, Lollipop, Cleveland
- Bar is most common for simple comparisons
- Lollipop would emphasize individual values
- Cleveland would be good for ranking
- No special requirements mentioned
- Decision: Use "Bar" as it's the standard for category comparisons

STEP 4: CONFIGURE AXES
Thought process:
- For Bar graph (one-dimensional), only need xAxis
- xAxis should be "Sales" because is the value being compared
- yAxis is not needed since it's a one-dimensional graph
- Configuration: "xAxis": ["Sales"]

STEP 5: SET ADDITIONAL PARAMETERS
Thought process:
- Need to consider:
  - Graph orientation (horizontal/vertical)
  - Color scheme
  - Title and subtitle
- No specific requirements mentioned
- Use default vertical orientation
- Configuration:
  "graphOrientation": "vertical",
  "colorScheme": "CanvasXpress",
  "title": "Sales by Product Category"

STEP 6: VALIDATE CONFIGURATION
Thought process:
- Check required parameters:
  - graphType is specified (Bar)
  - xAxis is specified correctly
- Check parameter compatibility:
  - Bar is one-dimensional, so only xAxis is used
  - graphOrientation is valid for Bar
- Check for errors:
  - No invalid parameters
  - No missing required parameters
- Final JSON:
```json
{
  "graphType": "Bar",
  "xAxis": ["Sales"],
  "graphOrientation": "vertical",
  "colorScheme": "CanvasXpress",
  "title": "Sales by Product Category"
}
