
<script>
import Todo from './views/Todo.vue'
export default{
  components:{
    Todo
  }
}
</script>

<template>
  <div class="container">
        <Todo/>
  </div>
</template>

<style>
.container{
  box-sizing: border-box;
  background: white;
  border-radius: 3px;
  box-shadow: rgba(0, 0, 0, 0.25) 0px 0.0625em 0.0625em,
    rgba(0, 0, 0, 0.25) 0px 0.125em 0.5em,
    rgba(255, 255, 255, 0.1) 0px 0px 0px 1px inset;
  color: rgb(83, 168, 202);
  margin: 1em 1em;
  width: 400px;
  height: 580px;
  overflow: hidden;
}
</style>