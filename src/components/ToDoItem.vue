<template>
  <div
    v-bind:class="{ completed: todoItem.completed }"
    class="flex justify-between my-2"
  >
    <div class="my-auto mr-3" v-if="!isEditing">
      <p @click="markComplete" class="font-bold text-lg">
        {{ todoItem.title }}
      </p>
    </div>
    <div v-else>
      <!-- v-model -->
      <input
        v-model="updatedTitle"
        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
      />
    </div>
    <div>
      <button
        @click="toggleEdit"
        :class="[isEditing ? 'bg-green-500' : '']"
        class="bg-slate-400 mx-2 p-2"
      >
        {{ isEditing ? "Save" : "Edit" }}
      </button>
      <button
        @click="$emit('delete-todo-event', todoItem.id)"
        class="bg-red-500"
      >
        Delete
      </button>
    </div>
  </div>
</template>

<style>
.completed {
  text-decoration: line-through;
}
</style>
<script>
export default {
  name: "ToDoItem",
  components: {},
  props: ["todoItem"],
  data() {
    return {
      isEditing: false,
      updatedTitle: this.todoItem.title,
    };
  },
  methods: {
    markComplete() {
      this.todoItem.completed = !this.todoItem.completed;
    },
    toggleEdit() {
      if (this.isEditing) {
        this.todoItem.title = this.updatedTitle;
      }
      this.isEditing = !this.isEditing;
    },
  },
};
</script>
