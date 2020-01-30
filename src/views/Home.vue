<template>
  <div id="app">
    <AddTodo v-on:app-addTodo="addTodo"/>
    <Todos v-bind:todos="todoList" 
           v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Todos from '../components/Todos';
import AddTodo from '../components/layout/AddTodo';
import axios from 'axios';

export default {
  name: 'home',
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
    todoList : []

    }
  },
  methods : {
    deleteTodo(id) {
        axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(() => this.todoList = this.todoList.filter(todo => todo.id!== id))
        .catch(err => window.console.log(err)); 
        this.todoList = this.todoList.filter(todoItem => todoItem.id !== id);
    },
    addTodo(newTodo) {
        const {title, completed} = newTodo;

        axios.post('https://jsonplaceholder.typicode.com/todos', {
          title,
          completed
        })
          .then()
          .catch(err => window.console.log(err)); 

        this.todoList = [...this.todoList, newTodo];
    }
  },
  created() {
      axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then(res => this.todoList = res.data)
      .catch(err=> window.console.log(err)); 
  }
}
</script>

<style>

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: Arial, Helvetica, sans-serif;
      line-height: 1.4;
    }
    .btn {
      display: inline-block;
      border : none;
      background: #555;
      color: #fff;
      padding: 7px 20px;
      cursor: pointer;
    }

    .btn:hover {
      background: #666;
    }
</style>
