##### 一、属性

| 属性 | 类型 | 默认值 | 说明 |
| ---- | ---- | ---- | ---- |
| height | String | '100px' | 垂直方向，内容超过此高度出现滚动条。最好不要使用百分比，除非父级元素设置了具体高度 |
| width | String | '100%'| 水平方向 ，内容超过此高度出现滚动条 。 | 
| trigger | String | 'always' | 触发显示滚动条。可填写的值有 'always'、'hover'、'none'。'always' 一直显示 ，'hover' 鼠标移动上去显示 ， 'none' 不显示|
|direction|String|'all'| 可滚动的方向。可填写的值有'all'、'x'、'y'。'all'垂直水平方向都可以滚动，'x'只可以在横向滚动，'y'只可以在垂直方向上滚动。|
|vBarStyle|Object|{'background-color': ''}| 垂直方向上轨道样式设置。修改垂直方向上轨道的样式|
|hBarStyle|Object|{'background-color': ''}| 水平方向上轨道样式设置。修改水平方向上轨道的样式|
|vThumbStyle|Object|{'background-color': 'rgba(0, 0, 0, 0.2)'}| 垂直方向上滑块样式设置。修改垂直方向上滑块滑块的样式|
|hThumbStyle|Object|{'background-color': 'rgba(0, 0, 0, 0.2)'}| 水平方向上滑块样式设置。修改水平方向上滑块滑块的样式|

##### 二、事件

|事件名| 说明|
| ---- | ---- |
|scroll| 滚动时触发|

##### 三、参考实例：

```
<template>
  <cScrollbar width="300px"
             height="100px"
             trigger="hover"
             direction="all"
             :vBarStyle="{
               'background-color':'rgba(0,0,0,0.1)'
             }"
             :hBarStyle="{
               'background-color':'rgba(0,0,0,0.2)'
             }"
             :vThumbStyle="{
                'background-color':'rgba(0,0,0,0.3)'
             }"
             :hThumbStyle="{
                'background-color':'rgba(0,0,0,0.4)'
             }"
             @scroll="handleScroll">
    <ol>
      <li>11111121212112121211212121121212112121211212121121212112
        1212112121221212111121212112121211212121121212112121211212121
        1212121121212112121221212111121212112121211212121121212112121
        211212121121212112121211212122121211212121121212112121211212121121
        212112121211212121121212112121221212</li>
      <li>1121212</li>
      <li>1121212</li>
      <li>1121212</li>
      <li>1121212</li>
      <li>1121212</li>
      <li>1121212</li>
      <li>1121212</li>
      <li>1121212</li>
      <li>1121212</li>
      <li>1121212</li>
    </ol>
  </cScrollbar>
</template>

<script lang="ts">
export default {
  setup() {
    function handleScroll(event: Event) {
      console.log(event);
    }
    return {
      handleScroll,
    };
  },
};
</script>
  
```

##### 四、实现核心思路

1. 通过MutationObserver、window.resize监听div元素内容或属性改变、监听窗口改变去更新滚动条滑块高度
2. 通过::-webkit-scrollbar隐藏原生滚动条
3. 通过监听原生scroll事件去改变滑块的高度
4. 点击轨道或拖动滑块时，监听mousedown事件去改变外层wrap的scrollTop或scrollLeft值。（改变此值会触发scroll事件）