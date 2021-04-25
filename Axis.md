# D3 Axis
###### tags: `D3.js`

* X-axis: `d3.axisBottom(scale)`
* Y-axis: `d3.axisLeft(scale)` 

* `d3.tickFormat()`: used to control which ticks are labelled.
* `d3.ticks()`: control which ticks are displayed by the axis
* `d3.tickSize()`:  used to set the inner and outer tick size

```javascript=
// SVG dimension
const svgSize={ width: 600,height: 500 };

//Create SVG
var svg = d3.select("body")
            .append("svg")
            .attr("width", svgSize.width)
            .attr("height", svgSize.height);


            
// Create Scale
var xScale = d3.scaleLinear()
               .domain([0, 100])
               .range([0, 400]);
var yScale = d3.scaleLinear()
               .domain([0, 100])
               .range([300, 0]);

// Create axis
var axisX = d3.axisBottom(xScale) 
              .tickSize(10)
              .tickFormat(d => (d+" 人"))
              .ticks(5)
var axisY = d3.axisLeft(yScale);

// Way 1
// Draw Axis
svg.append("g")
   .call(axisX)
   .attr("transform","translate(100,310)")
svg.append("g")
   .call(axisY)
   .attr("transform", "translate(100,10)");

// Way 2, group axis would be easy to make changes
// Group axis
var chart = svg.append("g")
               .attr("class","chart")
//move the axis groups               .attr("transform","translate(50,50)")

// Draw Axis
chart.append("g")
   .call(axisX)
   .attr("transform","translate(100,310)")
chart.append("g")
   .call(axisY)
   .attr("transform", "translate(100,10)");
```
![](https://i.imgur.com/tpFeaEw.png)

* change the axis style
```css=
.chart path {
    stroke-width: 3px;
    stroke: #51c8d8;
}
.chart line {
    stroke: #51c8d8;
}
.chart text {
    color: #3c86cc;
    font-size: 12px;
}
```
![](https://i.imgur.com/ghHLWnn.png)
