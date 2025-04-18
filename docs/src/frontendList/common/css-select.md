
# 前言

选择器优先级

默认(继承) < 通配符选择器 < 标签选择器 < 类选择器 < id选择器 < 行内样式 < !important

## 案例
```js
<template>
  <div>
    <exitButton />
    <h3 class="mt-2">下面UnoCss的使用---------------------------------------</h3>
    <p class="w-125 bg-pink h-25 text-5 rounded-full">直接类里就是样式,原子化Css确实不错</p>
    <p class="h-[10px] mt-[30px]">指定高度和margin-top,配合vs插件 WindiCSS IntelliSense使用,看我其他文章介绍</p>
    <p class="text-[20px] mt-4">文本20大小,不指定则X4,比如mt-4就是margin-top:16px</p>
    <br />
    <el-button type="success">深度选择器使用有 >>> ::v-deep /deep/ :deep()</el-button>
    <br />
    <h3 class="mt-2">回顾一下其他选择器的使用---------------------------------------</h3>
    <span>标签选择器aqua</span>
    <div class="cls">
      类选择器blueviolet
      <span>类子代，如果span有声明颜色则使用申明的，否则继承cls颜色aqua</span>
    </div>
    <div id="id1">id选择器red</div>
    <hr />
    <h3 class="mt-2">复合选择器的使用---------------------------------------</h3>
    <div class="clsF">
      <p class="children1">
        子代选择器 和 后代选择器
        <span>
          你干嘛1
          <span>
            你干嘛2
            <span>你干嘛3</span>
          </span>
        </span>
      </p>
      <p class="clsB1">并集选择器1</p>
      <p class="clsB2">并集选择器2</p>
      <p class="clsB1 clsJ2 clsJ1">交集选择器</p>
      <p class="hoverT">伪类选择器</p>
    </div>
    <input type="text" />
  </div>
</template>

<script setup></script>

<style lang="scss" scoped>
[type='text'] {
  //属性选择器还可以[type]、[type^=a]、[title$=a] 解释：包含这个属性以属性值a开头、以a结尾
  color: blue;
}

.clsF > p:first-child {
  //结构伪类选择器第一个
  color: skyblue !important;
}
.clsF > p:nth-child(2n) {
  //结构伪类选择器2的倍数
  color: red !important;
}
.clsF > p:last-child {
  //结构伪类选择器最后一个
  color: skyblue !important;
}

.hoverT:hover {
  //伪类选择器鼠标放上文字变红
  color: crimson;
}

//交集选择器   如果自己样式几个不用空格同级别
.clsJ2.clsJ1 {
  font-weight: 600;
  background: green;
}
.clsJ2 {
  background: gray !important; //优先级最高
}
.clsB2,
.clsB1 {
  //并集选择器，都有
  background: pink;
}
.clsF > .children1 {
  //子代选择器
  font-weight: 800;
}

.clsF span {
  //后代选择器
  color: chartreuse;
}
span {
  //标签选择器
  color: aqua;
}
.cls {
  //类型选择器
  color: blueviolet;
}
#id1 {
  //id选择器
  color: red;
}
* {
  //通配符选择器 所有标签
  font-size: 20px;
}
:deep(.el-button > span) {
  //深度选择器
  color: pink;
}
</style>


```

## 深度选择器

深度选择器一般作用于第三方的组件里的样式---如element-ui

如下style有scoped的情况，不加深度选择器则无法修改span里的颜色
```css
<style lang="scss" scoped>
::v-deep(.el-button > span) {
  color: green;
}
</style>

:deep(.el-button > span) {
  color: green;
}

::v-deep .dv-scroll-board .header {
  margin-bottom: 15px;
}
```

使用

.el-form >>> .el-form-item__error

::v-deep 

:deep()

## 常用居中方式
![flex1](https://imgs.luckynwa.top/profile/mdS/cssCenter.png)


水平垂直居中   子绝父相
```html
    <div style="position: relative; 
      width: 100%; height: 600px; background: pink">
       <div 
       style="position: absolute; 
       top: 50%; left: 50%; 
       transform: translate(-50%, -50%)"
       >测试</div>
    </div>
```
水平垂直居中   flex布局
```html
  <div style="display: flex; 
    justify-content: center; 
    align-items: center; 
    width: 100%; 
    height: 600px; 
    background: pink">
      <div style="background-color: green">测试</div>
  </div>
```