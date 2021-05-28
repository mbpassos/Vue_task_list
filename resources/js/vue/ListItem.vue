<template>
  <div class="row mb-2">
      <div class="col-9">
        <input type="checkbox" class="form-check-input ml-0 position-relative" @change="updateCheck()" v-model="task.completed">
        <span :class="[task.completed ? 'completed' : '']">{{ task.content }}</span>
      </div>
      <div class="col-3 d-flex justify-content-end">
          <button class="btn btn-outline-danger" @click="removeTask()">Remove</button>
      </div>
  </div>
</template>

<script>
export default {
    props:['task'],
    methods: {
        updateCheck(){
            axios.put('api/task/' + this.task.id, {
            task: this.task
        })
        .then( response => {
            if (response.status == 200) {
                this.$emit('taskChanged')
            }
        })
        .catch(error => {
            console.log(error)
        })
        },
        removeTask() {
            axios.delete('api/task/' + this.task.id,)
            .then( response =>{
                if ( response.status == 200) {
                    this.$emit('taskChanged')
                }
            })
            .catch( error =>{
                console.log(error)
            })
        }
    }
}
</script>

<style>

.completed {
    text-decoration: line-through;
    color: green;
}


</style>
