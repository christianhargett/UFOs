# UFOs

## Overview

### In this project we are helping our customer, Dana, who is a data journalist from McMinnville, Oregon. McMinnville is famous for its UFO sightings and even hosts an annual gathering for UFO enthusiasts. As such, Dana is extremely interested in this topic and she wants us to create a webpage that will allow users to sort through data regarding UFO sightings across North America. After utilizing JavaScript, HTML, CSS, and Bootstrap we have built a website that displays [UFO sighting data](https://github.com/christianhargett/UFOs/blob/master/static/js/data.js) in a table format. We are even able to filter this table for specific dates that the UFO sighting took place. In order to build this webpage we utilized three different files: a JavaScript file, an HTML file, and another JS file that contains our source data. In the JS file we imported the source data of UFO sightings. We then utilized the D3 library in order to grab the "tbody" tag from our HTML file. After this, we created a function that builds a table to holds all of our data that will eventually be displayed on the webpage. We did this by looping through each object in our data, and for each loop we appended one table row to the table. We then looped through each field in every row and appended the data into each column. The entire code snippet is displayed below:

```
// import the data from data.js
const tableData = data;

// Reference the HTML table using D3
var tbody = d3.select('tbody');

function buildTable(data) {
    // First, clear out any existing data
    tbody.html("");
  
    // Next, loop through each object in the data
    // and append a row and cells for each value in the row
    data.forEach((dataRow) => {
      // Append a row to the table body
      let row = tbody.append("tr");
  
      // Loop through each field in the dataRow and add
      // each value as a table cell (td)
      Object.values(dataRow).forEach((val) => {
        let cell = row.append("td");
        cell.text(val);
        }
      );
    });
  }
  ```

### Dana has asked us to update our code so that the webpage also contains filters for city, state, country, and shape of the sighted UFO. 
