<template>
  <div class="container">
      <div class="row h-100">
          <div class="col-12 align-self-center bg-white p-4">
            <div class="row">
                <div class="col-12">
                    <h2>Todo List</h2>
                </div>
            </div>
            <div class="row">
                <div class="col-12">
                    <add-task-form v-on:reloadList="getList()"></add-task-form>
                </div>
            </div>
            <div class="row">
                <div class="col-12">
                    <list-view :tasks="tasks" v-on:reloadList="getList()"></list-view>
                </div>
            </div>
          </div>
      </div>
    </div>
</template>

<script>
import AddTaskForm from './AddTaskForm.vue'
import ListView from './ListView.vue'
export default {
  components: { AddTaskForm, ListView },
  data: function() {
      return {
          tasks: []
      }
  },
  created(){
      this.getList();
  },
  methods: {
      getList(){
          axios.get('api/task')
          .then( response => {
              this.tasks = response.data

          })
          .catch( error => {
              console.log( error );
          })
      }
  }
}
</script>

<style>

html, body {
    height: 100%;
}

#app {
    width: 100vw;
    height: 100vh;
    background-color: lightcyan;
}

.container {
    height: 100%;
    width: 60%;
}

</style>
