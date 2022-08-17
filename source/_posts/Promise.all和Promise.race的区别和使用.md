---
layout:
  - page
title:  Promise.all和Promise.race的区别和使用
date: 2021-10-19 16:16:53
tags: 
   - [vue]
   - [js]
---
<br>
<!--more-->

1. Promise.all

Promise.all可以将多个实例组装成一个新的实例，成功的时候返回一个成功数组，失败的时候则返回最先被reject失败状态的值

当一个页面需要在很多个模块的数据都返回过来才正常显示，否则loading

```js
let wake =(time)=>{
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(`${item/1000}秒`)
        }, time);
    })
}

let p1=wake(3000)
let p2=wake(2000)
Promise.all(p1,p2).then((result)=>{
    console.log(result);
}).catch((error)=>{
    console.log(error)
})

```
比如当数组里的P1，P2都执行完成时，页面才显示。
返回的数组结果顺序不会改变，即使P2的返回要比P1的返回快，顺序依然是P1，P2


2. Promise.race

race是赛跑的意思，Promise.race[p1,p2,p3]里面的结果哪个获取的快，就返回哪个结果，不管结果本身是成功还是失败

![](https://upload-images.jianshu.io/upload_images/14796064-e349fddd89796ad5.png?imageMogr2%2Fauto-orient%2Fstrip%7CimageView2%2F2%2Fw%2F619%2Fformat%2Fwebp)

一般用于和定时器绑定，比如将一个请求和一个三秒的定时器包装成Promise实例，加入到race队列中，请求三秒中还没有回应时，给用户一些提示或一些相应的操作。

