### 特点

与其他语言不同的是，ECMAScript 数组的每一项可以保存任何类型的数据

数组多可以包含2^32个项，这几乎已经能够满足任何编程需求了

-----------------------------------------------------------------------

### 创建

创建数组的基本方式有两种

使用 Array 构造函数：如果传递的是数值，则会按照该数值创建包含给定项数的数组，而如果传递的是其他类型的参数，则会创建包含那个值的只有一项的数组

```js
var colors1 = new Array();   // 空数组
var colors2 = new Array(20); // 指定数组长度为20
var colors3 = new Array("red", "blue", "green"); // 创建数组，并赋初始值
```

使用 [] 字面量：与对象一样，在使用数组字面量表示法时，也不会调用 Array 构造函数

```js
var colors = ["red", "blue", "green"];
```

--------------------------------------------------------

### length

数组的length属性很有特点——它不是只读的，可以通过设置这个属性，可以从数组的末尾移除项或向数组中添加新项

```js
var colors = ["red", "blue", "green"]; // 创建一个包含 3 个字符串的数组 
colors.length = 4; 
alert(colors[3]); //undefined

var colors = ["red", "blue", "green"];    // 创建一个包含 3 个字符串的数组 
colors[colors.length] = "black";          //（在位置 3）添加一种颜色 
colors[colors.length] = "brown";          //（在位置 4）再添加一种颜色  

var colors = ["red", "blue", "green"];     // 创建一个包含 3 个字符串的数组 
colors[99] = "black";                    // （在位置 99）添加一种颜色 
alert(colors.length); // 100

// 向colors数组的位置99插入了一个值，数组新长度就是100 (99+1)
// 而位置3到位置98实际上都是不存在的，所以访问它们都将返回 undefined
```

---------------------------------------------------------------

### 检测对象是不是数组

方法一：instanceof，前提是只有一个全局环境

方法二：Arrya.isArray，最好用的方法

```js
var arr = [1,2,3];
console.log(arr instanceof Array); // true
console.log(Array.isArray(arr); // true
```

----------------------------------------------------------------------

### 常用方法

##### 栈方法和队列方法 **[数组本身改变]**

| 方法    | 功能         |
| ------- | ------------ |
| push    | 数组尾加元素 |
| pop     | 数组尾弹元素 |
| unshift | 数组头加元素 |
| shift   | 数组头弹元素 |

##### 转换方法 **[数组本身没有改变]**

| 方法             | 功能                                                         |
| ---------------- | ------------------------------------------------------------ |
| toString()       | 返回由数组中每个值的字符串形式拼接而成的一个以逗号分隔的字符串，为了创建这个字符串会调用数组每一项的 toString()方法 |
| toLocaleString() | 返回由数组中每个值的字符串形式拼接而成的一个以逗号分隔的字符串，为了创建这个字符串会调用数组每一项的 toString()方法 |
| valueOf()        | 返回的还是数组                                               |

##### 排序方法和倒置方法 **[数组本身改变]**

| 方法          | 说明                        |
| ------------- | --------------------------- |
| sort()        | 按照valueOf的值从小到大排序 |
| sort(compara) | 自定义排序方法              |
| reverse()     | 数组倒置                    |
```js
function compara(left, right) {
    if (left < right) { return -1; }
    else if (left === right) { return 0; }
    else { return 1; }
}
```

##### 搜索方法 **[数组本身没有改变]**

| 方法                           | 功能                                                        |
| ------------------------------ | ----------------------------------------------------------- |
| indexOf(value)                 | 自开头从左向右搜索value对应的下标，找不到就返回-1           |
| indexOf(value, startIndex)     | 自startIndex下标从左向右搜索value对应的下标，找不到就返回-1 |
| lastIndexOf(value)             | 自最后从右向左搜索value对应的下标，找不到就返回-1           |
| lastIndexOf(value, startIndex) | 自startIndex下标从右向左搜索value对应的下标，找不到就返回-1 |

##### 迭代方法 **[数组本身没有改变]**

| 方法          | 功能                                                         |
| ------------- | ------------------------------------------------------------ |
| every()       | 对数组中的每一项运行给定函数，如果该函数对每一项都返回 true，则返回 true |
| some()        | 对数组中的每一项运行给定函数，如果该函数对任一项返回 true，则返回 true |
| map()         | 对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组 |
| filter()      | 对数组中的每一项运行给定函数，返回该函数会返回 true 的项组成的数组 |
| forEach()     | 对数组中的每一项运行给定函数。这个方法没有返回值             |
| reduce()      | 从数组的第一项开始，逐个遍历到最后                           |
| reduceRight() | 从数组的后一项开始，向前遍历到第一项                         |

迭代函数中接收都是接收两个参数

参数1：function(item,index,array)
* item： 必须，当前处理的数组的值
* index：可选，当前处理的值得索引
* array：可选，当前处理的值所属于的数组对象

参数2：可选

该对象作为该执行回调时使用，传递给函数用作"this"的值。如果省略了 thisValue，"this"的值为 "undefined"

##### 数组拼接裁剪

concat **[数组本身没有改变]**
```js
var colors = ["red", "green", "blue"]; 
var colors2 = colors.concat("yellow", ["black", "brown"]); 
 
alert(colors);     //red, green, blue         
alert(colors2);    //red, green, blue, yellow, black, brown 
```

slice **[数组本身没有改变]**
| 方法                        | 功能                                               |
| --------------------------- | -------------------------------------------------- |
| slice(startIndex)           | 返回从startIndex开始到数组末尾的所有项组成的新数组 |
| slice(startIndex, endIndex) | 返回从startIndex开始到endIndex的所有项组成的新数组 |
注意：[startIndex, endIndex)，左闭右开区间，不包括 endIndex 位置的元素

splice **[数组本身改变]**

> splice(操作的下标，删除元素个数，...要插入的元素)，始终返回一个空数组

| 例子                       | 说明                                                         |
| -------------------------- | ------------------------------------------------------------ |
| splice(0,2)                | 删除数组中的前两项，返回一个空数组                           |
| splice (2,1,"red","green") | 删除数组位置2的项，然后再从位置2开始插入字符串"red"和"green"，返回一个空数组 |
| splice(2,0,"red","green")  | 从位置2开始插入字符串"red"和"green"，返回一个空数组          |