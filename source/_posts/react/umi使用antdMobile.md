---
layout:
  - page
title: umi使用antdMobile
subtitle: "优化" # 副标题
date: 2021-08-16 16:16:53
tags:
  - [react]
  - [umi]
  - [antd-mobile]
  - [前端]
author: evacat # 博主 站长
language: zh-Hans # 默认语言
---

使用 antd-mobile 报错 找不到依赖
These dependencies were not found:
antd-mobile/es/button in ./src/pages/home-my/index.tsx
antd-mobile/es/button/style in ./src/pages/home-my/index.tsx

根目录 .umirc.ts 下配置

```ts
export default defineConfig({
  antd: {
    mobile: false,
  },
});
```
