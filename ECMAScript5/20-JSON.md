### JSON中的数据类型

* number：和JavaScript的number完全一致；
* boolean：就是JavaScript的true或false；
* string：就是JavaScript的string；
* null：就是JavaScript的null；
* array：就是JavaScript的Array表示方式——[]；
* object：就是JavaScript的{ ... }表示方式
### JSON的规定

* 字符集：必须是UTF-8
* 必须使用双引号，且键名需要用双引号引起来，不能省略引号
### JSON序列化

* 使用JSON.stringify来序列化一个对象
* 可以为对象添加名为toJSON的方法来定制序列化的操作
### JSON反序列化

* 反序列化指由一个JSON格式字符串，生成它对应的JavaScript对象
* 使用JSON.parse将JSON字符串生成一个JavaScript对象