<template>
    <div class="filters">
        <span class="filter active">全部</span>
        <span class="filter">已完成</span>
        <span class="filter">未完成</span>
    </div>
</template>
<script>
export default {
    name:"TodoFilter",
    setup(){
      const filters = [
        {label:'全部', value:'all'},
        {label:'已完成', value:'done'},
        {label:'未完成', value:'todo'},
      ]
    }
}
</script>

<style>
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

</style>