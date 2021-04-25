# Pie Chart

```javascript=
const svgSize = { width: 600, height: 500 };
const margin = { top: 50, right: 40, bottom: 50, left: 60 };
var width = svgSize.width - margin.left - margin.right;
var height = svgSize.height - margin.top - margin.bottom;

// Create graph topic
d3.select("body").append("h2").html("台灣各學年大學畢業生數");

// Create color scheme
var color = d3.scaleOrdinal(d3.schemeCategory10);

// Create SVG
var svg = d3
  .select("body")
  .append("svg")
  .attr("width", svgSize.width)
  .attr("height", svgSize.height);

// Create Chart graph
var chart = svg
  .append("g")
  .attr("transform", `translate(${width / 2},${height / 2})`)
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
    var radius = Math.min(width, height) / 2;
    // Pie Chart
    var arc = d3
      .arc()
      // outerRadius
      .outerRadius(radius)
      //innerRadius
      // if innerRadius != 0, then it would be a donut chart
      .innerRadius(0);
    // Create arc scale
    var pie = d3.pie().value((d) => d.students);

    // Draw the pue chart
    chart
      .selectAll("path")
      .data(pie(data))
      .enter()
      .append("path")
      .attr("d", arc)
      .attr("fill", (d, i) => color(i))
      .attr("stroke", "#fff")
      .on("mousemove", (e, d) => {
        tip
          .text(`${d.data.years} 學年度有 ${d.data.students} 學生`)
          .style("visibility", "visible")
          .style("top", e.clientY + 20 + "px")
          .style("left", e.clientX - 50 + "px");
      })
      .on("mouseout", () => {
        tip.style("visibility", "hidden");
      });

    // Add text on the pie chart
    chart
      .selectAll("text")
      .data(pie(data))
      .enter()
      .append("text")
      .attr("text-anchor", "middle")
      .attr("transform", (d) => {
        return `translate(${arc.centroid(d)})`;
      })
      .text((d, i) => data[i].students);
  })
  .catch((error) => {
    console.log(error);
  });

```


![](https://i.imgur.com/Pt9E9tA.png)
