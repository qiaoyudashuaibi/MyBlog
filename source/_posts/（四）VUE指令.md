---
title: （四）VUE指令
date: 2019-11-24 23:48:06
tags:
---
vue.js的el是什么？
例：
var app = new Vue({
el : '#app',
data : {
name : 'Hello World'
}
})
这是实例一个vue对象最基本的写法，el用于提供一个页面上已存在的DOM元素作为Vue实例的挂载目标。可以使Css选择器，也可以是一个HTMLElement实例。

插值表达式
我们可以使用插值表达式来对页面进行取值。
格式：{{ }} （两个花括号，也叫Moustache表达式）。

下面介绍两个vue指令
v-bind和v-on。

v-bind用于绑定属性。
绑定后的标签属性会自动查找写好的属性，没有写v-bind的普通属性是字符串。
可能在以后的开发当中会频繁的使用v-bind来绑定属性，所以v-bind有简写形式为冒号形式（:）。

如果想在一个元素绑定多个class属性，可以使用数组形式，多个属性以逗号隔开。
例：<h1 :class="[red,width]">我是例子</h1>
这样写的意思就是给h1标签添加了两个class，red和width。
还有一种写法，写成对象的形式。
例：<h1 :class="{red: true}">我是例子</h1>
对象内部写成键值的形式，值固定为布尔值，表示属性是否生效。
数组和对象两种形式可以混合使用。
例：<h1 :class="[{red: true},width]">我是例子</h1>

绑定过的属性和没有绑定的属性可以同时出现，不冲突。

v-on用于事件监听。
可以简写为@。
例：<button @click="handleClick">点击</button>
这样button标签就监听到了handleClick事件。

下面做一个小例子，点击一个按钮，每点击一次，h1标签字体的颜色就改变一次。
例：
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>点击更换字体颜色</title>
    <!-- script标签引用vue -->
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.0"></script>
    <style>
        .red {
            color: red;
        }

        .yellow {
            color: yellow;
        }

        .green {
            color: green;
        }
    </style>
</head>

<body>
    <!-- 使用el引用vue -->
    <div id="app">
        <!-- v-bind绑定属性 -->
        <h1 :class="h1ClassArr[h1ClassArrIndex]">点击按钮，我的颜色会变化。</h1>
        <!-- v-on监听事件 -->
        <button @click="handleClick">点击</button>
    </div>

    <script>
        const vueObj = new Vue({
            el: '#app',
            // data存放数据
            data: {
                h1ClassArr: ['red', 'yellow', 'green'],
                h1ClassArrIndex: 0,
                index: 0
            },
            // methods存放方法
            methods: {
                // 按钮点击方法
                handleClick() {
                    // this代表当前vue对象vueObj
                    this.h1ClassArrIndex = ++this.index % 3;
                }
            }
        })
    </script>
</body>
</html>

上述代码实现了h1标签字体三种颜色的改变，我们发现handleClick方法写在了methods属性下，可不可以写在data属性下呢？
答案是不可以，如果将方法写在data下，我们会发现this根本取不到data下的值。原因是如果方法写在data下的话，this代表的是window。只有将方法写在methods下的话，this指的才是vue对象vueObj。 

v-if 和v-show指令

都能控制元素的显示和隐藏
有什么区别？
1.v-if控制dom的移除和添加，v-show控制dom的样式的显示与隐藏（display）
如果频繁的显示和隐藏推荐使用v-show，只判断一次的情况推荐使用v-if。
2.v-if可以写在template上，v-show不可以，即使写了也不起作用。
template标签用于做逻辑判断，而不添加实际的html元素。

v-for
1.不能通过索引的方式更改数组，这样不会渲染页面。	
2.不能通过更改长度的方式更改数组，不能渲染。
3.数组变异方法：pop，shift，unshift，splice，sort，reverse，push。
4.向对象内添加或者删除属性，不会渲染页面。
5.可以使用this.$set(对象，属性，值)，来更改并渲染对象。$set也可用于数组等。

v-model
实现数据双向绑定，其实就是:value（绑定数据）和@input（监听事件）的语法糖。