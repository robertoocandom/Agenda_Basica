<template>
 <div> 
   <div id="header">
     <Search v-on:query-change="querySearch"/>
   </div>

   <div id="main-container">
     <h2>TO DO's</h2>
     <ToDoAdd v-on:add-todo="addTodo"/>
     <Todos v-bind:todoslist="copyTodos" v-on:delete-todo="deleteTodo" /> 
   </div>
 </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import Search from './components/Search';
import Todos from './components/Todos';
import ToDoAdd from './components/ToDoAdd';


export default {
  name: 'App',
  components: {
    Todos, ToDoAdd, Search
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id != id)
      this.copyTodos = [... this.todos];
    },
    addTodo(todo) {
      this.todos.push(todo);
      this.copyTodos = [... this.todos]
    },
    querySearch(query) {
      if(query.trim() === '') {
        this.copyTodos = [... this.todos];
      } else {
        const temp = this.todos.filter(todo => {
          return todo.title.includes(query)
        });

      this.copyTodos = [... temp];
      }
    }
  },

  data() {
    return {
      todos: [
        {
          id: 0,
          title: 'Comprar la cena',
          completed: false
        },
        {
          id: 1,
          title: 'Sacar a pasear el perro',
          completed: true
        },
        {
          id: 2,
          title: 'Jugar xbox',
          completed: false
        },
        {
          id: 3,
          title: 'Terminar el Curso',
          completed: false
        },
        {
          id: 4,
          title: 'Terminar Proyecto Dilupa',
          completed: true
        },
      ],
      copyTodos: [],
    }
  },
  created() {
    this.copyTodos = [... this.todos];
  }
}
</script>

<style>
#app {


}
</style>
