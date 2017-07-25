## Ajax

- 什么是服务器

  - 网页浏览过程分析

  - 如何配置自己的服务器程序（AMP）


- 什么是Ajax
  - 无刷新数据读取
    - 用户注册、在线聊天室
    - 异步、同步

### 使用Ajax

*引入ajax.js*

**function ajax(url, fnSucc, fnFaild)**

- 基础：请求并显示静态TXT文件
  - 字符集编码
  - 缓存、阻止缓存
- 动态数据：请求JS（或json）文件
  - eval的使用-----计算字符串里的值
  - DOM创建元素
- 局部刷新：请求并显示部分网页文件
  - page1,page2,page3