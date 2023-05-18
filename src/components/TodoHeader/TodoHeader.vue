<script>
export default{
props:['inputText'],
emits:['addTodo'],
  data(){
    return{

    }
  }
}
</script>
<template>
  <div class="header">
    <!-- <div>Date</div> -->
    <!-- <div>Total</div> -->
    <div class="form">
      <!-- <input v-model="inputText" placeholder="Add a todo"> -->
      {{ inputText }}
      <button @click="addTodo">Add</button>
    </div>
  </div>
</template>