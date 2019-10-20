### 组件化思想

对于一个应用，如果将页面中所有的处理逻辑全部放在一起，处理起来就会变得非常复杂，而且不利于后续的管理以及扩展，但如果将一个页面拆分成一个个小的功能块，每个功能块完成属于自己这部分独立的功能，则整个页面的管理和维护就变得非常容易了

这样一个一个的功能块称为组件，任何的应用都可以抽象为一颗组件树

![](./image/component-tree.png)

<br/>

### 创建组件

通过调用Vue的`Vue.extend`方法来创建组件

```js
const myComponent = Vue.extend({
    template: `
        <div>
            <h2>{{ name }}</h2>
            <p>我是组件中的段落内容</p>
        </div>
    `,
    data: () => {
        return {
            name: "Vue",
            age: 10
        }
    }
});
```

注意点：

* 没有`el`属性
* `data`必须一个函数，这个函数返回数据对象，原因是在于Vue让每个组件对象都返回一个新的对象，因为如果是同一个对象的，组件在多次使用后会相互影响
* 在新版本的Vue中，可以不使用`Vue.extend`函数，而是直接使用参数对象就可以创建组件

<br/>

### 注册组件

注册组件可以分为`全局注册`和`局部注册`

#### 全局注册

通过`Vue.component`来实现全局注册组件，使用全局注册的组件，可以作为任何Vue实例的组件

`Vue.component`注册语法

```js
Vue.component("组件名", 组件对象)
```

例子

```js
const myComponent = Vue.extend({
    template: "<div>{{name}}</div>",
    data: () => ({ name: "Vue" })
});

Vue.component("MyComponent", myComponent)
```

在新版本的Vue中，可以不使用`Vue.extend`函数，而是直接使用参数对象就可以创建组件

```js
Vue.component("MyComponent", {
    template: "<div>{{name}}</div>",
    data: () => ({ name: "Vue" })
});
```

#### 局部注册

通过Vue实例对象的components属性来实现局部注册组件，使用局部的组件，只能在该Vue实例下使用

局部注册语法

```js
new Vue({
    components: {
        "组件名": 组件对象
    }
});
```

例子

```js
new Vue({
    components: {
        "MyComponent": {
            template: "<div>{{name}}</div>",
            data: () => ({ name: "Vue" }),
            components: {
                template: "<h2>{{number}}</h2>",
                data: () => ({ number: 10 }),
            }
        }
    }
});
```

#### 模板分离写法

如果将模板字符串写在组件对象中，如下

```js
const myComponent = Vue.extend({
    template: `
        <div>
            <h2>{{ name }}</h2>
            <p>我是组件中的段落内容</p>
        </div>
    `
});
```

则会使代码难以书写和维护，看起来很不舒服，则此时可以将模板分离出去，通过id进行绑定

写法1：通过template标签（推荐写法）

```html
<template id="my-template">
<div>
    <h2>{{ name }}</h2>
    <p>我是组件中的段落内容</p>
</div>
</template>

<script>
new Vue({
    template: "#my-template"
})
</script>
```

写法2：通过script标签

```html
<script type="text/x-template" id="my-template">
<div>
    <h2>{{ name }}</h2>
    <p>我是组件中的段落内容</p>
</div>
</script>

<script>
new Vue({
    template: "#my-template"
})
</script>
```

<br/>

### 使用组件

在实例的template中直接使用组件名即可

```html
<div>
    <Home></Home>
</div>
```

注意：由于HTML是不区分大小写的，所以如果组件名使用了Pascal命名方式，则在标签中需要使用`-`进行连接

```html
<div>
    <my-component></my-component>
</div>

<script>
Vue.component("MyComponent", {
    template: "<div>{{name}}</div>",
    data: () => ({ name: "Vue" })
});
</script>
```

<br/>

### 组件间通信

每个组件的数据是独立且不公开的，即一个组件不能直接访问另外一个组件的数据，需要进行组件间通讯

#### 父组件 ==> 子组件通讯

父组件通过使用 `v-bind` 指令绑定需要传递的属性，实现父组件向子组件传值

```html
<div id="app">
    <my-component :num="123" :flag="true" />
</div>
```

子组件通过`props`属性对传入值进行验证、接收和设置默认值，`props`的值可以是数组或对象

如果是数组，则只能接收，不能进行验证和设置默认值

```html
<div id="app">
    <my-component :num="123" :flag="true" />
</div>

<script>
Vue.componenet("MyComponent", {
    props: ["num", "flag"]
});
</script>
```

如果是对象，则可以进行验证、接收和设置默认值

```html
<div id="app">
    <my-component :num="123" :flag="true" />
</div>

<script>
Vue.componenet("MyComponent", {
    props: {
        num: {
            type: Number,
            required: true,
        },
        flag: {
            type: Boolean,
            required: false,
            default: false
        }
    }
});
</script>
```

支持验证的类型：Number, String, Boolean, Array, Object, Function, Symbol, Date

#### 子组件 ==> 父组件通讯

Vue是单向数据流，当子组件从父组件获取到数据后props，不能直接修改props上的数据，而是应该把props上的数据拷贝一份到data或computed中，再进行修改

通过父组件在子组件上设置自定义事件以及回调函数，子组件通过使用`$emit`触发事件执行回调函数来向父组件传值

`$emit`使用语法

```js
$emit("事件名", 参数列表)
```

例子：计时器

```html
<div id="app">
    <child-cpn @increment="changeTotal" @decrement="changeTotal"></child-cpn>
    <h2>点击次数：{{total}}</h2>
</div>

<template id="childCpn">
    <div>
        <button @click="doIncrement">+1</button>
        <button @click="doDecrement">+1</button>
    </div>
</template>

<script>
new Vue({
    el: "#app",
    data: {
        total: 0
    },
    methods: {
        changeTotal(count) {
            this.total = count;
        }
    },
    components: {
        "childCpn": {
            template: "#childCpn",
            data() {
                return {
                    count: 0
                }
            },
            methods: {
                doIncrement() {
                    this.count++;
                    this.$emit("increment", this.count);
                },
                doDecrement() {
                    this.count--;
                    this.$emit("decrement", this.count);
                }
            }
        }
    }
});
</script>
```

#### BUS总线机制进行组件间通讯

#### 父组件直接获取子组件对象

有时候我们需要父组件直接访问子组件

##### $children

`this.$children`是一个数组类型，它包含所有子组件对象

##### $refs

通过`$children`访问子组件时，是一个数组类型，访问其中的子组件必须通过索引值，但是当子组件过多，我们需要拿到其中一个时，往往不能确定它的索引值，甚至还可能会发生变化，这时可以使用`$refs`明确获取其中一个特定的组件

$refs和ref指令通常是一起使用的，通过ref给某一个子组件绑定一个特定的ID，然后就可以通过`this.$refs.ID`访问到该组件

```html
<child-cpn1 ref="child1"></child-cpn1>
<child-cpn2 ref="child2"></child-cpn2>
<button @click="showRefsCpn">通过refs访问子组件</button>

showRefsCpn() {
    console.log(this.$refs.child1.message);
    console.log(this.$refs.child2.message);
}
```

#### 子组件直接获取父组件对象

有时候我们需要子组件直接访问父组件，或者是子组件访问根组件，

##### $parent

`this.$parent`指向父组件对象

应用内尽量不要直接访问父组件对象，更不应该通过`$parent`直接修改父组件的状态

##### $root

`this.$root`指向根组件对象

<br/>

### 插槽slot机制

