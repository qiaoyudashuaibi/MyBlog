---
title: （五）DOM
date: 2019-11-25 18:51:16
tags: JavaScript
---
# DOM

## 文档：DOM中的“D”

文档（document），当创建一个网页并把它加载到Web浏览器中时，浏览器就把你写的文档转换为一个文档对象。

## 对象：DOM中的“O”

JS中对象可分为三类：
+ 用户定义对象（user-defined object）：由程序员自行创建的对象。
+ 内建对象（native object）：内建在JS语言里的对象。
+ 宿主对象（host object）：由浏览器提供的对象。

其中，window是一个宿主对象，window对应着浏览器的本身，这个对象的属性和方法统称为BOM（浏览器对象模型）。

## 模型：DOM中的“M”

模型（model），含义是某种事物的表现形式。

DOM把一份文档表示为一棵树，如果我们能把文档的各种元素想象成一颗节点树，我们就可以清晰的描述DOM。

## 节点

节点（node），在DOM中，文档是由节点构成的集合，此时节点就代表文档树上的树枝和树叶。

下面介绍三种节点：元素节点、文本节点和属性节点。

### 元素节点

DOM的原子是元素节点（element node）。

如果把Web上的文档比作一座大厦，元素就是建造这座大厦的砖块，这些元素在文档中的布局形成了文档的结构。

### 文本节点

文本节点（text node），表示拥有信息（比如文字）的节点。

在XHTML中，文本节点总是被包含在元素节点中，但并非所有的元素节点都包含文本节点。

比如：

```html
<ul>
<li>文本</li>
</ul>
```

ul元素没有直接包含任何文本节点，它包含着li元素节点，后者包含着文本节点。

### 属性节点

属性节点（attribute node），用来对元素做出更具体的描述。属性节点总是被包含在元素节点中，但并非所有元素节点都包含属性节点。

总结一下，元素节点就是具体的标签（比如p标签），属性节点代表标签中的属性（比如p标签的title属性），而文本节点代表标签中写的文本。

### CSS

CSS（层叠样式表）。

对样式的声明可以嵌在文档的head部分，就是style标签之间，也可以单独放在一个样式表文件里。

基本语法：

```css
selector{
  property: value;
}
```

继承（inheritance）是CSS技术中的一项强大功能，类似于DOM，CSS也把文档的内容视为一颗节点树。节点树上的各个元素将继承其父元素的样式属性。

例如，我们给body定义了一些颜色或字体，包含在body元素里的所有元素都将动态获得这些样式。

有时我们需要区别某一个或某几个元素，这时需要class属性和id属性。

1.class属性：我们可以在所有元素上任意使用class属性，元素拥有相同的class属性，我们可以统一设置这些元素的样式。

2.id属性：id属性用于给网页中的某个元素加上一个独一无二的标识符。

id属性就像一个挂钩，一头连着文档中的某个元素，另一头连着CSS样式表里的某个样式。DOM也可以使用这种挂钩。

### 获取元素

DOM有三种方法可以获取元素节点，分别是通过元素ID、通过标签名和通过类名来获取。

1.getElementById

getElementById是document对象特有的函数，这个方法将返回有着特定id属性的元素节点对应的对象。

getElementById方法只有一个参数，就是输入的id值，输入时一定要加上单引号或双引号。

下面看“00.html”，使用typeof操作符看看getElementById的返回值。

浏览器弹框中显示object，表示使用getElementById方法的返回值是一个对象。


2.getElementsByTagName

getElementsByTagName方法返回值是一个对象数组，每个对象分别表示着文档中有着给定标签的一个元素。

这个方法的参数也只有一个，就是标签的名字。

使用方法与getElementById类似，但它的返回值是个数组。

看“01.html”，使用length属性查看返回值，浏览器弹框显示为3。

看“02.html”，使用for循环遍历getElementsByTagName返回的数组中的值，用typeof操作符查看返回的结果是什么类型的，结果是浏览器弹窗返回三个object。

getElementsByTagName允许使用通配符（星号字符“*”），如果想知道文档中共有多少元素节点，使用如下语句就可以。

`alert(document.getElementsByTagName("*").length)`

getElementById和getElementsByTagName可以混合使用。

如果想知道id是特定id值的元素下包含了多少元素节点，我们可以两种方法混合使用。看“03.html”,浏览器弹窗结果是3。

```js
var shopping = document.getElementById("purchases");
var items = shopping.getElementsByTagName("*");
alert(items.length);
```

3.getElementsByClassName

getElementsByClassname方法可以通过类名返回元素对象，参数只有一个就是类名，返回值是一个对象数组。

通过下述代码，返回类名为“sole”的所有元素。

`document.getElementsByClassName("sale");`

要指定多个类名的话，在字符串参数中用空格隔开即可。

`document.getElementsByClassName("important sale")`;

### 盘点知识点

现在对上述知识做一个总结：

+ 一份文档就是一颗节点树。
+ 节点分为不同的类型：元素节点、属性节点和文本节点等。
+ getElementById返回文档中的一个特定的对象。
+ getElementsByTagName和getElementsByClassName返回的是一个对象数组，他们分别对应文档中的一组特定元素节点。
+ 每个节点都是一个对象。

## 获取和设置属性

至此，我们可以使用三种方法来获取元素：getElementById,getElementsByTagName,getElementByClassName。

获取元素之后，我们就可以获取和设置元素的属性。

### getAttribute

getAttribute是一个函数，它只有一个参数，就是你要查询的属性名称。

`object.getAttribute(attribute);`

getAttribute方法不属于document对象，不能通过document调用。

不过他可以跟getElementsByTagName合用，获取每一个p标签的title属性，代码如下：

```js
var paras = document.getElementsByTagName("p");
for(var i = 0; i < paras.length; i++) {
  alert(paras[i].getAttribute("title"));
}
```

如果页面有多个p标签，而有些p标签没有title属性的话，这些没有title属性的p标签getAttribute的返回值为“null”。

我们可以添加if语句，来判断这些p标签有没有title属性，如果有的话才弹出弹框。代码如下：

```js
var paras = document.getElementsByTagName("p");
for(var i = 0; i < paras.length; i++) {
  var title_text = paras[i].getAttribute("title");
  if (title_text != null){
  alert(title_text);
  }
}
```

判断title存不存在，我们可以不用写“!=”，直接写这个属性。简化代码如下：

```js
var paras = document.getElementsByTagName("p");
for(var i = 0; i < paras.length; i++) {
  var title_text = paras[i].getAttribute("title");
  if (title_text) alert(title_text);
}
```

### setAttribute

setAttribute方法用于设置元素节点的属性，语法如下：

`object.setAttribute(attribute,value);`

我们在设置一个节点的属性时，如果这个属性原先不存在，setAttribute会先创建这个属性，后给这个属性赋值。如果原先有属性的话，后面setAttribute会覆盖这个值。

例子如下（看04.html）：

```js
var paras = document.getElementsByTagName("p");
for(var i = 0; i < paras.length; i++) {
  var title_text = paras[i].getAttribute("title");
  if (title_text){
    paras[i].setAttribute("title","brand new title text");
    alert(paras[i].getAttribute("title"));
  }
}
```

上述代码实现将文档中所有带title属性的p标签获取出来，然后把它们的title属性全部修改为“brand new title text"。

这里有一个非常值得注意的点，通过setAttribute对文档做出修改之后，通过浏览器查看源代码（view source）选项去查看文档的源代码时我们可以发现，title属性依旧是修改之前的属性，也就是和setAttribute做出的修改不会反应在文档本身的源代码中。

这就要说到DOM的工作模式，DOM先加载文档的静态内容，再动态刷新，动态刷新并不影响文档的静态内容。

这就是DOM的真正威力：对页面内容进行刷新却不需要在浏览器里刷新页面。

## 小结

本章介绍了DOM提供的五个方法：

+ getElementById
+ getElementsByTagName
+ getElementsByClassName
+ getAttribute
+ setAttribute

这五种方法是今后编写DOM脚本的基石。


