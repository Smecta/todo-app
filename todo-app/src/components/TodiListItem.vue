<template>
<!-- 设置样式 完成后添加class属性 -->
  <div class="todo-item" :class="{ done: todoItem.completed }">
    <label>
      <input type="checkbox" 
      :checked="todoItem.completed" 
      @click="$emit('change-state',$event)" />
      {{ todoItem.content }}
      <span class="check-button"></span>
    </label>
  </div>
</template>

<script>
export default {
  name: "TodoListItem",
  props: ["todoItem"],
};
</script>

<style>
/* 设置每一个todo的样式 */
.todo-item {
  /* 设置背景颜色为白色 */
  background: white;
  /* 设置内边距为16 */
  padding: 16px;
  /* 设置圆角为8 */
  border-radius: 8px;
  /* 设置颜色 */
  color: #626262;
}
.todo-item label {
  /* 设置定位为相对定位 */
  position: relative;
  /* 设置弹性盒布局 */
  display: flex;
  /* 设置垂直居中对齐 */
  align-items: center;
}

/* 已完成后添加样式 */
.todo-item.done label{
  /* 删除线 */
  text-decoration: line-through;
  /* 斜体 */
  font-style:italic;
  /* 设置颜色 */
  color:#c0c2ce;
}

/* 复选框按钮 */
.todo-item label span.check-button {
  /* 使用绝对定位 */
  position: absolute;
  /* 设置上边0像素 */
  top: 0;
}

/* 自定义复选框选中和不选中状态 使用伪元素 */
.todo-item label span.check-button::before,
.todo-item label span.check-button::after {
  /* 伪元素的内容为空 */
  content: "";
  /* 设置属性为块元素 */
  display: block;
  /* 设置绝对定位 */
  position: absolute;
  /* 设置宽 */
  width: 18px;
  /* 设置高 */
  height: 18px;
  /* 设置圆角50% */
  border-radius: 50%;
}
/* 设置before伪元素 空心圆 */
.todo-item label span.check-button::before {
  border: 1px solid #b382f9;
}
/* 设置选中状态after伪元素 实心圆 */
.todo-item label span.check-button::after {
  /* 设置过渡时间 */
  transition: 0.4s;
  /* 设置背景颜色 */
  background: #b392f9;
  /* 设置缩小0.8倍 向右下移动1像素 */
  transform: translate(1px, 1px) scale(0.8);
  /* 设置刚开始的透明度为0 */
  opacity: 0;
}

/* 设置原生的复选框 */
.todo-item input {
  /* 设置右外边距为16 */
  margin-right: 16px;
  /* 设置透明度为0 隐藏 */
  opacity: 0;
}
/* 小技巧 当lanbel 选中状态的时候 那么就选取相邻的 自定义复选框的after选中状态的 */
.todo-item input:checked + span.check-button::after {
  /* 设置透明度为1 */
  opacity: 1;
}

</style>
