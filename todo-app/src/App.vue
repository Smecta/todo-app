<template>
  <main>
    <div class="container">
      <h1>TodoList 待办事项</h1>
      <!-- 通过add-todo 监听 todo-add组件时间 再给todo-add组件传递tid的属性 用于生成新的todo的id 这里简单的是数组的长度 -->
      <todo-add :tid="todos.length" @add-todo="addTodo"></todo-add>
      <todo-filter></todo-filter>
      <!-- 使用todos属性把tudo列表传递给todo-list组件  需要注意的是 使用ref包装的数据 需要value属性才能得到数据 但是在template里面vue 会自动拆解出value属性。这里直接传递就可以了-->
      <todo-list :todos="todos"></todo-list>
    </div>
  </main>
</template>

<script>
import {ref} from 'vue'
import TodoAdd from './components/TodoAdd'
import TodoFilter from './components/TodoFilter'
import TodoList from './components/TodoList'

export default {
  name: 'App',
  components:{
    TodoAdd,
    TodoFilter,
    TodoList
  },
  // vue3使用setup函数
  setup(){
    // 使用其他方式定义数据
    // ref 包装基本类型数据 简单数据 
    // reactive 复杂的对象数据
    // 使用ref包装一个数组 作为默认todo列表数据
    const todos = ref([]);
    // 定一个添加todolist的函数 通过事件接受一个参数保存信息 让后把它追缴的todos列表中
    const addTodo = (todo) => todos.value.push(todo);
    // 为了能在template使用数据或者函数 需要在setup中以对象的形式return返回    
    return {
      todos,
      addTodo
    }
    
  }
}
</script>

<style>
/* 所有元素设置 */
*{
  /* 设置boder-box 盒子模型 */
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  /* 设置字体 */
  font-family: Arial, Helvetica,"PingFang SC",'Microsoft Yahei', sans-serif;
}

/* 整个页面 */
main {
  width:100vw;
  /* 设置min-height 背景色 如果数量多则背景色一直存在 如果height 则背景色不存在 */
  min-height:100vh;
  display:grid;
  align-items: center;
  justify-items: center;
  background: rgb(203, 210, 240);
}

/* 设置容器 */
.container{
  width: 60%;
  max-width:400px;
  /* 阴影 */
  box-shadow: 0px 0px 24px rgba(0, 0, 0, 0.15);
  border-radius:24px;
  padding:48px 28px;
  background: rgb(245,246,252);
}

/* h1标题 */
h1{
  /* 外边距 上下24 左右0 */
  margin:24px 0;
  /* 字体大小 */
  font-size:28px;
  /* 颜色 */
  color:#414873;
}






</style>
