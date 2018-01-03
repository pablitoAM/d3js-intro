# D3js Introduction
Basic exercises with D3js

* Exercise 1: Using the browser console start playing with D3JS
* Exercise 2: Create a kind of Mickey Mouse head in SVG

## Notes

The main cycle using D3js is always

`selectAll` -> `data` -> `enter` -> `append`

Example: Generate 5 circles
```
    const svg = d3.select("svg");

    let radius = [3, 6, 9, 12, 15];

    svg.selectAll("circle") // find or select all circles in the SVG: initally none
        .data(radius)       // bind the data in radius array
        .enter()            // create placeholders to hold the data: five in this case
        .append("circle")   // fill the placeholders with circles: create five circles
        .text(d => d)
```