# D3 Animation


## transition()
* change shape
```javascript=
d3.select("body")
  .append("svg")
  .append("rect")
  .attr("fill", "rgb(74,144,226)")
  .attr("height", 50)
  .attr("width", 50)
  //change the shape 
  .transition()
  .attr("width", 100)
  //change seperately
  .transition()
  .attr("width", 300)
  .transition()
  .attr("width", 100)
  .transition()
  .attr("width", 50);
```
![](https://i.imgur.com/jaedCk1.gif)

* change color
```javascript=
d3.select("body")
  .append("svg")
  .append("rect")
  .attr("width", 300)
  .attr("height", 50)
  .attr("fill", "pink")
  .transition()
  .attr("fill", "lightblue");
```
![](https://i.imgur.com/x4OkG6F.gif)

* move
```javascript=
d3.select("body")
  .append("svg")
  .append("circle")
  .attr("cx", 50)
  .attr("cy", 50)
  .attr("r", 30)
  .attr("fill", "rgb(74,144,226)")
  .transition()
  .attr("cx", 250);
```
![](https://i.imgur.com/8x2ama2.gif)


Combine all above
```javascript=
d3.select("body")
  .append("svg")
  .append("rect")
  .attr("fill", "red")
  .attr("width", 100)
  .attr("height", 100)
  .transition()
  //change the shape 
  .attr("width", 300)
  //change seperately
  .transition()
  .attr("height", 50)
  //change the color
  .attr("fill", "blue");
```
![](https://i.imgur.com/zF1PT3G.gif)
```javascript=
d3.select("body")
  .append("svg")
  .append("circle")
  .attr("fill", "red")
  .attr("cx", 50)
  .attr("cy", 50)
  .attr("r",30)
  .transition()
  .attr("cx",250)
  .attr("fill","yellow")
  .transition()
  .attr("cy",100)
  .attr("fill","purple")

```
![](https://i.imgur.com/A7ZE4Os.gif)


## duration(), delay()
* The default time is 0.25s (2500ms)
* duration(250)
```javascript=
d3.select("body")
  .append("svg")
  .append("circle")
  .attr("cx", 50)
  .attr("cy", 50)
  .attr("r", 30)
  .attr("fill", "rgb(74,144,226)")
  .transition()
  //Animation continue 1 s
  .duration("1000")
  // delay 0.8s
  .delay("800")
  .attr("cx", 250);
```
![](https://i.imgur.com/Ve0aKuq.gif)


## easing 
線性過渡(easing): 一段動畫在相同時間，以不同的速度執行，讓效果更真實/更多元
[![](https://i.imgur.com/JXWdtSJ.png)](https://easings.net/)


Common ease function
* d3.easeLinear(t)
* d3.easePolyIn(t)
* d3.easePolyOut(t)
* d3.easePoly(t)
* d3.easePolyInOut(t)
* d3.easeQuadIn(t)
* d3.easeQuadOut(t)

![](https://i.imgur.com/1SKhm1s.png)

```javascript=
var svg= d3.select("body")
           .append("svg")
           .attr("width","100%")
  
  svg.append("rect")
     .attr("fill", "#4A90E2")
     .attr("height", 25)
     .attr("width", 50)
     .transition()
     .duration(2000)
     .ease(d3.easeBounce)
     .attr("width", 300);

  // other effect
  //  d3.easeLinear
  //  d3.easeQuad
  //  d3.easeCubic
  //  d3.easeExp
```
easeBounce
![](https://i.imgur.com/T1CWcYm.gif)

[![](https://i.imgur.com/xEXrcCD.gif)](https://www.oxxostudio.tw/articles/201501/svg-d3-14-transition-1.html)

