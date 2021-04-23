# D3 Add, Delete, Trigger

HTML DOM (Document Object Model)
![](https://i.imgur.com/IiKxfy0.png)

## append() : Add element
```htmlembedded=
<!DOCTYPE html>
<html lang="zh-Hant-TW">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://d3js.org/d3.v6.min.js"></script>    
    <link rel="stylesheet" type="text/css" href="./css/styles.css" />
    <title>D3.js</title>
</head>

<body>
    <h3> Items list</h3>
    <ul id="list">
      <li class="item"> Item 1</li>
      <li class="item"> Item 2</li>
      <li class="item"> Item 3</li>
      <li class="item"> Item 4</li>
    </ul>
    <script src="./js/app.js"></script>
</body>
</html>
```
./js/app.js
```javascript=
d3.selectAll(".item")
  .append("strong")
  .text(" Recommend");
  
//different order 
d3.selectAll(".item")
  .text(" Recommend")
  .append("strong");
```
![](https://i.imgur.com/H0vnygr.png)


> The connect order will cause difference


## remove() : Remove element
```javascript=
//remove()
d3.select("#list")
  .select(".item:nth-child(3)") // select the 2nd .item
  .remove();
```
![](https://i.imgur.com/Q9BTk2v.png)

## insert() : insert element
```javascript=
//insert()
d3.select("#list")
  .insert("div", ".item:nth-child(3)")
  .text("Custom Item");
```
![](https://i.imgur.com/0yKwDX3.png)

![](https://i.imgur.com/iardBFi.png)
