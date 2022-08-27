---
layout:
  - page
title: vue打包优化
subtitle: "优化" # 副标题
date: 2020-05-16 16:16:53
tags:
  - [python]
  - [数据分析]
description: "Stay Hungry.<br>Stay Foolish." # 简介，分两行显示
author: evacat # 博主 站长
language: zh-Hans # 默认语言
---

<br>
<!--more-->

## 一、路由懒加载：分割代码块

Vue 支持异步组件，即可以在使用组件的地方使用一个 Promise，Promise 最终会通过 resolve 回传一个组件对象。而 webpack 的动态 import 的方式可以让代码分块进行打包，并且返回一个 Promise（正是异步组件所需要的）。在路由配置表里使用 import 可以将各个页面组件分割成不同的代码块，然后当路由被访问的时候才加载对应的组件，这样就避免将所有内容打包在一个 chunk 里，从而“按需加载”，大大提高响应速度。
　　使用 () => import('xxx')的形式引入组件：

## 二、压缩请求资源

1. 原理介绍

日常我们在使用网盘的时候，上传一个很大的文件夹肯定很慢，这时候我们会把它压缩成一个压缩包，需要下载的时候下载下来解压就可以了，这样大大节省了上传和下载的时间。同样的原理可以用于网络请求，当我们向服务器请求一个资源时，比如 js 或者 css 文件，服务器将文件压缩，然后返回到浏览器，浏览器操作解压之后即可使用。

首先浏览器在发送请求的时候，会通过请求头 Accept-Encoding 告知服务器，本浏览器支持哪些编码格式的资源。打开浏览器的 network，查看当前网页的某个请求的请求头：

Accept-Encoding 的值表示浏览器支持 gzip 生成的编码格式或者 deflate 压缩算法生成的编码格式，这就告诉服务器，如果可以把该请求的资源用这两个方法压缩一下给我也是可以的。Accept-Encoding 可能还会有 compress 压缩、identity 不压缩的默认格式。

如果服务器对资源进行压缩编码了，它就会通过响应头 Content-Encoding 告知当前请求用了什么编码格式，当然如果服务器没干这事，则不会返回这个响应头，比如某个请求用 gzip 压缩了返回的内容：

2. 服务器配置

一般我们部署到服务器会使用 nginx 来做代理服务器，所有的请求都通过 nginx 转发，这里演示一下 nginx 配置 gzip 压缩文件后再返回。

```javascript
server {

    gzip on;

    gzip_types text/plain application/javascript application/x-javascript text/javascript text/xml text/css;

}
```

3. webpack 打包时直接使用 gzip 压缩

上一步骤中，返回内容是在请求服务器的时候使用 gzip 进行压缩的。这样存在的问题时，对于同一个资源的不同请求，反复压缩，这无疑会增加服务器的 CPU 和内存消耗。使用 webpack 的话，可以直接用 compression-webpack-plugin 插件对我们的代码进行压缩。先安装 compression-webpack-plugin 到 dev 依赖：

```js


// yarn安装

yarn add compression-webpack-plugin -D

// 或npm

npm install compression-webpack-plugin --save-dev
```

简单配置，更多配置可了解官方文档：compression-webpack-plugin:

```js
const CompressionPlugin = require("compression-webpack-plugin");

module.exports = {
  // ...

  configureWebpack: {
    plugins: [
      new CompressionPlugin({
        test: /\.(js|css)?$/i, // 哪些文件要压缩

        filename: "[path].gz[query]", // 压缩后的文件名
        algorithm: "gzip", // 使用gzip压缩
        minRatio: 1, // 压缩率小于1才会压缩
        deleteOriginalAssets: true, // 删除未压缩的文件，谨慎设置，如果希望提供非gzip的资源，可不设置或者设置为false
      }),
    ],
  },
};
```

经过压缩之后 chunk-vendors 仅有 176K，比起原始的 725K，压缩了近 80%。像图片、字体之类的也可以用这个方法进行压缩，只要修改 test 配置项的正则表达式匹配这类文件即可。不过现在，还需要在 nginx 服务器配置一下静态压缩：

```
server {

  gzip on;

  gzip_types text/plain application/javascript application/x-javascript text/javascript text/xml text/css;

  gzip_static on;

}
```
