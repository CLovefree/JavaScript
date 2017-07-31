## 第八章：BOM

### 1.理解window对象

BOM的核心是window

window既是JavaScript访问浏览器窗口的一个接口，又是ECMAScript规定的Global对象

#### 1.1全局作用域

所有在全局作用域中声明的变量、函数都会变成window的属性和方法

```javascript
        var age = 29;
        window.color = "red";
        
        //throws an error in IE < 9, returns false in all other browsers
        delete window.age;

        //throws an error in IE < 9, returns true in all other browsers
        delete window.color;    //returns true
        
        alert(window.age);      //29
        alert(window.color);    //undefined
```

全局变量不能通过delete删除，直接在window对象上定义的可以

尝试访问未声明的变量会抛出错误，但是通过查询window对象，可能知道某个未声明的变量是否存在

#### 1.2窗口关系及框架

window.frames[0]、、、最好用top.frames[0]

top:指向最高层的框架

parent：当前框架的直接上层框架

self：始终指向window

#### 1.3窗口位置

跨浏览器取得窗口左边和上边的位置

```javascript
var leftPos = (typeof window.screenLeft == "number") ? 
               window.screenLeft : window.screenX;
var topPos = (typeof window.screenTop == "number") ? 
               window.screenTop : window.screenY;

        alert("Left: " + leftPos);
        alert("Top: " + topPos);
```

将窗口精确移动到一个新位置

moveTo():新位置的x和y 坐标

moveBy()：水平和垂直方向移动的像素数

window.moveTo(0,0);

window.moveBy(0,100);向下移动100像素

#### 1.4 窗口大小

innerWidth,innerHeight/outerWidth,outerHeight

页面视图大小（减去边框宽度）/浏览器窗口本身尺寸

*document.documentElement.clientWidth*和*document.body.clientWidth*

标准模式/混杂模式

document.compatMode == "CSS1Compat"确定浏览器是否处于标准模式

**取得页面视口的大小**

```javascript
var pageWidth = window.innerWidth,
    pageHeight = window.innerHeight;
            
     if (typeof pageWidth != "number"){
         if (document.compatMode == "CSS1Compat"){
                pageWidth = document.documentElement.clientWidth;
                pageHeight = document.documentElement.clientHeight;
            } else {
                pageWidth = document.body.clientWidth;
                pageHeight = document.body.clientHeight;
            }
        }

        alert("Width: " + pageWidth);
        alert("Height: " + pageHeight);
```

调整浏览器窗口大小

resizeTo()

resizeBy()

#### 1.5 导航和打开窗口

window.open()方法导航到一个特定的URL，也可以打开一个新的浏览器窗口

四个参数（要加载的URL，窗口目标，一个特性字符串，一个表示新页面是否取代浏览器历史记录中当前加载页面的布尔值）

URL：

窗口目标：_self, _parent, _top, _blank或者框架的名字

第三个参数时一个逗号分隔的设置字符串

```
var wroxWin = window.open("http://www.wrox.com/","wroxWindow",
"height:400,width:400,top:10,left:10,resizable==yes";);
```

wroxWin.close();关闭新打开的窗口

#### 1.6 简写调用和超时调用

超时调用：setTimeOut()

间歇调用：setInterval()

取消:clearTimeout

常见使用间歇调用案例；

```javascript
 var num = 0;
 var max = 10;
 var intervalId = null;
        
 function incrementNumber() {
            num++;
        
     //if the max has been reached, cancel all pending executions
     if (num == max) {
         clearInterval(intervalId);
         alert("Done");
     }
 }
        
 intervalId = setInterval(incrementNumber, 500);

```

#### 1.7 系统对话框

alert()

confirm()：确认和取消

prompt():提示用户输入文本

window.print()

window.find()

### 2.location对象

保存着当前文档的信息

使用location对象可以通过编程方式访问浏览器的导航系统。设置相应的属性，可以逐段或整体地修改兰兰器URL

既是window对象属性也是document对象属性

window.location和document.location引用的是同一个对象



 Location 对象属性

| 属性                                       | 描述                          |
| ---------------------------------------- | --------------------------- |
| [hash](http://www.w3school.com.cn/jsref/prop_loc_hash.asp) | 设置或返回从井号 (#) 开始的 URL（锚）。    |
| [host](http://www.w3school.com.cn/jsref/prop_loc_host.asp) | 设置或返回主机名和当前 URL 的端口号。       |
| [hostname](http://www.w3school.com.cn/jsref/prop_loc_hostname.asp) | 设置或返回当前 URL 的主机名。           |
| [href](http://www.w3school.com.cn/jsref/prop_loc_href.asp) | 设置或返回完整的 URL。               |
| [pathname](http://www.w3school.com.cn/jsref/prop_loc_pathname.asp) | 设置或返回当前 URL 的路径部分。          |
| [port](http://www.w3school.com.cn/jsref/prop_loc_port.asp) | 设置或返回当前 URL 的端口号。           |
| [protocol](http://www.w3school.com.cn/jsref/prop_loc_protocol.asp) | 设置或返回当前 URL 的协议。            |
| [search](http://www.w3school.com.cn/jsref/prop_loc_search.asp) | 设置或返回从问号 (?) 开始的 URL（查询部分）。 |

 Location 对象方法

| 属性                                       | 描述           |
| ---------------------------------------- | ------------ |
| [assign()](http://www.w3school.com.cn/jsref/met_loc_assign.asp) | 加载新的文档。      |
| [reload()](http://www.w3school.com.cn/jsref/met_loc_reload.asp) | 重新加载当前文档。    |
| [replace()](http://www.w3school.com.cn/jsref/met_loc_replace.asp) | 用新的文档替换当前文档。 |

assign()方法传递URL

replace()可以装载一个新文档而无须为它创建一个新的历史记录，也就是说，在浏览器的历史列表中，新文档将替换当前文档。

location.reload();//重新加载，有可能从缓存中加载

location.reload(true);//重新加载，从服务器重新加载

### 3.navigator对象

识别客户端浏览器的事实标准

navigator对象属性

#### 3.1 检测插件

非IE浏览器使用plugins数组

- name:插件的名字
- description:插件的描述
- filename:插件的文件名
- length:插件所处理的MIME类型数量

```javascript
//plugin detection - doesn't work in IE
function hasPlugin(name){
    name = name.toLowerCase();
    for (var i=0; i < navigator.plugins.length; i++){
        (navigator.plugins[i].name.toLowerCase().indexOf(name) > -1){
            return true;
        }
    }
        
    return false;
}
         //detect flash 
alert(hasPlugin("Flash"));
         //detect quicktime
alert(hasPlugin("QuickTime"));
        
//detect Java
alert(hasPlugin("Java"));
```

toLowerCase()转成小写，indexOf方法对大小写敏感

indexOf()

indexOf() 方法可返回某个指定的字符串值在字符串中首次出现的位置。位置是从0开始的，如果要检索的字符串值没有出现，则该方法返回 -1。 

IE中的插件比较麻烦，要检测特定的插件就要知道COM标识符

因此要检测某个插件要分别创建检测函数，而不时用上面的通用方法

```javascript
//plugin detection - doesn't work in IE
function hasPlugin(name){
name = name.toLowerCase();
for (var i=0; i < navigator.plugins.length; i++){
    if (navigator.plugins[i].name.toLowerCase().indexOf(name) > -1){
        return true;
    }
}

return false;
}        

//plugin detection for IE
function hasIEPlugin(name){
try {
    new ActiveXObject(name);
    return true;
} catch (ex){
    return false;
}
}
//检测所有浏览器中的Flash
//detect flash for all browsers
function hasFlash(){
var result = hasPlugin("Flash");
if (!result){
    result = hasIEPlugin("ShockwaveFlash.ShockwaveFlash");
}
return result;
}
//检测所有浏览器quicktime
//detect quicktime for all browsers
function hasQuickTime(){
var result = hasPlugin("QuickTime");
if (!result){
    result = hasIEPlugin("QuickTime.QuickTime");
}
return result;
}

//detect flash
alert(hasFlash());

//detect quicktime
alert(hasQuickTime());
```

#### 3.2 注册处理程序

Firefox

### 4.screen对象

screen对象基本只用来表明客户端的能力，其中包括浏览器窗口外部的显示器信息，如像素宽和高

window.resizeTo(screen.availWidth和screen.availHeight）使其占用屏幕的可用空间

screen.width

### 5.history对象

用户上网历史记录

go()方法在用户历史记录中任意跳转

参数为数字：history.go(-1);后退一页

参数为字符串：history.go("wrox.com");跳转到最近的wrox.com页面

back()和forward()代替go()表示后退和前进

length属性保存着历史记录的数量

```
if(history.length==0){
//这应该是用户打开窗口后的第一个页面
}
```

## 第九章：客户端检测

不到万不得已不要使用客户端检测，而是找到更通用的方法，优先采用

方法很多

### 1.能力检测

最为人们广泛接受的客户端检测形式

又叫特性检测

能力检测的目标不是识别特定浏览器，而是识别浏览器的**能力**

如检测对象是否存在sort()方法

```
function isSortable(object){
return typeof object.sort == "function";
}
通过typeof方法，确定sort确实是函数，而不是包含sort属性的对象
```

### 2.怪癖检测

目标是识别浏览器的特殊行为；想知道浏览器存在什么缺陷（“怪癖”也就是bug)

### 3.用户代理检测

在服务器端常用的方法，在客户端万不得已才用

通过检测用户代理字符串来识别浏览器

电子欺骗的历史

检测技术：

- 识别呈现引擎

  五大呈现引擎：IE、Gecko、Webkit、KHTML、Opera

- 识别浏览器

- 识别平台

  三大主流平台：Windows、Mac、Unix（包括Linux）

- 识别Windows操作系统

- 识别移动设备

- 识别游戏系统

完整的代码，包括检测呈现引擎、平台、Windows操作系统、移动设备和游戏系统

[代码](file://E:\Web前端\练习\JavaScript\JavaScript高级程序设计（二）/client.js)

#### 使用方法

- 不能直接准确使用能力检测和怪癖检测
- 同一款浏览器在不同平台下具有不同能力，就必须确定浏览器位于哪个平台下
- 为了跟踪分析等目的需要知道确切的浏览器

## 第十章：DOM

DOM是针对HTML和XML文档的一个API（应用程序编程接口）。DOM描绘了一个层次化的节点树，允许开发人员添加、移除和修改页面的某一部分。

注意LIE中所有的DOM对象都是以COM对象的形式实现的。这意味着IE中的DOM对象与原生JavaScript对象的行为和活动特点并不一致

### 1.节点层次

12种节点类型

#### 1.1Node类型

每个节点都有一个nodeType属性

nodeType 属性返回以数字值返回指定节点的节点类型。

如果节点是元素节点，则 nodeType 属性将返回 1。

如果节点是属性节点，则 nodeType 属性将返回 2。

| 类型   | 描述                    | 子节点                            |                                          |
| ---- | --------------------- | :----------------------------- | :--------------------------------------- |
| 1    | Element               | 代表元素                           | Element, Text, Comment, ProcessingInstruction, CDATASection, EntityReference |
| 2    | Attr                  | 代表属性                           | Text, EntityReference                    |
| 3    | Text                  | 代表元素或属性中的文本内容。                 | None                                     |
| 4    | CDATASection          | 代表文档中的 CDATA 部分（不会由解析器解析的文本）。  | None                                     |
| 5    | EntityReference       | 代表实体引用。                        | Element, ProcessingInstruction, Comment, Text, CDATASection, EntityReference |
| 6    | Entity                | 代表实体。                          | Element, ProcessingInstruction, Comment, Text, CDATASection, EntityReference |
| 7    | ProcessingInstruction | 代表处理指令。                        | None                                     |
| 8    | Comment               | 代表注释。                          | None                                     |
| 9    | Document              | 代表整个文档（DOM 树的根节点）。             | Element, ProcessingInstruction, Comment, DocumentType |
| 10   | DocumentType          | 向为文档定义的实体提供接口                  | None                                     |
| 11   | DocumentFragment      | 代表轻量级的 Document 对象，能够容纳文档的某个部分 | Element, ProcessingInstruction, Comment, Text, CDATASection, EntityReference |
| 12   | Notation              | 代表 DTD 中声明的符号。                 | None                                     |

##### 1.nodeName 和 nodeValue属性

了解节点的具体信息

```javascript
if(someNode.nodeType==1){

value=someNode.nodeName;//nodeName的值是元素的标签名

}
nodeValue的值为null

```

##### 2.节点关系

每个节点都有一个childNodes属性，其中保存一个NodeList对象;

NodeList是一种类数组对象，用来保存一组有序的节点。但他不是Array的实例！！！是动态的

```
var firstChild=someNode.childNode[0];
```

将arguments对象使用Array.prototype.slice()方法可以转换成数组

```javascript
function convertToArray(nodes){
var array =null;
try{
array Array.prptptype.slice.call(node,0);//针对非IE浏览器
catch(ex){
array = new Array();
for(var i=0,len=nodes.length;i<len;i++){
array.push(nodes[i]);
}
}
return array;
}
```

parentNode属性

previousSibling

nextSinling

hasChildNode():是否有一个或多个子节点

ownerDocument指向整个文档的文档节点

##### 3.操作节点

appendChild():向childNodes列表末尾添加一个节点

innerBefore():要插入的节点和作为参照的节点

replaceChild()：要插入的节点和要替换的节点

removeChild():要移除的节点

##### 4.其他方法

cloneNode()

- true：深度复制节点及其真个子节点树
- false：只复制节点本身

#### 1.2Document类型

特征：

- nodeType值为9
- nodeName为"#document"
- nodeValue的值为null
- parentNode为null
- ownerDocument为null