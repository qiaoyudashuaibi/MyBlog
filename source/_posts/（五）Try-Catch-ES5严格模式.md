---
title: （五）Try Catch ES5严格模式
date: 2019-11-15 14:10:13
tags: JavaScript
---
代码写在try里面，出现错误终止，执行catch中的代码，不影响后续代码的执行。
不确定自己写的代码是否有错，将代码写在trycatch中。
```
try(){

}catch() {

}
```
Error.name分为六种对应的信息：
1.EvalError：eval()的使用与定义不一致。
2.RangeError：数值越界。
3.ReferenceError：非法或不能识别的引用数值。
4.SyntaxError：发生语法解析错误。
5.TypeError：操作数类型错误。
6.URIError：URI处理函数使用不当。


es5严格模式
当前浏览器是基于es3.0 + es5.0的新增方法。
5.0与3.0冲突的部分，采用3.0的标准。
如果采用es5严格模式，则冲突的部分采用es5.0。

如何启用es5标准模式：
```
"use strict";
function test() {
console.log(arguments.callee);
}
test();
```

在代码开头写上“use strict”，表示启用es5严格模式。
这时在浏览器输出的结果是：
![Image text](https://github.com/qiaoyudashuaibi/MyBlog/tree/master/source/images/clipboard.png)


表示callee不能在es5严格模式中使用arguments调用，如果不输入“use strict”，则结果如下：
![Image text](https://github.com/qiaoyudashuaibi/MyBlog/tree/master/source/images/clipboard(1).png)

es5严格模式有两种用法：
1.全局严格模式，写在整个js文件的开头。
2.局部函数内严格模式，写在函数的开头。（推荐）

为什么要使用字符串来开启es5严格模式？
因为我们无法保证所有的浏览器都升级了es5内核，如果将开启es5严格模式写成函数调用的形式，就有可能报错，而写成字符串的形式，浏览器会把字符串看成一个表达式，低版本浏览器虽然不能识别这个字符串为开启es5严格模式的语句，但不会报错。

es5严格模式下还禁止了哪些函数呢？
with函数
```
   var obj = {
            name: "obj"
        }
        var name = 'window';
        function test() {
            var name = 'scope';
            with (obj) {
                console.log(name);
            }
        }
        test();
```


最后test()，的输出结果为obj。可见with函数可以改变作用域对象AO。
由于with修改的是作用域链，功能过于强大，所以es5严格模式中，禁止使用with。

严格模式还规定：
1.变量赋值前必须声明。
```
a = 1;
a = b =  1;
```

这种写法在严格模式中是不被允许的。
2.局部的this必须被赋值，而且赋值什么就是什么。
```
"use strict";
 function test () {
            console.log(this);
        }
        test();
```

![Image text](https://github.com/qiaoyudashuaibi/MyBlog/tree/master/source/images/clipboard(2).png)


在严格模式下，上述代码返回值是undefined，因为当前this并没有被赋值，如果将test方法实例化，则当前this的值为test。
```
 "use strict";
function test () {
            console.log(this);
        }
            new test();
```

![Image text](https://github.com/qiaoyudashuaibi/MyBlog/tree/master/source/images/clipboard(3).png)


在全局情况下this不受影响，因为this无法被改变，默认是window。
3.严格模式下拒绝重复的参数和属性。