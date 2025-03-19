# 项目亮点特性

1. 上手成本低：一行命令即可创建一个后台管理系统
2. 最新技术栈：前端基于 Vue3 + TypeScript，后端基于 NestJS
3. 强大的功能：支持组件粒度的权限管理、页签模式、多级菜单、多种布局方式、个性化主题、国际化、Mock数据等丰富的特性，开箱即用
4. 使用成本低：支持在线方式快速配置角色、用户、菜单、权限、国际化词条，无需写代码，用户使用成本低，没有开发基础的设计师、产品经理也能操作
5. 开发者友好：支持 Vite、Webpack、Rspack、Farm 等多种构建工具

---

# 项目目录结构

后端项目目录结构（仅列出关键目录和文件）

```
tiny-pro/nestJs
├── README.md
├── docker-compose.yml
├── dockerfile
├── libs
|  ├── db // MySQL 数据库
|  |  ├── src
|  |  |  ├── db.module.ts
|  |  |  ├── db.service.ts
|  |  |  └── index.ts
|  |  └── tsconfig.lib.json
|  ├── models // MySQL 数据库表结构
|  |  ├── src
|  |  |  ├── i18n.ts
|  |  |  ├── index.ts
|  |  |  ├── lang.ts
|  |  |  ├── menu.ts
|  |  |  ├── order.ts
|  |  |  ├── permission.ts
|  |  |  ├── role.ts
|  |  |  └── user.ts
|  |  └── tsconfig.lib.json
|  └── redis // Redis 数据库
|     ├── redis.module.ts
|     └── redis.service.ts
├── locales.json // 初始国际化词条数据
├── nest-cli.json
├── package.json
├── pnpm-lock.yaml
├── src
|  ├── app.module.ts // 入口模块
|  ├── auth // 登录鉴权
|  |  ├── auth.controller.ts
|  |  ├── auth.guard.ts
|  |  ├── auth.module.ts
|  |  ├── auth.service.ts
|  |  └── dto
|  |     ├── create-auth.dto.ts
|  |     ├── logout-auth.dto.ts
|  |     └── update-auth.dto.ts
|  ├── main.ts // 入口文件
|  ├── menu // 菜单管理
|  |  ├── dto
|  |  |  ├── create-menu.dto.ts
|  |  |  └── update-menu.dto.ts
|  |  ├── init
|  |  |  └── data.ts
|  |  ├── menu.controller.ts
|  |  ├── menu.module.ts
|  |  └── menu.service.ts
|  ├── order // 订单管理
|  |  ├── dto
|  |  |  ├── create-order.dto.ts
|  |  |  ├── remove-order.ts
|  |  |  └── update-order.ts
|  |  ├── init.ts
|  |  ├── order.controller.ts
|  |  ├── order.module.ts
|  |  └── order.service.ts
|  ├── permission // 权限管理
|  |  ├── dto
|  |  |  ├── create-permission.dto.ts
|  |  |  └── update-permission.dto.ts
|  |  ├── permission.controller.ts
|  |  ├── permission.guard.ts
|  |  ├── permission.module.ts
|  |  └── permission.service.ts
|  ├── public
|  |  ├── permission.decorator.ts
|  |  ├── public.decorator.ts
|  |  ├── reject.decorator.ts
|  |  └── reject.guard.ts
|  ├── role // 角色管理
|  |  ├── dto
|  |  |  ├── create-role.dto.ts
|  |  |  └── update-role.dto.ts
|  |  ├── entities
|  |  |  └── role.entity.ts
|  |  ├── role.controller.ts
|  |  ├── role.module.ts
|  |  └── role.service.ts
|  └── ...
├── tsconfig.build.json
└── tsconfig.json
```

前端项目目录结构（仅列出关键目录和文件）

```
web
├── config // Vite 配置
|  ├── plugin
|  |  ├── arcoResolver.ts
|  |  ├── compress.ts
|  |  ├── imagemin.ts
|  |  └── visualizer.ts
|  ├── utils
|  |  └── index.ts
|  ├── vite.config.base.ts
|  ├── vite.config.dev.ts
|  └── vite.config.prod.ts
├── index.html
├── package.json
├── src
|  ├── App.vue // 应用入口
|  ├── api // API 请求方法（需要请求后台接口时，需要在这里增加 API 请求方法）
|  |  ├── form.ts
|  |  ├── menu.ts
|  |  ├── order.ts
|  |  ├── role.ts
|  |  ├── user.ts
|  |  └── ...
|  ├── assets // 静态资源
|  |  ├── images
|  |  |  ├── avatar.png
|  |  |  ├── collapse.png
|  |  |  ├── error.png
|  |  |  ├── expand.png
|  |  |  ├── filter.png
|  |  |  └── ...
|  |  ├── style // 样式文件
|  |  |  ├── breakpoint.less
|  |  |  ├── exception.less
|  |  |  ├── global.less
|  |  |  └── menu.less
|  ├── components // 公共组件（多个页面复用的公共组件）
|  |  ├── breadcrumb
|  |  |  └── index.vue
|  |  ├── footer
|  |  |  └── index.vue
|  |  ├── global-setting
|  |  |  └── index.vue
|  |  ├── index.ts
|  |  ├── menu
|  |  |  └── index.vue
|  |  ├── navbar
|  |  |  └── index.vue
|  |  └── ...
|  ├── directive // 公共指令
|  |  ├── index.ts
|  |  └── permission
|  |     └── index.ts
|  ├── hooks // 公共 Hooks(Composables)
|  |  ├── useDeepClone.ts
|  |  ├── useDisclosure.ts
|  |  ├── useI18nMenu.ts
|  |  ├── useMenuId.ts
|  |  ├── useTheme.ts
|  |  └── ...
|  ├── layout // 布局
|  |  ├── default-layout.vue
|  |  ├── general-layout.vue
|  |  └── page-layout.vue
|  ├── main.ts // 入口文件
|  ├── router // 路由（一般不用改）
|  |  ├── constant.ts
|  |  ├── guard
|  |  |  ├── index.ts
|  |  |  ├── info.ts
|  |  |  ├── menu.ts
|  |  |  ├── permission.ts
|  |  |  └── tabs.ts
|  |  ├── index.ts
|  |  ├── routes
|  |  |  ├── index.ts
|  |  |  └── modules
|  |  └── typings.d.ts
|  ├── store // 数据
|  |  ├── index.ts
|  |  └── modules
|  |     ├── app
|  |     ├── locales.ts
|  |     ├── router.ts
|  |     ├── tab-bar
|  |     ├── tabs.ts
|  |     └── user
|  ├── style.css // 样式入口
|  ├── utils // 工具函数（需要熟悉，随时可以取用）
|  |  ├── auth.ts
|  |  ├── base-utils.ts
|  |  ├── env.ts
|  |  ├── event.ts
|  |  ├── formatter.ts
|  |  ├── hwcClient.service.ts
|  |  ├── monitor.ts
|  |  ├── pub.ts
|  |  ├── route-listener.ts
|  |  ├── setup-mock.ts
|  |  └── time.ts
|  └── views // 页面（主要修改这个文件）
|     ├── form
|     |  ├── base
|     |  ├── index.vue
|     |  └── step
|     ├── menu
|     |  ├── demo
|     |  ├── index.vue
|     |  └── info
|     ├── order
|     |  ├── bought
|     |  ├── create
|     |  └── index.vue
|     ├── permission
|     |  ├── index.vue
|     |  └── info
|     ├── role
|     |  ├── index.vue
|     |  └── info
|     ├── ...
|     └── userManager
|        ├── index.vue
|        ├── info
|        ├── setting
|        └── useradd
├── tiny.config.js
└── tsconfig.json
```

---

# 实操：增加订单管理

后端

前端：
- 创建国际化词条、创建菜单、绑定目录
- 编写订单列表页面
- 后端接口联调
- 分页、筛选
- 编写新建订单页面
- 文件上传

小作业：
- 增加编辑订单功能

---

# 未来规划

- 页面设计器
- 移动端适配
- Java Spring Boot 后端
- 支持 AI

---

# 如何参与共建

- Issue 任务
- 贡献指南
