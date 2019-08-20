> 项目地址 [vue-admin-webapp](https://github.com/gcddblue/vue-admin-webapp) 欢迎star，fork

## 前言

相信许多人和我一样刚接触 vue 时看文档都很枯燥，看完 vue，还有 vueRouter 、vuex 、vue-cli 到现在 vue cli3(尤大大不要更新，学不动了。。。 )  对于看完教程之后又迟迟不能上手实际项目，只能写一些简单的小demo,这肯定和实际生产工作是有出入的，于是乎我就打算自己从零开始使用最新的技术栈搭建一个vue后台管理系统，依此加深对理论知识的学习，并增强自己的项目能力，所以希望本系列教程对你开发vue项目有所帮助。

## 介绍

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
│   │── favicon.ico            # favicon图标
│   |── index.html             # html模板
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

