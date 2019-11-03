### Number的小数表示

#### Number类型保留小数点【num.toFixed】

```js
var num = 10; 
alert(num.toFixed(2));     //"10.00"

var num = 10.005; 
alert(num.toFixed(2));     //"10.01"
```

#### number类型以科学计数法表示【num.toExponential】

```js
var num = 10; 
alert(num.toExponential(1));  //"1.0e+1" 

var num = 99; 
alert(num.toPrecision(1));  //"1e+2" 
alert(num.toPrecision(2));  //"99" 
alert(num.toPrecision(3));  //"99.0" 
```

----------------------------------------------------------------------

### typeof 和 instanceof 对于 Number 类型

```js
var numberObject = new Number(10); 
var numberValue = 10; 

alert(typeof numberObject);   //"object" 
alert(typeof numberValue);    //"number" 

alert(numberObject instanceof Number);  //true 
alert(numberValue instanceof Number);   //false
```

--------------------------------------------------------

### 非数值转数值

有 3个函数可以把非数值转换为数值：Number()、parseInt()和 parseFloat()

#### Number() 函数规则(**与使用一元加操作符"+"的效果相同** )

* 如果是 Boolean 值，true 和 false 将分别被转换为1和 0
* 如果是 Number 值，直接返回本身
* 如果是 Null 值，返回 0
* 如果是 Undefined 值，返回 NaN
* 如果是 String 值，则使用以下规则
  * 如果字符串中只包含数字（包括前面带正号或负号的情况），则将其转换为十进制数值，即"1" 会变成 1，"123"会变成 123，而"011"会变成 11（注意：前导的零被忽略了） 
  * 如果字符串中包含有效的浮点格式，如"1.1"，则将其转换为对应的浮点数值（同样，也会忽 略前导零）
  * 如果字符串是空的（不包含任何字符），则将其转换为 0
  * 如果字符串中包含除上述格式之外的字符，则将其转换为 NaN
* 如果是 Object 值，则调用对象的valueOf()方法，然后依照前面的规则转换返回的值

#### parseInt() 函数规则

* 忽略字符串前面的空格，直至找到第一个非空格字符
* 如果第一个字符不是数字字符或者负号，parseInt()就会返回NaN，也就是说，用parseInt()转换空字符串会返回 NaN（Number()对空字符返回 0）
* 如果第一个字符是数字字符，parseInt()会继续解析第二个字符，直到解析完所有后续字符或者遇到了一个非数字字符
  * "1234blue"会被转换为 1234，因为"blue"会被完全忽略
  * "22.5" 会被转换为 22，因为小数点并不是有效的数字字符
* 如果字符串中的第一个字符是数字字符，parseInt()也能够识别出各种整数格式
  * 字符串以"0x"开头且后跟数字字符，就会将其当作一 个十六进制整数
  * 字符串以"0"开头且后跟数字字符，则会将其当作一个八进制数
* 这个函数提供第二个参数：转换 时使用的基数（即多少进制）

#### parseFloat() 函数规则

* 类似 parseInt()