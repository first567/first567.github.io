---
layout:
  - page
title: css使图片自适应

date: 2021-09-14 16:16:53
tags:
  - [css]
  - [前端]
author: evacat # 博主 站长
language: zh-Hans # 默认语言
---

<!--more-->

1. background
   我们把图片作为背景，然后用 background-size 属性进行调节

```css
.img-container {
  width: 100px;
  height: 100px;
  background: black url("1.png") no-repeat center center;
  background-size: contain;
}
```

2. object-fit 属性

设置好图片的宽高，然后设置 object-fit 属性为 contain 就是常见的图片自适应效果

```css
img {
  width: 100px;
  height: 100px;
  object-fit: contain;
}
```

| 值         | 描述                                                                                                                 |
| ---------- | -------------------------------------------------------------------------------------------------------------------- |
| fill       | 默认，不保证保持原有的比例，内容拉伸填充整个内容容器。 尝试一下                                                      |
| contain    | 保持原有尺寸比例。内容被缩放。 尝试一下                                                                              |
| cover      | 保持原有尺寸比例。但部分内容可能被剪切。 尝试一下                                                                    |
| none       | 保留原有元素内容的长度和宽度，也就是说内容不会被重置。 尝试一下                                                      |
| scale-down | 保持原有尺寸比例。内容的尺寸与 none 或 contain 中的一个相同，取决于它们两个之间谁得到的对象尺寸会更小一些。 尝试一下 |
| initial    | 设置为默认值，关于 initial                                                                                           |
| inherit    | 从该元素的父元素继承属性。 关于 inherit                                                                              |
