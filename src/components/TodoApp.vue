<template>
  <div class='container'>
  <h2 class='text-center mt-5'>Todo App</h2>

  <div class='d-flex'>
  <input type='text' class='form-control' placeholder='Enter task'>
  <button class='btn btn-warning rounded-0'>Add Task</button>
  </div>
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