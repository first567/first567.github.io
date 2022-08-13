---
title: hexo本地图片找不到
date: 2020-1-20 12:31:19
tags: 
    - hexo
---


### 主要解决Hexo图片不加载
<!--more-->

将`_config.yml` 中 `false`改为`true`
```
post_asset_folder: true
/**
    @description 再生成md文件会自动创建 跟文件同名文件夹
 */
hexo new [layout] <title>
```
>hexo 引用图片的几种方式
```
//静态资源：
    {% asset_path slug %}
    {% asset_img slug [title] %}
    {% asset_link slug [title] %}
//图片：
    第一种：
        {% asset_img abc.png 图片信息描述 %}
        <div style="width:70%;margin:auto">{% asset_img abc.png 图片信息描述 %}</div>
    第二种：
    <center>
        <img src="../hexo本地图片找不到/bing.jpg" width="30%" alt="兵长">
    </center>
    第三种：
    yarn add https://github.com/CodeFalling/hexo-asset-image
    就可以用md格式配置图片
    ![]()
    但我试之后第三种生效前两种就不生效了

```

<!-- <img src="hexo本地图片找不到/bing.jpg" alt="img" style="zoom:33%;" /> -->
![a](hexo本地图片找不到/bing.jpg)
