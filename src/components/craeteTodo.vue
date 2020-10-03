<template>
  <div class='ui basic content center aligned segment'>
    <button class='ui basic button icon' v-on:click="openForm" v-show="!isCreating">
      <i class='plus icon'></i>
    </button>
    <div class='ui centered card' v-show="isCreating">
      <div class='content'>
        <div class='ui form'>
          <div class='field'>
            <label>Title</label>
            <p> {{ error_a }}</p>
            <input v-model="titleText" type='text' ref='title' defaultValue="">
          </div>
          <div class='field'>
            <label>Project</label>
            <p> {{ error_b }} </p>
            <input v-model="projectText" type='text' ref='project' defaultValue="">
          </div>
          <div class='ui two button attached buttons'>
            <button class='ui basic blue button mybtn' v-on:click="sendForm">
              Create
            </button>
            <button class='ui basic red button mybtn' v-on:click="closeForm">
              Cancel
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      titleText: '',
      projectText: '',
      isCreating: false,
      error_a : '',
      error_b : '',
    };
  },
  methods: {
    openForm() {
      this.isCreating = true;
      this.error_a = '';
      this.error_b = '';
    },
    closeForm() {
      this.isCreating = false;
      this.titleText= '';
      this.projectText= '';
      this.error_a = '';
      this.error_b = '';
    },
    sendForm() {
      this.error_a = '';
      this.error_b = '';
      if(this.titleText.length == 0 ){
        this.error_a = 'This is not completed';
      }
      if(this.projectText.length == 0 ){
        this.error_b = 'This is not completed';
      }
      
      else if (this.titleText.length > 0 && this.projectText.length > 0) {
        let mytitle = this.titleText;
        let myproject = this.projectText;
        this.$emit('add-todo', {
          mytitle,
          myproject,
        });
      
        // todo.title,
        // todo.project,
        // todo.done = false,
        // todo.Complete = 'Pending'
        // this.newTodoText = '';
        this.isCreating = false;
        this.titleText= '';
        this.projectText= '';
        this.error_a = '';
        this.error_b = '';
      }
      
    },
  },
};
</script>

<style scoped>
p{
  font-size: 10px;
  color: red;
}
.mybtn{
  margin: 0 5px;
}
</style>