# Line Graph

###### tags: `D3.js`
```javascript=
// Set up SVG size
const svgSize = { width: 600, height: 500 };
// Set up Margin
const margin = { top: 50, right: 40, bottom: 50, left: 40 };
// Set up graph dimension
var width = svgSize.width - margin.left - margin.right;
var height = svgSize.height - margin.top - margin.bottom;

// Create SVG
var svg = d3
  .select("body")
  .append("svg")
  .attr("width", svgSize.width)
  .attr("height", svgSize.height);

// Create Chart graph
var chart = svg
  .append("g")
  .attr("transform", `translate(${margin.left},${margin.top})`)
  .attr("class", "chart");

// Create graph topic
d3.select("body").append("h2").html("台灣各日期發生病例數統計");

// Create a pop-up window
var tip = d3
  .select("body")
  .append("div")
  .attr("class", "tip")
  .style("position", "absolute")
  .style("z-index", "10")
  .style("visibility", "hidden");

// Import Data
d3.json("./data/data.json")
  .then((data) => {
    // Create Scale
    var xScale = d3
      .scaleBand()
      .domain(data.map((d) => d.day))
      .range([0, width]);

    var yScale = d3.scaleLinear().domain([0, 30]).range([height, 0]);

    // Create axes
    var axisX = d3.axisBottom(xScale);
    var axisY = d3.axisLeft(yScale).ticks(10);
    var axisZ = d3.axisLeft(yScale).tickFormat("").tickSize(-500, 0);

    chart.append("g").call(axisX).attr("transform", `translate(0,${height})`);
    chart.append("g").call(axisY);

    // Create axes reference line
    chart.append("g").call(axisZ).attr("stroke-width", "0.1px");

    // Create information of axes
    chart
      .append("text")
      .attr("y", 440)
      .attr("x", width / 2)
      .attr("text-anchor", "start")
      .text("日期");
    chart
      .append("text")
      .attr("transform", "rotate(-90)")
      .attr("y", "20px")
      .attr("text-anchor", "end")
      .text("發生人數");

    // Calculate each break point
    var line = d3
      .line()
      .x((d) => xScale(d.day))
      .y((d) => yScale(d.number));

    var gPath = chart.append("g").style("transform", "translate(40px,0)");

    gPath
      .append("path")
      .datum(data)
      .attr("class", "line")
      .attr("d", line)
      .style("fill", "none")
      .style("stroke", "#9AC3F3")
      .style("stroke-width", "4px");

    gPath
      .selectAll("circle")
      .data(data)
      .enter()
      .append("circle")
      .attr("class", "dot")
      .attr("cx", (d) => xScale(d.day))
      .attr("cy", (d) => yScale(d.number))
      .attr("r", 10)
      .style("fill", "#4A90E2")

      // Create a mouse event
      .on("mouseover", (e, d) => {
        tip
          .text(`${d.day}, ${d.number} 例`)
          .style("visibility", "visible")
          .style("top", yScale(d.number) + 50 + "px")
          .style("left", xScale(d.day) + 40 + "px");
      })
      .on("mouseout", () => {
        tip.style("visibility", "hidden");
      });
  })
  .catch((error) => {
    console.log(error);
  });

```
```json=
[
    { "day": "3/21", "number": 6 },
    { "day": "3/22", "number": 10 },
    { "day": "3/23", "number": 12 },
    { "day": "3/24", "number": 7 },
    { "day": "3/25", "number": 8 },
    { "day": "3/26", "number": 20 },
    { "day": "3/27", "number": 11 },
    { "day": "3/30", "number": 9 }
  ]
```
![](https://i.imgur.com/w8AJFF4.png)

