<template>
  <div class="container">
    <h2 class="text-center mt-5">Todo App</h2>

    <div class="d-flex">
      <AddTodo :categories="categories" :categorizedTasks="categorizedTasks" />
    </div>

    <div class="d-flex mt-4">
      <div v-for="category in categories" :key="category" @click="selectCategory(category)" :class="{ 'folder-active': category === selectedCategory }" class="folder">{{ category }}</div>
    </div>

    <table v-if="selectedCategory" class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col">Category</th>
          <th class="text-center" scope="col">Edit</th>
          <th class="text-center" scope="col">Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in categorizedTasks[selectedCategory]" :key="index">
          <td>
            <span :class="{ 'line-through': task.status === 'Finished' }">{{ task.name }}</span>
          </td>
          <td style="width: 120px">
            <span class="pointer" @click="statusUpdate(task)">{{ task.status }}</span>
          </td>
          <td>
            {{ task.category }}
          </td>
          <td>
            <div class="text-center" @click="editTask(task)">
              <span class="fa fa-pen pointer"></span>
            </div>
          </td>
          <td>
            <div class="text-center" @click="deleteTask(task)">
              <span class="fa fa-trash pointer"></span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>

    <EditTodo v-if="editedTask !== null" :task="categorizedTasks[selectedCategory][editedTask]" :categories="categories" :categorizedTasks="categorizedTasks" :editedTask="editedTask" @task-updated="taskUpdated" />
    <DeleteTodo v-if="deletedTask !== null" :task="categorizedTasks[selectedCategory][deletedTask]" :categorizedTasks="categorizedTasks" @task-deleted="taskDeleted" />
  </div>
</template>

<script>
import AddTodo from "./Todo/AddTodo.vue";
import EditTodo from "./Todo/EditTodo.vue";
import DeleteTodo from "./Todo/DeleteTodo.vue";

export default {
  name: "TodoApp",
  data() {
    return {
      selectedCategory: null,
      editedTask: null,
      deletedTask: null,
      availableStatuses: ["To-do", "In-progress", "Finished"],
      categories: ["Personal", "Business", "Study"],
      categorizedTasks: {
        Personal: [
          {
            name: "ankush wants to give a test",
            status: "To-do",
            category: "Personal",
          },
        ],
        Business: [],
        Study: [],
      },
    };
  },
  methods: {
    selectCategory(category) {
      if (this.selectedCategory === category) {
        this.selectedCategory = null;
      } else {
        this.selectedCategory = category;
      }
    },
    editTask(task) {
      const index = this.categorizedTasks[task.category].indexOf(task);
      this.editedTask = index;
    },
    deleteTask(task) {
      const index = this.categorizedTasks[task.category].indexOf(task);
      this.deletedTask = index;
    },
    taskUpdated() {
      this.editedTask = null;
    },
    taskDeleted() {
      this.deletedTask = null;
      alert("To-do task deleted successfully!!!");
    },
    statusUpdate(task) {
      const newIndex = this.availableStatuses.indexOf(task.status) + 1;
      task.status = this.availableStatuses[newIndex % this.availableStatuses.length];
    },
  },
  components: {
    AddTodo,
    EditTodo,
    DeleteTodo,
  },
};
</script>

<style scoped>
.pointer {
  cursor: pointer;
}

.line-through {
  text-decoration: line-through;
}

.folder {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100px;
  height: 50px;
  background-color: lightgray;
  margin-right: 10px;
  cursor: pointer;
}

.folder-active {
  background-color: lightblue;
}
</style>
