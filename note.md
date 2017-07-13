# Javascript

- EMCAScript


- DOM


- BOM
----

- [ ] ？？？理解对象和object


- [x] ？？？位操作符中的32位符号
- [ ] 字符编码？比较字符编码"23"<"3"

---

## 第一章：简介

1.出现、版本更新

ECMAScript，由ECMA-262定义，提供核心语言功能；

2.文档对象模型（Document Object Model）是针对XML但是经过扩展用于HTML的应用程序编程接口（API）

DOM把整个页面映射为一个多节点结构→开发人员获得控制页面和结构的主动权

**提供访问和操作网页内容的方法和接口**

3.浏览器对象模型（BOM）控制浏览器显示的页面以外的部分

**提供与浏览器交互的方法和接口**

## 第二章：在HTML中使用JavaScript

#### <\script>元素

1.插入方法

- ```
  <script type="text/javascript">
    function sayHi(){
       alert("Hi");
    }
   </script>
  嵌入js代码
  ```


- ```
  <sript type="text/javascript" src="example.js"></script>
  导入外部js
  ```

2.解析顺序

- defer属性：延迟脚本，**立即下载但延迟执行**解析和显示后执行（只对外部脚本有效）


- async属性：异步脚本，立即下载，不影响其他操作（只对外部脚本有效）**目的不让页面等待两个脚本下载和执行，从而异步加载页面其他内容**，表示当前脚本不必等待其他脚本
- 除此之外，浏览器会按照<script>*在页面的先后顺序依次解析*

3.标签的位置

多放在body元素中页面内容的后面

4.在XHTM中的用法

*CData*片段包含JavaScript代码，表示区域内不解析

```
<script>//<![CDATA[
    function{...}
        //]]>
</script>
//注释是为了不兼容XHTML的浏览器
```

## 第三章：基本概念

#### 1.语法

1.1区分大小写

1.2标识符：指变量、函数、属性的名字，或者函数的参数

- 第一个字母必须是一个字母、下划线_、或者一个$
- 其他字符除以上三者还可以是数字
- 惯例驼峰大小写格式、第一个字母小写，剩下每个单词首字母大写

1.3注释

//单行注释

/*多行

注释*/

1.4严格模式

在顶部添加代码“use strict”告诉引擎切换到严格模式

1.5语句    ①分号句尾②使用代码块{}

#### 2.关键字和保留字

不能作为标识符

#### 3.变量

3.1ECMAScript的变量是松散型的，就是可以用来保存任何类型的数据；换句话说，每个变量仅仅是一个用于保留值得占位符而已

3.2

var message；//未初始化变量，值为undefined

var message=“hi";//初始化变量，赋值

3.3**使用var操作符定义的变量将成为定义该变量作用域的局部变量，函数退出即销毁**

省略var，即为全局变量，不推荐使用

```
fuancion text{
    message="hi";//全局变量
}
text();//调用函数
alert(message);//hi
```

3.4可以使用一条语句定义多个变量

#### 4.数据类型

①五种基本数据类型（简单数据类型）

- Undefined→undefined

- Null→object

- Boolean→

- Number

- String

②一种复杂数据类型

- Object:一组无序的名值对组成

③不支持任何创建的自定义类型，所以值都是上述六种之一

##### 4.1 typeof操作符

**检测给定变量的数据类型**

###### 可能返回的字符串

- undefined

- boolean

- string

- numble

- object:这个值是对象（*?*）或者null

- function：函数


typeof是一个*操作符*而不是函数，所以可以alert（typeof(message));//string;圆括号可以用但是却不是必须的

function函数在ECMAScript中是**对象**，不是数据类型

通过typeof操作符来区分函数和其他对象

##### 4.2 Undefined类型

- 使用var声明变量但是未对其加以初始化，默认取得undefined值
- var message=undefned,使用undefined显示初始化变量（没必要）
- 未声明的变量，typeof操作符同样返回undefined值

##### 4.3 Null类型

①从逻辑角来看，null值表示一个*空对象指针*，这也是typeof操作符检测null值会**返回“object”**的原因.

②如果定义的变量准备在将来用来保存对象，那么最好初始化为null，而不是其他

③实际上，undefined是派生自null值得，所以他们的相等性测试返回true

④尽管二者有这样的关系，但是用法却完全不同。初始化undefined没必要，初始化null却是有必要的；这可以提现null作为空对象指针惯例，也进一步*区分*null和undefined。

##### 4.4 Bollean类型

- 只有两个字面值true和false；区分大小写，只有小写才是布尔值，不然只是标识符；
- 虽然字面值只有两个，但是ECMAScript中所有类型的值都有与这两个Boolean值等价的值

| 数据类型      | 转换为true的值           | 转换为false的值 |
| --------- | ------------------- | ---------- |
| Boolean   | true                | false      |
| String    | 任何非空字符串             | “”（空字符串）   |
| Number    | 任何非零数字值（包括无穷大)      | 0和NAN      |
| Object    | 任何对象                | null       |
| Undefined | n/a(not applicable) | undefined  |

##### 4.5 Numble类型：

表示整数和浮点数值

（一）数值字面量格式

①最基本的数据字面量格式：十进制整数

②八进制：第一位是0,然后八进制数字序列（0-7）

③十六进制：第一位是0x，然后（0-9及A-F）

如果字面值中的数值超出范围，则前导0被忽略，按照十进制解析

（二）浮点数值

由于浮点数值需要的内存空间是保存整数值得两倍，所以如果能转换为整数的数值将转换为整数保存

科学计数法e表示法

浮点数值的最高精度为17位，但是进行算数计数时精度远不如整数

例如0.1+0.2=0.300000000000004，舍入误差

因此*永远不要测试某个特定的浮点数值*

（三）数值范围

MAX_VALUE 属性是 JavaScript 中可表示的最大的数。它的近似值为 1.7976931348623157 x 10308

MIN_VALUE 属性是 JavaScript 中可表示的最小的数（接近 0 ，但不是负数）。它的近似值为 5 x 10-324

如果得到一个超出JavaScript数值范围的值，则被转换成Infinity

负数则被转换成-Infinity(负无穷)

**Infinity不能参与计算**

可以使用*isFinite（）函数*   确定数值是不是有穷的，如果是，返回true

```javascript
var result=Number.MAX_VALUE+1;

alert(isFinite(result));//false
```

在执行极小或者极大数值的计算时，要检测监控这些值

（四）NaN

Not a Numble非数值，是一个特殊的数值；这样ECMAScript就不会抛出错误，不会影响其他代码的执行；

- 任何涉及NaN的操作都会返回NaN；
- NaN与任何值都不相等，包括NaN本身；
- 0除以0返回NaN，整数除以NaN返回Infinity，负数除以0返回-Infinity

*isNaN（）函数*    确定参数是否“不是数值”，函数接受一个数值会尝试转换成数值，如果不能转换成数值，函数返回true

```javascript
alert(NaN == NaN);       //false
alert(isNaN(NaN));       //true
alert(isNaN(10));        //false – 10 is a number
alert(isNaN("10"));      //false – can be converted to number 10
alert(isNaN("blue"));    //true – cannot be converted to a number
alert(isNaN(true));      //false – can be converted to number 1
```

（五）数值转换

- Number（）：用于*任何数据*类型

  ```javascript
   var num1 = Number("Hello world!");  //NaN
   var num2 = Number("");              //0
   var num3 = Number("000011");        //11
   var num4 = Number(true);            //1
   var num5 = Number(null);            //0
   var num6 = Number(undefined);       //NaN
   var num7 = Number(0xA);             //10
  ```

- parseInt（）：专门用于把*字符串*转换成数值

  由于Number（）函数在转换字符串时比较复杂和不够合理，因此在处理整数时更常用parseInt（）函数；

  忽略前面的空格，找到第一个**非空格字符**

```javascript
  var num1 = parseInt("1234blue"); //1234
  var num2 = parseInt("");        //NaN
  var num3 = parseInt("0xA");     //10 - hexadecimal
  var num4 = parseInt(22.5);      //22 -小数点不是有效的                                     数字字符
  var num5 = parseInt("070");     //70 - decimal
  var num6 = parseInt("0xf");    //15 – hexadecimal
  var num7 = parseInt("blue123"); //NaN
```

ECMAScript3认为“070”是56（八进制），而ECMAScript5以后被认为是十进制，所以parseInt（）函数以不具备解析八进制的能力了

为解决这个问题，可以为函数提供第二个参数：转换时使用的基数

```javascript
 var num1 = parseInt("AF", 16);        //175
 var num2 = parseInt("AF");            //NaN
 如果指定了16作为基数，则可以不带"0x"
 var num3 = parseInt("10", 10);        //10 – parsed                                          as decimal
 var num4 = parseInt("10", 2);         //2 – parsed                                            as binary
```

不指定基数意味着让函数决定如何解析输入的字符，因此为了避免错误解析，我们建议**无论什么情况下都明确指定基数**

- parseFloat（）：专门用于把*字符串*转换成数值

*区别*：

①第一个小数点有效；

②始终会忽略前导的0；

③只解析十进制，十六进制始终被转换成0；

```
var num1 = parseFloat("1234blue");   //1234 - integer
var num2 = parseFloat("0xA");         //0
var num4 = parseFloat("22.34.5");     //22.34
var num5 = parseFloat("0908.5");      //908.5
var num6 = parseFloat("3.125e7");     //31250000
var num7 = parseFloat(1.000);        //1
```

#####4.6 String类型 

用于表示由0个或者多个16位Unicode字符组成的字符序列，及*字符串*。　　

【Unicode编码：一个英文等于两个字节，一个中文（含繁体）等于两个字节。16位指的是：字符串每个字符所占用的空间为16bits 比特(2 bytes字节)】

双引号和单引号的字符写法在ECMAScript中完全相同

（一）字符字面量

String数据类型包含一些特殊的字符字面量，也叫专业序列；

| 字面量   | 含义                                     |
| ----- | -------------------------------------- |
| \n    | 换行                                     |
| \t    | 制表                                     |
| \b    | 空格                                     |
| \r    | 回车                                     |
| \f    | 进纸                                     |
| \\    | 斜杠                                     |
| \'    | 单引号                                    |
| \"    | 双引号                                    |
| \xnn  | 以十六进制代码nn表示一个字符（n为0-F）。\x41表示“A”       |
| \unnn | 以十六进制代码nnnn表示一个字符（n为0-F）。\u03as表示希腊字符∑ |

```
alert(text.length);//获得字符串长度
其中\u03as六个字符长的转义序列表示一个字符
```

*alert（text.length）*

（二）字符串的特点

字符串时不可变的，一旦创建后想要改变某个变量保存的字符串，首先要销毁原来的字符串，然后再用另一个新值填充

```
var lang = "JAVA";
lang =lang+"Script";//过程在后台发生并拼接
```

（三）转换为字符串

- toString()函数

  返回相应值得字符串表现。但是null和undefined没有这个方法

  通过指定基数，改变输出的值num.toString(8)八进制。

- String()转型函数

  ①有toString（）方法则调用；②值为null则返回"null";

  ③值为undefined则返回"undefined"。



##### 4.7 Object类型

ECMAScript中的对象其实就是 **一组数据和功能的集合**。

ECMAScript中的对象是可变的键控集合（即一组数据和功能的集合）

对象可以通过执行new操作符后跟要创建的对象类型的名称来创建；

创建自定义对象，并为其添加属性和方法

```javascript
var o = new Object();
```
*关键要理解一个重要思想*

在ECMAScript中，Object类型是它所有实例的基础！

Object的每个实例都具有下列的属性和方法？？？？？？



ECMA-262中的对象和行为不一定适用于JavaScript中的其他对象。浏览器环境对象，比如BOM和DOM中的对象，都属于宿主对象。

#### 5.操作符

用于操作数据，包括算术操作符、位操作符、关系操作符、相等操作符。

##### 5.1 一元操作符

（一）递增很递减操作符

- 前置型

  执行前置型递减和递增操作时，变量的值都是在语句被求值之*前*改变的

  *先递减再进行计算*

  ```javascript
   var age = 29;
   var anotherAge = --age + 2;      
   alert(age);         //outputs 28
   alert(anotherAge);  //outputs 30
  ```


- 后置型

  被求值之*后*才执行

  即*先完成计算再递减*（**则计算时使用的值没有经过递减**）

```javascript
var num1 = 2;
        var num2 = 20;
        var num3 = --num1 + num2;    //equals 21
        var num4 = num1 + num2;      //equals 21
```

```javascript
 var num1 = 2;
        var num2 = 20;
        var num3 = num1-- + num2;    //equals 22
        var num4 = num1 + num2;      //equals 21
```

- 规则

```javascript
var s1 = "2";
    var s2 = "z";
    var b = false;
    var f = 1.1;
    var o = { 
        valueOf: function() {
            return -1;
        }
    };
     s1++;   //value becomes numeric 3
     s2++;   //value becomes NaN
     b++;    //value becomes numeric 1
     f--;    //value becomes 0.10000000000000009
     o--;    //value becomes numeric –2  

          
```
（二）一元加和减操作符

- 再对非数值应用一元加操作符时，该操作符会像Number（）转型函数一样对这个值进行转换；

- 一元减操作符：用于表示负数；与加操作符相同规则，然后加负号；

```javascript
   var s1 = "01";
          var s2 = "1.1";
          var s3 = "z";
          var b = false;
          var f = 1.1;
          var o = { 
              valueOf: function() {
                  return -1;
              }
          };
          
          s1 = -s1;   //value becomes numeric -1
          s2 = -s2;   //value becomes numeric -1.1
          s3 = -s3;   //value becomes NaN
          b = -b;     //value becomes numeric 0
          f = -f;     //change to –1.1
          o = -o;     //value becomes numeric 1
```

##### 5.2 位操作符

位于最基本的层次上，因此速度更快；

ECMAScript中所有数都以IEEE-754 64位存储→转换成32位→**执行操作**→转换成64位；整个过程就像只存在32位一样；

以二进制码存储；对于有符号的整数，32位中的前31位用于表示整数的值，第32位用于表示负号：**0→正数；1→负数；**

负数以二进制码存储的步骤①数值的绝对二进制编码②二进制反码③得到的二进制反码加1

但是ECMAScript输出时直接是负数绝对值的二进制编码前面加一个负号

转换过程中导致NaN和Infinity值应用位操作符时，都会被当成0来处理

| 操作符       | 表示方法 |         返回值          |
| :-------- | :--: | :------------------: |
| 按位非（NOT）  |  ~   | 返回数值的反码(本质：操作符负值减1)  |
| 按位与（AND）  |  &   |   相同位置上的两个数都是1时返回1   |
| 按位或（OR）   |  \|  | 有一位是1时返回1；两位都是0时返回0  |
| 按位异或（XOR） |  ^   |     *只*有一位是1返回1；     |
| 左移        |  <<  | 向左移动指定位数，以0填充，不影响符号位 |
| 有符号的右移    |  >>  |        不影响符号位        |
| 无符号的右移    | >>>  |      所有32位都向右移动      |

正数有无符号右移结果相等，而负数无符号右移会结果非常大。

##### 5.3 布尔操作符

可以应用于任何类型的操作数

| 操作符  | 表示方法 |        返回值         |
| ---- | :--: | :----------------: |
| 逻辑非  |  !   | 与Boolean（）转型函数结果相反 |
| 逻辑与  |  &&  |    同为true则为true    |
| 逻辑或  | \|\| |   一个为true则为true    |

- 逻辑非使用两个则会模拟Boolean（）转型函数；

- 逻辑与和逻辑或都属于短路操作，第一个函数能决定结果就不对第二个 求值；

- 逻辑非返回值都为true或者false

  逻辑与和逻辑或返回值不一定为布尔值；可以为

  ​     *对象、null、undefined、NaN*

##### 5.4 乘性操作符

操作符为非数值的情况下会自动进行Number()转型函数转为数值。

| 操作符  | 表示方法 |   返回值    |
| ---- | ---- | :------: |
| 乘法   | *    |    乘积    |
|      | /    | 第一个除以第二个 |
|      | %    |    余数    |

返回值可以是：Infinity、-Infinity、NaN、常规数值

undefined结果NaN

##### 5.5 加性操作符

- 加法
- 减法

*转换规则*：

①Infinity+-Infinity，结果Infinity

​                    -0+0，结果+0；-0-0，结果+0；

②如果一个是字符串，另一个不是字符串也要是字符串！

```javascript
var num1 = 5;
var num2 = 10;
var message = "The sum of 5 and 10 is " + num1 + num2;
alert(message);    //"The sum of 5 and 10 is 510"
```

**每个加法独立执行**

③操作符为非数值的情况下会自动进行Number()转型函数转为数值。

```javascript
 var result1 = 5 + 5;      //10
 var result2 = 5 + "5";    //"55"
 var result3 = NaN - 1;    //NaN
 var result4 = 5 - "" ;    //5.因为""被转换成0
 var result5 = 5 - null ;  //5.因为null被转换成0
 var result6 = 5 - "2" ;   //3,因为"2"被转换成2
```

##### 5.6关系操作符

| <    | >    | <=   | >=   |
| ---- | ---- | ---- | ---- |
| 小于   | 大于   | 小于等于 | 大于等于 |

操作符为非数值的情况下会自动进行数据转换或完成一些奇怪的操作

- 都是数值，则进行比较；

- 都是字符串，则比较对应的字符编码；*？？？*

- 一个是数值，则另一个转成数值；

- 一个是对象，则调用valueOf（）方法，进行比较，如果没有，则调用toString（）方法，得到的结果进行比较；

- 如果一个是布尔值，则转换成数值进行比较；

返回值为布尔值。

任何数值与NaN进行比较，结果都是false；

```javascript
var result1 = NaN < 3;//false
var result2 = NaN >= 3;//false
```

##### 5.7相等操作符

两组操作符

- 相等和不相等：先转换再比较

- 全等和不全等：仅比较不转换

（一）相等和不相等（==）和（!=）

比较前进行 *强制转换*

规则：

- 如果有一个是布尔值，则先转换成0或者1；

- 把字符串转换为数值；

- null和undefined是相等的；

- 比较相等性之前不能把null和undefined转换为其他值；

- 如果有一个值是NaN,则相等操作符返回false，不相等操作符返回true；即使两个操作符都是NaN，相等操作符也返回false，因为NaN不等于NaN；

- 如果两个操作符都是对象，则比较是不是同一个对象。

```javascript
var num1 = "123" ;
var num2 = "你好" ;
alert( num1 == 123) ;       //true
alert( num2 = num1 + 2) ;   //"1232"   虽然把字符串转换成数值计算，但是没有真正改变字符串类型，依然是字符串；
```
（二）全等和不全等

区别：**不转换**

===全等：两个操作符未经转换就相等返回true；

!==不全等：两个操作符未经转换就不相等；

```
var result1 = ("55" == 55);    //true – equal because of conversion
var result2 = ("55" === 55);   //false – not equal because different data types
```

**null == undefined会返回true ，因为他们是类似的值；但null === undefined 返回false，因为它们是不同类型的值**

#####5.8 条件操作符

```
var max = (num1 > num2)?num1:num2
```

问号前的结果返回为true，则将第一个num1赋值给max→max中将保存一个最大的值；

##### 5.9 赋值操作符

等于号(=)表示，就是把右侧的值赋值给左侧的变量；

如果在等号前面加上算数操作符（以及个别其他操作符），就可以完成复合操作符；

```javascript
var num = 10;
num = num + 10;
```

第二行用一个复合操作符代替：（理解为在原值上加的数是10）

```javascript
var num = 10;
num + = 10;
```

简化赋值操作，并不会带来性能上的提升

##### 5.10 逗号操作符

在一条语句中执行多个操作

- 声明多个变量

```
  var num1=1,num2=2,num3=3;
```

- 用于赋值，不常见

```
  var num = (5,6,2,0);//num的值为0
```

#### 6.语句

ECMA-262规定了一组语句（流控制语句），从本质看，语句定义了ECMAScript中的主要语法，语句通常使用一个或者多个关键词来完成任务。

##### 6.1 if语句





