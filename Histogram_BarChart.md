# Histogram, Bar Chart

![](https://i.imgur.com/QvvPbn4.png)
## Histogram
```javascript=
// Set up SVG size
const svgSize = { width: 600, height: 500 };
// Set up Margin
const margin = { top: 50, right: 40, bottom: 50, left: 60 };
// Set up graph dimension
var width = svgSize.width - margin.left - margin.right;
var height = svgSize.height - margin.top - margin.bottom;

// Create graph topic
d3.select("body").append("h2").html("各學年度大學畢業學生數");

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

// Create colorscheme
var color = d3.scaleOrdinal(d3.schemeCategory10);
// var color2 = ["red","orange","yellow","green","blue","indigo ","purple"];

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
      .domain(data.map((d) => d.years))
      .range([0, width]);

    var yScale = d3.scaleLinear().domain([0, 350000]).range([height, 0]);

    // Create axes
    var axisX = d3.axisBottom(xScale);
    var axisY = d3.axisLeft(yScale).ticks(10);
    var axisZ = d3.axisLeft(yScale).tickFormat("").tickSize(-500, 0);
    chart.append("g").call(axisX).attr("transform", `translate(0,${height})`);
    chart.append("g").call(axisY);
    chart.append("g").call(axisZ).attr("stroke-width", "0.1px");
    chart
      .append("text")
      .attr("y", 440)
      .attr("x", width / 2 - 20)
      .text("畢業學年度");
    chart
      .append("text")
      .attr("transform", "rotate(-90)")
      .attr("y", "20px")
      .attr("text-anchor", "end")
      .text("學生數");

    // Create rect
    chart
      .selectAll("rect")
      .data(data)
      .enter()
      .append("rect")
      .attr("class", "bar")
      .attr("x", (d) => xScale(d.years))
      .attr("y", () => height)
      .attr("width", xScale.bandwidth())
      .attr("height", 0)
      .attr("fill", (d, i) => color(i))

      // Create mouse event
      .on("mouseover", (e, d) => {
        tip
          .text(`畢業學生數： ${d.students}`)
          .style("visibility", "visible")
          .style("top", yScale(d.students) + 50 + "px")
          .style("left", xScale(d.years) + xScale.bandwidth() - 50 + "px");
      })
      .on("mouseout", () => {
        tip.style("visibility", "hidden");
      })
      .transition()
      .duration(2000)
      .attr("y", (d) => yScale(d.students))
      .attr("height", (d) => height - yScale(d.students));
  })
  .catch((error) => {
    console.log(error);
  });

```

![](https://i.imgur.com/qUOcjXA.gif)

## Bar Chart 
> add some setting from histogram could be a bar chart
> `.paddingInner(0.4)` : the space btw rect
>  `.paddingOuter(0.5)`: the first and last one space




```javascript=
// Set up SVG size
const svgSize = { width: 600, height: 500 };
// Set up Margin
const margin = { top: 50, right: 40, bottom: 50, left: 60 };
// Set up graph dimension
var width = svgSize.width - margin.left - margin.right;
var height = svgSize.height - margin.top - margin.bottom;

// Create graph topic
d3.select("body").append("h2").html("台灣六都大學學生人數");

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

// Create colorscheme
var color = d3.scaleOrdinal(d3.schemeCategory10);

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
      .domain(data.map((d) => d.city))
      .range([0, width])
      .paddingInner(0.4) //the space btw rect
      .paddingOuter(0.5); // the first and last one space

    var yScale = d3.scaleLinear().domain([0, 50000]).range([height, 0]);
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
      .attr("x", width / 2 - 30)
      .text("都市名稱");
    chart
      .append("text")
      .attr("transform", "rotate(-90)")
      .attr("y", "20px")
      .attr("text-anchor", "end")
      .text("學生數");

    // Create rect
    chart
      .selectAll("rect")
      .data(data)
      .enter()
      .append("rect")
      .attr("class", "bar")
      .attr("x", (d) => xScale(d.city))
      .attr("y", () => height)
      .attr("width", xScale.bandwidth())
      .attr("fill", (d, i) => color(i))

      // Create mouse event
      .on("mouseover", (e, d) => {
        tip
          .text(`學生人數： ${d.students}`)
          .style("visibility", "visible")
          .style("top", yScale(d.students) + 60 + "px")
          .style("left", xScale(d.city) + xScale.bandwidth() - 40 + "px");
      })
      .on("mouseout", () => {
        tip.style("visibility", "hidden");
      })
      .transition()
      .duration(2000)
      .attr("y", (d) => yScale(d.students))
      .attr("height", (d) => height - yScale(d.students));
  })
  .catch((error) => {
    console.log(error);
  });
```
![](https://i.imgur.com/Jw2wd1e.gif)

