
## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
``` 

```sh
Todo List Component
Description: This component displays a todo list with the ability to add, search, edit, and filter todos.

Title: Displays the title "Todo List".
Search Input: Allows users to search for todos.
Filter Buttons: Allows users to filter todos by "All," "Done," or "Incomplete."
Add Todo Input: Lets users add new tasks.
Display Todo Items: Displays the list of todos.
Script
Data: Contains properties for managing todos, search, editing, and filters.
Computed Properties: Filter and style-related computed properties.
Methods:
searchHandler: Handles search input and displays a loading indicator.
addTodo: Adds a new todo to the list.
deleteTodo(index): Deletes a todo based on its index.
editTodo(index, newText): Enters edit mode for a todo.
saveEdit: Saves changes made to an edited todo.
filterTodos(filterType): Sets the filter criteria for displaying todos.
buttonColor(type): Defines button color based on the selected filter.
Todo Item Component
Description: This component represents an individual todo item within the todo list.

Editing Mode: Displays the todo item in editing mode with an input field and save/cancel buttons.
Display Mode: Shows the todo item in display mode with a checkbox for marking as done and edit/delete buttons.
Styling: Applies a line-through style to completed todos.
Script
Props: Receives a "todo" object as a prop.
Data: Manages the editing state and edited text.
Methods:
edit: Enters edit mode for the todo.
saveEdit: Saves changes and exits edit mode.
cancelEdit: Cancels edit and reverts to the original text.
Chart Component
Description: This component displays a chart with dynamic bar heights. 
``` 


```sh
Chart JS

Container: Contains a chart with dynamically positioned images for bars.
Styling: Uses images to represent bar heights with random seed-based colors.
Script
Dependencies: Imports Chart.js and chart-related components.
Data: Includes configuration options for the chart and the bar width.
Mounted Hook: Calls a method to get the width of the chart bar.
Methods:
getWdithOfBar: Retrieves the width of the chart bar element.
Chart Data and Options
Description: This module defines data and options for the chart component.

Data: Contains labels and datasets for the chart.
Options: Configures responsiveness and aspect ratio for the chart.
``` 