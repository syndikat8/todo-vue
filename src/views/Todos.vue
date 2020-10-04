<template>
  <div>
    <h2>TODOLIST</h2>
    <router-link to="/">Home</router-link>
    <hr>
    <AddTodo
        @addTodo="addTodo"
    />
    <hr>
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not-completed</option>
    </select>
    <hr>
    <Loader v-if="isLoading"/>
    <Todolist
        v-else-if="filteredTodos.length"
        @onDeleteTask="onDeleteTask"
        :todos="filteredTodos"/>
    <p v-else>No todos!</p>
  </div>
</template>

<script>
import Todolist from '@/components/TodoList/TodoList.vue'
import AddTodo from "@/components/TodoList/AddTodo/AddTodo";
import Loader from "@/components/common/Loader/Loader";

export default {
  name: 'App',
  components: {
    Loader,
    AddTodo,
    Todolist,
  },
  data() {
    return {
      todos: [],
      isLoading: true,
      filter: "all"
    }
  },
  methods: {
    onDeleteTask(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo(newTodo) {
      this.todos.push(newTodo)
    }
  },
  computed: {
    filteredTodos() {
      if (this.filter === "all") {
        return this.todos
      } else if (this.filter === "completed") {
        return this.todos.filter(t => t.completed)
      } else {
        return this.todos.filter(t => !t.completed)
      }
    }
  },
  // watch: {
  //   filter(value) {
  //
  //   }
  // },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
        .then(response => response.json())
        .then(json => {
          this.todos = json
          this.isLoading = false
        })
  }
}
</script>

<style scoped>

</style>
