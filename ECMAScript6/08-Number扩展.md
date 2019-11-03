#### 最大值和最小值

```js
console.log(Number.MAX_VALUE);
console.log(Number.MIN_VALUE);
```

--------------------------------------------------------------------

#### 最大整数和最小整数

MAX_SAFE_INTEGER合法的最大整数和最小整数
```js
console.log(Number.MAX_SAFE_INTEGER); // 2^53
console.log(Number.MIN_SAFE_INTEGER); // 2^(-53)
```

-----------------------------------------------------------

#### 2进制、8进制和16进制

二进制：以0b或0B开头

八进制：以0o或0O开头

十六进制：以0x或0X开头

```js
console.log(0b10010101010); // 二进制
console.log(0B10010101010); // 二进制
console.log(0o123747364); // 八进制
console.log(0O123747364); // 八进制
```

--------------------------------------------

#### Number.isNaN

判断是否是无限值/NaN

```js
Number.isNaN(123); // false
Number.isNaN(NaN); // true
```

--------------------------------------------------------------

#### Number.isFinite

判断是否是无限值

```js
Number.isFinite(Number.MIN1_SAFE_INTEGER); // true
Number.isFinite(Number.MAX_SAFE_INTEGER + 1); // false
```

---------------------------------------------

#### Number.isInteger

判断是否是整数

```js
Number.isInteger(25); // true
Number.isInteger(25.0); // true
Number.isInteger(25.1); // false
Number.isInteger("25"); // false
```

-----------------------------------

#### Number.isSafeInteger

判断是否是合法范围的整数

```js
Number.isSafeInteger(10); // true
Number.isSafeInteger(Number.MAX_SAFE_INTEGER+10); // true
```