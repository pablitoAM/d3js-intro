# D3js Introduction
Basic exercises with D3js

* Exercise 1: Using the browser console start playing with D3JS
* Exercise 2: Create a kind of Mickey Mouse head in SVG
* Exercise 3: Create random circles from data
* Exercise 4: Add transition to the circles

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

### Transitions

`transtion` -> `duration`

Example: Transition a circle
```
    let svg = d3.select("body")
        .append("svg")
        .attr("width", 400)
        .attr("height", 400);

    svg.append("circle")
        .attr("cx", 100)
        .attr("cy", 100)
        .attr("r", 50)
        .attr("fill", "black")
        .transition()
        .duration(2000)
        .attr("cx", 200)
        .attr("cy", 0)
        .attr("r", 25)
        .attr("fill", "green");
```