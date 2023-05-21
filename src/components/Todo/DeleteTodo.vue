<template>
  <div>
    <p>Are you sure you want to delete the task "{{ task.name }}"?</p>
    <button @click="deleteTask" class="btn btn-danger rounded-0">Delete</button>
  </div>
</template>

<script>
export default {
  name: "DeleteTodo",
  props: {
    task: Object,
    categorizedTasks: Object,
  },
  methods: {
    deleteTask() {
      const categoryTasks = this.categorizedTasks[this.task.category];
      const index = categoryTasks.indexOf(this.task);
      categoryTasks.splice(index, 1);

      this.$emit("task-deleted");
    },
  },
};
</script>

<style scoped>
</style>
