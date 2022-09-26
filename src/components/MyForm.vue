<template>
  <form @submit.prevent id="form">
    <input v-model="todo" type="text" placeholder="add your todo" />
    <button :disabled="!this.todo || !this.todo.trim()" @click="addTodo">
      Elave et
    </button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      todo: "",
    };
  },
  methods: {
    addTodo() {
      const newTodo = {
        id: Date.now(),
        title: this.todo,
        isCompleted: false,
      };
      this.todo = "";
      this.$emit("addTodo", newTodo);
    },
    
  },
};
</script>

<style scope>
#form {
  display: flex;
  justify-content: center;
  gap: 10px;
}

#form input {
  flex-grow: 0.5;
  padding: 10px 5px;
  font-size: 25px;
  border: none;
  border-radius: 8px;
}

#form button {
  flex-grow: 0.2;
  font-size: 22px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  background: lightgreen;
  padding: 5px;
  color: #fff;
}

#form button:disabled {
  opacity: 0.5;
}
</style>
