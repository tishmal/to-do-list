<template>
  <div class="todo-input-wrapper">
    <input
      v-model="taskText"
      type="text"
      placeholder="Добавьте новую задачу"
      @keyup.enter="addTask"
    />
    <button @click="addTask">Добавить</button>
  </div>
</template>

<script>
export default {
  name: "TodoInput",
  data() {
    return {
      taskText: "",
    };
  },
  methods: {
    addTask() {
      if (!this.taskText.trim()) return; // валидация пустого ввода
      this.$emit("add-task", this.taskText);
      this.taskText = ""; // очищаем поле
    },
  },
};
</script>
