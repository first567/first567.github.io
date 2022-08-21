---
title: js继承
date: 2021-03-13 09:15:03
tags:
  - [前端]
---

<br>
<!--more-->

## js 继承六种方式

1. 原型链继承

原型链继承其核心在于将父类的实例作为子类的原型

```js
function Person(name, age, sex) {
  this.name = name;
  this.age = age;
  this.sex = sex;
}
Person.prototype.sayHi = function () {
  console.log("大家好，我是" + this.name);
};
//子类型
function Student() {
  this.score = 100;
}
Student.prototype = new Person();
Student.prototype.constructor = Student;

var s1 = new Student();
s1.sayHi(); //大家好，我是undefined
console.log(s1.name); //undefined
console.log(s1.age); //undefined
console.log(s1.constructor); //student
```

2. 构造函数继承

借用构造函数继承其核心

```js
function Dog() {
  Animal.call(this);
  this.name = name || "大黄狗";
}

var dog = new Dog();
console.log(dog.name);
dog.eat("大骨头");
console.log(dog instanceof Animal); // false
console.log(dog instanceof Dog); // true
```
