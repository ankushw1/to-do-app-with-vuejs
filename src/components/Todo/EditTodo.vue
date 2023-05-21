<template>
  <div>
    <input v-model="editedTaskName" type="text" class="form-control" placeholder="Enter task" />
    <select v-model="editedTaskCategory" class="form-control mt-2">
      <option value="" disabled>Select category</option>
      <option v-for="category in categories" :value="category" :key="category">{{ category }}</option>
    </select>
    <button @click="updateTask" class="btn btn-warning rounded-0 mt-2">Update Task</button>
  </div>
</template>

<script>
export default {
  name: "EditTodo",
  props: {
    task: Object,
    categories: Array,
    categorizedTasks: Object,
    editedTask: Number,
  },
  data() {
    return {
      editedTaskName: this.task.name,
      editedTaskCategory: this.task.category,
    };
  },
  methods: {
    updateTask() {
      const editedTask = this.categorizedTasks[this.task.category][this.editedTask];
      editedTask.name = this.editedTaskName;
      editedTask.category = this.editedTaskCategory;

      this.$emit("task-updated");

      this.editedTaskName = "";
      this.editedTaskCategory = "";
    },
  },
};
</script>

<style scoped>
</style>
