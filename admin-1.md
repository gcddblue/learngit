> 项目地址 [vue-admin-webapp](https://github.com/gcddblue/vue-admin-webapp) 欢迎star，fork

## 前言

相信许多人和我一样刚接触 vue 时看文档都很枯燥，看完 vue，还有 vueRouter 、vuex 、vue-cli (学不动了。。。 )  对于看完教程之后又迟迟不能上手实际项目，只能写一些简单的小demo,这肯定和实际生产工作是有出入的，于是乎我就打算自己从零开始使用最新的技术栈搭建一个vue后台管理系统，依此加深对理论知识的学习，并增强自己的项目能力，所以希望本系列教程对你开发vue项目有所帮助。

## 1.项目基本简介

[vue-admin-webapp](https://gcddblue.github.io/vue-admin-webapp) 是一个后台管理 spa 页面，它基于 [vue](https://github.com/vuejs/vue) 和 [element-ui](https://github.com/ElemeFE/element) 采用了最新的前端技术栈，实现了登录权限验证，动态路由生成，并使用 [easy-mock](https://github.com/easy-mock/easy-mock) 来模拟请求数据，实现了典型的业务模型案例，它可以帮你快速搭建后台管理系统模板，并根据实际的业务需求添加路由来实现企业级管理页面，相信本项目一定能帮助到你。



\- [在线预览-github](https://gcddblue.github.io/vue-admin-webapp)

\- [在线预览-gitee](https://gcddblue.gitee.io/vue-admin-webapp) （推荐国内用户）



**目前版本基于  `webpack 4.0+` 和 `vue-cli 3.x ` 版本构建，需要 [Node.js](https://nodejs.org/) 8.9或更高版本（推荐8.11.0+），相关知识可以自行进官网进行了解**

#### 功能

```

- 登录 / 注销
  - 登录仿GeeTest-极验安全策略
  
- 页面
  - 初次进入引导用户
  - sideBar收缩和展开
  - 全屏控制
  
- 侧边栏
  - 根据不同用户权限展示相应的动态左侧菜单
  
- 权限验证
  - 管理员页面
  - 权限设置
  
- 表格操作
  - 涉及平常业务遇到的相关表格操作（参考）
  
- Excel
 - Excel导出
 - Excel导入
 - 多级表头导出
 
- Echarts
 - 滑动显示更多数据
 - 动态切换charts
 - map地图使用
 
- Icons
 - element-icon
 - 阿里iconfont
 
```

#### 准备工作

在开始之前，请确保在本地安装 node 和 webpack 及 git。 本项目涉及的技术栈主要有 [ES6](http://es6.ruanyifeng.com/) 、[vue](https://cn.vuejs.org/) 、[vuex](https://vuex.vuejs.org/zh/) 、[vue-router](https://router.vuejs.org/zh/) 、[vue-cli](https://cli.vuejs.org/zh/guide/) 、[axios](http://www.axios-js.com/) 、[webpack](https://www.webpackjs.com/) 、[element-ui](https://element.eleme.io/#/zh-CN) 、[easyMock](https://www.easy-mock.com/) ,所以你最好提前熟悉了解这些知识，这将对你认识学习该项目有很大帮助

#### 目录结构

下面是整个项目的目录结构

```

├── public                     # 静态资源
│   ├── favicon.ico            # favicon图标
│   └── index.html             # html模板
├── src                        # 源代码
│   ├── api                    # 所有请求
│   ├── assets                 # 图片、字体等静态资源
│   ├── components             # 全局公用组件
│   ├── layout                 # 页面整体布局盒子
│   ├── mixins                 # 全局混入模块
│   ├── plugins                # 全局插件部分
│   ├── router                 # 路由
│   ├── store                  # 全局store管理
│   ├── style                  # 全局样式
│   ├── utils                  # 全局公用方法
│   ├── vendor                 # 公用vendor（excel导入导出）
│   ├── views                  # views所有页面
│   ├── App.vue                # 入口页面
│   ├── main.js                # 入口文件 加载组件 初始化等
├── .borwserslistrc            # 浏览器兼容相关
├── .env.xxx                   # 环境变量配置　
├── .eslintrc.js               # eslint 配置项
├── .gitignore.js              # git忽略文件设置
├── .babelrc.config.js         # babel-loader 配置
├── package.json               # package.json
├── postcss.config.js          # postcss 配置
└── vue.config.js              # vue-cli 配置

```

#### 安装

```
# 克隆项目
git clone git@github.com:gcddblue/vue-admin-webapp.git

# 进入项目目录
cd vue-admin-webapp

# 安装依赖
npm install

# 启动服务
npm run serve
```

启动完成后将打开浏览器访问 `http://localhost:8080`,登陆成功后，将看到如下页面

![](/Users/gaochenhui/Desktop/QQ20190825-223245.png)

接下来你就可以根据自己的实际需求，可以添加或修改路由，编写自己的业务代码。

## 2.axios封装

在vue项目中，和后台进行请求交互这块，我们通常都会选择axios库，它是基于promise的http库，可运行在浏览器端和node.js中。在本项目中主要实现了请求和相应拦截，get，post请求封装。

#### 配置不同环境

![](/Users/gaochenhui/Desktop/QQ20190826-220155@2x.png)

通过在项目中创建不同环境的文件，我这里只创建了开发和生产环境的，当然，你也可以创建基于测试的`.env.test` 等文件

```
ENV = 'production'
# base api
VUE_APP_BASE_API = 'https://www.easy-mock.com/mock/5cee951f11690b5261b75566/admin'
```

只有以 `VUE_APP_` 开头的变量会被 `webpack.DefinePlugin` 静态嵌入到客户端侧的包中。你可以在应用的代码中这样访问它们，例如我在@/api/index.js中初始化axios：

```
const $axios = axios.create({
  timeout: 30000,
  // 基础url，会在请求url中自动添加前置链接
  baseURL: process.env.VUE_APP_BASE_API
})
```

这里我在项目中创建api文件夹，将所有接口都集中在这个文件夹中，根据不同的业务创建不同js文件，来更好划分接口的功能，其中index.js中代码如下：

```
import axios from 'axios'
import Qs from 'qs' // 处理post请求数据格式
import store from '@/store'
import router from '@/router'
import Vue from 'vue'
import { Loading, Message } from 'element-ui' // 引用element-ui的加载和消息提示组件

const $axios = axios.create({
  // 设置超时时间
  timeout: 30000,
  // 基础url，会在请求url中自动添加前置链接
  baseURL: process.env.VUE_APP_BASE_API
})
Vue.prototype.$http = axios // 这里并发请求以便在组件使用this.$http.all()，具体看dashborad页面

// 在全局请求和响应拦截器中添加请求状态
let loading = null

/**
 * 请求拦截器
 * 用于处理请求前添加loading、判断是否已保存token，并在每次请求头部添加token
 */
$axios.interceptors.request.use(
  config => {
    loading = Loading.service({ text: '拼命加载中' })
    const token = store.getters.token
    if (token) {
      config.headers.Authorization = token // 请求头部添加token
    }
    return config
  },
  error => {
    return Promise.reject(error)
  }
)
/**
 * 响应拦截器
 * 用于处理loading状态关闭、请求成功回调、响应错误处理
 */
$axios.interceptors.response.use(
  response => {
    if (loading) {
      loading.close()
    }
    const code = response.status
    // 请求成功返回response.data
    if ((code >= 200 && code < 300) || code === 304) {
      return Promise.resolve(response.data)
    } else {
      return Promise.reject(response)
    }
  },
  error => {
    if (loading) {
      loading.close()
    }
    console.log(error)
    if (error.response) {
      switch (error.response.status) {
        case 401:
          // 返回401 清除token信息并跳转到登陆页面
          store.commit('DEL_TOKEN')
          router.replace({
            path: '/login',
            query: {
              redirect: router.currentRoute.fullPath
            }
          })
          break
        case 404:
          Message.error('网络请求不存在')
          break
        default:
          Message.error(error.response.data.message)
      }
    } else {
      // 请求超时或者网络有问题
      if (error.message.includes('timeout')) {
        Message.error('请求超时！请检查网络是否正常')
      } else {
        Message.error('请求失败，请检查网络是否已连接')
      }
    }
    return Promise.reject(error)
  }
)

// get，post请求方法
export default {
  post(url, data) {
    return $axios({
      method: 'post',
      url,
      data: Qs.stringify(data),
      headers: {
        'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8'
      }
    })
  },
  get(url, params) {
    return $axios({
      method: 'get',
      url,
      params
    })
  }
}

```

如上，大家可以看我的注释说明，axios配置的封装是整个项目中很重要的模块，其实在不同的项目中，axios封装都大同小异，所以，只要掌握了一种技巧，下次开发新项目也就很容易完成封装这块。

## 3.路由和侧边栏

#### 路由

路由是组织一个vue项目的关键，在对项目原型分析后，接下来的第一步就是编写路由，本项目中，主要分为两种路由，`currencyRoutes` 和 `asyncRoutes`

`currencyRoutes`：代表通用路由，意思就是不要权限判断，不同角色用户都显示的页面，如：登陆页、404等

`asyncRoutes`： 代表动态路由，需要通过判断权限动态分配的页面，有关的权限判断的方法接下来会介绍。

#### 侧边栏