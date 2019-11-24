---
title: （四）JavaScript语法
date: 2019-11-24 23:57:07
tags: JavaScript
---
# JavaScript语法

## 准备工作
JavaScript代码必须通过HTML或XHTML文档才能执行。有两种方法可以做到这点。
+ 一种是写在文档&lt;head&gt;标签中的&lt;script&gt;标签之间。
+ 另一种是将代码存为一个扩展名为.js的独立文件。

最好的做法是把&lt;script&gt;标签放到HTML文档的最后。

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Example</title>
</head>

<body>
<!-- Mark-up goes here -->
  <script src=""></script>
</body>
</html>
```

这样写能够使浏览器更快的加载页面，之后会详细说明。

程序设计语言分为解释型和编译型两大类。Java或C++等语言需要一个编译器（compiler）。编译器是一种程序，能够把用Java等高级语言编写出来的源代码翻译为直接在计算机上执行的文件。

解释型程序设计语言不需要编译器——他们仅需要解释器，对于JavaScript语言，在互联网环境下，Web浏览器负责完成有关的解释和执行工作。浏览器中的JS解释器将直接读入源代码并执行。浏览器中如果没有解释器，JS代码就无法执行。

用编译型语言编写的代码有误，这些错误汪汪在代码编译阶段就能被发现。而解释型语言代码中的错误只能等到解释器执行到相关代码时才能发现。

与解释型语言相比，编译型语言往往速度更快，可移植性更好，但学习曲线也往往更陡峭。

##语法
语言结构方面的规则，我们称之为“语法”。

###语句
语句是构成任何一个脚本的基本单位，只有正确的语法编写出来的语句才能得到正确的解释。

如果要把多条语句写在一行上，就要写成如下的格式：

`first statement; second statement;`

建议在每条语句的末尾都加上一个分号，这样使代码更容易阅读，更容易跟踪JS脚本的执行顺序。

```
first statement;
second statement;
```

###注释
注释用于自己参考或提醒自己，JS解释器会忽略这些信息。

单行注释：

`//我是注释内容`

多行注释：

```JavaScript
/* 我是多行注释，
我是多行注释，
我是多行注释，
我是多行注释，
我是多行注释，
*/
```

JavaScript也可以使用HTML中的注释形式“&lt;!-- -->”，视为单行注释。不过JS不要求写后半部分“-->”，JS会把后半部分也视为注释内容。不过还是建议使用“//”，和“/* */”来注释单行或者多行。

###变量
我们一般把变化的东西称为变量（variable）。

把值存入变量的操作称为赋值（assignment）。

我们可以在JS中给变量赋值，再通过alert方法弹出警告式弹窗。（代码：00.html）

JS允许我们直接对变量赋值无须事先声明（declare），虽然JS没有强制要求声明，但提前声明变量是一种良好的编程习惯。

```js
var mood;
var age;
```

还可以一条语句声明多个变量。

```js
var mood,age;
```

还可以声明变量和赋值一次完成。

```js
var mood = "happy";
var age = 33;
```

甚至还可以这样：

```js
var mood = "happy",age = 33;
```

JS中，变量和其他元素的名称是区分大小写的，大小写不同的变量或其他元素，他们是不同的。

JS不允许变量名中包括空格或者标点符号（美元符号$除外）。

JS变量名允许包括字母、数字和下划线，数字不允许开头，还可以使用驼峰式（camel case）命名，通常驼峰式是函数名、方法名和对象属性命名的首选格式。

###数据类型
必须明确数据类型声明的语言称为“强类型”（strongly typed），不需要明确数据类型的语言称为“弱类型”（weakly typed），JS是弱类型语言，这意味着程序员可以在任何阶段改变变量的数据类型。

1.字符串

通过单引号或双引号包含的字面量，称为字符串。

如果想要在字符串中添加单引号或双引号，就要使用“\”来进行转义。

`var mood = 'don\'t ask';`

2.数值

如果想给变量赋值一个数值，不用限定它必须是一个整数，他还可以是浮点数或负数。

3.布尔值

布尔值只有两个可选值：true和false。

###数组

字符串、数值和布尔值都是标量（scalar），标量的意思是它在任意时刻就只能有一个值。如果想用一个变量来存储一组值，就需要使用数组（array）。

我们可以对数组进行声明，可以执行数组的长度，也可以不指定。

```js
var arr1 = Array(4);
var arr2 = Array();
```

向数组中添加元素的操作称为填充（populating），我们需要给出数组的下标。

```js
arr1[index] = element;
```

还可以声明数组的同时填充数组。

```js
var arr = Array("a","b","c","d");
```

我们可以不用明确表示我们是在创建数组。

```js
var arr = ["a","b","c","d"];
```

其中数组元素的数据类型可以不同，字符串，数值，布尔值都可以，还可以是变量，甚至是其他的数组。

```js
var arr1 = ["a","b","c","d"];
var arr2 = [];
arr[0] = arr1;
```

关联数组

传统数组的意思是使用下标来记录每个存在数组中的值，而关联数组的意思是用字符串代替数字作为下标，这样做的好处是代码更具有可读性，但不推荐这种做法，本质上这种做法的意思是创建了Array对象的属性。

```js
var arr = Array();
arr["name"] = "qiaoyu";
arr["age"] = 18;
arr["height"] = 1.88;
```

###对象

对象也是用一个名字表示一组值，对象的每个值都是对象的一个属性。

```js
var obj = {name:"qiaoyu",age:18,height:1.88}
```

##操作

算术操作符

加减乘除（+ - * /）

##条件语句

条件语句（conditional statement）

基本语法：

```js
if(condition){
  statements;  
}
```

if语句中的花括号是可以不写的，如果花括号部分只包含一条语句的话，那就可以不使用花括号。

```js
if(1>2) alert("The world has gone mad!")
```

上述弹框是不会出现的。

不过，因为花括号可以提高脚本的可读性，所以在if语句中总是使用花括号是个好习惯。

if语句还有个else字句，表示条件为假时执行else字句中的代码。

```js
if(1>2){
  alert("The world has gone mad!");
}else{
  alert("All is well with the world!");
}
```

###比较操作符

大于（>），小于（<），大于等于（>=），小于等于（<=），相等（==），不相等（!=），严格相等（===），严格不相等（!==）

###逻辑操作符

逻辑与（&&），逻辑或（||），逻辑非（!）

##循环语句
需要重复执行同一代码块时，要使用循环语句。

###while循环

```js
while(condition){
  statements;
}
```

do...while循环

我们希望包含在循环语句中的代码至少执行一次的时候，这时最好使用do...while循环

```js
do{
  statements;
}while (condition);
```

###for循环

```
for(initial condition; test condition ; alter condition){
  statements;
}
```

##函数

如果需要多次使用同一段代码，可以把它们封装成一个函数（function）。

```js
function shout(){
  var arr = Array("a","b","c","d");
  for (var count = 0 ; count < arr.length; count++){
  alert(arr[count]);
  }
}
```

上述函数封装了一段代码，可以通过下述代码调用：

`shout();`

我们可以向函数中传递参数（argument）。

```js
function name(arguments){
  statements;
}
```

参数还可以有返回值。

```js
function multiply(num1,num2){
  var total = num1 * num2;
  return total;
}
```

还可以用一个变量接收函数的结果。

```js
var a = 10;
var b = 20;
var result = multiply(a,b);
alert(result);
```

变量的作用域（scope）

全局变量（global variable）：可以在脚本中的任何位置被引用。

局部变量（local variable）：只存在于声明它的那个函数内部。

##对象

对象是自包含的数据集合，对象内部的数据可以通过两种形式访问，属性（property）和方法（method）。

实例（instance），实例是对象的具体个体。

例如，你和我都是人，都可以用Person对象来描述，但你和我是两个不同的个体，很可能有着不同的属性（可能年龄不一样，身高不一样），因此，你和我对应着两个不同的Person对象，它们虽然都是Person对象，但它们是两个不同的实例。

###内建对象

数组就是内建对象的一种，初始化一个数组相当于创建一个Array对象的实例。

```js
var arr = new Array();
```

Math对象和Date对象也是内建对象，他们的作用分别是提供了处理数值和日期值。

内建对象的作用就是，可以帮助我们快速、简单的完成许多任务。

###宿主对象

宿主对象不是由JavaScript提供的预定义对象被称为宿主对象（host object），而是具体到Web应用，就是浏览器，由浏览器提供的预定义对象被称为宿主对象。

宿主对象包括Form、Image和Element等，我们可以通过这些对象获得关于网页上表单、图像和各种表单元素的信息。

其中还有一个宿主对象document，后续会说。

##小结
没啥说的，学就完事了。





