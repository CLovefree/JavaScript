## 定时器

- 开启定时器
  - setInterval  间隔型（函数，时间ms）
  - setTimeout  延时型
  - 两种定时器的区别(无限执行和只执行一次)
- 停止定时器
  - clearInterval（）
  - clearTimeout（）
  - 开启定时器指定一个返回值，关闭的时候关这个

### 数码时钟

- 获取系统时间

  - Date对象
  - getHours、getMinutes、getSeconds

- 显示系统时间

  - 字符串连接
  - 空位补零

- 设置图片路径

  - charAt方法解决低版本浏览器ie7的兼容性

    - 字符串的方法：获取字符串某一位的方法
    - str.charAt();

```javascript
for(var i=0;i<aImg.length;i++)
    	{		aImg[i].src='img/'+str[i]+'.png';
    	}
```

- Date对象其它方法

  //alert(oDate.getFullYear());
  //alert(oDate.getMonth()+1);:arrow_right:需要加1
  //alert(oDate.getDate());

  alert(oDate.getDay());→周日是0

### 延时提示框

- 移入显示，移出隐藏

- 移出时*延时*隐藏

- 简化代码

  - 合并两个相同的mouseover和mouseout


### 无缝滚动-基础

- 物体运动基础

  - 让Div一动起来→offsetLeft+10px
  - offsetLeft的作用
  - 用定时器让物体连续移动

- 效果原理

  - 让ul一直向左移动

- 复制li

  - innerHTML和+=
  - 修改ul的width

- 滚动过界后，重新设置

  - 判断过界

- 改变滚动方向

  - 修改speed
  - 修改判断条件

- 鼠标移入暂停

  - 移入关闭定时器
  - 移出重新开启定时器

  ​