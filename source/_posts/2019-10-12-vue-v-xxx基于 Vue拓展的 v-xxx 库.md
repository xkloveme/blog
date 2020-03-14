---
layout: post
title: 基于 Vue拓展的 v-xxx 库
date: 2019-10-12
tags: [vue, GitHub, 指令]
categories: 前端
---

> **君问归期未有期，巴山夜雨涨秋池。** > **何当共剪西窗烛，却话巴山夜雨时。**

作为`vue`轻车熟路的老司机，经常会用到一些指令，`vue`官方提供的指令又太少，无法满足旺盛的欲望，而每次要写一遍，终日郁郁寡欢，从小就教育我们乐于助人，为了将奉献精神贯彻始终，用了这个库，空下来大把时间陪陪家人朋友岂不乐哉。

闲话少叙，直逼主题，毕竟我们是正经的官方软文。

- **[查看官网](https://www.jixiaokang.com/vue-v-xxx/)**
- **[查看源码](https://github.com/xkloveme/vue-v-xxx/)**

## 什么是 vue 指令?

---

- 在我们了解库之前,我们先回顾一下`Vue`指令

### 1. 我们经常用的有一下几种指令

```js
v-text 、 v-html 、 v-show 、 v-if 、 v-else 、v-for 、 v-bind 、 v-on 、
v-model 、 v-once
```

> 具体用法[前去官网](https://cn.vuejs.org/v2/guide/conditional.html),不再赘述

### 什么是自定义指令?

> 有的情况下，你仍然需要对普通 DOM 元素进行底层操作，这时候就会用到自定义指令.

```js
<input  v-focus>// 为例

// 在组件内部
directives: {
  focus: {
  // 指令的定义
  inserted: function (el) {
    el.focus()
    }
  }
}
```

### 钩子函数

一个指令定义对象可以提供如下几个钩子函数 (均为可选)：

- `bind`：只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置。

- `inserted`：被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)。

- `update`：所在组件的 VNode 更新时调用，**但是可能发生在其子 VNode 更新之前**。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新。

- `componentUpdated`：指令所在组件的 VNode **及其子 VNode** 全部更新后调用。

- `unbind`：只调用一次，指令与元素解绑时调用。

### 钩子函数的参数

- `el`：指令所绑定的元素，可以用来直接操作 DOM 。
- `binding`：一个对象，包含以下属性：
  - `name`：指令名，不包括 `v-` 前缀。
  - `value`：指令的绑定值，例如：`v-my-directive="1 + 1"` 中，绑定值为 `2`。
  - `oldValue`：指令绑定的前一个值，仅在 `update` 和 `componentUpdated` 钩子中可用。无论值是否改变都可用。
  - `expression`：字符串形式的指令表达式。例如 `v-my-directive="1 + 1"` 中，表达式为 `"1 + 1"`。
  - `arg`：传给指令的参数，可选。例如 `v-my-directive:foo` 中，参数为 `"foo"`。
  - `modifiers`：一个包含修饰符的对象。例如：`v-my-directive.foo.bar` 中，修饰符对象为 `{ foo: true, bar: true }`。
- `vnode`：Vue 编译生成的虚拟节点。
- `oldVnode`：上一个虚拟节点，仅在 `update` 和 `componentUpdated` 钩子中可用。

## 怎么安装 vue-v-xxx?

---

> 基于 vue 指令,又新增丰富一些常用的指令,看看是怎么使用的吧

### 安装

- 您可以通过 npm 安装,推荐使用 `npm` 的方式安装，它能更好地和 `webpack` 打包工具配合使用。

```bash

# install vue-v-xxx

 npm install vue-v-xxx --save

# or

 yarn add vue-v-xxx --save

```

- 您也可以通过 unpkg.com/vue-v-xxx 获取到最新版本的资源，在页面上引入 js 和 css 文件即可开始使用。

```html
<!-- 引入样式 -->

<link rel="stylesheet" href="https://unpkg.com/vue-v-xxx/lib/vue-v-xxx.css" />

<!-- 引入组件库 -->

<script src="https://unpkg.com/vue-v-xxx"></script>
```

### 使用

- 您可以在`main.js`里面全局注册,在组件内就可以应用了[推荐工程](https://github.com/xkloveme/vue-v-xxx-project)

```js
import Vue from "vue";

import App from "./App";

import Vxxx from "vue-v-xxx";

import "vue-v-xxx/lib/vue-v-xxx.css";

Vue.config.productionTip = false;

Vue.use(Vxxx);

/* eslint-disable no-new */

new Vue({
  el: "#app",

  components: { App },

  template: "<App/>"
});
```

- 您可以通过 CDN 可以快速使用 vue-v-xxx 写出一个示例，您可以复制下面代码或[在线预览](https://codesandbox.io/s/vue-v-xxx-bndj4)

```html
<!DOCTYPE html>

<html>
  <head>
    <meta charset="utf-8" />

    <title>vue-v-xxx</title>

    <link
      rel="stylesheet"
      href="https://unpkg.com/vue-v-xxx/lib/vue-v-xxx.css"
    />
  </head>

  <body>
    <div id="app">
      <h1 title="Welcome">欢迎使用 {{ value }}</h1>

      <button v-copy="value">Click me!</button>
    </div>
  </body>

  <!-- import Vue before vue-v-xxx -->

  <script src="https://unpkg.com/vue/dist/vue.js"></script>

  <!-- import JavaScript -->

  <script src="https://unpkg.com/vue-v-xxx/lib/vue-v-xxx.umd.js"></script>

  <script>
    new Vue({
      el: "#app",

      data: {
        value: "vue-v-xxx"
      }
    });
  </script>
</html>
```

## 我们提供了那些额外的指令?

---

### v-call 拨打指令

> 该指令快速唤起拨打电话或者发送短信

- [在线预览](https://www.jixiaokang.com/vue-v-xxx/configurations/v-call.html)

- 使用案例

```
<template lang="pug">
.v-xxx
  div(v-call="tel") 点击拨打☎️
  div(v-call:sms="10086") 点击发短信💬
</template>
<script>
  export default {
    name: 'v-call',
    data() {
      return {
        tel: '10086'
      }
    }
  }
</script>
```

### v-copy 复制指令

> 在很多情况下，我们需要复制操作

- [在线预览](https://www.jixiaokang.com/vue-v-xxx/configurations/v-copy.html)

- 使用案例

```
<template lang="pug">
.v-xxx
  Button(@click="handleClick" v-copy="value") 点击复制
  div
    textarea(placeholder="Paste here" style="margin-top:40px;width:100%;height:100%;")
</template>
<script>
  export default {
    name: 'v-copy',
    data() {
      return {
        value: ''
      }
    },
    methods: {
      handleClick(html = '你复制了我,去粘贴吧') {
        this.value = html
      }
    }
  }
</script>
```

### v-debounce 防抖指令

> `v-debounce` 支持传入防抖时间`v-debounce:500` 默认 500ms

- [在线预览](https://www.jixiaokang.com/vue-v-xxx/configurations/v-debounce.html)

```
<template lang="pug">
.v-xxx
  h1 未加防抖
  h2 点击次数:{{num}}
  Button(@click="addNum") (点我)
  h1 加入防抖
  h2 点击次数:{{num2}}
  Button(v-debounce="addNum2") (点我)
</template>
<script>
export default {
  name: 'v-debounce',
  data () {
    return {
      num: 0,
      num2: 0,
    }
  },
  methods: {
    addNum () {
      this.num++
    },
    addNum2 () {
      this.num2++
    }
  }
}
</script>
```

### v-throttle 节流指令

> `v-throttle` 支持传入防抖时间`v-throttle:2000` 默认 2s

- [在线预览](https://www.jixiaokang.com/vue-v-xxx/configurations/v-throttle.html)

```
<template lang="pug">
.v-xxx
  h3 立即触发:{{num}}
  input(v-model="num")
  h3 节流后:{{num2}}
  input(v-throttle:2000="num2")
</template>
<script>
  export default {
    name: 'v-throttle',
    data() {
      return {
        num: '立即改变',
        num2: '节流值'
      }
    }
  }
</script>
```

### v-ellipsis 省略指令

> `v-ellipsis` 在表格中经常使用,`v-ellipsis`默认单行省略

- [在线预览](https://www.jixiaokang.com/vue-v-xxx/configurations/v-ellipsis.html)

```
<template lang="pug">
.v-xxx
  div(v-ellipsis) {{des}}
  div(v-ellipsis:3)
    p {{des2}}
</template>
<script>
export default {
  name: 'v-ellipsis',
  data() {
    return {
      des:
        '单行省略单行省略单行省略单行省略单行省略单行省略单行省略单行省略单行省略单行省略单行省略单行省略单行省略单行省略单行省略单行省略',
      des2:
        '多行省略多行省略多行省略多行省略多行省略多行省略多行省略多行省略多行省略多行省略多行省略多行省略多行省略多行省略多行省略多行省略多行省略多行省略多行省略多行省略多行省略多行省略'
    }
  }
}
</script>
```

### v-pin 固定指令

> `v-pin` 支持传入定位位置和定位值`v-pin:left || top` 默认 left

- [在线预览](https://www.jixiaokang.com/vue-v-xxx/configurations/v-pin.html)

```
<template lang="pug">
.v-xxx
  div(v-pin="200") 顶部200px
  div(v-pin:left="300") 左边300px
</template>
<script>
  export default {
    name: 'v-pin'
  }
</script>
```

### v-focus 聚焦指令

> `v-focus` 在移动端登录时异常好用

- [在线预览](https://www.jixiaokang.com/vue-v-xxx/configurations/v-focus.html)

```
<template lang="pug">
.v-xxx
  input(v-focus)
</template>
<script>
export default {
  name: 'v-focus'
}
</script>
```

### v-click-out 外部点击指令

> `v-click-out` 点击外部 dom 触发

- [在线预览](https://www.jixiaokang.com/vue-v-xxx/configurations/v-click-out.html)

```
<template lang="pug">
.v-xxx
  div(style="border:1px solid red;width:200px;height:200px;" @click="handleClick" v-click-out="handleClickOut") {{name}}
</template>
<script>
  export default {
    name: 'v-click-out',
    data() {
      return {
        name: '内部'
      }
    },
    methods: {
      handleClick() {
        this.name = '您点击了内部'
      },
      handleClickOut() {
        this.name = '您点击了外部'
      }
    }
  }
</script>

```

## 结束语

> **如果您有好的指令欢迎 👏 来提 issue,尽可能多的覆盖,一旦选用将获取神秘礼品,期待您的加入**

## 神交

觉得不错的话给个`star`

- [GitHub](https://github.com/xkloveme/vue-v-xxx/)
- [blog](https://www.cnblogs.com/xkloveme/)
