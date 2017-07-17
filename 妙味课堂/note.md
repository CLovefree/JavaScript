## 第一部分-案例1

###记住密码提示框

- 效果原理
- JS中的事件

  - 当。。。的时候

  - onmouseover、onmouseout

  - alert的使用
- 元素的获取
  - id
  - document.getElementById  
### 属性操作

- obj.style.display='block'（页面怎么写，JS就怎么写，除了class）

- 赋值

- 点理解为“的”

- 引号

- class的使用

  -obj.*className*='xxx'

### 网页换肤

- 效果原理
  - 准备几套css样式表
  - 调试好兼容性
  - 点击按钮时，改变href值


- onclick的使用

  - 当点击时

  - 事件可以随意改变

### JS中的函数

- 函数的定义  function toFace1 (){...}

- 函数的调用  onclick="toFace1()"

- 函数的名字加()

- 变量的使用

   function toFace1 (){

  var oDiv1=document.getElementById('div1');

  oDiv1.style.width='200px';

  oDiv1.style.height='300xp';

  }

## 第二部分-案例2

### 匿名函数

- window.onload=function(){

  oDiv.onmouseover=toGreen;

  }

- function后面括号前面不加函数名

- 调用函数没加括号
 ### 收缩展开菜单

- 效果思路

  如果原来是隐藏的，就显示

  否则，就隐藏

  注意：两个变量。点击变量1，隐藏显示变量2

- if条件判断

  判断是否相同，==

- 更复杂的判断

  if,else if,else

  if(条件）

  {语句1}

  else if

  {语句2}

  else

  {语句3}

### 全选功能

- 效果原理
- 控制checkbox的状态-checked=true；
- 如何获取一组元素-getElementsByTagName('input')

### for循环

- 初始化 i=0
- 条件 i<5
- 程序语句
- 自增

### 选项卡

- 点击按钮时，改变class和style.display
- 头部标签：改变className
- 内容:改变display

###简易日历

- innerHTML；支持内部标签
- 数组的使用
- index索引值？怎么理解？

### 定时器

- 开启定时器

  - 间隔型   setInterval（  函数，时间）//不断重复
  - 延时型   setTimeout(  函数，时间 )//只执行一次

- 停止定时器

  - clearInterval

  - clearTimeout

###数码时钟