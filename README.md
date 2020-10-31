## 交作业项目

## 实战项目 
在学习前端例子几乎都是 todolist  它涵盖了完整的增删改查 过滤功能 等技术面

* 技术栈：vue3 的 Composition API

1. 寻找灵感
2. 搭建项目
3. 编写页面
4. 拆分组件
5. 实现功能

## 第一部分 寻找灵感

寻找方案： 
1. 在 Github 上 找到 Explore 的 Topics 或者Trending 当前比较热门的项目 可以简化应用自己的项目里面 
也可以访问 Github上的 Tuvtran 的 [project-based-learning](github.com/tuvtran/project-based-learning) 寻找灵感用到自己的项目中
2. 使用谷歌图片搜索 搜索你要想做的 App 比如 Todo App
3. 浏览设计师分析作品的平台 [dribbble](dribbbe.com)

## 第二部分 搭建项目

创建项目 工程化项目 vue-cli 很方便的添加管理依赖 提高开发项目的效率

使用vue-cli 版本4.5.x以上

``` bash 
npm install -g @vue/cli 

# 安装完成后 找一个合适的文件夹使用vue create 创建项目
vue create todo-app
# 选择 Vue3 的项目 Default (Vue 3 Preview)
```
创建完毕后

可以使用 `vue ui `启动项目 去管理 vue 项目 比如依赖安装 插件安装 等等

这里使用 命令行运行
``` bash
# 进入项目文件夹
cd todo-app
# 使用 yarn 或者 npm
yarn serve

```

* App.vue 是 vue 的入口文件 
> 要想 vue 代码高亮 VsCode 需要安装插件 Vetur
![Vetur.png](https://upload-images.jianshu.io/upload_images/25076556-f987f71f9e274b17.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* components 开发独立组件

* assets 存放静态资源文件 图片 视频

* main.js 创建了 vue 实例 并挂载到id为app的入口文件

* pubilc 文件夹是 打包生成的html的模板 

## 第三部分 编写页面（HTML部分）

编写之前，先把应用程序界面分析一下

整理原型 分析部分以及html结构

* main 占满整个浏览器的容器
  * todo的应用在容器里面居中水平对齐 
* h1  标题

* div input-add input button 输入框 和 按钮

* div filters span.fileter 过滤栏 

* div todo-list todo-item label input todo列表和todo的每一项

* 小型项目 采取 自顶向下的开发方式进行开发应用
* 现在app.vue 写好 html代码 最后再拆分组件

* html代码部分
    * 前期放到app.vue里面后期独立拆分到组件
``` vue
<template>
  <main>
    <div class="container">
      <h1>TodoList 待办事项</h1>
      <div class="input-add">
        <input name="todo" type="text" />
        <button>
          <i class="plus"></i>  
        </button> 
      </div>
      <div class="filters">
        <span class="filter active">全部</span>
        <span class="filter">已完成</span>
        <span class="filter">未完成</span>
      </div>
      <div class="todo-list">
        <div class="todo-item">
          <label>
              <input type="checkbox" />
              Todo 1
              <span class="check-button"></span>
          </label>
        </div>
        <div class="todo-item">
          <label>
              <input type="checkbox" />
              Todo 2
              <span class="check-button"></span>
          </label>
        </div>
        <div class="todo-item">
          <label>
              <input type="checkbox" />
              Todo 3
              <span class="check-button"></span>
          </label>
        </div>
      </div>
    </div>
  </main>
</template>

```

## 第四部分 编写样式（CSS部分）

* 拆解CSS样式 一步一步分析
* 分析设计：如果有设计稿要尽量还原设计稿
* 外层分析
    * 背景是淡紫色 rgb(203,210,240) 整体主题色
    * 外层有个阴影 是淡紫色
* 内层容器分析
    * 宽度占父容器的 60% 最大400
    * 标题文字颜色和字号
    * 添加输入框 添加按钮是圆形 背景是渐变色 css 实现加号
    * 过滤选项 选中是大文字 颜色比较深 
    * todo项目 白色背景 圆角边框 复选框 选中取消 复选框按钮 右侧文本内容

* css代码部分
    * 前期放到app.vue里面后期独立拆分到组件
``` css
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

/* 设置过滤块 */
.filters{
  /* 设置flex弹性盒布局 默认左右布局 */
  display:flex;
  /* 设置外边距 上下24px 左右2px */
  margin:24px 2px;
  /* 设置颜色 */
  color: #c0c2ce;
  /* 设置字体大小 */
  font-size:14px;
}

/* 设置过滤块的每一项的过滤元素span样式 */
.filters .filter {
  /* 右边外边距为14px */
  margin-right:14px;
  /* 过渡为0.8秒 */
  transition:0.8s;
}

/* 设置选中状态下的 span样式 */
.filters .filter.active{
  /* 设置颜色 */
  color:#6b729c;
  /* 使用scale函数放大1.2倍 */
  transform: scale(1.2);
}

/* 设置todo列表样式 */
.todo-list{
  /* 使用grid布局 */
  display: grid;
  /* 给每一个设置行间距 设置为14 */
  row-gap: 14px;;
}
/* 设置每一个todo的样式 */
.todo-item{
  /* 设置背景颜色为白色 */
  background: white;
  /* 设置内边距为16 */
  padding:16px;
  /* 设置圆角为8 */
  border-radius:8px;
  /* 设置颜色 */
  color:#626262;
}
.todo-item label{
  /* 设置定位为相对定位 */
  position:relative;
  /* 设置弹性盒布局 */
  display:flex;
  /* 设置垂直居中对齐 */
  align-items:center;
}
/* 复选框按钮 */
.todo-item label span.check-button{
  /* 使用绝对定位 */
  position:absolute;
  /* 设置上边0像素 */
  top:0;
}

/* 自定义复选框选中和不选中状态 使用伪元素 */
.todo-item label span.check-button::before,
.todo-item lable span.check-button::after{
  /* 伪元素的内容为空 */
  content:'';
  /* 设置属性为块元素 */
  display:block;
  /* 设置绝对定位 */
  position:absolute;
  /* 设置宽 */
  width: 18px;
  /* 设置高 */
  height: 18px;
  /* 设置圆角50% */
  border-radius: 50%;
}
/* 设置before伪元素 空心圆 */
.todo-item label span.check-button::before{
  border: 1px solid #b382f9
}
/* 设置选中状态after伪元素 实心圆 */
.todo-item label span.check-button::after{
  /* 设置过渡时间 */
  transition:0.4s;
  /* 设置背景颜色 */
  background:#b392f9;
  /* 设置缩小0.8倍 向右下移动1像素 */
  transform:translate(1px,1px) scale(0.8);
  /* 设置刚开始的透明度为0 */
  opacity:0;
}

/* 设置原生的复选框 */
.todo-item input{
  /* 设置右外边距为16 */
  margin-right:16px;
  /* 设置透明度为0 隐藏 */
  opacity:0;
}
/* 小技巧 当lanbel 选中状态的时候 那么就选取相邻的 自定义复选框的after选中状态的 */
.todo-item input:checked + span.check-button::after{
  /* 设置透明度为1 */
  opacity:1;
}


</style>
```

## 第五部分 抽离组件
* 组件的拆离思路
    * 卡片组件和标题 放入 App
    * 添加选项 放入 TodoAdd
    * 过滤选项 放入 TodoFilter
    * 外层todo列表 放入 TodoList
    * 内层todo列表项 放入 TodoListItem
> 观察设计稿 -> 拆分组件 -> 拆解复杂组件 -> 减少嵌套层次 -> 复用组件或功能

## 第六部分 添加数据

加上事件和数据的处理。首先定义Todo 列表数据，然后实现添加Todo 展示Todo 完成Todo 和过滤Todo的功能
这里使用了 vue 3 的Composition API 以及父组件监听子组件的语法

1. 添加 Todo
   
2. 完成 Todo

3. 过滤 Todo

4. 