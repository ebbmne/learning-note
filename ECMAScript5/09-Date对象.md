### 创建

在调用 Date 构造函数而不传递参数的情况下，新创建的对象自动获得当前日期和时间

```js
const nowDate = new Date();
```

如果想根据特定的日期和时间创建日期对象，必须传入表示该日期的毫秒数，为了方便使用，可以两个方法
```js
//返回毫秒数，可以使用毫秒数生成Date对象，如果传入的字符串不能表示日期，那么它会返回NaN
Date.parse('01 Jan 1970 00:00:00 GMT');  

// 返回毫秒数，可以使用毫秒数生成Date对象
Date.UTC(2019, 9, 30, 18, 10, 22);

// 返回当前时间毫秒数
Date.now();
```

### Date常用方法

| 方法               | 功能            |
| ------------------ | --------------- |
| date.getFullYear() | 年              |
| date.getMonth()    | 月，1月是0      |
| date.getDate()     | 日              |
| date.getHours()    | 时              |
| date.getMinutes()  | 分              |
| date.getSeconds()  | 秒              |
| date.getDay()      | 星期，星期天是0 |
| date.getTime()     | 时间戳          |