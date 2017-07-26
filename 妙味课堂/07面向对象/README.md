## 面向对象

什么是对象

- 对象是一个整体，对外提供一些操作

什么是面向对象

- 使用对象时，只关注对象提供的功能，不关注其内部细节
- 比如 JQuery

*面向对象是一种通用思想*，并非只有编程中能用，任何事情都可以用

#### JS中的面向对象

- 面向对象编程(OOP)的特点

  - 抽象：抓住核心问题
  - *封装*：不考虑内部实现，只考虑功能使用
  - *继承*：从已有对象上，继承出新
    - 多重继承
    - *多态*

- 对象的组成

  - 方法——函数：过程、动态的

  - 属性——变量：状态、静止的

    **区分函数和方法，属性和变量**

```javascript
    function show()	//函数
    {
    	alert('a');
    }
    arr.fn=function ()	//方法，属于一个对象
    {
    	alert('a');
    };
    var a=12;		//变量：自由

    arr.a=5;		//属性：属于一个对象
```
#### 第一个面向对象程序

为对象添加方法和属性

- this详解，事件处理中this的本质windowthis——函数属于谁
- 不能在系统对象中随意附加方法、属性，否则会覆盖已有方法、属性
- object对象

#### 工厂方式

- 什么是工厂
  - 原料
  - 加工
  - 出厂
- 工厂方式
  - 用构造函数创建一个类
  - 什么是类、对象（实例）：模具和零件

```javascript
//用工厂方式构造对象
function createPerson(name, sex)	//构造函数
{
	//1.原料
	var obj=new Object();	
	//2.加工
	obj.name=name;
	obj.sex=sex;	
	obj.showName=function ()
	{
		alert('我的名字叫：'+this.name);
	};
	obj.showSex=function ()
	{
		alert('我是'+this.sex+'的');
	};	
	//3.出厂
	return obj;
}
var p1=createPerson('blue', '男');
```

- 工厂方式不常用
- 缺点和问题
  - 没有new
  - 函数重复定义，每个对象都有一套自己的函数-及其浪费资源
- 加上new

```javascript
function createPerson(name, sex)	//构造函数
{
	//假想的系统内部工作流程
	//var this=new Object();
	
	this.name=name;
	this.sex=sex;
	
	this.showName=function ()
	{
		alert('我的名字叫：'+this.name);
	};
	this.showSex=function ()
	{
		alert('我是'+this.sex+'的');
	};
	
	//假想的系统内部工作流程
	//return this;
}

var p1=new createPerson('blue', '男');
var p2=new createPerson('leo', '女');
```

- 偷偷做了两件事

  - 替你创建了一个空白对象

  - 替你返回了这个对象


- new和this

#### 原型——prototype

- 什么是原型

  - 原型是class，修改他可以影响一类元素
  - 在已有对象中加入自己的属性、方法
  - 原型修改对已有对象的影响

  ```
  var arr=new Array();
  Array-类——不具备实际功能，只能用来构造对象
  arr-对象——真正有功能的东西，被类给构造出来
  ```

- 为Array添加sum方法

  - 给对象添加方法，类似于行间样式
  - 给原型添加方法，类似于class
  - 原型的重要应用：扩展系统对象的功能

```javascript
var arr1=new Array(12, 5, 8, 4);
var arr2=new Array(44,6,5,4,5,55,9);

//arr1.sum=function ()
Array.prototype.sum=function ()
{
...
};
```

- 原型的小缺陷无法限制覆盖

##### //解决工厂方式第二个问题

```javascript
function Person(name, sex)
{
	this.name=name;
	this.sex=sex;
}

Person.prototype.showName=function ()
{
	alert(this.name);
};

Person.prototype.showSex=function ()
{
	alert(this.sex);
};

var p=new Person('blue', '男');

p.showName();
p.showSex();
```