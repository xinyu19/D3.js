# Bubble Chart
###### tags: `D3.js`

```javascript=
const svgSize = { width: 600, height: 500 };
const margin = { top: 50, right: 40, bottom: 50, left: 60 };
var width = svgSize.width - margin.left - margin.right;
var height = svgSize.height - margin.top - margin.bottom;

// Create graph topic
d3.select("body").append("h2").html("台灣各縣市平均所得與人口數");

// Create color scheme
var colorScale = d3.scaleOrdinal(d3.schemePaired);

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

// Create a pop-up window
var tip = d3
  .select("body")
  .append("div")
  .attr("class", "tip")
  .style("position", "absolute")
  .style("z-index", "10")
  .style("visibility", "hidden");

//Import Data
d3.json("./data/data.json")
  .then((data) => {
    // Create Scale
    var xScale = d3.scaleLinear().domain([0, 2000000]).range([0, width]);
    var yScale = d3.scaleLinear().domain([0, 500]).range([height, 0]);

    // Create Scale for bubble circle
    // set the max circle radius = 60
    var cScale = d3
      .scaleLinear()
      .domain([0, d3.max(data.map((d) => d.number))])
      .range([0, 60]);

    // Create axes
    var axisX = d3.axisBottom(xScale);
    var axisY = d3.axisLeft(yScale).ticks(10);
    var axisZ = d3.axisLeft(yScale).tickFormat("").tickSize(-500, 0);
    chart.append("g").call(axisX).attr("transform", `translate(0,${height})`);
    chart.append("g").call(axisY);
    chart.append("g").call(axisZ).attr("stroke-width", "0.1px");
    chart
      .append("text")
      .attr("text-anchor", "end")
      .attr("x", width / 2 + 80)
      .attr("y", height + 40)
      .text("平均年所得");
    chart
      .append("text")
      .attr("transform", "rotate(-90)")
      .attr("y", "20px")
      .text("縣市人口數 (萬)")
      .attr("text-anchor", "end");

    // Draw buubles
    chart
      .append("g")
      .selectAll("dot")
      .data(data)
      .enter()
      .append("circle")
      .attr("cx", (d) => xScale(d.salary))
      .attr("cy", (d) => yScale(d.number))
      .attr("r", () => 0)
      .on("mousemove", (e, d) => {
        tip
          .text(`${d.city}, 平均所得：${d.salary}`)
          .style("visibility", "visible")
          .style("top", e.clientY + 20 + "px")
          .style("left", e.clientX - 60 + "px");
      })
      .on("mouseout", () => {
        tip.style("visibility", "hidden");
      })
      .transition()
      .duration(2000)
      .attr("r", (d) => cScale(d.number))
      .style("fill", (d, i) => colorScale(i))
      .attr("stroke", "black");
  })
  .catch((error) => {
    console.log(error);
  });

```
![](https://i.imgur.com/rLNhBXD.gif)
