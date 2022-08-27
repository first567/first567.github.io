---
title: js继承
date: 2021-03-13 03:15:03
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

3. 组合继承

```js
function Super() {
  // 只在此处声明基本属性和引用属性
  this.val = 1;
  this.arr = [1];
}
//  在此处声明函数
Super.prototype.fun1 = function () {};
Super.prototype.fun2 = function () {};
//Super.prototype.fun3...
function Sub() {
  Super.call(this); // 核心
  // ...
}
Sub.prototype = new Super(); // 核心

var sub1 = new Sub(1);
var sub2 = new Sub(2);
alert(sub1.fun === sub2.fun); // true
```

4. 寄生组合继承

```js
function beget(obj) {
  // 生孩子函数 beget：龙beget龙，凤beget凤。
  var F = function () {};
  F.prototype = obj;
  return new F();
}
function Super() {
  // 只在此处声明基本属性和引用属性
  this.val = 1;
  this.arr = [1];
}
//  在此处声明函数
Super.prototype.fun1 = function () {};
Super.prototype.fun2 = function () {};
//Super.prototype.fun3...
function Sub() {
  Super.call(this); // 核心
  // ...
}
var proto = beget(Super.prototype); // 核心
proto.constructor = Sub; // 核心
Sub.prototype = proto; // 核心

var sub = new Sub();
alert(sub.val);
alert(sub.arr);
```
