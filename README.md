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

var zhangsan = new Person();
zhangsan.setName('张三')；
console.log(zhangsan.getName());

//打印结果：张三
```

##继承 （Inheritance）
JavaScript 通过允许在构造器函数中与原型对象相关联的方式来实现继承的。这样，您可以创建完全一样的 Persion — Students 示例，不过需要使用略微不同的术语。首先，定义 Employee 构造器函数，指定 name 和 age 属性；然后，定义 Students 构造器函数，指定 id 属性。最后，将一个新的 Persion 对象赋值给 Students 构造器函数的 prototype 属性。这样，当创建一个新的 Students 对象时，它将从 Persion 对象中继承 name and age 属性

```javascript
function Person(){
  this.name = ‘张三’;
  this.age = ‘’;
}

function Students(id){
  this.id = id;
}
Students.prototype = new Person;

var zhangsan = new Students(1001);

//zhangsan.name = 张三;
//zhangsan.age = '';
//zhangsan.id = 1001;


```

```javascript
function Person(name,age){
  this.name = name || ‘张三’;
  this.age = age || 0;
}

function Students(id,name){
  this.id = id || 0;
  this.name = name || ''
}
Students.prototype = new Person;

var lisi = new Students(1001,'李四');

//lisi.name = 李四;
//lisi.age = 0;
//lisi.id = 1001;
```
，由上面对类的定义，您无法为诸如 name 这样的继承属性指定初始值。如果想在JavaScript中为继承的属性指定初始值，您需要在构造器函数中添加更多的代码。
```javascript
var Person = function(firstName) {
  this.firstName = firstName;
};

Person.prototype.walk = function(){
  console.log("I am walking!");
};

Person.prototype.sayHello = function(){
  console.log("Hello, I'm " + this.firstName);
};

function Student(firstName, subject) {

  Person.call(this, firstName);

  this.subject = subject;
};


Student.prototype = Object.create(Person.prototype);

Student.prototype.constructor = Student;

Student.prototype.sayHello = function(){
  console.log("Hello, I'm " + this.firstName + ". I'm studying "
  + this.subject + ".");
};

Student.prototype.sayGoodBye = function(){
  console.log("Goodbye!");
};

var student1 = new Student("Janet", "Applied Physics");

console.log(student1 instanceof Person);  // true
console.log(student1 instanceof Student); // true
```

## 多态
先来说明一下重载和覆盖的区别。重载的英文是 overload，覆盖的英文是 override。发现网上大多数人把 override 当成了重载，这个是不对的。重载和覆盖是有区别的。

重载的意思是，同一个名字的函数（注意这里包括函数）或方法可以有多个实现，他们依靠参数的类型和（或）参数的个数来区分识别。

而覆盖的意思是，子类中可以定义与父类中同名，并且参数类型和个数也相同的方法，这些方法的定义后，在子类的实例化对象中，父类中继承的这些同名方法将被隐藏。

##### 重载

javascript 中函数的参数是没有类型的，并且参数个数也是任意的，例如，尽管你可以定义一个：

```javascript
function add(a, b) {
  return a + b;
}
```
这样的函数，但是你仍然可以再调用它是带入任意多个参数，当然，参数类型也是任意的。至于是否出错，那是这个函数中所执行的内容来决定的，javascript 并不根据你指定的参数个数和参数类型来判断你调用的是哪个函数。

因此，要定义重载方法，就不能像强类型语言中那样做了。但是你仍然可以实现重载。就是通过函数的 arguments 属性。例如：

```javascript
function add() {
  var sum = 0;
  for (var i = 0; i < arguments.length; i++) {
    sum += arguments[i];
  }
  return sum;
}
```
这样你就实现了任意多个参数加法函数的重载了。

当然，你还可以在函数中通过 instanceof 或者 constructor 来判断每个参数的类型，来决定后面执行什么操作，实现更为复杂的函数或方法重载。总之，javascript 的重载，是在函数中由用户自己通过操作 arguments 这个属性来实现的。

##### 覆盖

实现覆盖也很容易，例如：

```javascript
function parentClass() {
  this.method = function() {
    alert("parentClass method");
  }
}
function subClass() {
  this.method = function() {
    alert("subClass method");
  }
}
subClass.prototype = new parentClass();
subClass.prototype.constructor = subClass;

var o = new subClass();
o.method();
```
这样，子类中定义的 method 就覆盖了从父类中继承来的 method 方法了。

你可能会说，这样子覆盖是不错，但 java 中，覆盖的方法里面可以调用被覆盖的方法（父类的方法），在这里怎么实现呢？也很容易，而且比 java 中还要灵活，java 中限制，你只能在覆盖被覆盖方法的方法中才能使用 super 来调用次被覆盖的方法。我们不但可以实现这点，而且还可以让子类中所有的方法中都可以调用父类中被覆盖的方法。看下面的例子：

```javascript
function parentClass() {
  this.method = function() {
    alert("parentClass method");
  }
}
function subClass() {
  var method = this.method;
  this.method = function() {
    method.call(this);
    alert("subClass method");
  }
}
subClass.prototype = new parentClass();
subClass.prototype.constructor = subClass;

var o = new subClass();
o.method();
```
你会发现，原来这么简单，只要在定义覆盖方法前，定义一个私有变量，然后把父类中定义的将要被覆盖的方法赋给它，然后我们就可以在后面继续调用它了，而且这个是这个方法是私有的，对于子类的对象是不可见的。这样跟其它高级语言实现的覆盖就一致了。

最后需要注意，我们在覆盖方法中调用这个方法时，需要用 call 方法来改变执行上下文为 this（虽然在这个例子中没有必要），如果直接调用这个方法，执行上下文就会变成全局对象了。

## javascript 如何定义属性和方法

##### 定义属性

javascript中在原型用定义属性有两种方法。一种是`var name = ''`,这种是定义私有变量。还有一种是 `this.name = ''`.

##### 定义方法（类方法和实例方法）
类方法
```javascript
function Person(){
  this.name = '';
}

Person.run = funtion(){
  return 'person runing';
}
```
实例方法
```javascript
Person.prototype.run = function(name){
  return name + 'runing';
}
```
