
<script>
import TodoHeader from '../components/TodoHeader/TodoHeader.vue';
import TodoList from '../components/TodoList/TodoList.vue'
export default {
  // name:"Todo",
  components: {
    TodoHeader,
    TodoList
  },
  data() {
    return {
      inputText: "",
      todos: [],
      editMode: false,
      editedItem: {}
    }
  },
  methods: {
    addTodo() {
      console.log(this.editMode, this.editedItem)
      if (!this.inputText.trim().length) return
      if (this.editMode) {
        const index = this.todos.findIndex(item => {
          return (this.editedItem.id === item.id)
        })
        this.todos[index].text = this.inputText
        this.editedItem = {}
        this.editMode = false
      } else {
        this.todos.push({ text: this.inputText, id: Date.now(), status: false })
      }
      this.inputText = ""
    },
    getDate() {
      const newDate = new Date();
      const date = newDate.getDate();
      const month = newDate.toLocaleString("default", { month: "long" });
      const day = newDate.toLocaleDateString("locale", { weekday: "long" });
      return `${day} ${month} ${date}`
    },
    setEditMode(item) {
      console.log("HIII", item)
      this.editMode = true
      this.inputText = item.text
      this.editedItem = item
    },
    deleteTodo(todo) {
      this.todos = this.todos.filter(item => item.id !== todo.id)
    },
    markComplete(todo) {
      const index = this.todos.findIndex(item => {
          return (item.id === todo.id)
        })
        console.log(index)
        this.todos[index].status = !this.todos[index].status
    }
  },
  mounted() {
    this.$refs.input.focus()
  }
}
</script>
<template>
  <!-- <TodoHeader :input-text="inputText" :addTodo = "addTodo" /> -->
  <div class="todo-header">
    <div class="todo-date">
      <h3>{{ getDate() }}</h3>
      <div>{{ todos.length }} Items</div>
    </div>
    <div class="form">
      <input  ref="input" class="todo-input" v-model="inputText" placeholder="Add a todo" v-on:keyup.enter="addTodo">
      <button class="todo-btn" @click="addTodo">{{ editMode ? "Edit" : "Add" }}</button>
    </div>
  </div>
  <div class="todo-list">
    <TodoList v-for="todo in todos" key="todo.id"
    :todo="todo"
    @set-edit-mode="setEditMode"
    :edited-item="editedItem"
      @delete-todo="deleteTodo"
      @mark-complete = "markComplete"
      />
  </div>
</template>

<style>
.todo-header {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  border-bottom:  solid rgb(83, 168, 202) 1px;
}

.todo-date {
  width: 100%;
  height: 60px;
  box-sizing: border-box;
  display: flex;
  align-items: center;
  padding: 10px 10px;
  justify-content: space-between;
}

.form {
  box-sizing: border-box;
  display: flex;
  justify-content: space-between;
  width: 100%;
  padding: 5px 10px 10px 10px;
  align-items: center;
  height: 55px;
}

.todo-input {
  background: transparent;
  border-radius: 3px;
  border: 2px solid rgb(83, 168, 202);
  width: 80%;
  height: 23px;
}

.todo-input:focus {
  outline: none;
  border: 2px solid rgb(83, 168, 202);
}
.todo-btn {
  background: rgb(83, 168, 202);
  border-radius: 50%;
  border: 2px solid rgb(83, 168, 202);
  color: white;
  height: 40px;
  width: 40px;
  cursor: pointer;
  float: right;
}

.todo-list {
  margin-top: 8px;
  width: 100%;
  height: auto;
  display: grid;
  grid-auto-rows: min-content;
  grid-gap: 2px;
  height: 415px;
  overflow-y: auto;
}
</style>