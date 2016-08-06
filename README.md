# JavaScript知识点的整理--每天更新一点点^_^

------------
## JS简介
#### JS简史
为了完成简单的表单验证而频繁的与服务器进行交换数据，只会加重用户的负担，想象一下：用户填写完一个表单，单击了“提交”按钮，等了30秒。服务器既然返回说：您有一个必填字段没有填好。。。敢问你什么心情，使所以为了解决这一问题，Netscape公司决定开发一种客户端语言，来处理简单的验证。
#### JS的实现
**一个完整的JS实现由三个不同的部分组成:**
- 核心（ECMAScript），由ECMA-262定义，提供核心语言功能
- 文档对象模型（DOM），提供访问和操作网页内容的方法与接口
- 浏览器对象模型（BOM），提供与浏览器交互的方法与接口

------------


## 在HTML中使用JS
#### `<script>`元素
`<script>`元素定义了6个属性：
- `async`:规定异步执行脚本（仅适用于外部脚本）。
- `charset`:规定在外部脚本文件中使用的字符编码。
- `defer`:规定是否对脚本执行进行延迟，直到页面加载为止。（仅适用于外部脚本）
- `language`:**已废弃**。规定脚本语言。请使用 type 属性代替它。
- `src`:规定外部脚本文件的 URL。
- `type`:可以看成是language的替代属性，表示编写代码使用的脚本语言的内容类型（也称为MIME类型）

使用`<script>`元素的方式：
1. 直接在页面中嵌入JS代码
使用该方法时，只须为`<script>`指定`type`属性
```javascript
<script type="text/javascript">
function sayScript() {
    alert("<\/script>");
    // 上述代码字符进行转义(escaping)操作
}
</script>
```
2. 外部JS文件，必须设定`src`属性为指向相应文件的URL，而这个文件可以是与包含它的页面位于同一服务器上的文件，也可以是其他任何域中的文件，并且有优点：
- 可维护性
- 可缓存
- 适应未来

```javascript
    <script type="text/javascript" src="example.js"></script>
```

#### 标签的位置
放在`<body>`元素的内容后面，这样在解析JS代码之前，页面的内容将完全呈现于浏览器中。
```javascript
    <!DOCTYPE html>
    <html lang="en">
    <head>
    	<meta charset="UTF-8">
    	<title>Document</title>
    </head>
    <body>
        <!-- 这里放内容 -->
    	<script type="text/javascript" src="example.js"></script>
    </body>
    </html>
```
------------
## 基本概念
#### 语法
- 区分大小写
- 标识符

  - 第一个字符必须是一个字母、下划线(_)、或者美元符号($);
  
  - 其他字符可以是字母、下划线、美元符号或数字
  
- 注释

  - //单行注释
  
  - /**/块级注释
  
- 严格模式 --- "use strict"

- 语句结尾的分号不能少


#### 数据类型
**1. `typeof`操作符**

```javascript
    		console.log(typeof(Object));   //function
    		console.log(typeof(Array)); //function
    		console.log(typeof(Function));//function
    		console.log(typeof(123)); //number
    		console.log(typeof(NaN));  //number
    		console.log(typeof('str'));  //string
    		console.log(typeof(''));    //string
    		console.log(typeof(true));   //boolean
    		console.log(typeof(false));  //boolean
    		console.log(typeof(Math.abs));  //function
    		console.log(typeof(undefined)); //undefined
    		console.log(typeof(null));   //object
    		console.log(typeof([]));     //object
    		console.log(typeof({}));    //object
```
`typeof`操作符的操作数可以是变量，也可以是数值字面量。注意：**`typeof`是一个操作符而不是函数**

**2.` Undefined`类型**
在使用var声明变量但未对其加以初始化的时候，这个变量的值就是`undefined`，例如：

```javascript
    var msg;
    alert(msg === undefined); //true
```
包含`undefined`值的变量与尚未定义的变量的不同之处：

```javascript
    var message ; //默认取得undefined值
    //下面这个变量未声明
    //var age 
    alert(message); //undefined
    alert(age);     //报错
    
    //对未初始化和未声明的变量执行typeof操作符都返回了undefined值
    alert(typeof(message));//undefined
    alert(typeof(age));    //undefined
```

**3.` Null`类型**
`null`值表示一个空对象指针，这也正是使用`typeof`操作符检测时会返回"`object`"的原因。
```javascript
    var car = null;
    alert(typeof(car)); //object
    alert(null === undefined);//false

//undefine值是派生自null值的：
alert(null == undefined); //true
```
如果定义的变量准备在将来用来保存对象，那么最好将该变量初始化为`null`，这样只要检查`null`值便可以知道变量是否已经保存了一个对象的引用，如：
```javascript
    if (car != null) {
    	// 对car对象进行操作
    }
```

**`null`与`undefined`的区别**
- 对于`undefined`，无论在什么情况下都没有必要把一个变量的值设置为`undefined`。
- 对于`null`，只要在保存对象的变量还没有真正的保存对象之前，就应该让该对象保存`null`值。

**4.` Boolean`类型**
为变量赋`Boolean`类型值的例子：

```javascript
    var found = true;
    var lost = false;
```

将一个值转换成对应的boolean值，可以调用转型函数Boolean(),例子：

```javascript
    var msg = "HEllO";
    var msgAsBoolean = Boolean(msg);
```

JS中会把 null undefined 0 NaN 和空字符串'' 视为false，其他的数据类型一律为true
```javascript
    var s = '123';
    if (s) {
    	alert("True");
    }
```
**5.` Number`类型**
- 十进制数：
```javascript
 var intNum = 55;
```
- 八进制数:第一位必须是零，然后是八进制数字序列（0 ~ 7）

```javascript
var octalNum = 070； //八进制的56`
var octalNum1 = 079； //无效的八进制数组--解析为79
var octalNum2 = 08； //无效的八进制数组--解析为8
```
- 十六进制数：前面两位必须是0x，后面跟十六进制数字（0 ~ 9及A ~ F）
```javascript
var hexNum = 0xA； //十六进制的10
var hexNum1 = 0x1f；  //十六进制的31
```
在进行算术运算时，所有的八进制与十六进制的数组最终会被转换成十进制数值进行运算。

**浮点数值**

```javascript
    var floatNum = 1.1; //1.1
    var floatNum1 = 10.0; //解析为整数  --- 10
    var floatNum2 = 3.125e7; //31250000
```
**注意**：由于浮点数计算会产生舍入误差的问题，例如：0.1加0.2的结果不是0.3，所以永远不要对某个浮点数值进行测试。

**数值范围**
ECMAScript的最小数组：`Number.MIN_VALUE`值为5e-324
ECMAScript的最大数组：`Number.MAX_VALUE`值为1.7976931348623157e+308

当计算的值超出范围时，这个值会自动转换成`Infinity`值，如果是负数，则转换为`-Infinity`，正数为`Infinity`

`isFinite()`函数会在参数位于最小与最大值之间返回`true`
```javascript
    var result = Number.MAX_VALUE + Number.MAX_VALUE;
    alert(isFinite(result));  //false
```
**NaN**
即非数值，任何数值除以0会返回`NaN`，这样的设计便不会影响其他代码的执行。
```javascript
alert(NaN == NaN); //false
alert(NaN === NaN); //false
```
`isNaN()`函数，该函数接受一个参数，该参数接受任何类型，用于判断其参数是否是 `NaN`，
该函数接受到一个数值后，会尝试将这个值转换成数值（某些不是数值的值会直接转换成数值，如字符串"10"与`Boolean`值），而不能被转换成数值的值会返回`true`。
例子：
```javascript
    alert(isNaN(NaN)); //true
    alert(isNaN(10));  //false (10为整数)
    alert(isNaN("10"));//false （可以转换成数值10）
    alert(isNaN("blue"));//true （不能转换成数值）
    alert(isNaN(true));//false   （可以转换成数值1）
```
**数值转换**
可以将非数值转换成数值的三个函数:
- `Number()`,可用于任何数据类型
- `parseInt()`，专门将字符串转换成数值
- `parseFloat()`，专门将字符串转换成数值


`Number()`函数的转换规则：
```javascript
    var num1 = Number(true); //1
    var num2 = Number(false);  //0
    var num3 = Number(5);  //5
    var num4 = Number(004);//4
    var num5 = Number(1.1);//1.1
    var num6 = Number(null);//0
    var num7 = Number(undefined); //NaN
    var num8 = Number("");//0
    var num9 = Number("Hello Wow");//NaN
    var num10 = Number("015.5");//15 .5（前导的零会被忽略）
```
由于`Number()`函数在转换字符串的时候比较复杂并且不合理，故在处理整数的时候更常用的是`parseInt()`函数。

`parseInt()`函数的转换规则：
```javascript
    var num0 = parseInt("abc12");//NaN
    var num1 = parseInt("");//NaN
    var num2 = parseInt("123blue");//123
    var num3 = parseInt("0xA");  //10
    var num4 = parseInt("0xf"); //15
    var num5 = parseInt(22.5);//22
    var num6 = parseInt(-10); //-10
    var num7 = parseInt("-10"); //-10
    var num8 = parseInt("015.5");//15
	
    //对于下面的例子会存在一些问题
    var num9 = parseInt("070");//70
    var num10 = parseInt("70");//70
    
    //为了消除上述疑惑，parseInt()函数提供第二个参数：转换时使用的基数（即多少进制）
    
    var num9fix = parseInt("070", 8);//56
    var num10fix = parseInt("070", 10);//70
    //指定基数会影响到转换的输出结果
    var num11 = parseInt("10", 2);//2
    var num12 = parseInt("10", 8);//8
    var num13 = parseInt("10", 10);//10
    var num14 = parseInt("10", 16);//16
```
`parseFloat()`函数的转换规则：
```javascript
    var num0 = parseFloat("abc12");//NaN
    var num1 = parseFloat("");//NaN
    var num2 = parseFloat("123blue");//123
    var num3 = parseFloat("0xA");  //0
    var num4 = parseFloat("0xf"); //0
    var num5 = parseFloat(22.5);//22.5
    var num6 = parseFloat(-10); //-10
    var num7 = parseFloat("-10"); //-10
    var num8 = parseFloat("015.5");//15.5
    var num9 = parseFloat("22.35.5");//22.35
    var num10 = parseFloat("3.125e7");//31250000
```
`parseFloat()`函数只能解析十进制数，因此它没有第二个参数来指定基数

**6.` String`类型**
1.  字符串的特点
字符串是不可变的，字符串一旦创建，它的值将不能改变。
要改变某个变量保存的字符串，必须先销毁原来的字符串。
2.  转换成字符串

toString()方法：数值、布尔值、对象和字符串值都有toString()方法，但是null与undefined没有toString()方法。

```javascript
    var age = 11;
    var ageAsString = age.toString(); //字符串"11"
    var found = true;
    var foundAsString = found.toString();//字符串"true"
```
大多数情况下，toString()方法不必传递参数，但是，在调用toString()方法时候可以传递一个参数。该参数规定了输出数组的基数。

```javascript
    var num = 10;
    alert(num.toString());  //"10"
    alert(num.toString(10));//"10"
    alert(num.toString(2));//"1010"
    alert(num.toString(8));//"12"
    alert(num.toString(16));//"a"
```

String()方法


