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
- 子节点可以是DocumentType、Element、ProcessingInstruction或Comment

##### 1.文档的子节点

documentElement、firstChild和childNodes[0]的值相同，都指向<html>

document.body指向<body>

以上两种属性所有浏览器都支持

document.doctype//取得对<!DOCTYPE>的引用

不同浏览器的差别很大，所以用处有限

##### 2.文档信息

title——document.title

URL页面完整URL

domain只包含页面域名

referrer链接到当前页面的那个页面的URL

##### 3.查找元素

①getElementById()

- 不要让表单字段的name特性与其他元素的ID相同

②getElementsByTagName()

- 返回的是包含零个或多元素的动态集合HTMLCollection
- 可以用[]或者item()放法访问
- HTMLCollection还有一个namedItem()方法，通过元素的name特性取得集合中的项。也可以使用方括号

```javascript
var images=document.getElementsByTagName("img")

var myImage=images.namedItem("myImage");
var myImage=images["myImage"];
```

- getElementsByTagName(*)取得文档中所有元素，第一项<html>第二项<head>

③getElementByName()：常用来选单选按钮

##### 4.特殊集合

为访问文档的常用部分提供了快捷方式

- document.anchors：带name特性的<a>元素

- document.forms

- document.images

- document.links：所有带href特性的<a>元素

  之前的快捷方式

- document.body 

- document.documentElement

- document.doctype

##### 5.DOM一致性检测

检测浏览器实现了DOM的哪些部分

DOM1级为document.implementstion属性规定了一个方法hasFeature()：接受两个参数（要检测的DOM功能的名称及版本号）

##### 6.文档写入

将输出流写入到网页的能力

四个方法：

- write()：原样写入
- writeln()：末尾添加换行符\n
- open()
- close()

```javascript
<script type="text/javascript">
    document.write("<script type=\"text\javascript\" src=\"file.js\">" +   
        "<\/script>");//注意加入转义字符\
</script>
```

#### 1.3 Element类型

Element类型勇于表现XML和HTML元素

nodeType的值为1；

nodeName的值为元素的标签名，tagName属性也是；

parentNode可能是DOcument或者Element；

在HTML中，标签名始终全部大写，XML中与源码相同

```
if(element.tagName.toLowerCase()=="div"){
//这样转换大小写比较最好，不容易出错
}
```

##### 1.HTML元素

标准特性

- id
- title：元素的附加说明信息
- lang
- dir
- className

##### 2. 取得特性

操作特性的DOM方法有三个

- getAttribute()
- setAttribute()
- removeAttribute()

也可以取得自定义特性（自定义特性前面加data-前缀）

特殊：

- style
- onclick这样的事件处理程序

他们虽然有对应的属性名，但是属性的值与通过getAttribute()返回的值并不同。

所以经常不适用getAttribute()，而是只使用对象的属性

##### 3.设置特性

setAttribute()：两个参数（要设置的特性名，值）

如果特性已存在则替换，如果无则创建

```
div.id="someOtherId"
dic.align="left"
```

直接给属性赋值

##### 4.attribute属性

Element类型是使用attribute属性唯一的DOM节点类型

attribute属性中包含一个NameNodeMap，动态的集合

NameNodeMap对象拥有下列方法

| 方法                 | 描述                         |
| ------------------ | -------------------------- |
| getNamedItem(name) | 可返回指定的节点（通过名称）             |
| setNamedItem(name) | 像列表中添加节点，以节点的nodeName属性为索引 |
| item(pos)          | 可返回处于数字pos位置的节点            |
| removeNamedItem()  | 可删除指定的节点（根据名称）             |

```javascript
var pairs = new Array(),
    attrName,
    attrValue,
    i,
    len;

for (i=0, len=element.attributes.length; i < len; i++){
    attrName = element.attributes[i].nodeName;
    attrValue = element.attributes[i].nodeValue;
    if (element.attributes[i].specified){
        pairs.push(attrName + "=\"" + attrValue + "\"");
    }
}
return pairs.join(" ");
}
//遍历元素特性，构造字符串
```

##### 5.创建元素

document.creatElement()方法

浏览器要呈现要先添加到文档树上

##### 6.元素的子节点

childNodes

浏览器对待节点的不同

```html
    <ul id="myList">
        <ll>item 1</ll>
        <ll>item 2</ll>
        <ll>item 3</ll>
    </ul>
```

IE浏览器:3个子节点

其他浏览器：7个子节点，包括了四个文本节点

*处理方法：在执行某项操作以前，检查nodeType属性==1（元素节点）*

```javascript
for (var i = 0; len = element.childNodes.length; i<len,i++) {
    if(element.childNodes[i].nodeType==1;){
        //执行某项操作
    }
}
```

#### 1.4 Text类型

包含可以照字面解释的纯文本内容，纯文本内容可以包括转义后的HTML字符，但不能包含HTML代码

- nodeType值为3
- nodeName值为"#text"
- 没有子节点

可以通过nodeValue属性或者data属性访问Text节点中包含的文本

操作节点的文本

- appendData(text)
- deleteData()
- insertData()
- replaceData()
- splitText()
- substringData()

##### 1.创建文本节点

document.createTextNode()

##### 2.规范化文本节点

在父元素上调用normalize()方法将相邻文本节点合并

##### 3.分割文本节点

splitText()

splitText(5)从位置5开始分割成原来的文本节点和新的文本节点，还在原来的父节点下

#### 1.5Comment类型

- nodeType值为8
- nodeName值为"#comment"
- 没有子节点

与Text类型继承自相同的基类，拥有除了splitText()之外的所有字符串操作方法

注释节点也是一个子节点

#### 1.6 CDATASection类型

针对基于XML的文档

#### 1.7DocumentType类型

- nodeType值为10

#### 1.8DOcumentFragment类型

轻量级文档，可以包含和控制节点

不会占用资源

可以当“仓库”来使用

#### 1.9Attr类型

元素的特性

尽管他们也是节点，但特性不被认为是DOM文档树的一部分

Attr对象三个属性：name，value，specified

### 2.DOM操作技术

#### 2.1 动态脚本

- 插入外部文件
- 直接插入JavaScript代码

#### 2.2动态样式

- link外部文件——插入head元素
- style嵌入

以上两种直接插入代码的方法，要注意兼容性，因为IE将<script>和<style>视为特殊的元素，不允许访问其子节点；所以可以用text属性

script.text=“”

而Safari3之前的版本不能正确支持text属性

#### 2.3操作表格

##### Table 对象集合

| 集合                                       | 描述                     |
| ---------------------------------------- | ---------------------- |
| [cells[\]](http://www.w3school.com.cn/jsref/coll_table_cells.asp) | 返回包含表格中所有单元格的一个数组。     |
| [rows[\]](http://www.w3school.com.cn/jsref/coll_table_rows.asp) | 返回包含表格中所有行的一个数组。       |
| tBodies[]                                | 返回包含表格中所有 tbody 的一个数组。 |

##### Table 对象方法

| 方法                                       | 描述                     |
| ---------------------------------------- | ---------------------- |
| [createCaption()](http://www.w3school.com.cn/jsref/met_table_createcaption.asp) | 为表格创建一个 caption 元素。    |
| [createTFoot()](http://www.w3school.com.cn/jsref/met_table_createtfoot.asp) | 在表格中创建一个空的 tFoot 元素。   |
| [createTHead()](http://www.w3school.com.cn/jsref/met_table_createthead.asp) | 在表格中创建一个空的 tHead 元素。   |
| [deleteCaption()](http://www.w3school.com.cn/jsref/met_table_deletecaption.asp) | 从表格删除 caption 元素以及其内容。 |
| [deleteRow()](http://www.w3school.com.cn/jsref/met_table_deleterow.asp) | 从表格删除一行。               |
| [deleteTFoot()](http://www.w3school.com.cn/jsref/met_table_deletetfoot.asp) | 从表格删除 tFoot 元素及其内容。    |
| [deleteTHead()](http://www.w3school.com.cn/jsref/met_table_deletethead.asp) | 从表格删除 tHead 元素及其内容。    |
| [insertRow()](http://www.w3school.com.cn/jsref/met_table_insertrow.asp) | 在表格中插入一个新行。            |
| insertCell()                             | 插入一个单元格                |

#### 2.4使用NodeList

NodeList

NamedNodeMap

HTMLCollection

这三个集合都是动态的

想要迭代一个NodeList，最好使用length属性初始化第二个变量，然后将迭代器与变量进行比较

```javascript
for (var i = 0; len = divs.length; i<len,i++)
```

## 第十一章：DOM扩展

### 1.选择符API

根据CSS选择符选择与某个模式匹配的DOM元素

#### 1.1querySelector()方法

接收一个css选择符，返回模式匹配的**第一个元素**

document类型调用，会在文档元素范围查找

Element类型调用，会在在元素后代查找

#### 1.2querySelector()

返回**所有**匹配元素，返回的是一个NodeList实例

要取得返回的NodeList的每个元素，可以用[]，或者item()

#### 1.3matchesSelector()

接收一个CSS选择符，如果调用元素与该选择符匹配，返回true

由于浏览器对于这一功能的支持不同，需要使用包装函数

### 2.元素遍历

支持Element Traversal 规范的浏览器有IE 9+、Firefox 3.5+、Safari 4+、Chrome 和Opera 10+。

对于元素间的空格，在IE9之前，都不会返回文档节点，其它的所有浏览器都会返回文档节点。

为了兼容浏览器这间的差异，又不更改已有的DOM 标准，所以有了 Element Traversal 规范。

这个规范为 元素增加了 5 个 属性

- childElementCount
- firstElementChild
- lastElementChild
- previousElementSibling
- nextElementSibling

```javascript
     child=element.firstElementChild;
while(child!=element.lastElementChild){
     processChild(child);
     child = child.nextElementSibling;
     }
```

### 3.HTML5

#### 3.1与类相关的扩充

##### 1.getElementsByClassName()方法

可以包含一个或者多个类名

返回的对象是NodeList

##### 2.classList属性

 classList 属性返回元素的类名，作为DOMTokenList 对象。
该属性用于在元素中添加，移除及切换 CSS 类。 
 classList 属性是只读的，但你可以使用add() 和 remove() 方法修改它

- add(class1, class2, ...)

- contains(class)：存在返回true

- remove(class1, class2, ...)

- toggle(class)：如果有就删除，没救就添加

-支持classList 属性的浏览器有Firefox3.6和Chrome

#### 3.2 焦点管理

document.activeElement属性：引用给当前获得焦点的元素

document.hasFocus()方法：确定文档是否获得了焦点

#### 3.3 HTMLDocument的变化

HTML5扩展了HTMLDocument

##### 1.readyState属性

- loading
- complete

```
if(document.readyState == "complete"){
//执行操作
};
```

##### 2.兼容模式

document.compatMode的值

- CSS1Compat——标准模式
- BackCompat——混杂模式

#### 3.4字符集属性

- document.charset
- document.defaultcharset

#### 3.5自定义数据属性

HTML5 规定可以为元素添加非标准的属性，但要添加前缀data-，目的是为元素提供与渲染无关的信息，或者提供语义信息。

可以通过dataset属性访问自定义属性的值

dataset属性的值是DOMStringMap的一个实例，也就是一对名值对的映射

#### 3.6插入标记

使用插入标记技术，直接插入HTML字符串更简单

##### 1.innerHTML属性

##### 2.outerHTML

返回调用它的元素及所有子节点的HTML标签

innerHTML 设置或获取位于对象起始和结束标签内的 **HTML** 
outerHTML 设置或获取对象及其内容的 HTML 形式 
innerText 设置或获取位于对象起始和结束标签内的**文本** 
outerText 设置(包括标签)或获取(不包括标签)对象的文本 

##### 3.insertAdjacentHTML()方法

两个参数（插入的位置，HTML文本）

第一个参数的值：

- beforebegin:之前同辈

- afterbegin：第一个子元素

- beforeend：最后一个子元素

- afterend：之后同辈

  ​

##### 4.内存与性能问题

单独构建字符串，再把结果字符串赋值给innerHTML

#### 3.7 scrollIntoView()方法

可以在所有HTML元素调用，通过滚动浏览器窗口或某个容器元素，焦勇元素就可以出现在视口中。

- true：调用元素的顶部与视口顶部齐平
- false：调用元素尽可能全部出现在视口

```
//让元素可见
document.forms[0].scrollInterView()
```

### 4.专有扩展

#### 4.1文档模式

#### 4.2children属性

#### 4.3contains()方法

某个节点是不是另一个节点的后代

#### 4.4插入文本

innerText属性

outerText属性

#### 4.5滚动

- scrollIntoViewIfNeeded()：如果不可见则让它可见
- scrollByLines():滚动指定的行高
- scrollByPages()：滚动指定的页面高度

## 第十二章：DOM2和DOM3

DOM1级主要定义的是HTML和XML文档的底层结构。DOM2与DOM3主要是在DOM1的基础上引入更多的交互能力，支持了更高级的XML特性。

DOM2 和DOM3级分为许多模块（模块之间具有某种关联），分别描述了DOM 的某个非常具体的子集。这些模块如下

- DOM2 级核心（DOM Level 2 Core）：在1 级核心基础上构建，为节点添加了更多方法和属性。
- DOM2 级视图（DOM Level 2 Views）：为文档定义了基于样式信息的不同视图。
- DOM2 级事件（DOM Level 2 Events）：说明了如何使用事件与DOM文档交互。
- DOM2 级样式（DOM Level 2 Style）：定义了如何以编程方式来访问和改变CSS 样式信息。
- DOM2 级遍历和范围（DOM Level 2 Traversal and Range）：引入了遍历DOM 文档和选择其特定部分的新接口。
- DOM2 级 HTML（DOM Level 2 HTML）：在1 级HTML 基础上构建，添加了更多属性、方法和新接口

### 1.DOM变化

DOM2和DOM3，实现了对既有的API进行扩展，提供了更好的错误处理以及特性检测能力。这从很大程度上支持了命名空间。要确定浏览器是否支持DOM2和DOM3，可以使用以下的代码：

```javascript
var supportsDOM2Core=document.implementation.hasFeature("Core","2.0");

var supportsDOM3Core=document.implementation.hasFeature("Core","3.0");

var supportsDom2HTML=document.implementation.hasFeature("HTML","2.0");

var supportsDOM2Views=document.implementation.hasFeature("Views","2.0");

var supportsDom2XML=document.implementation.hasFeature("XML","2.0");

```



#### 1.1针对XML命名空间的变化

有了XML的命名空间，不同XML可以合并成为一个XML。从技术上说，html不支持XML命名空间，但是XHTML支持。命名空间要使用xmlns特性来指定。

使用示例：

<html  xmlns="http://www.w3.org/1999/xhtml">, 使用它来替换<html>

但是，想要明确的为XML命名空间创建前缀，可以使用xmlns后跟冒号，再后跟前缀。

<xhtml:html xmlns:xhtml= "http://www.w3.org/1999/xhtm" > ,使用它来替换<html>

为了区分XHTML中元素，避免混乱，也需要使用命名空间来进行限定标签名称和标签属性。

DOM2提供的针对命名空间的解决方法

##### 1.Node类型的变化

在DOM2级别中，Node类型包含特定于命名空间的属性

- localname:不带命名空间前缀的节点名称


- namespaceURI：命名空间的URI或者（未指定的情况下）null


- prefix：命名空间前缀或者（未指定的情况下）null

DOM3在此基础上更进一步，引入例如与命名空间相关的方法：

- isDefaultNamespace(namespaceURI):在指定的namespaceURI是当前节点的默认命名空间的情况下返回true

- lookupNamespaceURI(prefix):返回给定的prefix的命名空间

- lookupPrefix(namespaceURI):返回给定的namespaceURI的前缀

##### 2.Document类型的变化

DOM2为命名空间创建了一下的方法：方法的意义类似DOM1的

- createElementNS(namespaceURI,tagName):
- createAttributeNS(namespaceURI,attributeName):
- getElementsByTagNameNS(namespaceURI,tagName):

##### 3.Element类型的变化

DOM2级核心中有关Element的变化主要涉及操作特性。新增方法具体意义参见DOM1的：
- getAttributeNS(namespaceURI,localname):
- getAttributeNodeNS(namespaceURI,localname):
- getElementsByTagNameNS(namespaceURI,tagName):
- hasAttributeNS(namespaceURI,attributeName):
- removeAttributeNS(namespaceURI,attributeName):
- setAttributeNS(namespaceURI,qualifiedName,value):
- setAttributeNodeNS(attNode):

##### 4.NamedNodeMap类型的变化,同上

- getNamedItemNS(namespaceURI,localName):
- removeNamedItemNS(namespaceURI,localName):
- setNamedItemNS(node):

#### 1.2 其他方面的变化

这些变化与XML命名空间无关，而是更倾向于确保API的可靠性和完整性。

##### 1.DocumentType类型的变化

新增了三个属性:
- publicId:
- systemId:
- interbalSubset:

以下面的标签为例：

```
<！DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 //EN" "http://www.w3.org/TR/html4/strict.dtd">
```

publicId=-//W3C//DTD HTML 4.01 //EN

systemId=“http://www.w3.org/TR/html4/strict.dtd](http://www.w3.org/TR/html4/strict.dtd) ”

  最后一个属性interSubset不常用，访问内部子集用的，XML用的较多。

##### 2.Document类型的变化

唯一与命名空间无关的方法是importNode()，这个是用来<u>从一个文档中取得一个节点，然后导入另一个文档的，使其成为另一个文档结构的一部分。</u>它接收两个参数：要复制的节点和一个鄙视是否复制子节点的布尔值。

##### 3.Node类型的变化

##### 4.框架的变化

### 2.样式

在 HTML 中定义样式的方式有3 种：

- 通过<link/>元素包含外部样式表文件、

- 使用<style>元素定义嵌入式样式

- 使用style 特性定义针对特定元素的样式。

“DOM2 级样式”模块围绕这3 种应用样式的机制提供了一套API。要确定浏览器是否支持DOM2 级定义的CSS 能力，可以使用下列代码         

```javascript
var supportsDOM2CSS = document.implementation.hasFeature("CSS", "2.0");
var supportsDOM2CSS2 = document.implementation.hasFeature("CSS2", "2.0");
```

#### 2.1访问元素的样式

- style.color普通
- style.backgroundImage短划线的变驼峰
- style.Float（IE）和CSSFloat：float的不同浏览器

##### 1.DOM样式属性和方法

- cssText：通过它能够访问和设置style 特性中的CSS代码.支持IE6+,chrome,firfox.
- length：应用给元素的CSS 属性的数量。支持IE9+,chrome,firfox.
- parentRule：表示CSS 信息的CSSRule 对象,后面将讨论CSSRule 类型。
- getPropertyPriority(propertyName)：如果给定的属性使用了!important 设置，则返回"important"；否则，返回空字符串。支持IE9+,chrome,firfox.
- getPropertyValue(propertyName)：返回给定属性的字符串值。支持IE9+、Safari,Chrome,firfox
- item(index)：返回给定位置的CSS 属性的名称。支持IE9+、Safari,Chrome,firfox
- removeProperty(propertyName)：从样式中删除给定属性。支持IE9+、Safari,Chrome,firfox
- setProperty(propertyName,value,priority)：将给定属性设置为相应的值，并加上优先权标志（"important"或者一个空字符串）。支持IE9+、Safari,Chrome,firfox

```javascript
//设置style对象的cssText属性
myDiv.style.cssText = "width: 25px; height: 100px; background-color: green";
alert(myDiv.style.cssText);
```

##### 2.计算的样式

#### 2.2操作样式表

CSSStyleSheet 类型表示的是样式表，包括通过<link>元素包含的样式表和在<style>元素中定义的样式表,使用下面的代码可以确定浏览器是否支持DOM2 级样式表：         

```javascript
var supportsDOM2StyleSheets =document.implementation.hasFeature("StyleSheets", "2.0");
```

CSSStyleSheet 继承自StyleSheet，后者可以作为一个基础接口来定义非CSS 样式表。从StyleSheet 接口继承而来的属性如下:

- disabled：表示样式表是否被禁用的布尔值。这个属性是可读/写的，将这个值设置为true可以禁用样式表。

- href：如果样式表是通过<link>包含的，则是样式表的URL；否则，是null。

- media：当前样式表支持的所有媒体类型的集合。与所有DOM 集合一样，这个集合也有一个length 属性和一个item()方法。也可以使用方括号语法取得集合中特定的项。如果集合是空列表，表示样式表适用于所有媒体。在IE 中，media 是一个反映<link>和<style>元素media特性值的字符串。

- ownerNode：指向拥有当前样式表的节点的指针，样式表可能是在HTML 中通过<link>或<style/>引入的（在XML 中可能是通过处理指令引入的）。如果当前样式表是其他样式表通过@import 导入的，则这个属性值为null。IE 不支持这个属性。

- parentStyleSheet：在当前样式表是通过@import 导入的情况下，这个属性是一个指向导入它的样式表的指针。

- title：ownerNode 中title 属性的值。

- type：表示样式表类型的字符串。对CSS 样式表而言，这个字符串是"type/css"。

除了 disabled 属性之外，其他属性都是只读的。在支持以上所有这些属性的基础上，CSSStyleSheet 类型还支持下列属性和方法：

- cssRules：样式表中包含的样式规则的集合。IE 不支持这个属性，但有一个类似的rules 属性。

- ownerRule：如果样式表是通过@import 导入的，这个属性就是一个指针，指向表示导入的规则；否则，值为null。IE 不支持这个属性。

- deleteRule(index)：删除cssRules 集合中指定位置的规则。IE 不支持这个方法，但支持一个类似的removeRule()方法。

- insertRule(rule,index)：向cssRules 集合中指定的位置插入rule 字符串。IE 不支持这个方法，但支持一个类似的addRule()方法。

应用于文档的所有样式表是通过 **document.styleSheets 集合**来表示的。也可以直接通过<link>或<style>元素取得CSSStyleSheet 对象。

DOM 规定了一个包含CSSStyleSheet 对象的属性，名叫sheet；除了IE，其他浏览器都支持这个属性。IE 支持的是styleSheet属性

##### 1.CSS规则

CSSRule对象表示样式表中的每一条规则

```javascript
function getStyleInfo(){
    var sheet = document.styleSheets[0];
    var rules = sheet.cssRules || sheet.rules;
    var rule = rules[0];
    alert(rule.selectorText);
}
```

```javascript
function changeStyleInfo(){        
     var sheet = document.styleSheets[0];
     var rules = sheet.cssRules || sheet.rules;
     var rule = rules[0];    

     rule.style.backgroundColor = "red";
}
```

##### 2.创建规则

insertRule()方法

跨浏览器插入规则

```javascript
function insertRule(sheet, selectorText, cssText, position){
    if (sheet.insertRule){
        sheet.insertRule(selectorText + "{" + cssText + "}", position);
    } else if (sheet.addRule){
        sheet.addRule(selectorText, cssText, position);
    }
}
```

##### 3.删除规则

deleteRule()方法

#### *2.3元素大小*

 ![12.2.3元素大小](12.2.3元素大小.png)

##### 1.偏移量

元素在屏幕上占用的所有可用空间。不包括外边距

- offsetHeight：元素在垂直方向上占用的空间大小，以像素计。包括元素的高度、（可见的）水平滚动条的高度、上边框高度和下边框高度。

- offsetWidth：元素在水平方向上占用的空间大小，以像素计。包括元素的宽度、（可见的）垂直滚动条的宽度、左边框宽度和右边框宽度。

- offsetLeft：元素的左外边框至包含元素的左内边框之间的像素距离。

- offsetTop：元素的上外边框至包含元素的上内边框之间的像素距离。

##### 2.客户区大小

元素内容及其内边距所占空间的大小

clientWidth 和clientHeight
- clientWidth 属性是元素内容区宽度加上左右内边距宽度；
- clientHeight 属性是元素内容区高度加上上下内边距高度

##### 3.滚动大小
- scrollHeight：在没有滚动条的情况下，元素内容的总高度。

- scrollWidth：在没有滚动条的情况下，元素内容的总宽度。

- scrollLeft：被隐藏在内容区域左侧的像素数。通过设置这个属性可以改变元素的滚动位置。

- scrollTop：被隐藏在内容区域上方的像素数。通过设置这个属性可以改变元素的滚动位置。


##### 4.确定元素大小

IE、Firefox 3+、Safari 4+、Opera 9.5 及Chrome 为每个元素都提供了一个*getBoundingClientRect()方法*。这个方法返回会一个矩形对象，包含4 个属性：left、top、right 和bottom。**这些属性给出了元素在页面中相对于视口的位置**。

但是，浏览器的实现稍有不同。IE8 及更早版本认为文档的左上角坐
标是(2, 2)，而其他浏览器包括IE9 则将传统的(0,0)作为起点坐标。因此，就需要在一开始检查一下位于(0,0)处的元素的位置，在IE8 及更早版本中，会返回(2,2)，而在其他浏览器中会返回(0,0).

### 3.遍历



### 4.范围