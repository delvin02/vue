<template>
  <div class="h-screen flex place-items-center min-w-min min-h-screen">
    <div class="p-10 mx-auto bg-[#242424] rounded z-10">
      <ToDos v-bind:toDoList="toDoList" @delete-todo-event="deleteToDoItem" />
      <SubmitToDoButton @add-todo-event="addToDoItem" />
    </div>
    <Fireworks
      :options="fireworksOptions"
      ref="fw"
      class="absolute inset-0 z-0"
    />
  </div>
</template>
<script>
import { Fireworks } from "@fireworks-js/vue";
import ToDos from "./components/ToDos.vue";
import SubmitToDoButton from "./components/SubmitToDoButton.vue";

export default {
  name: "App",
  components: {
    ToDos,
    Fireworks,
    SubmitToDoButton,
  },
  data() {
    return {
      title: "To Do List",

      fw: null,
      fireworksOptions: {
        // firework configurations
        opacity: 0.5,
        explosion: 8,
        intensity: 6,
        rocketSpawnInterval: 3000,
        particles: 200,
      },
      toDoList: [
        {
          id: 1,
          title: "a sammeln",
          completed: false,
        },
        {
          id: 2,
          title: "zInfos sammeln",
          completed: false,
        },
        {
          id: 3,
          title: "c Infos sammeln",
          completed: false,
        },
      ],
    };
  },
  created() {
    document.title = this.title;
  },
  methods: {
    addToDoItem(newToDoItem) {
      this.toDoList = [...this.toDoList, newToDoItem];
    },
    deleteToDoItem(toDoId) {
      this.toDoList = this.toDoList.filter((item) => item.id !== toDoId);
    },
  },
};
</script>
