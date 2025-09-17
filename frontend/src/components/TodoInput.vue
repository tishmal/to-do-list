<template>
  <div class="w-full max-w-md mx-auto mt-10 flex">
    <input
      v-model="taskText"
      type="text"
      placeholder="Добавьте новую задачу"
      class="w-full p-4 bg-gray-800 text-white rounded-l-lg shadow-md
             focus:outline-none focus:ring-2 focus:ring-green-400
             placeholder-gray-400 transition-all duration-300"
      @keyup.enter="addTask"
    />
    <button
      @click="addTask"
      class="p-4 bg-green-500 text-white rounded-r-lg shadow-md hover:bg-green-600 transition-colors duration-300"
    >
      Добавить
    </button>
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

<style scoped>
/* Плавные переходы при фокусе */
input:focus {
  box-shadow: 0 0 10px rgba(110, 231, 183, 0.7);
}

/* Добавляем стили для кнопки, чтобы она сочеталась с инпутом */
.flex {
  display: flex;
}
.rounded-l-lg {
  border-top-right-radius: 0;
  border-bottom-right-radius: 0;
}
.rounded-r-lg {
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}
</style>