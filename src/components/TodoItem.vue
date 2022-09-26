<template>
  <li class="todo__item">
    <div class="todo__item-name" v-if="!isEdit">
      <input class="todo__item-checkbox" type="checkbox" />
      <strong>{{ todo.title }}</strong>
    </div>
    <div v-else="isEdit">
    <input 
    type="text" 
    v-model="editText"
     />
    </div>
    <div class="todo__btns">
      <button @click="editTodo">Redakte et</button>
      <button @click="this.$emit('removeTodo', todo.id)">Sil</button>
    </div>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true,
    },

    data() {
      return {
        isEdit:true,
        editText:""
      };
    },
    methods: {
      
      editTodo() {
        this.isEdit=true
        // this.$emit('editTodo', this.editText)
      },
    },
  },
};
</script>

<style scope>
.todo__item {
  padding: 10px 30px;
  font-size: 18px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 5px;
}

.todo__item-checkbox {
  width: 20px;
  height: 20px;
  cursor: pointer;
}

.todo__item-name,
.todo__btns {
  display: flex;
  gap: 10px;
}

.todo__btns button {
  padding: 5px;
  font-size: 15px;
  border: none;
  cursor: pointer;
  border-radius: 5px;
}

.todo__btns button:first-child {
  background: lightblue;
  color: green;
}

.todo__btns button:last-child {
  background: red;
  color: #fff;
}
</style>
