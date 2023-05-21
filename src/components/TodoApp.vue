<template>
  <div class='container'>
  <h2 class='text-center mt-5'>Todo App</h2>

  <div class='d-flex'>
  <input v-model='task' type='text' class='form-control' placeholder='Enter task'>
  <button @click='submitTask' class='btn btn-warning rounded-0'>Add Task</button>
  </div>


  <table class="table table-bordered mt-5">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Staus</th>
      <th class='text-center' scope="col">Edit</th>
      <th class='text-center' scope="col">Delete</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for='(task,index) in tasks' :key='index'>
      <th><span :class="{ 'line-through': task.status === 'Finished' }">
              {{ task.name }}
            </span></th>
      <td style='width:120px'><span class='pointer'  @click='statusUpdate(index)'>{{task.status}}</span></td>
            <td><div class='text-center' @click='editTask(index)'>
              <span  class="fa fa-pen pointer"></span>
            </div></td>
            <td><div class='text-center' @click='deleteTask(index)'>
              <span class="fa fa-trash pointer"></span>
            </div></td>
    </tr>
  </tbody>
</table>



  </div>

</template>

<script>
export default {
    name:'HelloWorld',
    props:{
        msg:String,
    },

    data(){
        return {
            task:'',
            editedTask:null,
            availableStatuses: ['To-do','In-progress','Finished'],
            tasks: [
                {name: 'ankush want to give test',
                status:'To-do'},
            ]
        }
    },

    methods: {
        submitTask(){

            if(this.task.length === 0) return;

            if(this.editedTask === null){

            this.tasks.push({
                name: this.task,
                status: 'to-do'
            })
            }else{
                this.tasks[this.editedTask].name = this.task;
                this.editedTask=null;
            }

            this.task = ''

        },

        deleteTask(index){
            this.tasks.splice(index,1)
            alert('To-do task deleted sussessfully!!!')
        },

        editTask(index){
            this.task = this.tasks[index].name;
            this.editedTask=index
        },
        statusUpdate(index){
          let newIndex = this.availableStatuses.indexOf(this.tasks[index].status)
          if(++newIndex > 2) newIndex = 0
          this.tasks[index].status = this.availableStatuses[newIndex]
        }
    },


}
</script>

<style scoped>
.pointer{
  cursor:pointer;
}
.line-through {
  text-decoration: line-through;
}
</style>