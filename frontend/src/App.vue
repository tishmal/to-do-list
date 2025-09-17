<template>
  <img id="logo" alt="Wails logo" src="./assets/images/dmark.png"/>

  <div class="app-container">
    <h1 class="title">Solo Leveling To-Do</h1>

    <TodoInput @add-task="handleAddTask" />

    <ul class="task-list">
      <li v-for="task in tasks" :key="task.id" :class="{ completed: task.completed }">
        {{ task.text }}
      </li>
    </ul>
  </div>
</template>

<script>
import TodoInput from "./components/TodoInput.vue";

export default {
  name: "App",
  components: { TodoInput },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    handleAddTask(taskText) {
      if (taskText.trim() === "") return;
      this.tasks.push({
        id: Date.now(),
        text: taskText,
        completed: false,
      });
    },
  },
};
</script>


<style scoped>
.app-container {
  background-color: #0a0a0a;
  min-height: 100vh;
  padding: 2rem;
  font-family: 'Arial', sans-serif;
  color: white;
}

.title {
  font-size: 2rem;
  text-align: center;
  margin-bottom: 2rem;
}

.task-list {
  margin-top: 1.5rem;
  list-style: none;
  padding: 0;
}

.task-list li {
  padding: 0.5rem 1rem;
  border: 1px solid #333;
  border-radius: 8px;
  margin-bottom: 0.5rem;
  transition: all 0.3s ease;
}

.task-list li.completed {
  text-decoration: line-through;
  color: #888;
}
</style>