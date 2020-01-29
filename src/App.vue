<template>
  <div id="app">
    <Todos v-bind:todos="todoList" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Todos from './components/Todos';
export default {
  name: 'app',
  components: {
    Todos
  },
  data() {
    return {
    todoList : [
      {
        id : 1,
        title : "Todo One",
        completed : false
      },
      {
        id : 2,
        title : "Todo Two",
        completed : false
      },
      {
        id : 3,
        title : "Todo Three",
        completed : false
      }
    ]

    }
  },
  methods : {
    deleteTodo(id) {
        this.todoList = this.todoList.filter(todoItem => todoItem.id !== id);
    }
  }
}
</script>

<style>

</style>
