---
title: （六）案例研究_JavaScript图片库
date: 2019-11-25 23:15:56
tags: JavaScript
---
# 案例研究：JavaScript图片库

## 标记

首先准备四张图片，然后为这些图片创建一个链接清单，标记清单代码如下：（看00.html）

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Image Gallery</title>
</head>
<body>
<h1>Snapshots</h1>
<ul>
  <li>
    <a href="./images/fireworks.jpg" title="A fireworks display">Fireworks</a>
  </li>
  <li>
    <a href="./images/coffee.jpg" title="A cup of black coffee">Coffee</a>
  </li>
  <li>
    <a href="./images/rose.jpg" title="A red,red rose">Rose</a>
  </li>
  <li>
    <a href="./images/bigben.jpg" title="The famous clock">Big Ben</a>
  </li>
</ul>
</body>
</html>
```

当然现在显示的结果并不是我想要的，我想在点击图片链接的时候不跳转页面，而是在本页面显示，现在在页面下方添加一个图片标签，起到占位的作用。

```html
<img src="./images/placeholder.jpg" alt="my image gallery" id="placeholder">
```

现在进行下一步操作。

## JavaScript

为了把占位符图片替换为想要查看的图片，需要改变它的src属性。所以要是用setAttribute方法，所以我需要写个函数来执行这一操作，参数为图片的链接。函数的写法如下：

```js
  function showPic(whicpic) {
   
    var source = whicpic.getAttribute("href");
    
    var placeholder = document.getElementById("placeholder");
   
    placeholder.setAttribute("src", source);
  }
```

这个函数我起名为showPic，传入参数whicpic，代表元素节点（a标签），之后获取a标签的href属性的值赋值给source，将占位符图片对象赋值给placeholder，将source赋值给占位符图片的src属性，这样这个函数就完成了属性替换。

### 非DOM解决方案

其实，不用DOM的setAttribute方法也可以改变图片的src属性。还可以写成这样：

```js
placeholder.src = source;
```

这种老办法虽然可以改变图片的src属性，但并非所有的元素节点都适用，使用setAttribute方法的优势是可以修改文档中的任何一个元素的任何一个属性。

这种可以修改任意元素节点的任意属性，是“第一级DOM”的组成部分，第一级DOM英文名叫DOM Level1。

第一级DOM的另一个优势是移植性更好，上述的老办法只适用于Web文档，DOM则适用于任何一种标记语言。

虽然这种差异对这个例子没有影响，但我希望我们要牢牢记住这一点：

DOM是适用于多种环境和多种程序设计语言的通用API，如果要把DOM技巧运用在Web浏览器以外的应用环境中，严格的遵守“第一级DOM”，能够让我们避免与兼容性相关的任何问题。

### 最终的函数代码清单

所以最终函数的形式为如下代码：

```js
  function showPic(whicpic) {
    var source = whicpic.getAttribute("href");
    var placeholder = document.getElementById("placeholder");
    placeholder.setAttribute("src", source);
  }
```

下面的任务是，把这个JS函数与标记文档结合起来。

## 应用这个JavaScript函数

函数已经写完，现在需要让图片库文档使用它，把这个函数单独的写在JS文件中，起名为“showPic.js”。

Tips ：若一个站点用到多个JS文件时，为了减少对站点的请求次数（提高性能），应该把这些JS文件放在一个子目录中。关于性能的问题以后会讨论。

所以，我创建了script目录用于存储JS文件，并使用如下代码将JS文件引入到HTML文件中：

```html
<script type="text/javascript" src="./Script/showPic.js"></script>
```

这样我们的HTML就可以使用showPic函数了，不过到此，如果不添加事件处理函数（event handler）的话，这个函数永远也不会执行。

事件处理函数

事件处理函数的作用是，在特定事件发生时调用特定的JS代码。

比如鼠标悬停时触发onmouseover事件处理函数，鼠标离开某元素时触发onmouseout事件处理函数，想要在我的图片库点击某个链接时触发一个动作，就要使用onclick事件处理函数。

还有一点，showPic是需要一个节点元素的参数的，this关键字正好可以使用。

this的意思就是表示“这个对象”。

所以，只要写成以下这样，就可以调用onclick事件处理函数了。

```
onclick = "showPic(this)";
```

下面代码，是加了onclick事件处理函数的li标签下的a标签：

```html
<li>
  <a href="./images/fireworks.jpg" title="A fireworks display" onclick="showPic(this)">Fireworks</a>
</li>
```

在浏览器中运行一下，我们会发现图片在新的页面显示了，这是我不希望的，我希望的是图片在占位符图片的位置显示。

其实，我们在点击链接的时候，不光showPic函数被调用了，链接点击的默认行为也调用了，这样我们就得禁用这个默认行为。

我们先了解一下事件处理函数的工作机制。在给某个元素添加了事件处理函数之后，一但事件发生，相应的JS代码就会执行。被调用的JS代码可以返回一个布尔值，这个布尔值将会返回给事件处理函数。如果是true，事件处理函数会认为这个事件发生了，如果返回值是false，事件处理函数就会认为事件没有发生。

这样，解决方法就出现了，在调用showPic的同时，给事件处理函数返回一个false，就可以禁用它的默认行为了。代码如下：

```html
<li>
  <a href="./images/fireworks.jpg" title="A fireworks display" onclick="showPic(this);return false;">Fireworks</a>
</li>
```

这样，在浏览器运行，点击图片时页面不会跳转到新的页面。

下面是完整代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Image Gallery</title>
</head>
<body>
<h1>Snapshots</h1>
<ul>
  <li>
    <a href="./images/fireworks.jpg" title="A fireworks display" onclick="showPic(this);return false;">Fireworks</a>
  </li>
  <li>
    <a href="./images/coffee.jpg" title="A cup of black coffee" onclick="showPic(this);return false;">Coffee</a>
  </li>
  <li>
    <a href="./images/rose.jpg" title="A red,red rose" onclick="showPic(this);return false;">Rose</a>
  </li>
  <li>
    <a href="./images/bigben.jpg" title="The famous clock" onclick="showPic(this);return false;">Big Ben</a>
  </li>
</ul>
<img src="./images/placeholder.jpg" alt="my image gallery" id="placeholder">

<script type="text/javascript" src="./Script/showPic.js"></script>
</body>
</html>
```

## 对这个函数进行扩展

下面为这个函数添加更多功能，图片库文档的每个图片链接都有一个title属性，把这个属性提取出来并让它和相应的图片一同显示在网页上。

这样我们就需要用到几个新的DOM属性。

### childNodes属性

在一颗节点数上，childNodes属性可以用来获取任何一个元素的所有子元素，它的返回值是一个包含着子元素对象的数组。

这样，我们写一个函数，用于统计图片库页面body有多少个子元素，代码如下：

```js
function countBodyChildren() {
  var body_element = document.getElementsByTagName("body")[0];
  alert("body标签下的子节点有：" + body_element.childNodes.length + "个");
}
```

这个函数的意思是，先用body_element变量存储body元素节点，因为HTML文档只存在一个body标签，所以用getElementsByTagName比较方便，之后用body_element调用childNodes属性，并把它的长度通过浏览器弹窗打印出来。

之后，我们把这个函数添加到onload事件处理函数中，表示页面加载时，这个函数就跟着调用，代码如下：

```js
window.onload = countBodyChildren();
```

这样，一刷新页面，就会弹出窗口，上面显示当前页面body下的子节点有多少个。

### nodeTpye属性

根据文档的结构，body应该只有3个子元素才对：一个h1元素，一个ul元素，一个img元素。可以countBodyChildren()函数的返回值却远大于此。

这是因为文档树的节点类型并非只有元素节点一种。

事实上，文档中几乎每一种东西都是一个节点，甚至空格和换行符都会被解释为节点，而它们也全部包含在childNodes属性所返回的数组当中。所以它的length才那么大。

幸好，nodeType属性可以记录节点是哪一种节点。

nodeType属性的返回值是数字而不是英文字符串，这种属性共有十二种数值，其中仅有三种具有实用价值：

+ 元素节点的nodeType：1
+ 属性节点的nodeType：2
+ 文本节点的nodeType：3

验证一下，在函数中添加如下代码：

```js
alert("body标签的节点类型是：" + body_element.nodeType)
```

弹框中显示“1”，看来body确实是一个元素节点。

### 在标记里添加一段描述

为了增强我的图片库，我决定添加一个p标签在图片的下方，给它一个id为“description”，意思是描述。代码如下：

```html
<p id="description">Choose an image.</p>
```

我要达到的效果是，当点击一个链接时，不仅要把占位符图片改变，还有把p标签的文本显示成图片的title属性。

### 用JavaScript改变这段描述

现在我要做的是获取whichpic的title属性和p标签元素节点。

下面用两个变量来存储上述的两个值，修改后showPic函数如下：

```js
function showPic(whicpic) {
  var source = whicpic.getAttribute("href");
  var placeholder = document.getElementById("placeholder");
  placeholder.setAttribute("src", source);

  var text = whicpic.getAttribute("title");
  var description = document.getElementById("description");
}
```

text用来存放title属性，description用来获取p元素节点对象。

下面的任务是进行文本切换。

### nodeValue属性

如果想改变一个文本节点的值，我们需要使用nodeValue属性，它用来得到和设置一个节点的值。

这里我们输入如下代码进行测试，打印一下p元素的nodeValue属性。

```js
alert(description.nodeValue);
```

奇怪的是，弹框中显示的值为“null”。

原来，p元素本身的nodeValue属性是一个空值，而我们真正想要得到的是p元素所包含的文本的值。包含在p元素内部的文本是另一种节点，它是p元素的第一个子节点，所以我们想要得到的是p元素的第一个子节点的nodeValue值。

修改上述代码为：

```js
alert(description.childNodes[0].nodeValue);
```

这样，弹框中显示的值为“Choose an image.”，正是我们想要的。

### firstChild和lastChild

数组元素childNodes[0]有个与他作用相同的属性，为firstChild，如果想访问子节点数组的第一个元素的话，两种写法功能是相同的。

与之对应，lastChild表示子节点数组中的最后一个元素，如果不想这么写，也可以写成：

```js
node.childNodes[node.childNodes.length - 1];
```

两种形式对比，前者拥有很好的可读性，建议使用前者。

### 利用nodeValue属性刷新这段描述

现在我们可以修改showPic函数了。

上述提过，nodeValue不仅能取出节点的值，也可以设置节点的值。利用nodeValue我们就可以改变p元素中的文本节点了。代码如下：

```js
function showPic(whicpic) {
  var source = whicpic.getAttribute("href");
  var placeholder = document.getElementById("placeholder");
  placeholder.setAttribute("src", source);
  var text = whicpic.getAttribute("title");
  var description = document.getElementById("description");
  description.firstChild.nodeValue = text;
}
```

text存放的是whicpic中title的值，description存放的是p元素，把p元素的第一个子节点的值赋值为text，这样就实现了p标签文本的改变。

最后的最后，我们要给图片库来点样式，新建一个styles目录用于存放CSS代码，其中创建一个layout.css的文件，代码如下：

```css
body {
  font-family: "Helvetica", "Arial", serif;
  color: #333;
  background-color: #ccc;
  margin: 1em 10%;
}

h1 {
  color: #333;
  background-color: transparent;
}

a {
  color: #c60;
  background-color: transparent;
  font-weight: bold;
  text-decoration: none;
}

ul {
  padding: 0;
}

li {
  float: left;
  padding: 1em;
  list-style: none;
}

img {
  display: block;
  clear: both;
  width: 400px;
  height: 300px;
}
```

至此，我们就完成了图片库的功能，最终的HTML代码和JS代码如下。

HTML部分：

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Image Gallery</title>
  <link rel="stylesheet" href="./styles/layout.css">
</head>
<body>
<h1>Snapshots</h1>
<ul>
  <li>
    <a href="./images/fireworks.jpg" title="A fireworks display" onclick="showPic(this);return false;">Fireworks</a>
  </li>
  <li>
    <a href="./images/coffee.jpg" title="A cup of black coffee" onclick="showPic(this);return false;">Coffee</a>
  </li>
  <li>
    <a href="./images/rose.jpg" title="A red,red rose" onclick="showPic(this);return false;">Rose</a>
  </li>
  <li>
    <a href="./images/bigben.jpg" title="The famous clock" onclick="showPic(this);return false;">Big Ben</a>
  </li>
</ul>
<img src="./images/placeholder.jpg" alt="my image gallery" id="placeholder">
<p id="description">Choose an image.</p>

<script type="text/javascript" src="./Script/showPic.js"></script>
</body>
</html>
```

JS部分：

```js
function showPic(whicpic) {
  var source = whicpic.getAttribute("href");
  var placeholder = document.getElementById("placeholder");
  placeholder.setAttribute("src", source);
  var text = whicpic.getAttribute("title");
  var description = document.getElementById("description");
  description.firstChild.nodeValue = text;
}
```

## 小结

本次我们完成了一个图片库的小项目，还介绍了DOM的几个新属性，他们是：

+ childNodes
+ nodeType
+ nodeValue
+ firstChild
+ lastChild

重点有两个：一是如何利用DOM提供的方法去编写图片库脚本，二是如何利用事件处理函数把JS代码与网页集成在一起。

虽然这个项目看起来不错，但还有很多地方需要我们改进。

我希望在接下来的学习中我们能领会这样一个道理：

达成目标的过程与目标本身同样重要。