<template>
  <div class="app-wrapper">
    <img id="logo" alt="DMark logo" src="./assets/images/dmark.png"/>

    <div class="app-container">
      <h1 class="title">DMARK To-Do</h1>

      <!-- Поле ввода задач -->
      <TodoInput @add-task="handleAddTask" class="todo-input-wrapper" />

      <!-- Фильтр -->
      <div class="filter-buttons">
        <button @click="filter='all'" :class="{active: filter==='all'}">Все</button>
        <button @click="filter='active'" :class="{active: filter==='active'}">Активные</button>
        <button @click="filter='completed'" :class="{active: filter==='completed'}">Выполненные</button>
      </div>

      <!-- Сортировка -->
      <div class="sort-buttons">
        <button @click="sortOrder='asc'" :class="{active: sortOrder==='asc'}">По возрастанию</button>
        <button @click="sortOrder='desc'" :class="{active: sortOrder==='desc'}">По убыванию</button>
      </div>

      <!-- Список задач -->
      <ul class="task-list">
        <li v-for="task in sortedTasks" :key="task.id" :class="{ completed: task.completed }">
          <input type="checkbox" v-model="task.completed" :disabled="task.completed" />
          <span class="task-text">{{ task.text }}</span>
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
      filter: 'all',
      sortOrder: 'asc'
    };
  },
  computed: {
    filteredTasks() {
      if (this.filter === 'all') return this.tasks;
      if (this.filter === 'active') return this.tasks.filter(t => !t.completed);
      if (this.filter === 'completed') return this.tasks.filter(t => t.completed);
    },
    sortedTasks() {
      return [...this.filteredTasks].sort((a, b) => {
        if (this.sortOrder === 'asc') return a.createdAt - b.createdAt;
        return b.createdAt - a.createdAt;
      });
    },
  },
  methods: {
    handleAddTask(taskText) {
      if (!taskText.trim()) return;
      this.tasks.push({
        id: Date.now(),
        text: taskText,
        completed: false,
        createdAt: Date.now(),
      });
    },
    handleRemoveTask(taskId) {
      this.tasks = this.tasks.filter(task => task.id !== taskId);
    },
  },
};
</script>