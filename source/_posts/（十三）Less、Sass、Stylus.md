---
title: （十三）Less、Sass、Stylus
date: 2019-12-28 16:58:31
tags: CSS
---
# Less、Sass、Stylus

## CSS预处理器

CSS预处理器是一种新的语言，开发者使用这种语言进行开发，最终这种编写好的语言可以转换为CSS语言。

CSS预编译器的好处：

+ 可读性强。
+ 适应性强。
+ 可维护性强。

## 简介

Less：Leaner Style Sheets，less和css语言非常像，因此非常容易学习。

Sass：Syntactically Awesome Stylesheets，sass基于Ruby语言开发而成，因此使用之前要安装Ruby。

Stylus：富有表现力的、动态的、健壮的CSS。

## 使用

Less

变量：
使用@定义变量，样式代码中可以直接使用。

```less
@height: 100px;
@width: 100px;

#a {
  width: @width;
  height: @height;
  border: solid 1px;

  position: absolute;
  top: 50%;
  left: 50%;
  -webkit-transform: translate(-50%,-50%);

  line-height: @height;
  text-align: center;
```

混合：

混合的意思就是将一组属性从一个规则集包含（或混合）到另一个规则集中。

```less
@height: 100px;
@width: 100px;

.box{
  width: @width;
  height: @height;
  border: solid red 1px;
}

#a {
  .box()
}
```

嵌套：

```html
<div id="a">
    a
    <div class="b">b</div>

    <div class="c">c</div>
</div>
```

```less
@fatherWidth: 500px;
@fatherHeight: 500px;
@width: 100px;
@height: 100px;

#a {
  width: @fatherWidth;
  height: @fatherHeight;
  border: solid red 1px;

  .b {
    width: @width;
    height: @height;
    border: solid green 1px;
  }

  .c {
    width: @width;
    height: @height;
    border: solid blue 1px;
  }
}
```
嵌套可以配合混合和伪类一起使用。

函数：

```less
@top: 0.5;
@left: 0.5;

#a {
  width: 100px;
  height: 100px;
  border: solid red 1px;

  position: absolute;
  top: percentage(@top);
  left: percentage(@left);
  -webkit-transform: translate(percentage(-@top),percentage(-@left));
}
```

其中percentage函数可以将数字转换为百分数。


Sass

Sass和Scss的异同

Scss是Sass引入的新的语法，其语法完全兼容CSS3，并且继承了Sass的功能，我们熟悉了Sass的语法也就了解了Scss的语法。

Sass与Scss唯一的不同就是，Sass是使用换行和空格缩进的，Scss是使用分号和花括号缩进的。

由于本人习惯，下面都使用Scss来举例。

变量：

使用$定义变量。

```scss
$wid: 100px;
$hei: 100px;

#a {
  width: $wid;
  height: $hei;
  border: solid red 1px;
}
```

混合：

使用@mixin定义重复使用的混合器，使用@include混合器。

```scss
@mixin center {
  position: absolute;
  top: 50%;
  left: 50%;
  -webkit-transform: translate(-50%,-50%);
}

#a {
  width: 100px;
  height: 100px;
  border: solid 1px red;
  @include center;
}
```

嵌套：

```html
  <div id="a">
    a
    <div id="b">b</div>
    <div id="c">
      c
      <div id="d">
        d
      </div>
    </div>
  </div>
```

```scss
@mixin bigbox{
  width: 500px;
  height: 500px;
  border: solid 1px red;
}

@mixin normalbox{
  width: 200px;
  height: 200px;
  border: solid 1px green;
}

@mixin smallbox{
  width: 100px;
  height: 100px;
  border: solid 1px;
}

#a {
  @include bigbox;
  #b {
    @include normalbox;
  }

  #c {
    @include normalbox;
    #d {
      @include smallbox;
    }
  }
}
```

继承：

我们可以继承某个类的属性，继承之后这个类的所有属性都会在这个元素生效，我们还可以继续细化样式，修改想要的样式。

使用@extend加类名继承。

```scss
.box {
  width: 100px;
  height: 100px;
  border: solid red 1px;
}

#a {
  @extend .box;
  border: solid green 2px;
}
```

这样我们继承了box类的属性，还修改了我们想要的样式。

Stylus

选择器：

Stylus的写法与Less和Scss不同，Stylus是使用换行和空格来规定格式的。

用换行和空格代替花括号和引号

```styl
#a
  height: 100px
  width: 100px
  border: solid red 1px
```

上述代码的冒号也可以省略。

```styl
#a
  height 100px
  width 100px
  border solid red 1px
```

选择多个元素，可以使用逗号隔开，也可使用换行隔开。

```styl
div, p
  color red
```

```styl
div
p
  color red
```

父级选择

使用&代替父级元素

```styl
#a
  & div
    width 100px
    height 100px
    border solid red 1px
```

变量：

Stylus使用赋值号定义变量。

```styl
font-size = 14px

body
  font-size Arial, sans-seri
```

混合：

Stylus混合写法与函数写法类似，但使用大相径庭。

```styl
border-radius(n)
  -webkit-border-radius n
  -moz-border-radius n
  border-radius n

form input[type=button]
  border-radius(5px)
```