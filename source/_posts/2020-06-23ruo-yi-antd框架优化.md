---
layout: ruo-yi-antd框架优化
title: 框架优化
date: 2020-06-23 16:59:32
tags: ["前端"]
---

<h1 align="center">Ant 若依前端框架</h1>

文档：http://doc.rycloud.zmrit.com

- 预览: http://ruoyi.ant.zmrit.com
- v3 测试版: http://v3.ant.zmrit.com

## 下载和运行

- 安装依赖

```
yarn install
```

- 开发模式运行

```
yarn run serve
```

- 编译项目

```
yarn run build
```

- Lints and fixes files

```
yarn run lint
```

## 优化

### 1. 「接口请求」自动封装挂载到`vue`实例上

- 调用方式

```bash
// 获取用户列表
 this.$api.getUserList().then(res => {
        console.log('🐛:: handleClickUser -> res', res)
      })
```

- 接口书写命名格式

1. 为避免命名冲突导致请求错误,采用一下命名

```bash
/*
 * Api命名建议:
  * 组成: {请求方法}{文件名}{接口用处}{Api}
  * 1.请求方法(get查询, post增加, put修改, delete删除, upload上传)
  * 2.当前js所在文件名称如gen, login
  * 3.接口用处, 如userList, deviceDetail
  * 4.Api, 表明是Api接口, 区别于其他方法
  * 目的: 语义化明确, 看到接口就知道类型用处
  * 示例: getManageUserListApi(获取用户列表api), putLoginMsCaptchaApi(获取验证码api)
 */
```

2. 接口命名一律采用小驼峰命名法

3. 新书写接口推荐一下写法,极度精简,可读性高

```bash
// get 请求 用户列表
export const getManageGetUserApi = params => axios.get(api.user, { params })
// OR
export const getManageGetUserApi = params => axios.get('/system/user/list', { params })

// post 请求
export const postManageServiceApi = data => axios.get('/service', data)

// 切换请求方法
export const postManageServiceApi = data => axios[data.id === 0 ? 'post' : 'put']('/service', data)
```

4. 每个 api 前面需要添加中文注释

### 2. 「权限」判断按钮级权限

- 自定义指令写法

```js
// 指令写法
<div v-auth="'system:dict:add'"></div>
// v-if写法
<div v-if="$pm('system:dict:add')"></div>
```

- 在`js`中使用

```js
// 挂载到`VM`实例上
this.$pm === checkPermission;
```

### 3. 「工具」常用工具封装

- 时间格式化封装

```js

// 过滤器封装 YYYY-MM-DD
<div>{{time | date}}</div>

// 过滤器封装 YYYY-MM-DD HH:mm:ss
<div>{{time | datetime}}</div>

// 挂载到vue实例上
this.$formatDate(new Date())
// OR
this.$formatDate(new Date(),'YYYY-MM-DD')

```

### 4. 「table」 封装,采用 jsx 书写方式

- 支持两种书写方式(直接传输数据和表头)

```js
// columns 列  tableData 表数据   params 默认请求数据
    <wt-table :columns="columns" :tableData="tableData" :params="params" ></wt-table>
```

- 支持传输接口和 api

```js
// columns 列  tableData 表数据   params 默认请求数据
    <wt-table :columns="columns" :api="$api.postManageServiceApi" :params="params" ></wt-table>
```

- 表格数据提供三种写法

1. 引入外部`js`,`table`表头数据,需要把`this`作为参数传进去

> 需要创建 `h` 函数,不然会报错,需要把`js`文件建立在同级目录便于管理

```js
// 外部数据
export default (props) => [
  {
    title: "序号",
    dataIndex: "index",
    customRender: (text, row, index) => {
      const h = props.$createElement; // 需要创建h函数
      return h("a", index + 1);
    },
  },
];

// 组件内部,需要把this传进去
import columns from "./table.js";
columns: columns(this);
```

> 表格渲染支持两种写法

```js
 {
    title: '创建时间',
    dataIndex: 'createTime',
    customRender: (text, row, index) => {
      return {
        children: props.$formatDate(text)
      }
    }
  },
  {
    title: '邮箱',
    dataIndex: 'email',
    customRender: (text, row, index) => {
      const h = props.$createElement
      return h('a', text)
    }
  }
```

2. 直接写在组件内部,但可能会造成单文件过长,不利于阅读

> 这种写法支持 `jsx` 形式,可以少些大部分代码「表格数据不多的时候推荐」

```js
columns: [
  {
    title: "创建时间",
    dataIndex: "createTime",
    customRender: (text, row, index) => {
      return {
        children: this.$formatDate(text),
      };
    },
  },
  {
    title: "邮箱",
    dataIndex: "email",
    customRender: (text, row, index) => {
      return <a>{text}</a>;
    },
  },
];
```

3. `mixins` 方式混入,同样可读性好,但此语法未来可能会废弃[不推荐]

### 5. 引入可配置`from`

- 基于配置表单,封装`wt-from`
- 地址[http://form-create.com/v2/ant-design-vue/](http://form-create.com/v2/ant-design-vue/)

#### 1.使用表单组件

```html
<wt-form :rule="rule" @submit="submit"></wt-form>
```

- 可配置项分为两种,直接用挂载在`VM`上的`$maker`和`JSON`配置,具体如下

```js
// 由$maker配置生成
rule: [
  this.$maker.input("goods_name", "goods_name"),
  this.$maker.date("create_at", "created_at"),
];
// json 配置生成
rule1: [
  {
    type: "input",
    title: "商品名称",
    field: "goods_name",
    value: "",
    props: {
      type: "text",
    },
  },
  {
    type: "select",
    field: "cate_id",
    title: "产品分类",
    value: ["104", "105"],
    options: [
      { value: "104", label: "生态蔬菜", disabled: false },
      { value: "105", label: "新鲜水果", disabled: false },
    ],
    props: {
      multiple: true,
    },
  },
];
```

> 更多内置配置参考[配置项](http://form-create.com/v2/ant-design-vue/components/hidden.html)

- 基于第三方组件的使用,通过`type:'codemirror'`,来使用

### 6. 封装`search`组件

> 对于表格常用的搜索进行封装,更少的代码,更多的灵活性

```html
<wt-search :rule="rule1" @submit="submit" :isSearch="true"></wt-search>
```

**配置同`wt-form`,`submit`为搜索结果回调**
