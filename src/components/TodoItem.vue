<template>
  <div>
    <!-- <div v-if="editing">
      <input v-model="editingText" @keyup.enter="saveEdit" @keyup.esc="cancelEdit" />
      <button @click="saveEdit">Save</button>
      <button @click="cancelEdit">Cancel</button>
    </div> -->
    <!-- <div v-else>
      <input type="checkbox" v-model="todo.done" />
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="edit">Edit</button>
      <button @click="$emit('delete')">Delete</button>
    </div> -->
    <!-- <v-row align="center">  
        <v-col cols="1"> 
          <v-checkbox-btn 
            v-model="todo.done" 
          ></v-checkbox-btn>
        </v-col>
        <span :class="{ done: todo.done }">{{ todo.text }}</span>
        <button @click="edit">Edit</button>
        <button @click="$emit('delete')">Delete</button>  
    </v-row> -->

    <v-layout class="align-center" v-if="editing" style="height: 40px">
      <v-flex class="flex-grow-1 flex-shrink-0">
        <input v-model="editingText" @keyup.enter="saveEdit" @keyup.esc="cancelEdit" style="width: -webkit-fill-available; padding: 0 10px;" class="mr-5" />
      </v-flex>  
      <v-btn @click="saveEdit" icon="mdi-content-save-all" size="x-small" class="mr-3"></v-btn>
      <v-btn @click="cancelEdit" icon="mdi-cancel" size="x-small"></v-btn>
    </v-layout>

    <v-layout class="align-center" v-else style="height: 40px">
      <v-flex>
        <v-checkbox-btn v-model="todo.done"></v-checkbox-btn>
      </v-flex>
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <v-spacer />
      <v-btn @click="edit" icon="mdi-book-edit" size="x-small" class="mr-3"></v-btn>
      <v-btn @click="$emit('delete')" icon="mdi-delete-alert" size="x-small"></v-btn>
    </v-layout>
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
