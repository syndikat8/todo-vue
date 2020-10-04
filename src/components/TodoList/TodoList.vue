<template>
  <div>
    <ul class="todoList">
      <TodoItem
          v-for="(todo, index) of todos"
          :index="index"
          :todo="todo"
          :key="todo.id"
          @onDeleteTask="onDeleteTask"
      />
    </ul>
  </div>
</template>
<script>
import TodoItem from "@/components/TodoList/TodoItem/TodoItem";

export default {
  name: 'TodoList',
  components: {
    TodoItem
  },
  props: ["todos"],
  methods: {
    onDeleteTask (id) {
      this.$emit("onDeleteTask", id)
    }
  }
}
</script>

<style scoped>
.todoList {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
