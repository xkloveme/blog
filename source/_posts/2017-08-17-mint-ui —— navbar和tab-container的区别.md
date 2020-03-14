---
title: mint-ui —— navbar和tab-container的区别
tags:
  - 技术
  - vue
date: 2017-08-17 08:15:00
---

# **navbar 的具体实现**

![](http://www.jixiaokang.com/wp-content/uploads/2018/05/ContractedBlock-2.gif)![](http://www.jixiaokang.com/wp-content/uploads/2018/05/ExpandedBlockStart-2.gif)

1 <template>  
 2 <div class="page-navbar">  
 3 <div class="page-title">Navbardiv>  
 4  
 5 <mt-navbar class="page-part" v-model="selected">  
 6 <mt-tab-item id="1">选项一 mt-tab-item>  
 7 <mt-tab-item id="2">选项二 mt-tab-item>  
 8 <mt-tab-item id="3">选项三 mt-tab-item>  
 9 mt-navbar>  
10  
11 <div>  
12 <mt-cell class="page-part" title="当前选中">{ { selected }}mt-cell>  
13 div>  
14  
15  
16 <mt-tab-container v-model="selected">  
17 <mt-tab-container-item id="1">  
18 <mt-cell v-for="n in 10" :title="'内容 ' \+ n" />  
19 mt-tab-container-item>  
20 <mt-tab-container-item id="2">  
21 <mt-cell v-for="n in 4" :title="'测试 ' \+ n" />  
22 mt-tab-container-item>  
23 <mt-tab-container-item id="3">  
24 <mt-cell v-for="n in 6" :title="'选项 ' \+ n" />  
25 mt-tab-container-item>  
26 mt-tab-container>  
27 div>  
28 template>  
29  
30 <script>  
31 export default { 32 name: 'page-navbar', 33  
34 data() { 35 return { 36 selected: '1'  
37 }; 38 } 39 }; 40 script>

navbar.vue

### **Import**

按需引入：

import { Navbar, TabItem } from 'mint-ui';

Vue.component(Navbar.name, Navbar);

Vue.component(TabItem.name, TabItem);

全局导入：全局导入后不用再导入

importMintfrom'mint-ui'

import'mint-ui/lib/style.css'

Vue.use(Mint);

### **API**

## API

### navbar

参数

说明

类型

可选值

默认值

fixed

固定在页面顶部

Boolean

false

value

返回当前选中的 tab-item 的 id

\*

### tab-item

参数

说明

类型

可选值

默认值

id

选中后的返回值

\*

## Slot

### navbar

name

描述

-

内容

### tab-item

name

描述

-

显示文字

icon

icon 图标

**show：**

![](http://img.blog.csdn.net/20170729231112350?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbWljaGFlbF9vdXlhbmc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

点击选项二

![](http://img.blog.csdn.net/20170729231121127?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbWljaGFlbF9vdXlhbmc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

# **navbar 是选项卡之间的切换，可以更改切换后选项卡的样式，因为每一个激活后都会有一个 mint-tab-item is-selected 的一个类，显示被激活，而\*\***tab-container 是按钮之间的切换，可以有左右滑动的特效，具体实现如下：\*\*

# tab-container 的具体实现

面板，可切换显示子页面。

常与 navbar、tabbar 结合使用

![](http://www.jixiaokang.com/wp-content/uploads/2018/05/ContractedBlock-2.gif)![](http://www.jixiaokang.com/wp-content/uploads/2018/05/ExpandedBlockStart-2.gif)

1 <template>  
 2 <div>  
 3 <div class="nav">  
 4 <mt-button size="small" @click.native.prevent="active = 'tab-container1'">tab 1mt-button>  
 5 <mt-button size="small" @click.native.prevent="active = 'tab-container2'">tab 2mt-button>  
 6 <mt-button size="small" @click.native.prevent="active = 'tab-container3'">tab 3mt-button>  
 7 div>  
 8  
 9 <div class="page-tab-container">  
10 <mt-tab-container class="page-tabbar-tab-container" v-model="active" swipeable>  
11 <mt-tab-container-item id="tab-container1">  
12  
13 <mt-cell v-for="n in 10" title="tab-container 1">mt-cell>  
14 mt-tab-container-item>  
15 <mt-tab-container-item id="tab-container2">  
16  
17 <mt-cell v-for="n in 5" title="tab-container 2">mt-cell>  
18 mt-tab-container-item>  
19 <mt-tab-container-item id="tab-container3">  
20  
21 <mt-cell v-for="n in 7" title="tab-container 3">mt-cell>  
22 mt-tab-container-item>  
23 mt-tab-container>  
24 div>  
25 div>  
26 template>  
27  
28 <script>  
29 export default { 30 name: 'page-tab-container', 31 data() { 32 return { 33 active: 'tab-container1'  
34 }; 35 } 36 }; 37 script>  
38  
39 <style lang="css" scoped>  
40 .item {  
41 display: inline-block;  
42 }  
43  
44 .nav {  
45 padding: 10px;  
46 }  
47  
48 .link {  
49 color: inherit;  
50 padding: 20px;  
51 display: block;  
52 }  
53 style>

tab-container.vue

### **Import**

按需引入：

import { TabContainer, TabContainerItem } from 'mint-ui';

Vue.component(TabContainer.name, TabContainer);

Vue.component(TabContainerItem.name, TabContainerItem);

全局导入：全局导入后不用再导入

importMintfrom'mint-ui'

import'mint-ui/lib/style.css'

Vue.use(Mint);

### **API**

## API

### tab-container

参数

说明

类型

可选值

默认值

value

当前激活的 id

\*

swipeable

显示滑动效果

Boolean

false

### tab-container-item

参数

说明

类型

可选值

默认值

id

item 的 id

\*

## Slot

### tab-container

name

描述

-

内容

### tab-container-item

name

描述

-

内容

show**：**

![](http://img.blog.csdn.net/20170803105647087?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbWljaGFlbF9vdXlhbmc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)
