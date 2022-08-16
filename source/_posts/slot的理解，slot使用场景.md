---
title: slot的理解，slot使用场景
date: 2021-06-19 06:15:03
tags:
    - [前端]
---

<br>
<!--more-->

html 中 slot元素，是web组件内的一个占位符，该占位符可以在后期使用自己的标记语言填充


```html
<template id="element-details-template">
  <slot name="element-name">Slot template</slot>
</template>
<element-details>
  <span slot="element-name">1</span>
</element-details>
<element-details>
  <span slot="element-name">2</span>
</element-details>
```

template 不会展示到页面中，需要用先获取他的引用，然后添加到dom中
```js
customElements.define('element-details',
  class extends HTMLElement {
    constructor() {
      super();
      const template = document
        .getElementById('element-details-template')
        .content;
      const shadowRoot = this.attachShadow({mode: 'open'})
        .appendChild(template.cloneNode(true));
  }
})

```
## 默认插槽
子组件用<slot>标签来确定渲染的位置，标签里面可以放DOM结构，当父组件使用的时候没有往插槽传入内容，标签内DOM结构就会显示在页面

父组件在使用的时候，直接在子组件的标签内写入内容即可

子组件Child.vue
```html
<template>
    <slot>
      <p>插槽后备的内容</p>
    </slot>
</template>
父组件

<Child>
  <div>默认插槽</div>  
</Child>
```
## 具名插槽
子组件用name属性来表示插槽的名字，不传为默认插槽

父组件中在使用时在默认插槽的基础上加上slot属性，值为子组件插槽name属性值

子组件Child.vue
```
<template>
    <slot>插槽后备的内容</slot>
  <slot name="content">插槽后备的内容</slot>
</template>
父组件

<child>
    <template v-slot:default>具名插槽</template>
    <!-- 具名插槽⽤插槽名做参数 -->
    <template v-slot:content>内容...</template>
</child>
```
## 作用域插槽
子组件在作用域上绑定属性来将子组件的信息传给父组件使用，这些属性会被挂在父组件v-slot接受的对象上

父组件中在使用时通过v-slot:（简写：#）获取子组件的信息，在内容中使用

子组件Child.vue
```html
<template> 
  <slot name="footer" testProps="子组件的值">
          <h3>没传footer插槽</h3>
    </slot>
</template>
```
父组件
```html
<child> 
    <!-- 把v-slot的值指定为作⽤域上下⽂对象 -->
    <template v-slot:default="slotProps">
      来⾃⼦组件数据：{{slotProps.testProps}}
    </template>
    <template #default="slotProps">
      来⾃⼦组件数据：{{slotProps.testProps}}
    </template>
</child>
```
## 小结：
v-slot属性只能在<template>上使用，但在只有默认插槽时可以在组件标签上使用
默认插槽名为default，可以省略default直接写v-slot
缩写为#时不能不写参数，写成#default
可以通过解构获取v-slot={user}，还可以重命名v-slot="{user: newName}"和定义默认值v-slot="{user = '默认值'}