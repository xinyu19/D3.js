# Stacked Graph
###### tags: `D3.js`

```javascript=
const svgSize = { width: 600, height: 500 };
const margin = { top: 50, right: 40, bottom: 50, left: 60 };
var width = svgSize.width - margin.left - margin.right;
var height = svgSize.height - margin.top - margin.bottom;

// Create graph topic
d3.select("body").append("h2").html("各分店水果銷售量統計");

// Create color scheme
var colors = ["#E74343", "#EEAB31", "#DEDE17"];

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

//Import Data
d3.json("./data/data.json")
  .then((data) => {
    // Branch Name
    var storeName = Object.keys(data);
    // stock
    var counts = Object.values(data);

    // Create Scale
    var xScale = d3
      .scaleBand()
      .domain(storeName)
      .range([0, width])
      .paddingInner(0.25)
      .paddingOuter(0.35);

    var yScale = d3
      .scaleLinear()
      .domain([0, d3.max(counts, (d) => d.apples + d.oranges + d.bananas)])
      .range([height, 0]);

    // Create axes
    var axisX = d3.axisBottom(xScale);
    var axisY = d3.axisLeft(yScale).tickFormat((d) => d + " 公斤");

    chart.append("g").call(axisX).attr("transform", `translate(0,${height})`);
    chart.append("g").call(axisY);
    chart
      .append("text")
      .attr("y", 440)
      .attr("x", width / 2 - 30)
      .text("分店名稱");
    chart
      .append("text")
      .attr("transform", "rotate(-90)")
      .attr("y", "20px")
      .attr("text-anchor", "end")
      .text("銷售總重量");

    // Grouped by fruit name
    const stack = d3.stack().keys(["apples", "oranges", "bananas"]);

    var groups = chart
      .selectAll(".stack")
      .data(stack(counts))
      .enter()
      .append("g")
      .attr("class", "stack")
      .style("fill", (d, i) => colors[i]);

    groups
      .selectAll("rect")
      .data((d) => d)
      .enter()
      .append("rect")
      .attr("x", (d, i) => xScale(storeName[i]))
      .attr("y", (d) => yScale(d[1]))
      .attr("width", xScale.bandwidth())
      .attr("height", (d) => yScale(d[0]) - yScale(d[1]));
  })
  .catch((error) => {
    console.log(error);
  });

```
![](https://i.imgur.com/hzCNgXw.png)
