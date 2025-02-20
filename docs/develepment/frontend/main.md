## 前端基础知识

这一部分内容不是很会，正在学习。

我们要通过css来调整网页的布局。

参考资料:

[CSS 选择器 - CSS：层叠样式表 | MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_selectors)

计划是我学一点东西就稍微记一点，然后等我掌握比较熟练，就出一下完整网页的讲解。

### CSS属性

#### 1.CSS语法

CSS 由 **选择器（Selector）** 和 **声明（Declaration）** 组成：

```css
选择器 {
    属性: 值;
}
```

##### 例子：

```css
p {
    color: red;       /* 设置文本颜色为红色 */
    font-size: 20px;  /* 设置字体大小为20px */
}
```

像这样就是设置所有的 `<p>` 标签的样式。

每个属性后面要分号，大括号后面不要分号！

#### 2.CSS选择器

选择器有好多种，只说一下我目前用过的。

##### 通用选择器

```css
* {
}
```

匹配文档的所有元素。给所有标签设置样式。

##### 元素选择器

```css
header {
    display: flex;
    padding: 5px;
    margin: 0px;
    align-items: center;
}
```

类似这种，前面是标签名。可以设置所有这个标签的样式。我这个就是设置的所有的 `<header>` 标签的样式。

##### 类选择器

选择特定的类。

```css
.navbar {
    display: flex;
    align-items: center;
    margin-left: auto; /* 使得导航栏自动移动到右边 */
    margin-right: 50px;
}
```

选择所有navbar类，大括号前面是 `.classname` ，一个点+类名。在需要的标签里设置class属性，然后通过class来选择元素。

##### ID选择器

按照 `id` 属性选择一个与之匹配的元素。需要注意的是，一个文档中，每个 ID 属性都应当是唯一的。

**语法：**`#idname`

**例子：**`#toc` 匹配 ID 为 "toc" 的元素。

这个还没用过，`id` 属性还没用过。

##### 组合选择器

可以同时选择多个元素。

```css
.search_button, .search_input {
    box-sizing: border-box; /* 使得输入框和搜索按钮高度相同 */
    height: 32px;
    align-items: center;
    display: flex;
    justify-content: center;
}
```

我这个就是同时设置这两个类的属性，可以简化这些共同的属性，不需要写两次了。。

用法就是 `A, B` ，可以选择多个元素，用逗号连接，可以是不同的选择器连一起，例如元素选择器和类选择器，也可以组成一个选择器列表。

##### 后代选择器

可以设置不同的层级。

```css
.product p {
    display: -webkit-box;
    -webkit-line-clamp: 2;  /* 限制最多显示3行 */
    -webkit-box-orient: vertical;  /* 垂直排列 */
    overflow: hidden;  /* 超出内容隐藏 */
    text-overflow: ellipsis;  /* 超出部分显示省略号 */
    white-space: normal;  /* 允许换行 */
    word-wrap: break-word;  /* 自动换行 */

    line-clamp: 2;                     /* 标准写法 */
    box-orient: vertical;              /* 标准写法 */
}
```

用法就是 `A B` ，用空格隔开，按层级选择的，也可以多层，但是一般没必要。也是可以类名和元素名这些混合的，非常的爽啊。

### 引入css的方式有3种常见方式:

#### 外部引入

在head部分添加 `link` 标签引入外部CSS文件。

```html
<link rel="stylesheet" href="./css/main.css">
```

还可以通过CDN引用，或者直接下载框架，有的会有写好的CSS，比如bootstrap。

CSS写在单独的文件里的一个很好的地方就是，VS Code用快捷键注释代码时，无法注释HTML里的style标签的内容，因为HTML和CSS的注释是不一样的。

注意单词不要写错了，`stylesheet` 后面没有s。

#### 内部CSS

直接在style标签中写CSS代码。

一般把style标签放在head标签里。

```html
<head>
    <style>
        body {
            background-color: lightblue;
        }
    </style>
</head>

```

#### 行内CSS

直接在HTML标签的 `style` 标签中写代码。

```html
<img src="img/junjie.jpg" width="64px" style="margin-right: 2em; ">
```

比较适合临时样式，而且比较方便控制。

### 引入字体

#### CDN引入

```css
/* 引入霞鹜文楷 */
@import url('https://cdn.jsdelivr.net/npm/lxgw-wenkai-webfont@1.1.0/style.css');

/* 全局设置字体 */
body {
  font-family: 'LXGW WenKai', serif !important;
}
```

