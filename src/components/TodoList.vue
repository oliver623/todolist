<template>
  <div class="TodoList">
    <div class="header">
      <span>ToDoList</span>
      <el-input v-model.trim="addTodo" placeholder="添加ToDo"></el-input>
    </div>
    <div class="body">
      <h2>正在进行</h2>
      <div v-for="(todo, index) in todoList" :key="index" class="doing">
        <el-checkbox></el-checkbox>
        <el-input v-if="todo.edit"></el-input>
        <span v-else>{{todo.name}}</span>
      </div>
    </div>
    <div class="body">
      <h2>已经完成</h2>
       <div v-for="(todo, index) in todoList" :key="index" class="doing">
        <el-checkbox></el-checkbox>
        <span >{{todo.name}}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TodoList',
  data () {
    return {
      addTodo: '',
      todoList: [
        {name: '待办事项1', status: 'done',edit: false},
        {name: '待办事项1', status: 'done',edit: false},
        {name: '待办事项1', status: 'todo', edit: false},
        {name: '待办事项1', status: 'todo',edit: false},
      ]
    }
  }
}
</script>

<style scoped lang="scss">
.TodoList{
  width: auto;
  height: 100vh;
}
.header {
  display: flex;
  justify-content: space-around;
  color: rgb(208, 215, 221);
  height: 60px;
  line-height: 60px;
  text-align: center;
  background: rgb(48, 42, 42);
  & .el-input ::v-deep .el-input__inner {
    width: 50%;
  }
}
.doing{
  display: flex;
}
</style>