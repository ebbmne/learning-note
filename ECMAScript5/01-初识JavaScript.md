### 浏览器中 JavaScript 的组成部分

1. ECMAScript
2. DOM - Document Object Model
3. BOM - Browser Object Model

<br/>

###  \<script> 标签的正确写法

符合规范的写法：
```html
<script type="text/javascript" src="example.js"></script>
```
不符合规范的写法：
```html
<script type="text/javascript" src="example.js" />
```

type属性的默认值是"text/javascript"，所以可以省略type属性

<br/>

###  \</script> 的使用注意点

在使用\<script>嵌入 JavaScript 代码时，记住不要在代码中的任何地方出现"\</script>"字符串，例如，浏览器在加载下面所示的代码时就会产生一个错误：
```html
<script type="text/javascript">
    function sayScript(){
        alert("</script>");
    }
</script>
```
而通过转义字符“/”可以解决这个问题，例如：
```html
<script type="text/javascript">
    function sayScript(){
        alert("<\/script>");
    }
</script> 
```

<br/>

###  \<script> 标签的 src 属性

带有 src 属性的\<script>元素不应该在其\<script>和\</script>标签之间再包含额外的 JavaScript 代码

如果包含了嵌入的代码，则只会下载并执行外部脚本文件，嵌入的代码会被忽略

src 属性可以包含来自外部域的 JavaScript 文件，即能够实现跨域（JSONP的实现原理）

<br/>

### \<script> 标签的位置

按照传统的做法，所有\<script>元素都应该放在页面的\<head>元素中这种做法的目的就是把所有外部文件（包括 CSS 文件和 JavaScript 文件）的引用都放在相同的地方。

但将 \<script> 全部放到 \<header> 标签中有存在这样的问题：必须等到全部JavaScript代码都被下载、解析和执行完成以后，才能开始呈现页面的内容（浏览器在遇到<body>标签时才开始呈现内容）。这对于那些需要很多JavaScript代码的页面来说，这无疑会导致浏览器在呈现页面时出现明显的延迟，而延迟期间的浏览器窗口中将是一片空白。

解决方法：现代 Web 应用程序一般都把全部JavaScript引用放在<body>元素中页面内容的后面，这样，在解析包含的 JavaScript代码之前，页面的内容将完全呈现在浏览器中。而用户也会因为浏览器窗口显示空白页面的时间缩短而感到打开页面的速度加快了。

<br/>

###  \<noscript> 标签

早期浏览器都面临一个特殊的问题，即当浏览器不支持JavaScript时如何让页面平稳地退化。对这个问题的最终解决方案就是创造一个\<noscript>元素，用以在不支持 JavaScript 的浏览器中显示替代
的内容
```html
<!DOCTYPE html>
<html>
    <head>
        <title>Example HTML Page</title>
        <script type="text/javascript" defer="defer" src="example1.js"></script>
        <script type="text/javascript" defer="defer" src="example2.js"></script>
    </head>
    <body>
        <noscirpt>
            你的浏览器不支持脚本，请更换更高级的浏览器
        </noscript>
    </body>
</html> 
```

包含在<noscript>元素中的内容只有在下列情况下才会显示出来

1. 浏览器不支持脚本
2. 浏览器支持脚本，但脚本被禁用

<br/>

### 延迟脚本(defer 属性)

在\<script>元素中设置defer 属性，相当于告诉浏览器立即下载，但延迟执行——脚本会被延迟到整个页面都解析完毕后再运行

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Example HTML Page</title>
        <script type="text/javascript" defer="defer" src="example1.js"></script>
        <script type="text/javascript" defer="defer" src="example2.js"></script>
    </head>
    <body>
        <!-- 这里放内容 -->
    </body>
</html> 
```

在现实当中，延迟脚本并不一定会按照顺序执行，也不一定会在 DOMContentLoaded 事件触发前执行，因此最好只包含一个延迟脚本。

<br/>

### 异步加载脚本

HTML5 为\<script>元素定义了async属性，async属性只适用于外部脚本文件，用于改变处理脚本的行为

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Example HTML Page</title>
        <script type="text/javascript" async="async" src="example1.js"></script>
        <script type="text/javascript" async="async" src="example2.js"></script>
    </head>
    <body>
        <!-- 这里放内容 -->
    </body>
</html> 
```

浏览器在遇到async标记的\<script>标签时，会下载并加载其src指向的 js 文件，但不会等待其下载加载完成后再执行之后的代码，而是立即执行下面的代码，所以异步脚本中不要在加载期对DOM节点进行修改操作

不能保证异步脚本按照它们在页面中出现的顺序执行，所以多个 async 标记的脚本不要存在依赖关系

<br/>

###  JavaScript代码写在外部js文件的优势（与写在\<script>标签中对比）

1. 更好的可维护性
2. 外部js文件可缓存
3. 更好的封装性和解耦

<br/>

### 浏览器的安全限制

以file://开头的地址无法执行如联网等JavaScript代码