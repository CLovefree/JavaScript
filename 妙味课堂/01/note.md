## JS基础

#### 组成

ECMAScript：解释器、翻译

DOM：Document Object Model

BOM：Browser Object Model

#### 变量类型

类型：typeof运算符

用法、

返回值常见类型：number、string、boolean、undefined、object、function

一个变量应该只存放一种类型的数据

#### 数据类型转换

例子：计算两个文本框的和

显式类型转换(强制类型转换)

- parseInt()、 parseFloat()

NaN的意义和检测

隐式类型转换

- ==、===（不转类型）


- 减法乘法除法

#### 变量作用域和闭包

- 变量作用域（作用范围）
  - 局部变量
  - 全局变量（不定义在任何一个函数里。尽量不用）
- 什么是闭包
  - 子函数可以使用父函数中的局部变量
  - 之前一直在使用闭包
  - 网上对于闭包的定义

#### 命名规范

命名规范及必要性

- 可读性——能看懂
- 规范性——符合规则

匈牙利命名法

- 类型前缀
- 首字母大写

| 类型    | 前缀   | 类型       | 实例           |
| ----- | ---- | -------- | ------------ |
| 数组    | a    | Array    | aItems       |
| 布尔值   | b    | Boolean  | bIsComplete  |
| 浮点数   | f    | Float    | fPrice       |
| 函数    | fn   | Function | fnHandler    |
| 整数    | i    | Integer  | iItemCount   |
| 对象    | o    | Object   | oDiv1        |
| 正则表达式 | re   | RegExp   | reEmailCheck |
| 字符串   | s    | String   | sUserName    |
| 变体变量  | v    | Variant  | vAnything    |

既适用于变量也适用于函数，只不过没有类型前缀

#### 运算符

- 算术：+ 加、- 减、* 乘、/ 除、% 取模

  - 实例：隔行变色、秒转时间
- 赋值：=、+=、-=、*=、/=、%=
- 关系：<、>、<=、>=、==、===、!=、!==
- 逻辑：&& 与、|| 或、! 否
  - 实例：全选与反选
- 运算符优先级：括号

#### 程序流程控制

- 判断：if、switch、?:

- 循环：while、for

- 跳出：break（终止整个循环）、continue（终止本次循环，继续下次循环）————都用的比较少

- 什么是真、什么是假：

  - 真：true、非零数字、非空字符串、非空对象
  - 假：false、数字零、空字符串、空对象null、undefined

#### Json

- 什么是Json

  JSON: JavaScript Object Notation(JavaScript 对象表示法)

  JSON 是存储和交换文本信息的语法。类似 XML。

  JSON 比 XML 更小、更快，更易解析。

- Json和数组

- Json和for in

#### 函数返回值

- 什么是函数返回值
  - 函数的执行结果
  - 可以没有return→undefined


- 一个函数应该只返回一种类型的值

#### 函数传参

可变参（不定参）：arguments

参数的个数可变，参数数组（arguments是一个数组，存放参数）



