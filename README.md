# javascript高级程序设计知识点整理--每天更新一点点^_^
初学JavaScript,若有不妥之处，欢迎提交问题。
------------
## JS简介
#### JS简史
为了完成简单的表单验证而频繁的与服务器进行交换数据，只会加重用户的负担，想象一下：用户填写完一个表单，单击了“提交”按钮，等了30秒。服务器既然返回说：您有一个必填字段没有填好。。。敢问你什么心情，使所以为了解决这一问题，Netscape公司决定开发一种客户端语言，**来处理简单的验证。**
#### JS的实现
**一个完整的JS实现由三个不同的部分组成:**
- **核心**（ECMAScript），由ECMA-262定义，提供核心语言功能
- **文档对象模型**（DOM），提供访问和操作网页内容的方法与接口
- **浏览器对象模型**（BOM），提供与浏览器交互的方法与接口

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
使用该方法时，**只须为`<script>`指定`type`属性**
```javascript
<script type="text/javascript">
function sayScript() {
    alert("<\/script>");
    // 上述代码字符进行转义(escaping)操作
}
</script>
```
2. 外部JS文件，**必须设定`src`属性为指向相应文件的URL**，而这个文件可以是与包含它的页面位于同一服务器上的文件，也可以是其他任何域中的文件，并且有优点：
- 可维护性
- 可缓存
- 适应未来

```javascript
    <script type="text/javascript" src="example.js"></script>
```

#### 标签的位置
**放在`<body>`元素的内容后面**，这样在解析JS代码之前，页面的内容将完全呈现于浏览器中。
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

  - 第一个字符**必须**是一个字母、下划线(_)、或者美元符号($);
  
  - 其他字符可以是字母、下划线、美元符号或数字
  
- 注释

  - //单行注释
  
  - /**/块级注释
  
- 严格模式 --- "use strict"

- 语句结尾的分号不能少

------------



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

------------


**2.` Undefined`类型**
在**使用var声明变量但未对其加以初始化**的时候，这个变量的值就是`undefined`，例如：

```javascript
    var msg;
    alert(msg === undefined); //true
```
包含`undefined`值的变量与尚未定义的变量的**不同之处**：

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

------------


**3.` Null`类型**
`null`值表示一个**空对象指针**，这也正是使用`typeof`操作符检测时会返回"`object`"的原因。
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
- 对于`undefined`，无论在什么情况下都**没有必要**把一个变量的值设置为`undefined`。
- 对于`null`，只要在保存对象的变量还没有真正的保存对象之前，**就应该让该对象保存`null`值**。

------------


**4.` Boolean`类型**
为变量赋`Boolean`类型值的例子：

```javascript
    var found = true;
    var lost = false;
```

将一个值转换成对应的`Boolean`值，可以调用转型函`数Boolean()`,例子：

```javascript
    var msg = "HEllO";
    var msgAsBoolean = Boolean(msg);//true
```

JS中会把 **null、 undefined、 0、 NaN和空字符串''** 视为false，其他的数据类型一律为true
```javascript
    var s = '123';
    if (s) {
        alert("True");
    }
```

------------


**5.` Number`类型**
- 十进制数：
```javascript
 var intNum = 55;
```
- 八进制数:**第一位必须是零**，然后是八进制数字序列（0 ~ 7）

```javascript
var octalNum = 070； //八进制的56`
var octalNum1 = 079； //无效的八进制数组--解析为79
var octalNum2 = 08； //无效的八进制数组--解析为8
```
- 十六进制数：**前面两位必须是0x**，后面跟十六进制数字（0 ~ 9及A ~ F）
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
**注意**：由于浮点数计算会产生舍入误差的问题，例如：0.1加0.2的结果不是0.3，所以**永远不要对某个浮点数值进行测试。**

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
即非数值，任何数值除以0会返回`NaN`，**这样的设计便不会影响其他代码的执行。**
```javascript
alert(NaN == NaN); //false
alert(NaN === NaN); //false
```
`isNaN()`函数，**该函数接受一个参数，该参数接受任何类型**，用于判断其参数是否是 `NaN`，
该函数接受到一个数值后，会尝试将这个值转换成数值（某些不是数值的值会直接转换成数值，如字符串"10"与`Boolean`值），而**不能被转换成数值的值会返回`true`。**
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
- `Number()`,可用于**任何数据类型**
- `parseInt()`，专门将**字符串**转换成**数值**
- `parseFloat()`，专门将**字符串**转换成**数值**


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
`parseFloat()`函数**只能解析十进制数**，因此它**没有第二个参数**来指定基数

------------


**6.` String`类型**

1.  字符串的特点
**字符串是不可变的**，字符串一旦创建，它的值将不能改变。
要改变某个变量保存的字符串，必须先销毁原来的字符串。

2.  转换成字符串

toString()方法：数值、布尔值、对象和**字符串值**都有toString()方法，但是null与undefined没有toString()方法。

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

String()方法:可以将null与undefined转换成字符串的"null"与"undefined"

```javascript
var value1 = 10;
var value2 = true;
var value3 = null;
var value4;

alert(String(value1));  //10
alert(String(value2));  //true
alert(String(value3));  //null
alert(String(value4));  //undefined

```



------------



**7.` Object`类型**
ECMAScript中的对象就是**一组数据和功能的集合**。对象可以通过new操作符后跟要创建的对象类型的名称来创建。
```javascript
var oObj = new Object();
var oStr = new String();
//第一行代码创建了 Object 类的一个实例，并把它存储到变量 oObj 中。
//第二行代码创建了 String 类的一个实例，把它存储在变量 oStr 中。
```


**Objec类型所具有的任何属性和方法也同样存在于更具体的对象中。**
Object的每个**实例**都具有下列属性和方法：
- Constructor：保存着用于创建当前对象的函数。
- hasOwnProperty(propertyName):用于检查给定的属性在当前对象实例中是否存在。其中参数必须以字符串的形式指定（如：oObj.hasOwnProperty("name")）。
- isPrototypeOf(object):用于检查传入的对象是否是另一个对象的原型。
- propertyIsEnumerable(propertyName):用于检查给定的属性是个能够使用for-in语句来枚举。
- toLocaleString():返回对象的字符串表示，该字符串与执行环境的地区对应。
- toString():返回对象的字符串表示。
- valueOf():返回对象的字符串、数值或布尔值表示。

------------



#### 操作符
**一元操作符**
（1）递增和递减操作符

a.前置型
```javascript
//前置递增
var age = 29;
++age;
console.log(age);  //30
//前置递减
var test = 29;
--test;
console.log(test); //28
```
执行前置递增和递减操作时，变量的值都是在语句被求值**之前**改变的：
```javascript
//例1--副效应--变量的值在语句求值前改变
var age = 29;
var anotherAge = --age + 2; //这里的age的值为28
alert(age);  //28
alert(anotherAge); //30
//例2--副效应--变量的值在语句求值前改变
var num1 = 2;
var num2 = 20;
var num3 = --num1 + num2; //结果为21（这里的num1为1）
var num4 = num1 + num2;   //结果为21（这里的num1为1）
//解析：因为num1会先减去1在进行下一步的运算
```

b.后置型
```javascript
//后置递增
var age = 29;
age++;
console.log(age);  //30
//后置递减
var test = 29;
test--;
console.log(test); //28
```
执行前置递增和递减操作时，变量的值都是在语句被求值**之后**改变的：
```javascript
//例1--副效应--变量的值在语句求值后改变
var age = 29;
var anotherAge = age-- + 2; //这里的age的值为29
alert(age);  //28
alert(anotherAge); //31
//例2--副效应--变量的值在语句求值后改变
var num1 = 2;
var num2 = 20;
var num3 = num1-- + num2; //结果为22（这里的num1为2）
var num4 = num1 + num2;   //结果为21（这里的num1为1）
```

对于以上四种操作符，它们对任何数据类型的值都适用，并且存在一些规则：
```javascript
var s1 = "2";
var s2 = "z";
var b = true;
var f = 1.1;
var o = {
    valueOf: function () {
         return -1; 
    }
};
s1++;//与++s1结果相同
s2++;//与++s2结果相同
b++;//与++b结果相同
f--;//与--f结果相同
o--;//与--o结果相同
console.log(s1++); //3
console.log(s2++); //NaN
console.log(b++);  //2
console.log(f--);  //0.10000000000000009
console.log(o--);  //-2
```
**位操作符**
对于有符号的整数，32为中的前31为用于表示整数的值，**第32位用于表示数值的符号：0表示正数，1表示负数。**
```javascript
var num = -18;
alert(num.toString(2)); //"-10010"
```
在以二进制字符串形式输出一个负数的时候，会输出这个负数绝对值的二进制码前面加了一个负号。
（1）按位非（NOT）
按位非操作符由一个波浪线（~）表示，用于**返回数值的反码（0和1互换）。**
```javascript
var num1 = 25; //二进制00000000000000000000000000011001（32位）
var num2 = ~num1;//11111111111111111111111111100110
alert(num2); //-26
```
对25进行了按位非操作，结果为-26。这也说明了**按位非操作的本质**是：**操作数的负值减1**。
```javascript
var num1 = 25;
var num2 = -num1 - 1;
alert(num2);//-26
```
以上两例代码可以返回同样的结果，但是由于**按位非是在数值表示的最底层执行操作**，因此速度更快！
（2）按位与（AND）
按位与操作只有在两个数值的对应位都是1时才返回1,任何一位是0，结果都是0。
|  第一个数值的位 |  第二个数值的位 | 结果  |
| :------------: | :------------: | :------------: |
| 1  |  1 |  1 |
| 1  |  0 | 0  |
| 0  | 1  |  0 |
| 0  |  0 |  0 |

```javascript
var result = 25 & 3;
alert(result); //1
```
我们也可以用一个数和1进行按位&操作来判断奇数与偶数，而且速度更快：
```javascript
function assert (n) {
	if (n & 1) {
	 		console.log( n + "是奇数");
	 	}else {
	 		console.log(n + "是偶数");
	 	}
}	
assert(3);	 //3是奇数
```
解析：**奇数的二进制码的最后一位数肯定是1**，和1进行按位&操作之后，结果肯定只有最后一位数为1。而**偶数的二进制表示的最后一位数是0**，和1进行按位&操作，结果所有位数都为0。
（3）按位或（OR）
按位或操作在有一个位是1的情况下就返回1，而只有在两个都是0的情况下才返回0。
|  第一个数值的位 |  第二个数值的位 | 结果  |
| :------------: | :------------: | :------------: |
| 1  |  1 |  1 |
| 1  |  0 | 1  |
| 0  |  1  | 1 |
| 0  |  0 |  0 |
```javascript
var result = 25 | 3;
alert(result); //27
```
（4）按位异或（XOR）
按位异或操作在两个数值对应位上只有一个1时才返回1，如果对应的两位都是1或是0，则返回0；
|  第一个数值的位 |  第二个数值的位 | 结果  |
| :------------: | :------------: | :------------: |
| 1  |  1 |  0 |
| 1  |  0 | 1  |
| 0  |  1  | 1 |
| 0  |  0 |  0 |
```javascript
var result = 25 ^ 3;
alert(result); //26
```
（5）左移
左移操作符由两个小于号（<<）表示，会将数值的所有位向左移动指定的位数。
```javascript
var oldValue = 2; //2的二进制为10
var newValue = oldValue << 5; //将10左移5位，变成1000000，等于十进制的64
```
注意：左移不会影响操作数的符号位，如果将-2向左移动5位，结果为-64。

如果要求2的n次方，可以这样：
```javascript
function power (n) {
	 return 1 << n; 
}
power(5); //32
```
（6）有符号的右移
用（>>）表示，会将数值的所有位向右移动指定的位数。但是保留符号位
```javascript
var oldValue = 64; //64的二进制为1000000
var newValue = oldValue >> 5; //将1000000右移5位，变成10，等于十进制的2
```
**注意：有符号左移与右移不会影响符号位。**
（7）无符号的右移
用（>>>）表示，正数的无符号右移与有符号右移结果是一样的。负数的无符号右移会把**符号位**也一起移动，而且无符号右移会把负数的二进制码当成正数的二进制码：
```javascript
//无符号的右移--对于正数
var oldValue = 64; //64的二进制为1000000
var newValue = oldValue >>> 5; //2
//无符号的右移--对于负数
var oldValue = -64; //等于十进制的11111111111111111111111111000000
var newValue = oldValue >> 5; //等于十进制的134217726
```
所以，我们可以利用无符号右移来判断一个数的正负：
```javascript
function isPos (n) {
 return (n == (n >>> 0)) ? true : false; 
}
isPos(-1);//false
isPos(1);//true
```
**布尔操作符**
（1）逻辑非
接受任何数据类型，会返回一个布尔值，该操作符会将它的操作数转换为一个布尔值，然后求其反值。
```javascript
alert(!{}); //false
alert(!Infinity);//false
alert(!null);//true
alert(!undefined);//true
alert(!false); //true
alert(!"blue"); //flase
alert(!0); //true
alert(!NaN);//true
alert(!"");//true
alert(!123456);//false
```
当然，如果你为操作数再加一个！，那么最终结果与对这个值使用Boolean()函数相同，如：
```javascript
alert(!!null);//false
alert(!!undefined);//false
alert(!!false); //false
alert(!!0); //false
alert(!!NaN);//false
alert(!!"");//false
```

（2）逻辑与
|  第一个操作数 |  第二个操作数 | 结果  |
| :------------: | :------------: | :------------: |
| true  |  true |  true |
| true  |  false | false  |
| false  |  true  | false |
| false  |  false |  false |
