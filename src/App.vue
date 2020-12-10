<template>
  <div id="app">
    <todo-list></todo-list>
  </div>
</template>

<script>
export default {
  name: "APP",
  components:{
     TodoList : () => import('./components/TodoList')
  }
}
</script>

<style lang="scss">
</style>
