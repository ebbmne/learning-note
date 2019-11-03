### 创建

String 类型是字符串的对象包装类型，可以像下面这样使用 String 构造函数来创建
```js
var stringObject = new String("hello world");
```

String 对象的方法也可以在所有基本的字符串值中访问到

-------------------------------------------------------------------------

### 获取特定字符

##### charAt()

方法以单字符字符串的形式返回给定位置的那个字符

```js
var stringValue = "hello world"; 
alert(stringValue.charAt(1));   //"e"
```

##### charCodeAt()

方法以单字符字符串的形式返回给定位置的那个字符的字符编码

```js
var stringValue = "hello world"; 
alert(stringValue.charCodeAt(1));   //输出"101"
```

##### fromCharCode()

方法由字符的字符编码返回单字符字符串

```js
var stringValue = "hello world"; 
alert(stringValue.charCodeAt(1));   //输出"101"
```

--------------------------------------------------------

### 拼接字符串

##### \+ 操作符

```js
var string1 = "Hello";
var string2 = "World";
var string3 = string1 + " " + string2;
```

##### concat

```js
var stringValue = "hello "; 
var result = stringValue.concat("world"); 
alert(result);          //"hello world" 
alert(stringValue);      //"hello"
```

------------------------------------------------------------------

### 搜索子串

##### indexOf

可以接收可选的第二个参数，表示从字符串中的哪个位置开始搜索

```js
var stringValue = "hello world"; 
alert(stringValue.indexOf("o")); //4 
alert(stringValue.indexOf("o", 5)); //7
```
##### lastIndexOf

可以接收可选的第二个参数，表示从字符串中的哪个位置开始搜索

```js
var stringValue = "hello world"; 
alert(stringValue.lastIndexOf("o")); //7 
alert(stringValue.lastIndexOf("o", 4)); //4 
```
##### search

```js
const str = "H123o H456o H789o H000o H999o";
const result = str.replace(/(\d+)/g, "66666");
console.log(result); // 1
```

----------------------------------------------------------

### 获取子串

##### slice

参数1：开始位置下标 | 参数2：结束位置下标

结果字符串：[ 开始位置下标，结束位置下标 )

注意：如果参数2不填，则默认值是字符串结尾

```js
const str = "Hello World";
str.slice(1,5); // "ello"
```

##### substring

参数1：开始位置下标 | 参数2：结束位置下标

结果字符串：[ 开始位置下标，结束位置下标 )

注意：如果参数2不填，则默认值是字符串结尾；所有负值参数都转换为 0

```js
const str = "Hello World";
str.substring(1,5); // "ello"
```

##### substr

参数1：开始位置下标 | 参数2：字符串长度

结果字符串：[ 开始位置下标，开始位置下标 + 字符串长度 )

注意：如果参数2不填，则默认值是字符串结尾

```js
const str = "Hello World";
str.substr(1,5); // "ello "
```

------------------------------------------------------

### 字符串大小写转换

##### toLowerCase、toLocaleLowerCase、toUpperCase、toLocaleUpperCase

```js
var stringValue = "hello world"; 
alert(stringValue.toLocaleUpperCase());  //"HELLO WORLD" 
alert(stringValue.toUpperCase());        //"HELLO WORLD" 
alert(stringValue.toLocaleLowerCase());  //"hello world" 
alert(stringValue.toLowerCase());        //"hello world" 
```

### 字符串切割

##### split

```js
const str = "1-2-3-4-5-6";
const result = str.split("-");
console.log(result); // [1,2,3,4,5,6]
```

----------------------------------------------------------------------

### 字符串去除首尾空格

##### trim

```js
const str = "   Hello World   ";
const result = str.trim();
console.log(result); // "Hello World"
```

-------------------------------------------------------

### 字符串比较函数

##### localeCompare(str)

这个方法比较两个字符串，并返回下列值中的一个 

* 如果字符串在字母表中应该排在字符串参数之前，则返回一个负数
* 如果字符串等于字符串参数，则返回 0
* 如果字符串在字母表中应该排在字符串参数之后，则返回一个正数

```js
var stringValue = "yellow";        
alert(stringValue.localeCompare("brick")); //1 
alert(stringValue.localeCompare("yellow")); //0 
alert(stringValue.localeCompare("zoo")); //-1
```

-------------------------------------------------

### 字符串的模式匹配方法

##### match

```js
const str = "H123o H456o H789o H000o H999o";
const result = str.match(/(\d+)/g);
console.log(result); // [123, 456, 789, 000, 999]
```

##### replace

```js
const str = "H123o H456o H789o H000o H999o";
const result = str.replace(/(\d+)/g, "66666");
console.log(result); // "H66666o H66666o H66666o H66666o H66666o";
```

##### search

```js
const str = "H123o H456o H789o H000o H999o";
const result = str.replace(/(\d+)/g, "66666");
console.log(result); // 1
```

