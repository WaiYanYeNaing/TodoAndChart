<template>
  <v-row justify="center" align="center" style="height: 100vh">
    <v-col cols="12" sm="8">
      <!-- Title of the Todo List -->
      <h1 class="font-weight-bold">Todo List</h1>
      <v-row class="mt-10" align="center">
        <!-- Search Input -->
        <v-text-field
          rounded="lg"
          append-inner-icon="mdi-magnify"
          :loading="loading"
          density="compact"
          variant="solo"
          label="Search"
          single-line
          hide-details
          v-model="search"
          @keydown="searchHandler"
          class="mx-2 mb-2"
          style="min-width: 240px"
        ></v-text-field>

        <!-- Filter Buttons -->
        <v-btn-toggle :style="buttonStyle" v-model="active" class="mb-2">
          <v-btn
            @click="filterTodos('all')"
            rounded="xl"
            :color="buttonColor('all')"
            :class="buttonClass"
            :style="buttonFontSize"
          >
            All
          </v-btn>
          <v-btn
            @click="filterTodos('complete')"
            rounded="xl"
            :color="buttonColor('complete')"
            :class="buttonClass"
            :style="buttonFontSize"
          >
            Done
          </v-btn>
          <v-btn
            @click="filterTodos('incomplete')"
            rounded="xl"
            :color="buttonColor('incomplete')"
            :class="buttonClass"
            :style="buttonFontSize"
          >
            Incomplete
          </v-btn>
        </v-btn-toggle>
      </v-row>

      <!-- Add Todo Input -->
      <v-text-field
        rounded="lg"
        class="mt-5"
        density="compact"
        variant="solo"
        @keyup.enter="addTodo"
        label="Add a new task"
        v-model="newTodo"
      ></v-text-field>

      <!-- Display Todo Items -->
      <div v-for="(todo, index) in filteredTodos" :key="index">
        <TodoItem
          :todo="todo"
          @delete="deleteTodo(index)"
          @edit="editTodo(index, $event)"
        />
      </div>
    </v-col>
  </v-row>
</template>

<script>
import TodoItem from "../components/TodoItem.vue";

export default {
  components: {
    TodoItem,
  },
  data() {
    return {
      loading: false,
      newTodo: "",
      search: "",
      // Array of Todo objects
      todos: [
        { text: "List clear priorities and due dates.", done: false },
        {
          text: "Divide large tasks or projects into small, manageable pieces.",
          done: false,
        },
        { text: "Cross things off your list.", done: false },
        {
          text: "Don't worry if you don't get everything done in the time you wanted to.",
          done: true,
        },
      ],
      editingIndex: -1,
      editingText: "",
      filter: "all",
      active: 0,
    };
  },
  computed: {
    // Filter and display Todos based on search and filter criteria
    filteredTodos() {
      return this.todos.filter((todo) => {
        const lowerCaseSearch = this.search.toLowerCase();
        if (this.filter === "all") {
          return todo.text.toLowerCase().includes(lowerCaseSearch);
        } else if (this.filter === "complete") {
          return todo.done && todo.text.toLowerCase().includes(lowerCaseSearch);
        } else if (this.filter === "incomplete") {
          return (
            !todo.done && todo.text.toLowerCase().includes(lowerCaseSearch)
          );
        }
      });
    },
    buttonStyle() {
      return `height: 38px; ${this.$vuetify.display.xs ? "scale: 90%;" : ""}`;
    },
    buttonClass() {
      return this.$vuetify.display.xs ? "mr-1" : "mx-2";
    },
    buttonFontSize() {
      return `font-size: ${this.$vuetify.display.xs ? "12px" : ""}`;
    },
  },
  methods: {
    // Handle search input
    searchHandler() {
      this.loading = true;
      setTimeout(() => (this.loading = false), 2000);
    },
    // Add a new Todo
    addTodo() {
      if (this.newTodo.trim() !== "") {
        this.todos.push({ text: this.newTodo, done: false });
        this.newTodo = "";
      }
    },
    // Delete a Todo by index
    deleteTodo(index) {
      this.todos.splice(index, 1);
    },
    // Edit a Todo by index and new text
    editTodo(index, newText) {
      this.editingIndex = index;
      this.editingText = newText;
      this.saveEdit();
    },
    // Save edited Todo
    saveEdit() {
      if (this.editingText.trim() !== "") {
        this.filteredTodos[this.editingIndex].text = this.editingText;
        this.editingIndex = -1;
        this.editingText = "";
      }
    },
    // Set the filter criteria for displaying Todos
    filterTodos(filterType) {
      this.filter = filterType;
    },
    // Define button color based on the selected filter
    buttonColor(type) {
      return this.filter === type
        ? type === "all"
          ? "blue"
          : type === "complete"
          ? "success"
          : "error"
        : "";
    },
  },
};
</script>
