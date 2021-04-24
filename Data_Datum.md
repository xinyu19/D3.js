# D3 Binding

## Data() 

HTML
```htmlmixed=
<body>
  <div>...</div>
  <div>...</div>
  <div>...</div>
  <script src="./js/app.js"></script>
</body>
```
```javascript=
d3.select("body")
  .select("div")
  .datum(20)
  .text(d => d);
```

*　Mutiple Datumn using data()
```javascript=
// Data Array
var arr=[20,30,40];
d3.select("body")
  .selectAll("div")
  .data(arr)
  .text((d) => d);
```
> `console.log(d3.selectAll("div"))"` can check the data 

## Datum()
```javascript=
// Data Array
var arr=[20,30,40];
for(var i=0;i<arr.length;i++){
  d3.select("body")
    .append("div")
    .datum(arr[i])
    .text(d => d);
``` 
![](https://i.imgur.com/DQQjucj.png)

### Data type vs Element type
* Data type = Element type : Combine directly
`var selection = d3.selectAll("rect").data("DataSet")`
* Data type > Element type : Add element amount
`selection.enter().append("rect")`

* Data type < Element type : Eliminate extra element 
`selection.exit().remove()`

```javascript=
//Array 
var arr = [10, 20, 30, 40, 50];

//Combine Data
var selection = 
  d3.select("body")
    .selectAll("div")
    .data(arr)
    .text(d => d);

// Complement the element 
selection.enter().append("div").text(d => d);

// Pruning the element 
selection.exit().remove();

```
![](https://i.imgur.com/aNc67L9.png)


## Key function
Key function reference: data & index
* data: `d`
* index: `i`

Data would be an array or .json, thus it would hvae key and value, its order is "index" 

```javascript=
// Data Array
var arr = [
  { name: "Michael", age: 23 },
  { name: "David", age: 42 },
  { name: "Tom", age: 47 },
  { name: "Allen", age: 32 },
  { name: "James", age: 29 }
];

d3.select("body")
  .selectAll("div")
  .data(arr)
  .text(d => d.name + "：" + d.age);
```

###### tags: `D3.js`