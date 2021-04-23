# D3 Selector, Attribute 

## Select() vs SelectAll()
* select(): select an assigned element or node
* selectAll() : select all assigned elements or nodes 

```htmlembedded=
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://d3js.org/d3.v6.min.js"></script>
    <title>D3.js Data Visualization</title>
</head>

<body>
    <p>...</p>
    <p>...</p>
    <p>...</p>
    <script src="./js/app.js"></script>
</body>

</html>
```
./js/app.js
```javascript=
// select
d3.select("body").select("p").text("Hello D3");

// selectAll
d3.selectAll("p").text("Hello D3");
```

![](https://i.imgur.com/YOCnnjl.png)



---


## Change HTML attribute: attr()
```htmlembedded=
<!DOCTYPE html>
<html lang="zh-Hant-TW">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://d3js.org/d3.v6.min.js"></script>
    <link rel="stylesheet" type="text/css" href="./css/styles.css" />
    <title>Example</title>
</head>

<body>
    <div class="box">
        <div class="header">
            <img src="img/logo.png" />
            <h1>Apple Inc</h1>
        </div>
        <div class="contentbox">
            <p>蘋果公司（英語：Apple Inc.），原稱蘋果電腦公司（英語：Apple Computer,
                Inc.），是總部位於美國加州庫比蒂諾的跨國科技公司，與亞馬遜，Google、微軟和Facebook一起被認為是五大技術公司之一，合稱為FAAMG。現時的業務包括設計、開發、手機通信和銷售消費電子、電腦軟體、線上服務和個人電腦。
            </p>
            <a href="http://www.apple.com" target="_blank">網站連結</a>
        </div>

    </div>
    <script src="./js/app.js"></script>
</body>

</html>

</html>
```



./js/app.js
```javascript=
d3.select("h1").attr("class", "title");
d3.select("p").attr("class", "content");
d3.select("a").attr("class", "link");
```

> We can see the `<h1>` ,`<p>` , `<a>` added the "class" attribute after we used d3.js 

![](https://i.imgur.com/W9N3z7u.png)



---

## Change CSS Style
* using select to select the element then using style to change/give css style

./js/app.js
```javascript=
d3.select("h1").style("color", "#fff")
               .style("background", "red");
d3.select("p").style("color", "#778899");
d3.select("a").style("color", "red");
```

![](https://i.imgur.com/nqvMBpK.png)


* setting multiples styles
> Using d3-selection-multi:  `<script src="https://d3js.org/d3-selection-multi.v1.min.js"></script>` 

```javascript=
//set multiple styles
//way 1
d3.select("p").style("color","#718b71")
    .style("font-size","16px")
    .style("font-weight","bold")
    .style("text-align","center")

//way 2
d3.select("p")
  .styles({
      "color":"#718b71",
      "font-size":"16px",
      "font-weight":"bold",
      "text-align":"center"
  })
// it is also used in attrs({})
```
![](https://i.imgur.com/HAksUrF.png)
