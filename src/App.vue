<template>
  <div class="container">
    <h1 class="title__app">Todo app from VueJS</h1>
    <MyForm @addTodo="addTodo" />

    <ul class="todo__wrapper">
      <TodoItem
        v-for="todoItem in todos"
        :key="todoItem.id"
        :todo="todoItem"
        @removeTodo="removeTodo"
        @editedTodo="editedTodo"
        @completedTask="completedTask"
      />
    </ul>
  </div>
</template>

<script>
import MyForm from "./components/MyForm.vue";
import TodoItem from "./components/TodoItem.vue";

export default {
  components: {
    MyForm,
    TodoItem,
  },
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    addTodo(newTodo) {
      this.todos.push(newTodo);
    },
    removeTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    editedTodo(newText, id) {
      // this.todos.map((todo) => todo.title=newText)
      // if(!newText.length || !newText.trim()) {
      //   return  alert('bosh xana olmaz  ')
      // }
      let f = this.todos.find((todo) => todo.id === id);
      f.title = newText;
    },
    completedTask(id) {
      let f = this.todos.find((todo) => todo.id === id);
      f.isCompleted = true;
    },
  },
};
</script>

<style scope>
.title__app {
  text-align: center;
  padding: 25px;
}

.todo__wrapper {
  width: 100%;
  background: #808080;
  border-radius: 5px;
}
</style>
