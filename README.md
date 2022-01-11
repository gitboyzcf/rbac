<p align="center">
  <a href="https://github.com/vuejs/vue-next">
    <img src="https://img.shields.io/badge/vue-3.0-brightgreen.svg" alt="vue">
  </a>
  <a href="https://github.com/element-plus/element-plus">
    <img src="https://img.shields.io/badge/element--plus-1.x-brightgreen.svg" alt="element-plus">
  </a>
  <a href="https://github.com/microsoft/TypeScript">
    <img src="https://img.shields.io/badge/typescript-4.x-brightgreen.svg" alt="typescript">
  </a>
</p>

[vue3-rbac](http://github.com/gitboyzcf/vue3-rbac.git)主要目的在于学习 __`vue3`__ + __`ts`__,功能在完善中,基于的 __`RBAC`__ 权限控制。

### 简介

[vue3-rbac](http://github.com/gitboyzcf/vue3-rbac.git) 是一个管理后台基础功能框架，基于 [vue3](https://github.com/vuejs/vue-next) 、 [element-plus](https://github.com/element-plus/element-plus) 和 [typescript](https://github.com/microsoft/TypeScript) 实现。内置了 i18n 国际化，动态路由，权限验证。


### 功能模块

- [X] 角色管理
- [X] 账户管理
- [X] 发送邮件/邮件记录
- [X] 登录日志
- [X] 操作日志
- [X] 定时任务日志
- [X] 异常日志
- [X] 菜单管理
- [X] 数据字典
- [X] 配置管理
- [X] 定时任务
- [X] 文件管理 - 现在默认使用的是七牛云，可直接配置存储位置
  - [X] 本地存储
  - [X] 七牛云存储 
- [X] 消息推送
- [X] 区域管理
- [X] 备份管理
- [X] 代码生成器
- [X] 接口文档
- [X] SQL监控

### 项目结构

```bash
vue3-src
├─api 接口模块
│
├─assets 静态资源模块
│  ├─icon svg图标
│  ├─images 图片
│  └─sass 样式
│ 
├─components 通用组件
│  ├─global 全局组件
│  │  ├─icon element-plus 内置图标组件重新封装
│  │  ├─page 分页组件
│  │  ├─svg 本地svg图片使用组件
│  │  └─index 统一全局注册
│  ├─editor 富文本组件
│  └─look-around 随便看看按钮组件
│ 
├─directive 全局自定义指令
│ 
├─mixins 代码复用 （vue2混入）
│  └─page 分页
│ 
├─router 动态路由
│ 
├─store vuex
│  ├─modules
│  │  ├─dictionary 数据字典模块
│  │  ├─menu 菜单模块
│  │  ├─setting 设置模块
│  │  ├─tab 标签页模块
│  │  └─user 用户登录信息模块
│  └─index 动态加载模块
│ 
├─utils 工具模块
│  ├─constant 常量
│  ├─dictionary 字典
│  ├─index 工具
│  ├─regular 正则
│  ├─request axios二次封装
│  └─storage 本地缓存工具
│
├─views 视图模块
│  ├─global 通用页面
│  │  ├─401 401页面
│  │  ├─404 404页面
│  │  ├─500 500页面
│  │  └─login 登录页面
│  ├─layout
│  │  ├─components
│  │  │  ├─edit-info 修改信息
│  │  │  ├─headbar 顶部导航
│  │  │  ├─sidebar 侧边栏
│  │  │  └─tabsbar 标签页
│  │  └─index 布局入口页面
│  └─modules 页面模块

```

### 开发

```bash
# 克隆项目
git clone http://github.com/gitboyzcf/vue3-rbac.git

# 进入项目目录
cd vue3-rbac

# 安装依赖
npm install

# 启动服务
npm run dev   # 开发环境
npm run prod  # 正式环境
npm run test  # 测试环境

# 发布
npm run build:dev   # 开发环境
npm run build:prod  # 正式环境
npm run build:test  # 测试环境
```
