<template>
  <div>
    <div v-if="editing">
      <input v-model="editingText" @keyup.enter="saveEdit" @keyup.esc="cancelEdit" />
      <button @click="saveEdit">Save</button>
      <button @click="cancelEdit">Cancel</button>
    </div>
    <div v-else>
      <input type="checkbox" v-model="todo.done" />
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="edit">Edit</button>
      <button @click="$emit('delete')">Delete</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['todo'],
  data() {
    return {
      editing: false,
      editingText: "",
    };
  },
  methods: {
    edit() {
      this.editing = true;
      this.editingText = this.todo.text;
    },
    saveEdit() {
      this.editing = false;
      this.$emit('edit', this.editingText);
    },
    cancelEdit() {
      this.editing = false;
      this.editingText = this.todo.text;
    },
  },
};
</script>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
