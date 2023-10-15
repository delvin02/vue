<template>
  <div>
    <form @submit="addToDo" class="w-full max-w-sm mt-5">
      <div class="flex items-center border-b border-teal-500 py-2 my-3">
        <input
          type="text"
          class="appearance-none text-center bg-transparent border-none w-full text-white mr-3 py-1 px-2 leading-tight focus:outline-none"
          v-model="title"
          name="title"
        />
      </div>
      <button
        type="submit"
        class="flex-shrink-0 bg-teal-500 hover:bg-teal-700 border-teal-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded"
      >
        Submit
      </button>
    </form>
    <p v-if="error" class="text-red-500 mt-2">
      Please enter a title for the to-do item.
    </p>
  </div>
</template>

<script>
import { v4 as uuidv4 } from "uuid";

export default {
  name: "SubmitToDoButton",
  data() {
    return {
      title: "",
      error: false,
    };
  },
  methods: {
    addToDo(event) {
      event.preventDefault();

      if (this.title.trim() === "") {
        this.error = true;
      } else {
        this.error = false;
        const newToDoObject = {
          id: uuidv4(),
          title: this.title,
          completed: false,
        };

        this.$emit("add-todo-event", newToDoObject);
        this.title = "";
      }
    },
  },
};
</script>
