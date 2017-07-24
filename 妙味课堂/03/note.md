## 事件

#### event对象和事件冒泡

- 什么是event对象
  - 用来获取事件的详细信息：鼠标位置、键盘按键
    - 例子：获取鼠标位置：clientX
    - document的本质：理解为最顶层的虚拟的父节点document.childNodes[0].tagName 
- 获取event对象(兼容性写法)
  - **var oEvent=ev||event;**（FF和IE的兼容）
- 事件流
  - 事件冒泡
  - 取消冒泡：oEvent.cancelBubble=true
  - 例子：仿select控件
  - DOM事件流

#### 鼠标事件

- 鼠标位置
  - 可视区位置：clientX、clientY
    - 例子1：跟随鼠标的Div    消除滚动条的影响
    - 滚动条的意义——可视区与页面顶部的距离scrollLeft
  - 获取鼠标在页面的绝对位置
    - 封装函数
    - 例子2：一串跟随鼠标的Div
    - 思考题：在鼠标不移动时，也能实现鼠标跟随

#### 键盘事件

- keyCode

  - 获取用户按下键盘的哪个按键oEvent.keyCode

  - 例子：键盘控制Div移动

    - offsetWidth/Height/Top/Left  卡？
    - 思考题：如何消除不卡顿的DIV移动
- 其他属性
  - ctrlKey、shiftKey、altKey
  - 例子：提交留言
    - 回车 提交
    - ctrl+回车 提交&&
- onkeypress=onkeydown+onkeyup

#### 默认行为

- 默认行为

  - 什么是默认行为

- 阻止默认行为

  - 普通写法：return false;
  - 例子1.屏蔽右键菜单  oncontextmenu
    - 弹出自定义右键菜单例子
  - 例子2.只能输入数字的输入框
    - 判断keyCode
    - keydown、keyup事件的区别

#### 拖拽

- 简易拖拽
  - 拖拽原理
    - 距离不变     disX和DisY
    - 三个事件      onmousedown/onmousemove/onmouseup
- 靠谱拖拽
  - 原有拖拽的问题//拖快了就按不到了
    - 直接给document加事件
  - FF下，空Div拖拽Bug   
    - 阻止默认事件   return false？
  - 防止拖出页面
    - 修正位置   左右上下的距离不超出![width](E:\Web前端\练习\JavaScript\妙味课堂\03\width.png)