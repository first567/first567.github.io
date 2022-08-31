---
layout:
  - page
title: apply,call,bind区别及使用

date: 2022-1-14 12:16:53
tags:
  - [js]
  - [前端]
author: evacat # 博主 站长
language: zh-Hans # 默认语言
---

<!--more-->

### 需要改变 this 指向

```js
var name = "lucy";
var obj = {
  name: "martin",
  say: function () {
    console.log(this.name);
  },
};
obj.say(); // martin，this 指向 obj 对象
obj.say.bind(obj); // lucy，this 指向 window 对象
```

### 区别

1. apply 第一个参数，要指向的 this，第二个参数 要传递的参数，以数组的方式传递，改变 this 指向后立即执行，只临时改变 this 指向一次

```js
function fn(...args) {
  console.log(this, args);
}
let obj = {
  myname: "张三",
};

fn.apply(obj, [1, 2]); // this会变成传入的obj，传入的参数必须是一个数组；
fn(1, 2); // this指向window
```

当第一个参数为 null undefined 默认指向 window

```js
fn.apply(null, [1, 2]); // this指向window
fn.apply(undefined, [1, 2]); // this指向window
```

2. call 第一个参数也是 this 指向，后面传递参数列表,改变 this 指向后立即执行，同样只临时改变 this 指向一次

```js
function fn(...args) {
    console.log(this,args);
}
let obj={
    myname='李四'
}

fn.call(obj,1,2)
fn(1,2)
```
