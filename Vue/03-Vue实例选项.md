#### el

类型：选择器字符串 | HTMLElement

作用：决定Vue实例会管理的DOM

注意：该选项只存在于Vue根实例中

```html
<div id="app"></div>

<script>
new Vue({
    el: "#app" 
});
</script>
```

```html
<div id="app"></div>

<script>
var dom = document.getElementById("app");
    
new Vue({
    el: dom 
});
</script>
```

<br/>

#### template

类型：HTML模板字符串 | 选择器字符串

作用：定义Vue实例/组件的模板

注意：必须只有一个根标签

```html
<div id="app"></div>

<script>
new Vue({
    el: "#app",
    template: `<div>Hello World</div>`
});
</script>
```

```html
<div id="app"></div>

<template id="tl">
    <div>Hello World</div>
</template>

<script>
new Vue({
    el: "#app",
    template: "#tl"
});
</script>
```

<br/>

#### component

#### data

类型：Object | Function

作用：Vue实例/组件中的数据

注意：组件中data必须是一个返回数据对象的函数，目的是为了避免多个组件的数据共享

#### props

#### methods

类型：{ 方法名: Function }

作用：定义属于Vue实例/组件的方法

```html
<div id="app"></div>

<script>
new Vue({
    el: "#app",
    template: `<div>Hello World</div>`,
    methods: {
        sayHello: function() {
            console.log("Hello WOrld");
        },
        sayBye() {
            console.log("Bye Bye");
        }
    }
});
</script>
```

#### computed

类型

* { 属性名: Function }
* { 属性名: { get: Function, set: Function }}

作用：用于对data中的数据进行逻辑操作和计算，得到新的属性

注意：

* 计算属性是有缓存的，当其依赖的数据没有发生改变时，计算属性不会重新进行计算（执行函数）
* 如果不设置setter，则计算属性是只读的，简写版本就是个 getter



