<template>
  <li class="todoItem">
    <span :class="{'todoItem-done': todo.completed }">
      <input class="todoItem__item" type="checkbox" v-on:change="todo.completed = !todo.completed">
      <strong>{{ index + 1 }}</strong>
          {{ todo.title | uppercase }}
    </span>
    <button
        @click="onButtonClick"
        class="todoItem__button"
    >
      &times;
    </button>
  </li>
</template>

<script>
export default {
  name: "TodoItem",
  props: ['todo', 'index'],
  methods: {
    onButtonClick() {
      this.$emit("onDeleteTask", this.todo.id)
    }
  },
  filters: {
    uppercase(value){
      return value.toUpperCase()
    }
  }
}
</script>

<style scoped>
.todoItem {
  border: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  padding: .5rem 2rem;
  margin-bottom: 1rem;
  width: 500px;
}

.todoItem__button {
  background: #7f52a8;
  color: #fff;
  border-radius: 50%;
  font-weight: bold;
  cursor: pointer;
}

.todoItem__item {
  margin-right: 1rem;
  cursor: pointer;
}

.todoItem-done {
  text-decoration: line-through;
}
</style>
