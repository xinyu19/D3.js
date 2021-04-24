# Import Data 

## JSON File
![](https://i.imgur.com/WR8ejaM.png)

### d3.json()
* import .json file
![](https://i.imgur.com/sS0oLks.png)


* Get the API 
```javascript=
// Open Data API
var url = "https://raw.githubusercontent.com/kiang/pharmacies/master/json/points.json";

// if already download json file
// var url = "./data/count.json"

// Connect the API to get the data
d3.json(url).then((data) => {
  console.log(data);
});
```
![](https://i.imgur.com/ksKofUu.png)


* Use Array to collect the data in order to read and use easily
```javascript=
// Data Array
var dataArray = [];

// Connect API to get the data
d3.json(url).then((data) => {
  // console.log(data);
  // console.log(data.features);
  // console.log(data.features[0])
  // console.log(data.features[0].properties
  var dataset = data.features;
  for (var i = 0; i < 20; i++) {https://i.imgur.com/XZnmCTZ.png
    var element = dataset[i];
    dataArray.push(element.properties);
  }
  console.log(dataArray);
});
```
![](https://i.imgur.com/uLLoqMM.png)

### Error
![](https://i.imgur.com/h7RbBdR.png)
```javascript=
var url =
  "https://raw.githubusercontent.com/kiang/pharmacies/master/json/pointss.json";

fetch(url)
  .then(response => {
    console.log(response);
    if (response.status === 200) {
      return response.json();
    }
  })
  .then(jsonData => {
    console.log(jsonData);
  })
  .catch(err => {
    console.log("Error: ", err);
  });

d3.json(url)
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.log(error);
  });

```


![](https://i.imgur.com/YZbIg8n.png)

![](https://i.imgur.com/5I4JyR2.png)





### import other data type
* d3.xml()
* d3.csv()
* d3.html()
* d3.tsv()
* d3.text()


### Practice
Get the json file from `".../json/count.json"`, bd save players name and their championship into different arrays

Count.json
```json=
[
        {
            "player": "James",
            "championship": "3"
        },
        {
            "player": "Kobe",
            "championship": "5"
        },		
        {
            "player": "Duncan",
            "championship": "5"
        },	 
        {
            "player": "Jordon",
            "championship": "6"
        }		
]
```
Answer:
```javascript=
var nameArray = [];
var champArray = [];

// Connect API to get the data
d3.json("./data/count.json").then(function(data){
  console.log(data)
  for (var i = 0; i < 4; i++){
    nameArray.push(data[i].player);
    champArray.push(data[i].championship);
  }
  console.log(nameArray);
  console.log(champArray);
}).catch(error => {
  console.log(error);
});
```



## Postman 
* we could use postman "Get" to get data from API
* Download：https://www.getpostman.com/apps
* Chrome: https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop?hl=zh-TW

![](https://i.imgur.com/XZnmCTZ.png)
