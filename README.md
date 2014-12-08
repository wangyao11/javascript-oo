# 类，对象和实例

## 类(class)
类（class）是一种面向对象编程的构成，class是创建对象的蓝图，通俗点说就是模板。类是抽象的事物，而不是所描述的对象中的任何的个体，根据类可以创建出你需要的对象。比如：Students类可以用来表示所有雇员的集和.

```javascript
//javascript中定义类
function Students(name,id){
  this.name = name;
  this.id = id;
}
```
```java
//java 中定义类
public class Students{
  String name = '';
  String id = '';
  public Students(name,id){
    this.name = name;
    this.id = id;
  }
}
```
## 对象（Object）
上面说到的类是一种抽象的事物，它是不存在于现实中的，而对象是实实在在存在的，他是具体，比如说：students 类，它是对学生的一种抽象，它具有学生都有的属性，如：学号。和行为，如：上课。但他没有具体数据。而对象就是某个学生，每个的学生都可以称为是对象。

```
students str;
//str 就是一个对象。
```

## 实例（Instance）

实例比对象的定义更小，实例是指具体到某个人，比如：学生A的姓名：XX。学号：XX；这就是以个学生实例，他也是一个对象。

```
var zhangsan = new Students('张三'，1002)；  //js实例化对象
students str = new Students('小李'，1001)；  //java实例化对象
//str这就是一个实例。
```

# 封装，继承和多态

##封装（Encapsulation）

封装就是隐藏对象的属性和实现细节，仅对外公开接口，控制在程序中属性的读取和修改的访问级别；这样作主要有：

1. 安全
2. 重用
3. 不必关系具体的实现

比如：我们通过封装把属性和行为(方法)组装起来,形成一个类(人类),我们可以让某个人（人类的一个对象）吃饭，跑步（调用方法）。但不能让某个人长第三只眼睛（就是说我们不应该去直接操作属性），而跑步要用到腿（属性），腿的长短可能决定跑的快慢（属性影响行为）下面说以下重用，只要我们为人类创建一个跑的方法，以后我们想让张三跑，那就世界实例化一个张三，调用跑的方法就可以了。

```javascript
function Person (){
  var name = '';
}
Person.prototype.getName = function(){
  return this.name;
}
Person.prototype.setName = function(name){
  return this.name = name;
}

var zhangsan = new Persion();
zhangsan.setName('张三')；
console.log(zhangsan.getName());

//打印结果：张三
```

##继承 （Inheritance）
JavaScript 通过允许在构造器函数中与原型对象相关联的方式来实现继承的。这样，您可以创建完全一样的 Persion — Students 示例，不过需要使用略微不同的术语。首先，定义 Employee 构造器函数，指定 name 和 age 属性；然后，定义 Students 构造器函数，指定 id 属性。最后，将一个新的 Persion 对象赋值给 Students 构造器函数的 prototype 属性。这样，当创建一个新的 Students 对象时，它将从 Persion 对象中继承 name and age 属性

```javascript
function Persion(){
  this.name = ‘张三’;
  this.age = ‘’;
}

function Students(id){
  this.id = id;
}
Students.prototype = new Persion;

var zhangsan = new Students(1001);

//zhangsan.name = 张三;
//zhangsan.age = '';
//zhangsan.id = 1001;


```

```javascript
function Persion(name,age){
  this.name = name || ‘张三’;
  this.age = age || 0;
}

function Students(id,name){
  this.id = id || 0;
  this.name = name || ''
}
Students.prototype = new Persion;

var lisi = new Students(1001,'李四');

//lisi.name = 李四;
//lisi.age = 0;
//lisi.id = 1001;
```
，由上面对类的定义，您无法为诸如 name 这样的继承属性指定初始值。如果想在JavaScript中为继承的属性指定初始值，您需要在构造器函数中添加更多的代码。
