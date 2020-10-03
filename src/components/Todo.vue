<template>
    <div class='ui centered card'>
      <div class="content" v-show="!isEditing">
        <div class='header'>
            {{ todo.title }}
        </div>
        <div class='meta'>
            {{ todo.project }}
        </div>
        <div class='extra content'>
          <span class='right floated edit icon' v-on:click="showForm">
              <i class='edit icon'></i>
          </span>
          <span class='right floated trash icon' v-on:click="deleteTodo(todo)">
              <i class='trash icon'></i>
          </span>
        </div>
      </div>
      <div class="content" v-show="isEditing">
        <div class='ui form'>
          <div class='field'>
            <label>Title</label>
            <input type='text' v-model="todo.title" >
          </div>
          <div class='field'>
            <label>Project</label>
            <input type='text' v-model="todo.project" >
          </div>
          <div class='ui two button attached buttons'>
            <button class='ui basic blue button' v-on:click="showForm">
              Close X
            </button>
          </div>
        </div>
      </div>
      <div class='ui bottom attached green basic button' v-on:click="completeTodo(todo)" v-show="!isEditing &&todo.done" disabled>
          {{ todo.Complete }}
      </div>
      <div class='ui bottom attached red basic button'  v-on:click="completeTodo(todo)" v-show="!isEditing && !todo.done">
          {{ todo.Complete }}
      </div>
    </div>
</template>

<script>
export default {
  props: ['todo'],
  data() {
    return {
      isEditing: false,
    };
  },
  methods: {
    showForm() {
      this.isEditing = !this.isEditing;
    },
    completeTodo(todo) {
        this.$emit('complete-todo', todo);
        if(todo.Complete == 'Completed'){
            todo.Complete = 'Pending'
            todo.done = false;
        }
        else {
            todo.Complete = 'Completed'
            todo.done = true;
        }

      },
    deleteTodo(todo) {
      this.$emit('delete-todo', todo);
    },
  },
};
</script>

<style scoped>

.red{
    color: red;
    border-color: red;
}
.green{
    color: green;
    border-color: green;
}
</style>