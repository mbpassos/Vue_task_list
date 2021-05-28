<template>
  <div class="row form-group g-2">
      <div class="col-xs-6 col-md-10 pr-0 ">
          <input type="text" class="form-control shadow-sm" placeholder="Add Todo" v-model="task.content">
      </div>
      <div class="col-md-2 col-xs-6 d-flex justify-content-end pl-0">
          <button type="submit" class="btn btn-outline-primary" @click="addTask">Add</button>
      </div>
  </div>
</template>

<script>
export default {
    data: function () {
        return {
            task:{
                content:''
            }
        }
    },
    methods: {
        addTask(){
            if(this.task.content == ''){
                return
            }
            axios.post('api/task/store', {
                task: this.task
            })
            .then( response => {
                if( response.status == 201){
                    this.task.content = '';
                    this.$emit('reloadList')
                }
            })
            .catch( error => {
                console.log( error )
            })
        }
    }
}
</script>

<style>

</style>
