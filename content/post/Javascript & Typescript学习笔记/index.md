---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Javascript&Typescript学习笔记"
subtitle: "附代码"
summary: "前端代码的基础学习"
authors: ["wushuang"]
tags: ["front-end"]
categories: ["front-end"]
date: 2020-05-08T20:46:57+08:00
lastmod: 2020-05-08T20:46:57+08:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

# Javascript 语法笔记
*主要用于备忘&快速查阅，仅记录个人学习过程中的易忘点，以代翻阅doc
##### 1.1	js和html文件分离情况：

```html
<!DOCTYPE html>
<html>
<body>
<script src="myScript.js"></script>
</body>
</html>
```

在*.js文件中：

```javascript
function myFunction()
{
  	document.getElementById("demo").innerHTML="我的第一个 JavaScript 函数";
}
```



##### 1.2	 onclick 调用js函数：

```javascript
<script> 
    function myfunction(){
         document.getElementById("demo").innerHTML="onclick事件触发";
        }</script>
    </head>
<body>
    <h1 id="demo">一个段落</h1>
    <button onclick="myfunction()" type="button">点击这里</button>
</body>
```



##### 1.3	输出：

- 使用 **window.alert()** 弹出警告框。

- 使用 **document.write()** 方法将内容写到 HTML 文档中。

  HTML 输出流中使用 document.write相当于insert了文本内容，但如果在函数中使用document.write会覆盖整个怕文档。

  document.write()可以write一个p元素，如date()

- 使用 **innerHTML** 写入到 HTML 元素。

  ```
  document.getElementById("demo").innerHTML = "段落已修改。";
  ```

- 使用 **console.log()** 写入到浏览器的控制台。

  用于debug，如console.loge(c)来查看c的值



##### 1.4	变量类型：

+ 数字字面量

+ 字符串字面量

  最好将字符串创建成对象如`var firstName = new String("John")`，否则创建String会拖慢速度；String类型有它自己的属性、方法。

+ 表达式字面量

+ 数组字面量

  ```javascript
  var cars=new Array();
  cars[0]="Saab";
  cars[1]="Volvo";
  cars[2]="BMW";
  ```

+ 对象字面量

  ```javascript
  var person = {
      firstName:"John",
      lastName:"Doe",
      age:50,
      eyeColor:"blue",
      fullName : function() //对象方法作为一个函数定义存储在对象属性中。
  	{
         return this.firstName + " " + this.lastName;
      }
  };
  /*访问*/
  name = person.firstname+“ ”+person.lastname;//属性
  name = person.fullname();//方法
  ```

+ 函数

声明新变量类型：

```javascript
/*声明*/
var carname=new String;
var x=      new Number;
var y=      new Boolean;
var cars=   new Array;
var person= new Object;
/*赋值*/
var length = 16;                                  // Number 通过数字字面量赋值
var points = x * 10;                              // Number 通过表达式字面量赋值
var lastName = "Johnson";                         // String 通过字符串字面量赋值
var cars = ["Saab", "Volvo", "BMW"];              // Array  通过数组字面量赋值
var person = {firstName:"John", lastName:"Doe"};  // Object 通过对象字面量赋值
```

如果把值赋给尚未声明的变量，该变量将被自动作为 window 的一个属性。通过var声明后赋值的变量是window的一个属性，可以通过 **this.x** 和 **window.x** 来调用，但不可delete；未声名直接赋值的变量可通过 **x** 调用，可以**delete x**删除。

你的全局变量，或者函数，可以覆盖 window 对象的变量或者函数。 局部变量，包括 window 对象可以覆盖全局变量和函数。



##### 1.5	事件

常见的html事件：

| onchange    | HTML 元素改变                |
| ----------- | ---------------------------- |
| onclick     | 用户点击 HTML 元素           |
| onmouseover | 用户在一个HTML元素上移动鼠标 |
| onmouseout  | 用户从一个HTML元素上移开鼠标 |
| onkeydown   | 用户按下键盘按键             |
| onload      | 浏览器已完成页面的加载       |



##### 1.6	格式规范

在js文件中语句后不加**分号**，但在html文件中的js语句后须加分号；

字母大小写敏感；

**{ }**内的语句不分先后，一并执行；

用**反斜杠**对代码拆行；



##### 1.7 绝对相等：===

数据类型和值都相等



##### 1.8	条件语句

```javascript
if (age<18) x="Too young";
voteable=(age<18)?"年龄太小":"年龄已达到";//三目运算符
if(..) xx;
else if(..) xx;
else xx;
```

continue：跳过本轮循环/break：跳出循环/return



##### 1.9	标签

```javascript
label:
statements

break labelname; 
continue labelname;
```

例子：

```javascript
cars=["BMW","Volvo","Saab","Ford"];
list: 
{
    document.write(cars[0] + "<br>"); 
    document.write(cars[1] + "<br>"); 
    document.write(cars[2] + "<br>"); 
    break list;
    document.write(cars[3] + "<br>"); 
    document.write(cars[4] + "<br>"); 
    document.write(cars[5] + "<br>"); 
}
```

continue 语句，带有或不带标签引用都只能用在循环中。break 语句不带标签引用，只能用在循环或 switch 中；通过标签引用，break 语句可用于跳出任何 JavaScript 代码块



##### 1.10	null的使用

**何时使用null?** 当使用完一个比较大的对象时，需要对其进行释放内存时，设置为 null，表示变量不再指向任何对象地址。



##### 1.11	对象类型

 <u>6 种不同的数据类型：</u>

- string
- number
- boolean
- object
- function
- symbol

<u>3 种对象类型：</u>

- Object
- Date
- Array

2 个不包含任何值的数据类型：

- null
- undefined





