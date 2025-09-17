<template>
  <img id="logo" alt="Wails logo" src="./assets/images/logo-universal.png"/>
  <HelloWorld/>

  <div>
    <TodoInput @add-task="handleAddTask" />
    <ul class="mt-6 space-y-2">
      <li v-for="task in tasks" :key="task.id" class="text-white">
        {{ task.text }}
      </li>
    </ul>
  </div>
</template>

<script>
import TodoInput from "./components/TodoInput.vue";

export default {
  components: { TodoInput },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    handleAddTask(taskText) {
      this.tasks.push({
        id: Date.now(),
        text: taskText,
        completed: false,
      });
    },
  },
};
</script>


<style>
#logo {
  display: block;
  width: 50%;
  height: 50%;
  margin: auto;
  padding: 10% 0 0;
  background-position: center;
  background-repeat: no-repeat;
  background-size: 100% 100%;
  background-origin: content-box;
}
</style>
