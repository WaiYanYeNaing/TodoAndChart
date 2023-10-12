<template>
  <div :style="`${$vuetify.display.xs && 'scale: .9'}`">
    <!-- Editing Mode -->
    <v-layout
      class="align-center"
      v-if="editing"
      :style="`min-height: ${$vuetify.display.xs ? 50 : 40}px;`"
    >
      <v-flex class="flex-grow-1 flex-shrink-0">
        <!-- Input field for editing text -->
        <input
          v-model="editingText"
          @keyup.enter="saveEdit"
          @keyup.esc="cancelEdit"
          style="width: -webkit-fill-available; padding: 0 10px"
          class="mr-5"
        />
      </v-flex>
      <!-- Save and Cancel buttons for editing mode -->
      <v-btn
        @click="saveEdit"
        icon="mdi-content-save-all"
        size="x-small"
        class="mr-3"
      ></v-btn>
      <v-btn @click="cancelEdit" icon="mdi-cancel" size="x-small"></v-btn>
    </v-layout>

    <!-- Display Mode -->
    <v-layout
      class="align-center"
      v-else
      :style="`min-height: ${$vuetify.display.xs ? 50 : 40}px;`"
    >
      <v-flex>
        <!-- Checkbox to mark the task as done -->
        <v-checkbox-btn v-model="todo.done"></v-checkbox-btn>
      </v-flex>
      <!-- Display the task text, with a line-through if it's marked as done -->
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <v-spacer />
      <!-- Edit and Delete buttons in display mode -->
      <v-btn
        @click="edit"
        icon="mdi-book-edit"
        size="x-small"
        class="mr-3"
      ></v-btn>
      <v-btn
        @click="$emit('delete')"
        icon="mdi-delete-alert"
        size="x-small"
      ></v-btn>
    </v-layout>
  </div>
</template>

<script>
export default {
  props: ["todo"], // Todo item as a prop
  data() {
    return {
      editing: false, // Flag to determine if the item is in edit mode
      editingText: "", // Text for editing the item
    };
  },
  methods: {
    // Enter edit mode
    edit() {
      this.editing = true;
      this.editingText = this.todo.text;
    },
    // Save changes and exit edit mode
    saveEdit() {
      this.editing = false;
      this.$emit("edit", this.editingText); // Emit an event to save the edit
    },
    // Cancel edit and revert to the original text
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
