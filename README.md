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

------------


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
assert(3);     //3是奇数
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

------------


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
当然，如果你为操作数再加一个！，那么最终结果与对这个值使用`Boolean()`函数相同，如：

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

逻辑与操作可以应用于任何数据类型，在有一个操作数不是布尔值的情况下，逻辑与操作就不一定返回布尔值，它有如下规则：
- 如果第一个操作数是对象，则返回第二个操作数。
- 如果两个操作数都是对象，则返回第二个操作数。
- 如果第二个操作数是对象，则只有在第一次操作数的求值结果为true的时候才返回该对象。
- 如果有一个操作数为`null`、`NaN`或者`undefined`，则返回`null`、`NaN`或者`undefined`。

**逻辑非为短路操作，即如果第一个操作数能够决定结果，便不会对第二个操作数求值**。例子：

```javascript
//短路操作--例（1）
var found = true;
var ans = (found && undefinValue);//这里会发生错误
alert(ans);//该行便不会执行
//短路操作--例（2）
var found = false;
var ans = (found && undefinValue);//不会发生错误
alert(ans); //执行该喊，结果为"false"
```
解析：
例子（1）说明:由于变量found的值为true，使用逻辑与操作符会对变量undefinValue求值，但是该变量未定义，故导致不会出现警告框。
例子（2)说明：由于变量found的值为false，意味着结果必定为false，所以无论变量undefinValue是否定义，都不会对它进行求值了，故会出现警告框 。
所以,**在使用逻辑与操作的时候始终记住它是一个短路操作符**
（3）逻辑或

|  第一个操作数 |  第二个操作数 | 结果  |
| :------------: | :------------: | :------------: |
| true  |  true |  true |
| true  |  false | true  |
| false  |  true  | true |
| false  |  false |  false |
逻辑或与逻辑与相似，有下列规则：
- 如果第一个操作数是对象，则返回第一个操作数。
- 如果第一个操作数的求值结果为false，则返回第二个操作数。
- 如果两个操作数都是对象，则返回第一个操作数。
- 如果有两个操作数为`null`、`NaN`或者`undefined`，则返回`null`、`NaN`或者`undefined`。
**逻辑或也是短路操作，如果第一个操作数的求值结果为true，就不会对第二个操作数求值了**。

```javascript
var found = true;
var result = (found || undefinedValue); //不发生错误
alert(result); //执行

var found = false;
var result = (found || undefinedValue); //发生错误
alert(result); //不执行
```
我们可以根据这一特性来避免为变量赋null或者undefined。例如：

`var myObject = preferredObject || backupObject;`

该赋值语句表面：变量myObject将被赋予等号后面两个值中的一个，变量preferredObject中包括优先赋给myObject的值，当preferredObject的值为null或者undefined时，backupObject作为后备值将会赋给myObject。

------------


**乘性操作符**
- 乘法（*）
- 除法（/）
- 求模（%）

如果参与上述计算的某个操作数不是数值，则在后台调用`Number()`函数将其转换成数值。

------------


**加性操作符**
（1）加法
对于不是数值的加法：
- 如果有两个字符串，则将第二个操作数与第一个操作数拼接起来。
- 如果只有一个操作数是字符串，则将另外一个操作数转换为字符串，然后拼接。
- 如果有一个操作数是对象、数值或者布尔值，则调用`toString()`来取得对应的字符串值，对于`undefined`与`null`，则调用`String()`函数取得字符串。

```javascript
var result = 5 + 5;
var result1 = 5 + "5";
alert(result);  //10
alert(result1); //55
```
在执行字符串与数值相加时，需要注意如下情况：

```javascript
var num1 = 5;
var num2 = 10;
var msg = "The sum of 5 and 10 is " + num1 + num2; //相当于字符串的相加
alert(msg);  //The sum of 5 and 10 is 510
var msg = "The sum of 5 and 10 is " + (num1 + num2); //用括号括起来，保证其优先性
alert(msg);  //The sum of 5 and 10 is 15
```

（2）减法
对于不是数值的减法：
- 如果有一个操作数是字符串、布尔值、`undefined`或`null`，则先在后台调用`Number()`函数进行转换，如果转换的结果为NaN,则减法的结果为NaN。
- 如果有一个操作数为对象，则调用`valueOf()`方法取得表示该对象的值，如果得到`NaN`,则结果为`NaN`，如果对象没有`valueOf()`方法，则调用`toString()`方法取得数值。

```javascript
var num1 = 5 - true; //4
var num2 = NaN - 1;  //NaN
var num3 = 5 - "";  //5
var num4 = 5 - "2";  //3
var num5 = 5 - null;  //5
```

------------


**关系操作符**
- 小于（<)
- 大于（>）
- 小于等于（<=）
- 大于等于（>=）

由于大写字母的字符编码全部小于小写字母的字符编码，所以会有如下现象:
```javascript
var result = "Brick" < "alphabet";  //true
```
若要真正的按字母顺序比较字符串，必须将其转换成相同的大小写格式，然后再进行比较：
```javascript
var ans = "Brick".toLowerCase() < "alphabet".toLowerCase();  //false
```
对于字符串的比较：

```javascript
var result = "23" < "3";//true
//因为"2"的字符编码是50.而"3"的是51
var result = "23" < 3;//false
//此时字符串"23"会转换为数值23
```
但是对于一个不能转换成合理数值的字符串来说：

```javascript
var result = "a" < 3; //false 因为a被转换成NaN
```
字母"a"不能转换成合理的数值，故变成NaN，
任何数与NaN进行比较，结果都是NaN。于是：

```javascript
var result = NaN < 3; //false
var result1 = NaN >= 3; //false
```

------------


**相等操作符**
（1）相等和不相等（== 与 ！=） --- 先转换在比较

|  表达式 | 值  |
| :------------: | :------------: |
| null == undefined  | true  |
| "NaN" == NaN  |  false |
| 5 == NaN  | false  |
| NaN == NaN  |  false |
|  NaN != NaN  | true  |
| false == 0  | true |
|  true == 1 |  true |
|  true == 2 | false  |
|  undefined == 0 | false  |
| null == 0  | false  |
| "5" == 5  | true  |

（2）全等和不全等（=== 与 ！==）--- 仅比较不转换

```javascript
var result = ("55" == 55);  //true,因为转换后相等
var result = ("55" === 55);  //false 因为是两个不同的数据类型
```

```javascript
var result = (null == undefined); //true
var result1 = (null === undefined); //false因为是两个不同的数据类型
```

------------


**条件操作符**
```javascript
var max = (num1 > num2) ? num1 : num2;
```

------------



**逗号操作符**
```javascript
var num = (5,6,8,1,0);  //num值为0
```

------------


#### 语句

**if语句**
例子：
```javascript
if (BMI < 18.5) {
    alert('过轻');
} else if (BMI >=18.5 && BMI <25){
    alert('正常');
} else if (BMI >=25 && BMI <28){
    alert('过重');
} else if (BMI >=28 && BMI <32){
    alert('肥胖');
} else {
    alert('严重肥胖');
}
```

------------


**do-while与while语句**
`do-while`循环体内的代码至少会被执行一次
`while`循环体内的代码可能永远不会被执行

------------


**for语句**
`for`循环体内的代码可能不会被执行

```javascript
var count = 10;
for (var i = 0; i < count; i++) {
    alert(i);
}
//上述for循环与下面的while循环功能相同
var count = 10;
var i = 0;
while (i < count) {
    alert(i);
    i++;
}
```
由于ECMAScript中不存在块级作用域，因此循环内部定义的变量也可以在外部访问到：

```javascript
var count = 10;
for (var i = 0; i < count; i++) {
    alert(i);
}
alert(i); //10
```
将表达式全部省略，会创建一个无限循环
```javascript
for(;;) {  //无限循环
    doSomething();
}
```

------------


**for-in语句**

```javascript
for (var propName in window) {
    document.write(propName);
}
```
**在使用for-in循环之前，先检测确认该对象的值不是`null`或`undefined`。**


------------

**lable语句**
使用`lable`语句可以在代码中添加标签，以便将来使用。

```javascript
start: for (var i = 0; i < count; i++) {
    alert(i);
}
```
定义好的`lable`可在将来由`break`或`continue`语句调用。加标签的语句一般都要与`for`语句等循环语句配合使用。

------------
**break和continue语句**
`break`：立即退出循环，强制继续执行循环后面的语句。

```javascript
var num = 0;
for (var i = 1; i < 10; i++) {
    if (i % 5 == 0) {
        break;
    }
    num++; 
}
alert(num);  //4
```
解析：
当i等于1时，if条件语句不满足，故num变为1，i变为2；
当i等于2时，if条件语句不满足，故num变为2，i变为3；
当i等于3时，if条件语句不满足，故num变为3，i变为4；
当i等于4时，if条件语句不满足，故num变为4，i变为5；
直到i为5时候（循环总共执行了4次），执行`break`语句退出`for`循环。**导致循环再num再次递增之前将推出了**，故出现警告框，num结果为4。

`continue`：立即退出循环，但是退出循环后会从循环的顶部继续执行。
```javascript
var num = 0;
for (var i = 1; i < 10; i++) {
    if (i % 5 == 0) {
        continue;
    }
    num++; 
}
alert(num);  //8
```
解析：
当i等于1时，if条件语句不满足，故num变为1，i变为2；
当i等于2时，if条件语句不满足，故num变为2，i变为3；
当i等于3时，if条件语句不满足，故num变为3，i变为4；
当i等于4时，if条件语句不满足，故num变为4，i变为5；
直到i为5时候，执行continue语句，使num再次递增前退出，导致**此次的num没有加1；但是不会退出循环**，故循环继续；
当i等于6时，if条件语句不满足，故num变为5，i变为7；
当i等于7时，if条件语句不满足，故num变为6，i变为8；
当i等于8时，if条件语句不满足，故num变为7，i变为9；
当i等于9时，if条件语句不满足，故num变为8，i变为10；
当i等于10时，循环结束，出现警告框，输出结果8。

`break`与`lable`:

```javascript
var num = 0;
outermost:
for (var i = 0; i < 10; i++) {
    for(var j = 0; j < 10; j ++){
        if (i ==5 && j ==5) {
            break outermost;
        }
        num++;
    }
}
alert(num); //55
```
如果每个循环（i，j）正常执行直到结束，则num的值为100，但是有了一个`break`与`lable`的"捣乱"，**使break不仅退出内部的for语句（即变量为j的），并且也会退出外部的for语句（即变量为i的）**，故当变量i与j为5时，num为55。

`continue`与`lable`:

```javascript
var num = 0;
outermost:
for (var i = 0; i < 10; i++) {
    for(var j = 0; j < 10; j ++){
        if (i ==5 && j ==5) {
            continue outermost;
        }
        num++;
    }
}
alert(num); //95
```
`continue`语句会强制继续执行循环 --- 退出内部循环（变量为j的），执行外部循环（变量为i的），**这便意味着内部循环少执行了5次**，故num的结果为95。

------------

**switch语句**
从根本上讲，`switch`语句是为让开发人员**免于编写**下面的代码：

```javascript
if (BMI == 18.5) {
    alert('18.5');
} else if (BMI == 25){
    alert('25');
} else if (BMI == 28){
    alert('28');
} else if (BMI == 32){
    alert('32');
} else {
    alert('Other');
}
```

而与之等价的`switch`为：
```javascript
switch (i) {
    case 18.5:
        alert("18.5");
        break;
    case 25:
        alert("25");
        break;
    case 28:
        alert("28");
        break;
    case 32:
        alert("32");
        break;
    default:
        alert("Other");
        break;
}
```

ECAMScript中`switch`语句的特点：`switch`语句中可以使用任何数据类型，每个`case`的值不一定是常量，也可以是变量，甚至是表达式。

```javascript
var num = 15;
switch (true) {
    case num < 0:
        alert("less than 0");
        break;
    case num >= 0 && num <= 10:
        alert("between 0 and 10");
        break;
    case num > 10 && num <= 20:
        alert("between 10 and 20");
        break;
    default:
        alert("more than 20");
        break;
}
```
上述例子中之所以给`switch`传递`true`，是因为每个`case`值都是可以返回一个布尔值的，这样每次`case`按住顺序进行求值，直到找到"归宿"。
注意：**`switch`语句在比较值的时候用的是全等操作符（===）**


#### 函数

**基本知识**
函数会在执行完`return`语句之后停止并立即退出。，位于`return`语句之后的任何代码对不会执行。
另外，`return`语句可以不带任何返回值。这种情况下，函数在停止执行后将返回`undefined`值。

```javascript
function sayHi (name,msg) {
	 return;//返回undefined
	 alert("Hello" + name + "," + msg);//不会调用 
}
```

**理解参数**

ECMAScript函数不介意传递进来多少参数，也不在乎参数的数据类型是什么。原因是参数的内部是用一个数组来表示的，函数体内可以通过`arguments`对象来访问这个参数数组，从而获取每一个参数。

```javascript
function sayYes () {
	 alert("Yes" + arguments[0] + "," + arguments[1]); 
}
sayYes("Carl","nice");//YesCarl,nice
```

让函数接受任意个参数并分别实现功能（这样可以模拟方法的重载）：

```javascript
function doAdd () {
	 if (arguments.length == 1) {  //一个参数
	  	return (10 + arguments[0]);//记得arguments以数值的形式来调用
	  }  //11
	  else if (arguments.length == 2) {//两个参数
	  	return (arguments[0] + arguments[1]);  //8
	  } else if (arguments.length == 0) { //零个参数
	  	alert("fuck");
	  }
}
```

**没有重载**
如果在ECMAScript中定义了两个名字相同的函数，则该名字只属于后定义的函数。
```javascript
function addSomething (num) {
	 return num + 100 ;
}
function addSomething (num) {
	 return num + 200; 
}
var s = addSomething(5);
alert(s); //205
```
后定义的函数会覆盖先定义函数。

------------

## 变量作用域和内存问题
#### 基本类型和引用类型的值
基本类型值：简单的数据段；
引用类型值：可能由多个值构成的对象。

**动态的属性**
对于引用类型的值，我们可以为其添加属性和方法，也可以改变和删除属性和方法：

```javascript
var person = new Object();
person.name = "Carl";
alert(person.name); //Carl
```
但是我们不能给基本类型的值添加属性：

```javascript
var name = "carl";
name.age = 27;
alert(name.age);//undefined
```

------------



**复制变量值**
- 从一个变量向另外一个变量复制**基本类型**的值

```javascript
var num1 = 5;
var num2 = num1;
```
num2中的5与num1中的5是**完全独立**的，这两个变量可以参与任何操作而**不会互相影响**
- 从一个变量向另外一个变量复制**引用类型**的值

```javascript
var obj1 = new Object();
var obj2 = obj1;
obj1.name = "Carl";
alert(obj2.name); //Carl
```
obj1和obj2指向同一个对象，，当obj1添加属性后，可以通过obj2来访问这个属性。


------------



**参数的传递**（比较难理解）
**参数也可以分为：基本类型值和引用类型值**，下面我们对这两类不同的参数的传递进行分析：但是记住：
> ECMAScript中的所有函数的参数都是按值传递的

函数外部的值赋值给函数内部的参数，与一个变量复制到另一个变量一样。
**基本类型值的传递和基本类型的复制一样，引用类型的传递和引用类型的复制一样。（参考上一节---复制变量值）**
- 向参数**传递基本类型**的值时，被传递的值会被复制给一个局部变量（即命名参数）。这个局部变量的变化会反映在函数的外部。

```javascript
function addTen (num) { //num相当于上述理论所说的"局部变量"
     num += 10;
     return num; 
}
var count = 20;   //相当于上述理论所说的"被传递的值"
var result = addTen(count);
alert(count); //20 没有变化
alert(result); //30
```
解析：虽然值为20的count被复制给了参数num，但是参数num与变量count互不认识完全独立，他们仅仅只是具有相同的值，不会相互影响。
但是如果num是按引用传递的话，那么变量count的值也会变成30，从而反映函数内部的修改，请看下面的代码：
- **按引用类型传递**的变量：
```javascript
function setName (obj) {
     obj.name = "Carl"; 
}
var person = new Object();
setName(person);
alert(person.name);//Carl
```
解析：obj与person引用的是同一个对象。
为了证明**对象的传递是按值传递的**，看下面的例子：
```javascript
function setName (obj) {
     obj.name = "Carl"; 
     obj = new Object();
     obj.name =  "Gray";
}
var person = new Object();
setName(person);
alert(person.name);//Carl
```
如果对象（在这里是person对象）的传递是按引用传递的，那么person就会自动被修改为Gray；但是事实表明这是错误的，所以**对象的传递是按值传递的**

------------

**检测类型**
虽然在检测基本数据类型时typeof是非常给力的助手，但是在检测引用类型的值时就显得力不从心了：
```javascript
var n = null;
var o = new Object();
alert(typeof(n)); //object
alert(typeof(o)); //object
```
为此提供了instanceof操作符，如果变量是给定引用类型的实例，那么instanceof会发挥true：
```javascript
var oStringObject = new String("hello world");
console.log(oStringObject instanceof String);  // 变量 oStringObject 是否为 String 对象的实例，输出 "true"
```



#### 本章小结

- **基本类型值**在内存中占据固定大小的空间，因此被保存在栈内存中
- 从一个变量向另外一个变量复制**基本类型的值**，会创建这个值的一个副本
- **引用类型值**是对象，保存在堆内存中
- 包含引用类型值的变量实际上包含的不是对象本身，而是一个指向该对象的指针，所以从一个变量向另外一个变量复制**引用类型的值**，复制的其实是指针，**因此两个变量始终指向同一个对象**
- 确定一个值是哪种**基本类型**可以使用`typeof`操作符，确定一个值是哪种**引用类型**可以使用`instanceof`操作符

------------

#### 执行环境及作用域

**基本概念**
**执行环境**定义了变量或函数有权访问的其他数据，决定它们各自的行为，每个执行环境都有一个与之关联的**变量对象**，环境中定义的所有变量和函数都保存在这个对象中。
**执行环境**的类型有两种---全局与局部（函数）。
**作用域链**保证对执行环境有权访问的所有变量和函数的有序访问。

```javascript
var color = blue;

function changeColor () {
     var anotherColor = "red";

     function swapColor () {
           var tempColor = anotherColor;
           anotherColor = color;
           color = tempColor; 

           //这里可以访问color、anotherColor和tempColor
      } 

      //这里可以访问color和anotherColor，但是不能访问tempColor
}
//这里只能访问color
changeColor();
```
以上代码共涉及3个执行环境：全局环境、changeColor()的局部环境和swapColor()的局部环境。

**没有块级作用域**
if语句中的变量声明会将变量添加到当前的执行环境中。

```javascript
if (true) {
    var color = "blue";
}

alert(color); //blue
```
for语句创建的变量即使在for循环执行结束之后，也会存在于循环外部的执行环境中。

```javascript
for(var i=0; i < 10; i++){
    var j = 0;
    j = j++;
}

alert(i);//10
```


#### 本章小结

- **执行环境**有全局执行环境与函数执行环境之分。
- 每次进入一个新的执行环境，都会创建一个用于搜索变量和函数的**作用域链**。
- 函数的**局部环境**不仅有权访问函数作用域中的变量，还可访问**父环境乃至全局环境**；而全局环境**只能**访问全局环境中定义的变量与函数。


------------

## 引用类型
#### 基本概念
对象是某个特定引用类型的实例。
新对象是使用new操作符后跟一个构造函数来创建的。
构造函数本身就是一个函数，只不过它出于创建新对象的目的而定义
`var person = new Object();`

------------

#### Object类型



