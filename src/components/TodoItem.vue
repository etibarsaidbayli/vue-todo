<template>
  <li :class="[todo.isCompleted ? 'todo__item completee' : 'todo__item']">
    <div class="todo__item-name" v-if="!this.isEdit">
      <input
        v-model="todo.isCompleted"
        @input="this.$emit('completedTask', todo.id)"
        class="todo__item-checkbox"
        type="checkbox"
      />
      <strong>{{ todo.title }}</strong>
    </div>
    <form @submit="handleFormSubmit" class="isEdit__form" v-else="this.isEdit">
      <input class="form__input" type="text" v-model="this.editedText" />
      <button
        class="formSave__btn"
        @click="this.$emit('editedTodo', this.editedText, todo.id)"
        :disabled="!this.editedText || !this.editedText.trim()"
      >
        Save
      </button>
    </form>

    <div class="todo__btns" v-show="!this.isEdit">
      <button @click="editTodo">Redakt</button>
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
  },
  data() {
    return {
      isEdit: false,
      editedText: "",
      completed: false,
    };
  },
  methods: {
    editTodo() {
      this.isEdit = true;
      // this.$emit("editTodo", this.editedText);
    },
    handleFormSubmit(e) {
      e.preventDefault();
      this.isEdit = false;
    },

    completeTask(task) {
      task.isCompleted = !task.isCompleted;
    },
  },
  computed: {},
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
  background: rgb(79, 104, 113);
  color: rgb(209, 224, 209);
}

.todo__btns button:last-child {
  background: red;
  color: #fff;
}

.isEdit__form {
  width: 100%;
  display: flex;
  gap: 20px;
  align-items: center;
}

.form__input {
  flex-grow: 1;
  padding: 5px;
}
.formSave__btn {
  padding: 5px;
  font-size: 15px;
  border: none;
  cursor: pointer;
  border-radius: 5px;
  background-color: greenyellow;
  color: rgb(6, 7, 7);
  font-weight: bold;
}

.formSave__btn:disabled {
  opacity: 0.7;
  color: #fff;
}

.completee {
  background-color: red;
}
</style>
