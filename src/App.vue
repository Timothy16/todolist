<template>
  <div id="app">
    <app-table/>
    <app-todo/>
  </div>
</template>
<script>
import Table from '@/components/Table.vue'
import todo from '@/components/todo.vue'
export default {
  components:{
    // 'app-table' : Table,
    'app-todo' :  todo
  }
}
</script>
<style>

</style>
