<template>
  <div>
    <input v-model="task" type="text" class="form-control" placeholder="Enter task" />
    <select v-model="selectedCategory" class="form-control mt-2">
      <option value="" disabled>Select category</option>
      <option v-for="category in categories" :value="category" :key="category">{{ category }}</option>
    </select>
    <button @click="submitTask" class="btn btn-warning rounded-0 mt-2">Add Task</button>
  </div>
</template>

<script>
export default {
  name: "AddTodo",
  props: {
    categories: Array,
    categorizedTasks: Object,
  },
  data() {
    return {
      task: "",
      selectedCategory: null,
    };
  },
  methods: {
    submitTask() {
      if (this.task.length === 0 || !this.selectedCategory) return;

      const categorizedTasksCopy = { ...this.categorizedTasks }; // Make a copy of categorizedTasks

      const newTask = {
        name: this.task,
        status: "To-do",
        category: this.selectedCategory,
      };
      categorizedTasksCopy[this.selectedCategory].push(newTask); // Modify the copy

      this.$emit("task-added", categorizedTasksCopy); // Emit the modified copy

      this.task = "";
      this.selectedCategory = null;
    },
  },
};
</script>

<style scoped>
</style>
