<template>
  <div id="app">
    <todo-header></todo-header>
    <todo-input v-on:addTodoItem="addOneItem"></todo-input>
    <todo-list v-bind:propsdata="todoItems"></todo-list>
    <todo-footer></todo-footer>
  </div>
</template>

<script>
import TodoFooter from './components/TodoFooter.vue'
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'

export default {
  name: 'App',
  components: {
    'TodoHeader': TodoHeader,
    'TodoInput': TodoInput,
    'TodoList': TodoList,
    'TodoFooter': TodoFooter
  },

  data: function() {
    return{
      todoItems: []
    }
  },

  methods: {
    addOneItem: function() {
      var obj = {completed: false, item: this.newTodoItem};
      localStorage.setItem(this.newTodoItem, JSON.stringify(obj));  //객체를 string으로 변환해주는 api
    }
  },

  created: function() {
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i ++) {
        if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
          console.log(JSON.parse(localStorage.getItem(localStorage.key(i)))); //JSON.parse: string을 다시 object로 변환
          this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
        }
      }
    }
  },

}
</script>

<style>
  body {
    text-align: center;
    background-color: #f6f6f6;
  }
  input {
    border-style: groove;
    width: 200px;
  }
  button {
    border-style: groove;
  }
  .shadow {
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
  }
</style>
