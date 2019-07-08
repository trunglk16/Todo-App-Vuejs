<template>
  <div>
    <input type="text" class="todo-input" v-model="newTodo" placeholder="List to do!!!!!" @keyup.enter="addTodo()">
    <div v-for="(todo, index) in todos" v-bind:key="todo.id" class="todo-item">
      <div class="todo-item-left">
        <input @click="status(todo)" type="checkbox" v-model="todo.completed">
        <div v-if="!todo.editing" :class="{completed : todo.completed}"  @dblclick="editTodo(todo)" class="todo-item-label">{{todo.title}}</div>
        <input v-else class="todo-item-edit" @keyup.esc="cancelEdit(todo)" @blur="doneEdit(todo)" @keyup.enter="doneEdit(todo)" type="text" v-model="todo.title" v-focus>
      </div>
      <div @click="removeTodo(index)" class="remove-item">&times;
      </div>
    </div>
    <div class="extra-container">
      <div>
        <label>
          <input type="checkbox" :checked="!anyRemaining" @change="checkAllTodos"> Check All
        </label>
      </div>
      {{remaining}} items left
    </div>
  </div>

</template>

<script>
 export default {
    name: 'TodoList',
    data () {
      return {
        newTodo: '',
        idForTodo: 3,
        beforeEditCache:'',
        todos: [
          {
            'id':1,
            'title': 'Finish Vue Screencast',
            'completed': true,
            'editing': false
          },
          {
            'id':2,
            'title': 'Take over world',
            'completed': false,
            'editing': false

          },
        ],
        content: "love ya"
      }
    },
   directives: {
     focus: {
       inserted: function (el) {
         el.focus()
       }
     }
   },
   methods: {
      addTodo() {
        if (this.newTodo.trim().length === 0) {
          return
        }
        this.todos.push({
          id: this.idForTodo,
          title: this.newTodo,
          completed: false,
          editing: false
        })

        this.newTodo = ''
        this.idForTodo++
      },

      removeTodo(index){
        this.todos.splice(index,1)
      },

     editTodo(todo) {
          this.beforeEditCache = todo.title
          todo.editing = true
     },

     doneEdit(todo) {
        if(todo.title.length === 0) {
          todo.title = this.beforeEditCache
        }
       todo.editing = false
     },

     cancelEdit(todo){
        todo.title = this.beforeEditCache
        todo.editing = false
     },

     status(todo){
        if(todo.completed) {
          todo.completed = false
          console.log(todo.completed)
        }
       else  {
         todo.completed = true
          console.log(todo.completed)
       }

     }
   }
  }

</script>

<style lang="scss">
  .todo-input {
    width: 100%;
    padding: 10px 18px;
    font-size: 12px;
    margin-bottom: 16px;

    & :focus {
      outline: 0;
    }
  }

  .todo-item {
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .remove-item {
    cursor: pointer;
    margin-left: 14px;

    & :hover {
      color: black;
    }
  }

  .todo-item-left {
    font-size: 18px;
    display: flex;
    align-items: center;
  }

  .todo-item-label {
    padding: 10px;
    border: 1px solid white;
    margin-left: 12px;
  }

  .todo-item-edit {
    font-size: 18px;
    color: #2c3e50;
    margin-left: 12px;
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;

    & :focus {
      outline: none;
    }
  }

  .completed {
    text-decoration: line-through;
    color: grey;
  }

  .extra-container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 16px;
    border-top: 1px solid lightgrey;
    padding-top: 14px;
    margin-bottom: 14px;
  }

  button{
    font-size: 14px;
    background-color: white;
    appearance: none;

    &:hover {
      background: lightgreen;
    }

    &:focus {
      outline: none;
    }
  }

  .active {
    background: lightgreen;
  }


</style>
