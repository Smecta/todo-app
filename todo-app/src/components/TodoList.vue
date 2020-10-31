<template>
  <div class="todo-list">
    <todo-list-item
      v-for="todo in todos"
      :key="todo.id"
      @change-state="todo.completed = $event.target.checked"
      :todo-item="todo"
    ></todo-list-item>
  </div>
</template>
<script>
import TodoListItem from "./TodiListItem";
export default {
  name: "TodoList",
  components: { TodoListItem },
  props: ["todos"],
};
</script>

<style>
/* 设置todo列表样式 */
.todo-list {
  /* 使用grid布局 */
  display: grid;
  /* 给每一个设置行间距 设置为14 */
  row-gap: 14px;
}
</style>
