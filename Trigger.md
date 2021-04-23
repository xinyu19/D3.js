# Trigger: on()

## Click Event
HTML
```htmlembedded=
<body>
    <h1 id="content"> Good morning!</h1>
    <script src="./js/app.js"></script>
</body>
```
### Change the console
./js/app.js
```javascript=
d3.select("#content").on("click",() => {
  console.log("hello world");
})
```
![](https://i.imgur.com/wkyTlC8.gif)


### Change the content
```javascript=
d3.select("#content").on("click" ,e => {
    d3.select(e.currentTarget).text("Good night");
  })
```

![](https://i.imgur.com/5AFy6yF.gif)


## Mouse Event (mouseover/mouseout)
HTML
```htmlembedded=
<body>
    <svg width="400" height="400">
        <rect/>
    </svg>
    <script src="./js/app.js"></script>
</body>
```
D3.js
```javascript=
d3.select("svg").style("background", "#58C7D4");

d3.select("rect")
  .attr("fill", "dark")
  .attr("x", 200)
  .attr("y", 100)
  .attr("width", 100)
  .attr("height", 100)
  .on("mouseover",e => {
    d3.select(e.currentTarget).attr("fill", "yellow");
  })
  .on("mouseout",e => {
    d3.select(e.currentTarget).attr("fill", "blue");
  });
```
![](https://i.imgur.com/GT3x7tp.gif)


## Keyboard Event 
* Keyup/ Keydown (any key)
```javascript=
d3.select("svg").style("background", "#58C7D4");

d3.select("rect")
  .attr("fill", "black")
  .attr("x", 200)
  .attr("y", 100)
  .attr("width", 100)
  .attr("height", 100);

d3.select("body")
  .on("keydown", () => {
    d3.select("rect").attr("fill", "yellow");
  })
  .on("keyup", () => {
    d3.select("rect").attr("fill", "green");
  });
```
![](https://i.imgur.com/hcc0EHh.gif)



* Specific Key
```javascript=
d3.select("svg").style("background", "#58C7D4");

var rect = d3
  .select("rect")
  .attr("fill", "Red")
  .attr("x", 200)
  .attr("y", 100)
  .attr("width", 100)
  .attr("height", 100);

// When Press the Key "A"
d3.select("body")
  .on("keydown", e => {
    // console.log(e);
    //A = "65", from KeyCode list
    if (e.keyCode === 65) {
      rect.attr("fill", "yellow");
    }
  })
```
![](https://i.imgur.com/WykjpHf.gif)

## touch Event
* chnage the color

HTML
```htmlembedded=
<body>
    <svg width="400" height="400">
        <rect />
    </svg>
    <script src="./js/app.js"></script>
</body>
```
```javascript=
d3.select("svg").style("background", "#58C7D4");

d3.select("rect")
  .attr("fill", "red")
  .attr("x", 200)
  .attr("y", 100)
  .attr("width", 100)
  .attr("height", 100);

d3.select("body")
  .on("touchstart", () => {
    d3.select("rect").attr("fill", "yellow");
  })
  .on("touchend", () => {
    d3.select("rect").attr("fill", "green");
  });
```
![](https://i.imgur.com/LsxixBd.gif)

* move item

HTML
```htmlembedded=
<body>
    <svg width="400" height="400">
        <circle />
    </svg>
    <script src="./js/app.js"></script>
</body>
```

```javascript=
d3.select("svg").style("background", "#58C7D4");

d3.select("circle")
  .attr("fill", "yellow")
  .attr("cx", 200)
  .attr("cy", 100)
  .attr("r", 50)

// touch 
d3.select("body").on("touchmove", e => {
  // console.log(e.touches);
  d3.select("circle")
    .attr("cx", e.touches[0].clientX)
    .attr("cy", e.touches[0].clientY);
});

//center -25, -25
d3.select("body").on("touchmove", e => {
  // console.log(e.touches);
  d3.select("circle")
    .attr("cx", e.touches[0].clientX-25)
    .attr("cy", e.touches[0].clientY-25);
});

```
![](https://i.imgur.com/Y1rcUw3.gif)

> There are two different touch events, the touch location is located in orgin and (-25,-25)

