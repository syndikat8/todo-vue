<template>
  <form @submit.prevent="onSumbit" class="addTodo">
    <input v-model="title" class="addTodo__input" type="text">
    <button type="submit">Add</button>
  </form>
</template>

<script>
export default {
  name: "AddTodo",
  data() {
    return {
      title: ""
    }
  },
  methods: {
    onSumbit() {
      if (this.title.trim()) {
        const newTodo = {
          id: Date.now(),
          title: this.title,
          completed: false
        }
        this.$emit("addTodo", newTodo)
        this.title = ""
      }
    }
  }
}
</script>

<style scoped>
.addTodo {
  display: flex;
  margin-bottom: 20px;
}

.addTodo__input {
  width: 400px;
  padding: 5px;
}
</style>
