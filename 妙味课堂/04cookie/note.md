## cookie

#### cookie基础

- 什么是cookie
  - 页面用来保存信息
    - 比如：自动登录、记住用户
  - cookie的特性
    - 同一个网站中所有页面共享一套cookie
    - 数量、大小有限
    - 过期时间
  - JS中使用
    - cookiedocument.cookie

#### 使用cookie

- cookie的使用
  - 设置cookie
    - 格式：名字=值
    - 不会覆盖
    - 过期时间：expires=时间
      日期对象的使用new Date()
    - 封装函数
  - 读取cookie
    - 字符串分割split( )
  - 删除cookie
    - 已经过期
    - 事件-1
- cookie的使用例子

  - 用cookie记录上一次Div的位置

    - 鼠标抬起——记录位置
    - window.onload——读取位置
  - 用cookie记录上次登录的用户名
    - 提交时——记录用户名
    - window.onload——读取用户名


