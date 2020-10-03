<template>
  <div>
    <p>Completed Tasks: {{todos.filter(todo => {return todo.done === true}).length}}</p>
    <p>Pending Tasks: {{todos.filter(todo => {return todo.done === false}).length}}</p>
    <div class=" myflex">
    <todo v-on:delete-todo="deleteTodo" v-on:complete-todo="completeTodo" :key="todo" v-for="todo in todos" :todo="todo"></todo>
    </div>
  </div>
</template>

<script type = "text/javascript" >

import Todo from './Todo.vue';

export default {
  props: ['todos'],
  components: {
    Todo,
  },
  methods : {
      completeTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos[todoIndex].done = true;
    },
    deleteTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex, 1);
    },
  }
};
</script>
<style scoped>
.myflex{
  width: 95%;
  margin: 0 auto;
  /* display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: baseline;
  flex-wrap: wrap; */
}
@media (max-width: 1200px){
  .myflex{
  width: 98%;
  }
}
</style>