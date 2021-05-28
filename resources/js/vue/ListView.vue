<template>
  <div>
      <div class="row" v-for="(task,index) in tasks" :key="index">
        <div class="col-12">
          <list-item :task="task" v-on:taskChanged="$emit('reloadList')"></list-item>
        </div>
      </div>
  </div>
</template>

<script>
import ListItem from './ListItem.vue'
export default {
  components: { ListItem },
    props: ['tasks']

}
</script>

<style>

</style>
