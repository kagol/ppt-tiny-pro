<div flex flex-col h-full>

<div h-fit>

# 项目目录结构

</div>

<div grid grid-cols-2 gap-4>

<div shrink-0 grow-0 h-full>

#### 后端

```bash {*}{maxHeight:'300px'}
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

</div>

<div shrink-0 grow-0 h-full>

#### 前端

```bash {*}{maxHeight:'300px'}
tiny-pro/web
├── config // Vite 配置
|  ├── plugin
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

</div>

</div>

</div>

<!--
了解完 TinyPro 的亮点特性，并且体验了 TinyPro 后台管理系统的基本使用，作为程序员，大家一定还是对代码比较感兴趣，想要迫不及待地看下它的源码，了解它的具体实现了吧？

接下来我就给大家分析下 TinyPro 项目的源码结构，带大家“一探究竟”！

`tiny init pro` 创建出来的项目，最外层主要包含两个目录：nestJs 和 web。

nestJs 是后端代码，web 是前端代码。

我们先来看下 nestJs 目录...
-->
