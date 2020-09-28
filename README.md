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

### We also created a function in our JS file that allows us to filter by date. This JS file combined with our HTML file creates a webpage that displays all of the UFO sightings data that the user can easily filter by a date of their choice.

### Dana then asked us to update our code so that the webpage also contains filters for city, state, country, and shape of the sighted UFO. In order to do this, we updated our HTML file to remove the filter "button" that we initially created and replaced it with four more additional lists for user input. These inputs were created for users to enter information about state, city, country, and shape (snippet provided below):

```
       <li class="list-group-item bg-dark">
                <label for="date">Enter Date</label>
                <input type="text" placeholder="1/10/2010" id="datetime" />
              </li>

              <li class="list-group-item bg-dark">
                <label for="city">Enter City</label>
                <input type="text" placeholder="benton" id="city" />
              </li>

              <li class="list-group-item bg-dark">
                <label for="state">Enter State</label>
                <input type="text" placeholder="ar" id="state" />
              </li>

              <li class="list-group-item bg-dark">
                <label for="country">Enter Country</label>
                <input type="text" placeholder="us" id="country" />
              </li>

              <li class="list-group-item bg-dark">
                <label for="shape">Enter Shape</label>
                <input type="text" placeholder="circle" id="shape" />
              </li>
```

### We then needed to update our JS file so that the website will respond to these new filter inputs. In order to do this, we created a function that detects if a user input a new filter. If a new input is detected, the key-value pair of data is appended to an empty variable, "filters", that we created outisde of the function. This filter data is used later in our JavaScript file to filter our table. 

### In order to filter our table with the new filter inputs, we had to create another function. To do this we initialized a new variable, "filteredData", and set it equal to our original source data. We then looped through all of our filters that we extracted from the previous function and kept any data that matched these filter values. We then called our original function that sets up the table on the webpage and used our new "filteredData" as an argument. This is what actually filters our table on the webpage when a user inputs a new filter. Finally, using D3 we created a new event that "listens" to when a user inputs a new filter value. These new functions are provided in the code snippet below:

```
// 1. Create a variable to keep track of all the filters as an object.
var filters = {};

// 3. Use this function to update the filters. 
function updateFilters() {

    // 4a. Save the element that was changed as a variable.

    let changedElement = d3.select(this);

    // 4b. Save the value that was changed as a variable.

    let elementValue = changedElement.property("value");
    console.log(elementValue);

    // 4c. Save the id of the filter that was changed as a variable.

    let filterId = changedElement.attr("id");
    console.log(filterId);

  
    // 5. If a filter value was entered then add that filterId and value
    // to the filters list. Otherwise, clear that filter from the filters object.
    if (elementValue) {
        filters[filterId] = elementValue;
    }
    else {
        delete filters[filterId];
    }
  
    // 6. Call function to apply all filters and rebuild the table
    filterTable();
  
  }
  
  // 7. Use this function to filter the table when data is entered.
  function filterTable() {
  
    // 8. Set the filtered data to the tableData.
    let filteredData = tableData;
  
    // 9. Loop through all of the filters and keep any data that
    // matches the filter values
    Object.entries(filters).forEach(([key, value]) => {
        filteredData = filteredData.filter(row => row[key] === value)
        });
  
    // 10. Finally, rebuild the table using the filtered data
    buildTable(filteredData);
  }
  
  // 2. Attach an event to listen for changes to each filter
  d3.selectAll("input").on("change", updateFilters);
  
  // Build the table when the page loads
  buildTable(tableData);
```

## Results

### Our final webpage has a sleek display that contains a "Jumbotron", a navigation bar at the very top labelled "UFO Sightings" that is used to reload the page/reset the filters, a title, and a paragraph that gives an overview of the background for the webpage and what the webpage can be used for. Towards the bottom left of the page are where the user can enter their filters, and towards the bottom right is the table that contains all of the data for the UFO sightings.

![](https://github.com/christianhargett/UFOs/blob/master/NoFilters.png)

### The user is then able to input data in each input box in the filter search. Once the user inputs the data (note: it is important that the user's input matches the placeholder format EXACTLY in order for the filter to work) and hits tab or clicks elsewhere, then the data table will be filtered:

![](https://github.com/christianhargett/UFOs/blob/master/DateFilter.png)

### The user is then able to continue adding filters to each input box and the table will reset to match each filter:

![](https://github.com/christianhargett/UFOs/blob/master/AllFilters.png)
