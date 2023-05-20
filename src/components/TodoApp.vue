<template>
  <div class='container'>
  <h2 class='text-center mt-5'>Todo App</h2>

  <div class='d-flex'>
  <input type='text' class='form-control' placeholder='Enter task'>
  <button class='btn btn-warning rounded-0'>Add Task</button>
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
      <th>{{task.name}}</th>
      <td>{{task.status}}</td>
            <td><div class='text-center'>
              <span class="fa fa-trash pointer"></span>
            </div></td>
            <td><div class='text-center'>
              <span class="fa fa-pen pointer"></span>
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
            tasks: [
                {name: 'ankush want to give tes',
                status:'to-do'},
                {name: 'prerana want to give test',
                status:'in-progress'}
            ]
        }
    }

}
</script>

<style scoped>
</style>