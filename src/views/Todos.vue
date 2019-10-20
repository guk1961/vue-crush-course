<template>
  <div>
   <h2>Todo application</h2>
 
   <AddTodo 
      @add-todo="addTodo"
    />
   <hr>
   <TodoList 
      v-bind:todos="todos"
      @remove-todo="removeTodo"
   />
  </div>
</template>


<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
export default {
  name: 'app',
  data(){
    return {
      todos: [
        // {id:1, title: 'Купить гречку', completed: false},
        // {id:2, title: 'Купить куриную грудку', completed: false},
        // {id:3, title: 'Сходить на тренировку', completed: false},
      ]
    }
  },
  mounted(){
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
  .then(response => response.json())
  .then(json => {this.todos = json})
  },
  methods:{
    removeTodo(id){
      this.todos = this.todos.filter(t=> t.id!==id)
    },
    addTodo(todo) {
      this.todos.push(todo)
    }
  },
  components: {
    TodoList, AddTodo
  }
}
</script>