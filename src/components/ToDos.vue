<script setup>
import ToDoItem from "./ToDoItem.vue";
</script>

<template>
  <div>
    <h1 class="text-3lg mb-10">To Do List</h1>
    <ul>
      <li
        v-bind:key="item.id"
        v-for="item in sortArray()"
        @delete-todo-event="deleteToDoItem"
      >
        <ToDoItem
          v-bind:todoItem="item"
          @delete-todo-event="$emit('delete-todo-event', item.id)"
        />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "ToDos",
  components: {
    ToDoItem,
  },
  methods: {
    sortArray: function () {
      return this.toDoList.slice().sort(function (a, b) {
        return a.title > b.title ? 1 : -1;
      });
    },
  },
  props: ["toDoList"],
};
</script>
