# DOM、BOM

[TOC]

### DOM基础

- 什么是DOM
- 浏览器支持情况

#### DOM节点

- childNodes	 nodeType
  - 获取子节点
  - children//理解为childNodes的兼容版


-   parentNode

    - 获取父节点
    - 例子：点击链接，隐藏整个li

-   offsetParent

    - 例子：获取元素在页面上的实际位置

-   首尾子节点

    - 有兼容性问题
    - firstChild、firstElementChild 
    - lastChild 、lastElementChild

-   兄弟节点

    - 有兼容性问题
    - nextSibling、nextElementSibling
    - previousSibling、previousElementSibling


#### 操纵元素属性 

- 元素属性操作
  - 第一种：oDiv.style.display=“block”;
  - 第二种：oDiv.style[“display”]=“block”;
  - 第三种：Dom方式
- DOM方式操作元素属性
  - 获取：getAttribute(名称)
  - 设置：setAttribute(名称, 值)
  - 删除：removeAttribute(名称)

#### DOM元素灵活查找

- 1.getElementById('')
- 2.document.getElementsByTagName('')
- 3.用className选择元素
  - 如何用className选择元素选出所有元素
    - 通过className条件筛选
    - 封装成函数


#### 创建、插入和删除元素

- 创建DOM元素

  - createElement(标签名)		创建一个节点

    - appendChild(节点)		追加一个节点//告诉它插在哪里，插在最好

    例子：为ul插入li

    父.appendChild(子节点)

- 插入元素

  - insertBefore(节点, 原有节点)	在已有元素前插入

  - 例子：倒序插入li

    oUl.insertBefore(oLi, aLi[0]);


- 删除DOM元素
  - removeChild(节点)删除一个节点
  - 例子：删除li

####文档碎片

- 文档碎片文档碎片可以提高DOM操作性能(理论上)
- 文档碎片原理document.createDocumentFragment()


### BOM

#### BOM基础

- 打开、关闭窗口
  - open运行代码功能
    - document.write() 方法
    - about:blank 打开新窗口及返回值
  - close关闭时提示问题
    - close()关闭当前窗口及新开窗口特性
- 常用属性
  - window.navigator.userAgent  检测浏览器版本
  - window.location   读写地址栏

#### 尺寸及坐标

- 窗口尺寸、工作区尺寸
  - 可视区尺寸-
    - document.documentElement.clientWidth
    - document.documentElement.clientHeight
  - 滚动距离
    - document.body.scrollTop
    - document.documentElement.scrollTop

#### 常用方法和事件

- 系统对话框
  - 警告框：alert(“内容”)，没有返回值
  - 选择框：confirm(“提问的内容”)，返回boolean
  - 输入框：prompt()，返回字符串或null
- window对象常用事件
  - onload
  - onscroll
  - onresize
  - 例子：回到顶部按钮、侧边栏广告闪烁问题（非IE6直接用fixed）