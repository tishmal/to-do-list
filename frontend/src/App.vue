<template>
  <div class="app-wrapper">
    <img id="logo" alt="DMark logo" src="./assets/images/dmark.png"/>

    <div class="app-container">
      <h1 class="title">DMARK To-Do</h1>

      <!-- Поле ввода задач -->
      <TodoInput @add-task="handleAddTask" />

      <!-- Список задач -->
      <ul class="task-list">
        <li v-for="task in tasks" :key="task.id" :class="{ completed: task.completed }">
          <span @click="toggleTask(task.id)" class="task-text">{{ task.text }}</span>
          <button class="delete-btn" @click="handleRemoveTask(task.id)">✖</button>
        </li>
      </ul>
    </div>
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
      if (!taskText.trim()) return;
      this.tasks.push({
        id: Date.now(),
        text: taskText,
        completed: false,
      });
    },
    handleRemoveTask(taskId) {
      this.tasks = this.tasks.filter(task => task.id !== taskId);
    },
    toggleTask(taskId) {
      const task = this.tasks.find(t => t.id === taskId);
      if (task) task.completed = !task.completed;
    },
  },
};
</script>

<style scoped>
.app-wrapper {
  background-color: #0a0a0a;
  min-height: 100vh;
  padding: 2rem;
  font-family: 'Arial', sans-serif;
  color: white;
  display: flex;
  flex-direction: column;
  align-items: center;
}

#logo {
  width: 120px;
  height: auto;
  margin: 1rem 0 2rem;
}

.title {
  font-size: 2rem;
  text-align: center;
  margin-bottom: 2rem;
  color: #ffcc00;
  text-shadow: 0 0 8px #ffcc00;
}

.task-list {
  margin-top: 1.5rem;
  list-style: none;
  padding: 0;
  width: 100%;
  max-width: 400px;
}

.task-list li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.5rem 1rem;
  border: 1px solid #333;
  border-radius: 8px;
  margin-bottom: 0.5rem;
  transition: all 0.3s ease;
  background: linear-gradient(90deg, #111 0%, #1a1a1a 100%);
}

.task-list li.completed .task-text {
  text-decoration: line-through;
  color: #888;
}

.task-text {
  cursor: pointer;
  flex: 1;
}

.delete-btn {
  background-color: #ff4d4f;
  border: none;
  color: white;
  padding: 0.2rem 0.5rem;
  border-radius: 5px;
  cursor: pointer;
  margin-left: 1rem;
  transition: transform 0.2s ease, background-color 0.2s ease;
}

.delete-btn:hover {
  transform: scale(1.2);
  background-color: #ff7875;
}
</style>
