# D3js Introduction
Basic exercises with D3js

* Exercise 1: Using the browser console start playing with D3JS
* Exercise 2: Create a kind of Mickey Mouse head in SVG
* Exercise 3: Create random circles from data
* Exercise 4: Add transition to the circles
* Exercise 5: Playing with the scales
* Exercise 6: Scatterplot

## Notes

### Basic Usage

The main cycle using D3js is always

`selectAll` -> `data` -> `enter` -> `append`

Example: Generate 5 circles
```
    let svg = d3.select("body")
        .append("svg")
        .attr("width", 400)
        .attr("height", 400);

    let radius = [3, 6, 9, 12, 15];

    svg.selectAll("circle") // find or select all circles in the SVG: initally none
        .data(radius)       // bind the data in radius array
        .enter()            // create placeholders to hold the data: five in this case
        .append("circle")   // fill the placeholders with circles: create five circles
        .text(d => d)
```

Example: Updating the 5 circles 
```
    let newRadius = [10, 20, 30, 40, 50];

    svg.selectAll("circle")
    .data(radius);
```

### Transitions

`transtion` -> `duration`

Example: Transition a circle
```
    let svg = d3.select("body")
        .append("svg")
        .attr("width", 400)
        .attr("height", 400);

    svg.append("circle")            // creating a circle
        .attr("cx", 100)            // initial attributes
        .attr("cy", 100)
        .attr("r", 50)
        .attr("fill", "black")
        .transition()               // definition of transition
        .delay(100)                 // It will start after 100 ms       
        .duration(2000)             // It will length 2000 ms
        .attr("cx", 200)            // final attributes
        .attr("cy", 0)
        .attr("r", 25)
        .attr("fill", "green");
```

### Scales

Creates a function which maintains the aspect ratio of two arrays of values. For example:

* Domain values: [0, 0.1, 0.2, 0.3, 0.4, 0.7, 1] --> min = 0 and max = 1.

If we want to paint these values as radius of circles in a SVG we'll need to multiply them for a ratio
in order to get the minimum values to paint. (We don't want to paint a circle of radius 0.1. Too small).

For that we "map" the Domain values to some Range values

* Range: [748, 1024]

These are the destination values. With a Scale function we will map automatically from 0 to 748 and from 1 to 1024 and the library will calculate automatically all the intermediate values.

Example: Scaling numbers
```
    const dataset = [0, 0.1, 0.2, 0.3, 0.4, 0.7, 1];

    let min = d3.min(dataset);  // min of the dataset
    let max = d3.max(dataset);  // max of the dataset

    const svgMinHeight = 748,
          svgMaxHeight = 1024;

    const xScale = d3.scaleLinear()           // xScale is a function.
                    .domain([min, max])
                    .range([svgMinHeight, svgMaxHeight]);

    console.log(xScale(0));     // 748
    console.log(xScale(1));     // 1024
    console.log(xScale(0.2));   // 803.2
```

Example: Scaling objects with properties
```
    const dataset = [
        { h: 100, w: 100, r: 100},
        { h: 10,  w: 10,  r: 10},
        { h: 200, w: 10,  r: 50},
        { h: 150, w: 50,  r: 200}
    ];

    let min = d3.min(dataset, d => d.h);    // min of h in the dataset: 10
    let max = d3.max(dataset, d => d.h);    // max or r in the dataset: 200

    const svgMinHeight = 748,
          svgMaxHeight = 1024;

    const xScale = d3.scaleLinear()           // xScale is a function.
                    .domain([min, max])
                    .range([svgMinHeight, svgMaxHeight]);

    console.log(xScale(0));     // 733.4736842105264
    console.log(xScale(10));    // 748
    console.log(xScale(50));    // 806.1052631578947
```