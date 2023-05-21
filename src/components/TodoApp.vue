<template>
  <div class="container">
    <h2 class="text-center mt-5">Todo App</h2>

    <div class="d-flex">
      <input v-model="task" type="text" class="form-control" placeholder="Enter task" />
      <select v-model="selectedCategory" class="form-control ml-2">
        <option value="" disabled>Select category</option>
        <option v-for="category in categories" :value="category" :key="category">{{ category }}</option>
      </select>
      <button @click="submitTask" class="btn btn-warning rounded-0">Add Task</button>
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
  </div>
</template>


<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },

  data() {
    return {
      task: '',
      selectedCategory: null,
      editedTask: null,
      availableStatuses: ['To-do', 'In-progress', 'Finished'],
      categories: ['Personal', 'Business', 'Study'],
      categorizedTasks: {
        Personal: [
          {
            name: 'ankush wants to give a test',
            status: 'To-do',
            category: 'Personal',
          },
        ],
        Business: [],
        Study: [],
      },
    };
  },

  methods: {
    submitTask() {
      if (this.task.length === 0 || !this.selectedCategory) return;

      if (this.editedTask === null) {
        const newTask = {
          name: this.task,
          status: 'To-do',
          category: this.selectedCategory,
        };
        this.categorizedTasks[this.selectedCategory].push(newTask);
      } else {
        const editedTask = this.categorizedTasks[this.selectedCategory][this.editedTask];
        editedTask.name = this.task;
        editedTask.category = this.selectedCategory;
        this.editedTask = null;
      }

      this.task = '';
    },

    deleteTask(task) {
      const categoryTasks = this.categorizedTasks[task.category];
      const index = categoryTasks.indexOf(task);
      categoryTasks.splice(index, 1);
      alert('To-do task deleted successfully!!!');
    },

    editTask(task) {
      this.task = task.name;
      this.selectedCategory = task.category;
      this.editedTask = this.categorizedTasks[task.category].indexOf(task);
    },

    statusUpdate(task) {
      const newIndex = this.availableStatuses.indexOf(task.status) + 1;
      task.status = this.availableStatuses[newIndex % this.availableStatuses.length];
    },

  selectCategory(category) {
  if (this.selectedCategory === category) {
    this.selectedCategory = '';
  } else {
    this.selectedCategory = category;
  }
},


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
