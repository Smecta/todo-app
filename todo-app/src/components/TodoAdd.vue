<template>
    <div class="input-add">
        <input name="todo" type="text" v-model="todoContent" @keyup.enter="emitAddTodo" />
        <button @click = "emitAddTodo">
          <i class="plus"></i>  
        </button> 
      </div>
</template>
<script>
import {ref} from 'vue'
export default {
    name:'TodoList',
    props:["tid"],
    // props 访问父组件传递过来的属性 context 是vue 上下文信息 里面有emit方法可以让我们触发事件
    setup(props, context){
      const todoContent = ref("")
      const emitAddTodo = () =>{
        const todo = {
          id: props.tid,
          // 这里需要访问value属性才能获取ref中的值
          content: todoContent.value,
          // 完成状态默认未完成
          completed:false,
        };
        // 然后触发add-todo事件，把新创建的 todo 对象当做参数传递给它 context
        context.emit("add-todo",todo);
        // 最后把输入框中的值设置为空
        todoContent.value = ""
      }
      
      return{
        todoContent,
        emitAddTodo
      }
    }
}
</script>

<style>

/* 添加todo的输入框 */
.input-add{
  /* 定位：相对定位 */
  position:relative;
  /* 布局弹性盒布局 */
  display:flex;
  /* 设置垂直居中 */
  align-items:center;
}

/* input输入框样式 */
.input-add input{
  /* 设置内边距 顺时针 上右下左 */
  padding: 16px 52px 16px 18px;
  /* 设置边框圆角 */
  border-radius:48px;
  /* 设置边框为无 */
  border:none;
  /* 设置外边线去除 */
  outline:none;
  /* 盒子阴影 */
  box-shadow: 0px 0px 24px rgba(0, 0, 0, 0.08);
  /* 设置宽度占满 */
  width:100%;
  /* 设置字体大小 */
  font-size:16px;
  /* 设置文字颜色 */
  color: #626262;
} 

/* input内输入框按钮样式 */
.input-add button{
  /* 设置宽高一样 然后圆角为50% 就是个圆形 */
  width: 46px;
  height: 46px;
  border-radius:50%;
  /* 设置渐变色 */
  background: linear-gradient(#c0a5f3,#7f95f7);
  /* 去除默认边框样式 */
  border:none;
  /* 去除外边线 */
  outline:none;

  /* 设置颜色为白色 */
  color:white;
  /* 设置定位为绝对定位 */
  position:absolute;
  /* 设置位置为右边 */
  right:0px;

  /* 设置鼠标指针为小手 */
  cursor: pointer;
}

/* 设置按钮里面的加号 */
.input-add .plus{
  /* 设置元素为块元素 */
  display:block;
  /* 设置宽度为100%占满整个按钮 */
  width:100%;
  /* 设置高度为100%占满整个按钮 */
  height:100%;
  /* 使用两个liner-gradient生成两个线  颜色设置一样就没有渐变效果*/
  background:linear-gradient(#fff,#fff),linear-gradient(#fff,#fff);
  /* 设置第一条是横着的线宽度50% 高度是2px 和 第二条竖着的线 宽度2px 高度是50%  */
  background-size: 50% 2px, 2px 50%;
  /* 设置背景位置 为居中 两条线在中间交叉 */
  background-position:center;
  /* 设置背景不重复 */
  background-repeat: no-repeat;
}

</style>