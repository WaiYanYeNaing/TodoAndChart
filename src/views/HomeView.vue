<template>
  <v-row justify="center" align="center" style="height: 100vh">
    <v-col cols="12" sm="4">
      <v-text-field rounded="xl" append-inner-icon="mdi-magnify" :loading="loading" density="compact" variant="solo" label="Search" single-line hide-details
        v-model="search" @keydown="searchHandler()"></v-text-field>

      <v-text-field rounded="xl" class="mt-5" density="compact" variant="solo" @keyup.enter="addTodo" label="Add a new task" v-model="newTodo" ></v-text-field>

      <div v-for="(todo, index) in filteredTodos" :key="index">
        <TodoItem :todo="todo" @delete="deleteTodo(index)" @edit="editTodo(index, $event)" />
      </div>
 
      <v-btn-toggle class="mt-5" style="height: 38px;">
        <v-btn @click="filterTodos('all')" rounded="xl" variant="outlined" class="mx-2">All</v-btn>
        <v-btn @click="filterTodos('complete')" rounded="xl" variant="outlined" class="mx-2">Complete</v-btn>
        <v-btn @click="filterTodos('incomplete')" rounded="xl" variant="outlined" class="mx-2">Incomplete</v-btn>
      </v-btn-toggle> 
    </v-col>
  </v-row>
</template>

<script>
import TodoItem from '../components/TodoItem.vue';

export default {
  components: {
    TodoItem,
  },
  data() {
    return {
      loading: false,
      newTodo: '',
      search: '',
      todos: [{ text: "Lorem Todos", done: false }],
      editingIndex: -1,
      editingText: '',
      filter: 'all',
    };
  },
  methods: {
    searchHandler() {
      this.loading = true;
      setTimeout(() => this.loading = false, 2000);
    },
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todos.push({ text: this.newTodo, done: false });
        this.newTodo = '';
      }
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
    },
    editTodo(index, newText) {
      this.editingIndex = index;
      this.editingText = newText;
      this.saveEdit();
    },
    saveEdit() {
      if (this.editingText.trim() !== '') {
        this.filteredTodos[this.editingIndex].text = this.editingText;
        this.editingIndex = -1;
        this.editingText = '';
      }
    },
    filterTodos(filterType) {
      this.filter = filterType;
    },
  },
  computed: {
    filteredTodos() {
      if (this.filter === 'all') {
        return this.todos.filter(todo => todo.text.toLowerCase().includes(this.search.toLowerCase()));
      } else if (this.filter === 'complete') {
        return this.todos.filter(todo => todo.done && todo.text.toLowerCase().includes(this.search.toLowerCase()));
      } else if (this.filter === 'incomplete') {
        return this.todos.filter(todo => !todo.done && todo.text.toLowerCase().includes(this.search.toLowerCase()));
      }
    },
  },
};
</script>
