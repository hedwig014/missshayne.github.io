---
title: 'Vue.js:自定义组件'
date: 2019-11-13 21:52:06
tags:
  - Vue.js
  - 前端
---
### 需求

> 在路由模式为hash时，通过后端的数据渲染，就会有判断是否外链

### 问题
1. 能否根据链接来决定渲染标签，而不会产生多余的标签
2. 为什么绑定在组件上的特性有的会应用到组件根元素上

<!-- more -->

### 涉及vue知识点
* [is特性](https://cn.vuejs.org/v2/api/index.html#is)
* [指令v-bind使用](https://cn.vuejs.org/v2/api/index.html#v-bind)
* [props使用](https://cn.vuejs.org/v2/guide/components-props.html)

### 解决
通过component + is的骚操作可以完美解决产生多余标签的问题，至于第二个问题，那就是[非props特性](https://cn.vuejs.org/v2/guide/components-props.html#%E9%9D%9E-Prop-%E7%9A%84%E7%89%B9%E6%80%A7)就能解疑啦

##### 总结
没事多瞅瞅文档，总会有不同的收获。   

### 代码
```vue
<template>
  <component v-bind="linkProps(to)">
    <slot />
  </component>
</template>

<script>
import { isExternal } from '~/utils'
export default {
  name: 'CLink',
  props: {
    to: {
      type: String,
      required: true
    }
  },
  methods: {
    linkProps(url) {
      if (isExternal(url)) {
        return {
          is: 'a',
          href: url
        }
      }
      return {
        is: 'nuxt-link',
        to: url
      }
    }
  }
}
</script>
```
使用就像平常使用a标签一样，只不过href要换成to