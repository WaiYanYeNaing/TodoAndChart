<!-- <template>
  <div>
    <div>
      <input v-model="search" placeholder="Search tasks" />
    </div>
    <div>
      <input v-model="newTodo" @keyup.enter="addTodo" placeholder="Add a new task" />
    </div>
    <div v-for="(todo, index) in filteredTodos" :key="index">
      <TodoItem
        :todo="todo"
        @delete="deleteTodo(index)"
        @edit="editTodo(index, $event)"
      />
    </div>
  </div>
</template>

<script>
import TodoItem from '../components/TodoItem.vue';

export default {
  components: {
    TodoItem,
  },
  data() {
    return {
      newTodo: '',
      search: '',
      todos: [],
      editingIndex: -1,
      editingText: '',
    };
  },
  methods: {
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
      this.saveEdit(index)
    },
    saveEdit(index) {
      if (this.editingText.trim() !== '') {
        this.todos[index].text = this.editingText;
        this.editingIndex = -1;
        this.editingText = '';
      }
    },
    cancelEdit() {
      this.editingIndex = -1;
      this.editingText = '';
    },
  },
  computed: {
    filteredTodos() {
      return this.todos.filter(todo => {
        return todo.text.toLowerCase().includes(this.search.toLowerCase());
      });
    },
  },
};
</script> -->


<template>
  <v-row justify="center" align="center" style="height: 100vh">
    <v-col cols="12" sm="4">
      <v-text-field :loading="loading" density="compact" variant="solo" label="Search" single-line hide-details
        v-model="search" @keydown="searchHandler()"></v-text-field>

      <v-text-field  class="mt-5" density="compact" variant="solo" @keyup.enter="addTodo" label="Add a new task" v-model="newTodo" ></v-text-field>

      <div v-for="(todo, index) in filteredTodos" :key="index">
        <TodoItem :todo="todo" @delete="deleteTodo(index)" @edit="editTodo(index, $event)" />
      </div>
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
      todos: [],
      editingIndex: -1,
      editingText: '',
    };
  },
  methods: {
    searchHandler() {
      this.loading = true

      setTimeout(() => {
        this.loading = false
      }, 2000)
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
      this.saveEdit()
    },
    saveEdit() {
      if (this.editingText.trim() !== '') {
        this.filteredTodos[this.editingIndex].text = this.editingText;
        this.editingIndex = -1;
        this.editingText = '';
      }
    },
    cancelEdit() {
      this.editingIndex = -1;
      this.editingText = '';
    },
  },
  computed: {
    filteredTodos() {
      return this.todos.filter(todo => {
        return todo.text.toLowerCase().includes(this.search.toLowerCase());
      });
    },
  },
};
</script>
