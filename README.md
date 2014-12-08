# 类，对象和实例

## 类(class)
类（class）是一种面向对象编程的构成，class是创建对象的蓝图，通俗点说就是模板。类是抽象的事物，而不是所描述的对象中的任何的个体，根据类可以创建出你需要的对象。比如：Students类可以用来表示所有雇员的集和.

```
//javascript中定义类
function Students(name,id){
  this.name = name;
  this.id = id;
}
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
