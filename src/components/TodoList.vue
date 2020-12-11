<template>
  <div class="TodoList">
    <div class="header">
      <span class="headerName">ToDoList</span>
      <el-input
        v-model.trim="addTodo"
        placeholder="添加ToDo"
        @keyup.enter.native="handleAdd(addTodo)"
      ></el-input>
    </div>
    <div class="body">
      <h2>正在进行</h2>
      <div v-for="(todo, index) in getTodoList" :key="index" class="doing">
        <el-checkbox v-model="todo.status" true-label="done" false-label="todo"></el-checkbox>
        <el-input
          v-if="todo.edit"
          v-model="todo.name"
          ref="editTodo"
          @blur="handleEdit(todo)"
          @keyup.enter.native="handleEdit(todo)"
        ></el-input>
        <span v-else class="showName" @dblclick="handleOpenEdit(todo)">{{todo.name}}</span>
        <i class="el-icon-delete" @click="handleDelete(todo)"></i>
      </div>
    </div>
    <div class="body">
      <h2>已经完成</h2>
      <div v-for="(done, index) in getDoneList" :key="index" class="doing">
        <el-checkbox checked disabled></el-checkbox>
        <span class="showName">{{done.name}}</span>
        <i class="el-icon-delete" @click="handleDelete(done)"></i>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TodoList',
  data() {
    return {
      addTodo: '', // 新增的待办事项的名称
      todoList: [
        { id: 0, name: '待办事项1', status: 'done', edit: false },
        { id: 1, name: '待办事项2', status: 'done', edit: false },
        { id: 2, name: '待办事项3', status: 'todo', edit: false },
        { id: 3, name: '待办事项4', status: 'todo', edit: false }
      ], // 默认待办事项
      index: 4
    }
  },
  computed: {
    // 计算已完成的事项
    getDoneList() {
      return this.todoList.filter(val => val.status === 'done')
    },

    // 计算待办事项
    getTodoList() {
      return this.todoList.filter(val => val.status === 'todo')
    }
  },
  methods: {
    // 新增待办事项
    handleAdd(item) {
      if (item == '')
        return this.$message({
          message: '请填写此字段',
          type: 'warning'
        })
      this.todoList.push({ id: this.index++, name: item, status: 'todo', edit: false })
      this.addTodo = ''
    },

    // 删除待办事项
    handleDelete(item) {
      // let idx = this.todoList.indexOf(item) //得到当前事项的index  方法1
      let idx = this.todoList.findIndex(val => val === item)  //得到当前事项的index  方法2
      this.todoList.splice(idx, 1)
    },
    
    // 编辑待办事项
    handleEdit(item) {
      if (item.name == '')
        return this.$message({
          message: '请填写此字段',
          type: 'warning'
        })
      item.edit = false
    },

    // 双击打开编辑状态
    handleOpenEdit(item) {
      item.edit = true
      this.$nextTick(() => {
        this.$refs.editTodo[0].focus()
      })
    }
  }
}
</script>

<style scoped lang="scss">
.TodoList {
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
.doing {
  display: flex;
}
.el-icon-delete {
  margin-left: 15px;
}
.headerName {
  margin-left: 300px;
}
.showName{
  margin: 0 15px;
}
</style>