## Ajax

- 什么是服务器

  - 网页浏览过程分析

  - 如何配置自己的服务器程序（AMP）


- 什么是Ajax
  - 无刷新数据读取
    - 用户注册、在线聊天室
    - 异步、同步

💛创建Ajax对象

:yellow_heart:连接服务区

💛发送请求

💛接受返回

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

### 编写Ajax

💛创建Ajax对象

```javascript
function ajax(url, fnSucc, fnFaild)//三个参数
{
	//1.创建ajax对象
	var oAjax=null;
	if(window.XMLHttpRequest)
	{
		oAjax=new XMLHttpRequest();
	}
	else
	{
		oAjax=new ActiveXObject("Microsoft.XMLHTTP");
	}
```

- ActiveXObject("Microsoft.XMLHTTP")//IE
- XMLHttpRequest()//用window.XMLHttpRequest验证的原因

💛连接服务区

- open(方法, <u>文件名</u>, 异步传输)

💛发送请求

- send()

:blue_heart:接收返回

- 请求状态监控

  **onreadystatechange事件**

  - readyState属性：请求状态
    - 0（未初始化）还没有调用open()方法
    - 1（载入）已调用send()方法，正在发送请求
    - 2（载入完成）send()方法完成，已收到全部响应内容
    - 3（解析）正在解析响应内容
    - 4（完成）响应内容解析完成，可以在客户端调用了
  - status属性：请求结果（==200）
  - responseText

- 如果失败返回的函数