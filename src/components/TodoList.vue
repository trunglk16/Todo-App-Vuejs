<template>
  <div>
    <input type="text" class="todo-input" v-model="newTodo" placeholder="todo list" @keyup.enter="addTodo()">
    <div v-for="todo in todos" v-bind:key="todo.id" class="todo-item">{{todo.title}}</div>
  </div>

</template>

<script>
 export default {
    name: 'TodoList',
    data () {
      return {
        newTodo: '',
        idForTodo: 3,
        todos: [
          {
            'id':1,
            'title': 'Finish Vue Screencast',
            'completed': false,
          },
          {
            'id':2,
            'title': 'Take over world',
            'completed': false,
          },
        ],
        content: "love ya"
      }
    },
   methods: {
      addTodo() {
        this.todos.push({
          id: this.idForTodo,
          title: this.newTodo,
          completed: false,
        })

        this.newTodo = ''
        this.idForTodo++
      }
   }
  }

</script>

<style scoped>

</style>
