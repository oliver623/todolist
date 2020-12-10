<template>
  <div class="TodoList">
    <div class="header">
      <span class="headerName">ToDoList</span>
      <el-input v-model="addTodo" placeholder="添加ToDo" @keyup.enter.native="handleAdd(addTodo)"></el-input>
    </div>
    <div class="body">
      <h2>正在进行</h2>
      <div v-for="(todo, index) in getTodoList" :key="index" class="doing">
        <el-checkbox></el-checkbox>
        <el-input v-if="todo.edit"></el-input>
        <span v-else>{{todo.name}}</span>
        <i class="el-icon-delete" @click="handleDelete(todo)"></i>
      </div>
    </div>
    <div class="body">
      <h2>已经完成</h2>
       <div v-for="(done, index) in getDoneList" :key="index" class="doing">
        <el-checkbox></el-checkbox>
        <span >{{done.name}}</span>
        <i class="el-icon-delete" @click="handleDelete(done)"></i>
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
        { name: '待办事项1', status: 'done',edit: false},
        { name: '待办事项2', status: 'done',edit: false},
        { name: '待办事项3', status: 'todo', edit: false},
        { name: '待办事项4', status: 'todo',edit: false},
      ]
    }
  },
  computed:{
    getDoneList() {
      return this.todoList.filter(val => val.status === 'done')
    },
    getTodoList() {
      return this.todoList.filter(val => val.status === 'todo')
    },
    getTodoId(){
      return this.todoList.map(val => val.id = )
    }
  },
  methods:{
    handleAdd(item) {
      this.todoList.push({name: item, status: 'todo', edit: false})
      this.addTodo = ''
    },
    handleDelete(item){
      console.log('item====', this.todoList.filter(val => val.id === item.id))
      // this.todoList.splice(index,1)
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
  font-size: bold;
  background: rgb(48, 42, 42);
  & .el-input ::v-deep .el-input__inner {
    width: 50%;
  }
}
.doing{
  display: flex;
}
.el-icon-delete{
  margin-left: 15px;
}
.headerName{
  margin-left:300px;
}
</style>