# D3 Scales

## Linear Scale

`d3.scaleLinear().domain().range()`

* Scale up/down
```javascript=
//Scale up
var linear = d3.scaleLinear()
               .domain([0, 8])
               .range([0, 160]);

console.log(linear(3));


//Scale down
var linear2 = d3.scaleLinear()
                .domain([0, 1000])
                .range([0, 50]);
```
![](https://i.imgur.com/STh4sgE.png)

* Scale data to make it easily to read

```javascript=
// Data Set：
var dataset = [1, 4, 3, 2, 5, 8];

// Create Data and binding data
var svg = d3
  .select("body")
  .append("svg")
  .attr("width", 400)
  .attr("height", 250)
  .attr("style", "border:1px solid black");

var selection = svg.selectAll("rect").data(dataset);
selection.enter().append("rect");
selection.exit().remove();

// Create Scale
var linear = d3.scaleLinear()
               .domain([0, 10])
               .range([0, 200]);

d3.selectAll("rect")
  .attr("width", 40)
  .attr("height", d => linear(d))
  .attr("x", (d, i) =>  i * 55 + 40)
  .attr("y", (d, i) => 250 - linear(d))
  .attr("fill", "blue");
```
![](https://i.imgur.com/aUQ3i0J.png)

* find the maximum and minimum
`d3.max([,])`
`d3.min([,])`

```javascript=
// Data set
var dataset1 = [ 8,60,34,28,51 ];

// find max and min
var max = d3.max(dataset1);
var min = d3.min(dataset1);

console.log(max);
console.log(min);

var dataset2 = [
  { name: "Taiwan" , population: 2537 },
  { name: "Japan" , population: 12650 },
  { name: "Korea" , population: 5164 }
]

//find max and min of specific data in array
var max = d3.max(dataset2, d => d.population);
var min = d3.min(dataset2, d => d.population);

console.log(max);
console.log(min);
```

* other type
    * d3.scaleIdentity()
    * d3.scaleSqrt()
    * d3.scaleLog()
    * d3.scaleQuantile()


## Color Scale
* Common Color Scheme
    * d3.schemeCategory10
    * d3.schemeAccent
    * d3.schemeDark2
    * de.schemePaired

![](https://i.imgur.com/sK7310I.png)

```javascript=
// Show the color code
console.log(d3.schemeCategory10);

// Create color scheme
var color = d3.scaleOrdinal(d3.schemeCategory10);

// Print ordinary
for (var i = 1; i <= 10; i++) {
  d3.select("body")
    .append("div")
    .attr("class", "box")
    .style("background-color", color(i));
}
```


```javascript=
// DataSet
var dataset = [1, 4, 3, 2, 5, 8];

// Create rect and binding data
var svg = d3
  .select("body")
  .append("svg")
  .attr("width", 400)
  .attr("height", 250)
  .attr("style", "border:1px solid black");

var selection = svg.selectAll("rect").data(dataset);
selection.enter().append("rect");
selection.exit().remove();

// Create scale
var linear = d3
  .scaleLinear()
  .domain([0, d3.max(dataset)])
  .range([0, 200]);

// Create color scale
var color = d3.scaleOrdinal(d3.schemeCategory10);

d3.selectAll("rect")
  .attr("width", 40)
  .attr("height", d => linear(d))
  .attr("x", (d, i) =>  i * 55 + 40)
  .attr("y", (d, i) => 250 - linear(d))
  .attr("fill", (d, i) => color(i));
```
![](https://i.imgur.com/T7OSHLk.png)


## Ordinal Scale
```javascript=
// Data
var dataset = [
  { country: "Taiwan", value: 2537 },
  { country: "Japan", value: 12650 },
  { country: "Korea", value: 5164 }
];

var svg = d3
  .select("body")
  .append("svg")
  .attr("width", 500)
  .attr("height", 500);

// Scale
var x = d3.scaleBand()
          .domain(["Taiwan", "Japan", "Korea"])
          .range([0, 300])

// console.log(x("Japan"));

var y = d3.scaleLinear()
          .domain([ d3.max(dataset, d => d.value),0 ])
          .range([0, 400]);

svg.selectAll("rect")
   .data(dataset)
   .enter()
   .append("rect")
   .attr("x", d => x(d.country))
   .attr("y", d => y(d.value))
   .attr("height", d => 400 - y(d.value))
   .attr("width", 50);

svg.selectAll("text")
   .data(dataset)
   .enter()
   .append("text")
   .text(d => d.country)
   .attr("x", d => x(d.country))
   .attr("y", 420);
```

![](https://i.imgur.com/PNEBSvA.png)


## Interpolate
* number: `d3.interpolateNumber(start value, end value)`
* color: `d3.interpolateLab(start color, end color`

```javascript=
// number interpolate
var i = d3.interpolateNumber(10, 20);

console.log(i(0));
console.log(i(0.2));
console.log(i(0.5));
console.log(i(1));

// Input exceed
console.log(i(150)); // 1510=10+150*(20-10)
console.log(i(-9)); // -80=10+(-9)*(20-10)

// color interpolate
var color = d3.interpolateLab("red", "gray");

console.log(color(0)); // rgb(255, 0, 0)
console.log(color(0.21)); // rgb(233, 66, 36)
console.log(color(1)); // rgb(128, 128, 128)
```