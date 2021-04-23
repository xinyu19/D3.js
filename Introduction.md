# 資料視覺化 (Data Visualization) - Introduction

## Data Visualization
* 資料的正確性: 讓數據進行美觀的呈現下進行製作，仍需要保有數據的正確性
* 讀者的閱讀動機: 幫助讀者去理解不熟悉的領域資訊
* 傳遞資訊的效率: 讀者理解圖表所耗費的時間，是否留下印象
* Visualization: 
    * Science Visulaziation
    * Information Visulization
    * Visual Analytics

## D3.js (Data-Driven Documents)
To use d3.js download the js file from D3 website.
Two way to use D3.js
* `<script src="https://d3js.org/d3.v6.min.js"></script>`
* `<script src="./js/d3.min.js"></script>`
> make sure the path is correct


```htmlembedded=
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://d3js.org/d3.v6.min.js"></script>
    <!-- <script src="./js/d3.min.js"></script> -->
    <title>D3.js Data Visualization</title>
</head>
<script src="./js/app.js"></script>
<body>
</body>

</html>
```
The app.js under js file
```json=
console.log(d3.version);
```

![](https://i.imgur.com/pF4ZkIh.png)





## Create SVG within HTML
```htmlembedded=
    <!DOCTYPE html>
<html lang="zh-Hant-TW">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://d3js.org/d3.v6.min.js"></script>
    <title>D3.js Data Visualization</title>
</head>
<body>
    <svg></svg>
    <script src="./js/app.js"></script>
</body>
</html>
```
/js/app.js
```json=
d3.select("svg")
    .append("text")
    .text("Hello D3")
    .attr("y", 20);
//This will be the left of following pic 
d3.select("body")
    .append("svg")
    .append("text")
    .text("Hello D3.js")
    .attr("y", 20);
//This will be the right of folloing pic
//Since it is append ("svg")
```

![](https://i.imgur.com/GzxFzAd.png)


## Create graph by SVG
### SVG Coordinate System
```htmlembedded=
<!DOCTYPE html>
<html lang="zh-Hant-TW">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://d3js.org/d3.v6.min.js"></script>
    <title>D3.js Data Visualization</title>
</head>
<body>
    <svg width = "500", height = "300" ></svg>
    <script src="./js/app.js"></script>
</body>
</html>
```
![](https://i.imgur.com/6iUExJT.png)


### Rectangle
```htmlembedded=
<rect x="100" y="50" width="120" height="60" fill="rgb(74,144,226)" />
```
![](https://i.imgur.com/WZbytL8.png)


### Circle
```htmlembedded=
<circle cx="160" cy="180" r="50" fill="rgb(74,144,226)" />
```
![](https://i.imgur.com/v4af6sr.png)


 
 
### ellipse
 ```htmlembedded=
<ellipse cx="160" cy="300" rx="70" ry="45" fill="rgb(74,144,226)" />
```
![](https://i.imgur.com/wwnqDUr.png)



### line
```htmlembedded=
<line x1="260" y1="50" x2="390" y2="110" style="stroke: rgb(74,144,226); stroke-width: 3px" />
```
![](https://i.imgur.com/6UGpQcK.png)



### polygon
```htmlembedded=
<polygon points="270,140 330,230 390,140" style="fill: rgb(200, 247, 244); stroke:red; stroke-width: 3px" />
```
![](https://i.imgur.com/koVrZRq.png)



### polyline
```htmlembedded=
<polyline points="300 300 600 300 600 200" style="fill: rgb(200, 247, 244); stroke:red; stroke-width: 3px" />
```
![](https://i.imgur.com/yBn9qlE.png)

> The different of `<polyine>` and `<polygon>` is the polygon will connect the start point and end point

### text
```htmlembedded=
<text x="420" y="90" fill="rgba(74,144,226)" font-size="40">Hello D3</text>
```
![](https://i.imgur.com/NEMxAow.png)


## Group graph <g></g>
Using `<g></g>` can make the same change/define of objects within the container 
```htmlembedded=
<svg>
    <g fill="#50E3C2" transform="translate(100,50) rotate(-10)">
        <circle cx="100" cy="400" r="50"></circle>
        <rect x="180" y="450" width="100" height="100"></rect>
    </g>
</svg>
```
![](https://i.imgur.com/J8OdLtl.png)



```htmlembedded=
<!DOCTYPE html>
<html lang="zh-Hant-TW">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://d3js.org/d3.v6.min.js"></script>
    <title>D3.js Data Visualization</title>
</head>

<body>
    <svg width="1000" height="1000">
        <rect x="100" y="50" width="120" height="60" fill="rgb(74,144,226)" />
        <circle cx="160" cy="180" r="50" fill="rgb(74,144,226)" />
        <ellipse cx="160" cy="300" rx="70" ry="45" fill="rgb(74,144,226)" />
        <line x1="260" y1="50" x2="390" y2="110" style="stroke: rgb(74,144,226); stroke-width: 3px" />
        <polygon points="270,140 330,230 390,140" style="fill: rgb(200, 247, 244); stroke:red; stroke-width: 3px" />
        <polyline points="300 300 600 300 600 200" style="fill: rgb(200, 247, 244); stroke:red; stroke-width: 3px" />
        <text x="420" y="90" fill="rgba(74,144,226)" font-size="40">Hello D3</text>
        <g fill="#50E3C2" transform="translate(100,50) rotate(-10)">
            <circle cx="100" cy="400" r="50"></circle>
            <rect x="180" y="450" width="100" height="100"></rect>
        </g>
    </svg>
</body>

</html>
```




## Practice
Draw the following graph 
![](https://i.imgur.com/E2NkMTq.png)


```htmlembedded=
<!-- problem 2 -->
<!DOCTYPE html>
<html lang="zh-Hant-TW">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://d3js.org/d3.v6.min.js"></script>
    <title>D3.js Data Visualization</title>
</head>
<body>
    <svg width="500" height="500">
        <circle cx="80" cy="80" r="50" stroke="black" stroke-width="4"fill="red"></circle>
        <polyline
          points="150,130 205,40 260,130 150,130"
          style="fill: yellow; stroke: black; stroke-width: 4;"
        />
        <rect x="290" y="40" width="90" height="90"
        style="fill:green;stroke-width:3;stroke:rgb(0,0,0)"/>
      </svg>
</body>
</html>
```

```htmlmixed=
<!-- problem 2 -->
<!DOCTYPE html>
<html lang="zh-Hant-TW">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://d3js.org/d3.v6.min.js"></script>
    <title>D3.js</title>
</head>
<body>
    <svg width="500" height="500">
      <g>
        <rect x="80" y="80" width="340" height="160" style="fill:#F3ECE0" />
        <line x1="100" y1="100" x2="400" y2="100" style="stroke: #333333; stroke-width: 2px"/>    
        <line x1="100" y1="130" x2="400" y2="130" style="stroke: #333333; stroke-width: 2px"/>    
        <line x1="100" y1="160" x2="400" y2="160" style="stroke: #333333; stroke-width: 2px"/>    
        <line x1="100" y1="190" x2="400" y2="190" style="stroke: #333333; stroke-width: 2px"/>    
        <line x1="100" y1="220" x2="400" y2="220" style="stroke: #333333; stroke-width: 2px"/>    
        <line x1="257" y1="100" x2="257" y2="175" style="stroke: #333333; stroke-width: 6px"/>
        <circle cx="245" cy="175" r="15" fill="#333333"/>
      </g>
    </svg>
</body>
</html>
```