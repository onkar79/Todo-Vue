<script>
export default {
  props: ['todo', "editedItem"],
  emits: ['setEditMode', "deleteTodo","markComplete"],
  emits: [],
  data() {
    return {
    }
  }
}
</script>
<template>
  {{ console.log(editedItem) }}
  <div class="todo-container " :class="{ editing: editedItem.id === todo.id }">
    <div class="todo-text">
      <input type="checkbox" class="checkbox" @change="$emit('markComplete', todo)" />
      <span :class="{completed : todo.status}">
        {{ todo.text }}
      </span>
    </div>
    <div class="todo-action">
      <button class="edit" @click="$emit('setEditMode', todo)">Edit</button>
      <button class="delete" @click="$emit('deleteTodo', todo)">Delete</button>
    </div>
  </div>
</template>

<style>
.todo-container {
  height: 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  background: #f5f5f5;
}

.editing {
  background-color: #fbffbd;
}
.todo-text{
  gap: 10px;
}
.checkbox {
  width: 10px;
  height: 10px;
}
.completed{
  color:grey;
  text-decoration: line-through;}
</style>