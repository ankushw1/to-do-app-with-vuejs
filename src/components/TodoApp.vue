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
    <tr>
      <th>mock final</th>
      <td>To-do</td>
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
        msg:String
    }
}
</script>

<style scoped>
</style>