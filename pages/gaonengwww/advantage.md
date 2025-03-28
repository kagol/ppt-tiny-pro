---
clicks: 7
---

## 我们的优势

<advantage />

<!--
服务端 细颗粒度权限管理
服务端 可视化创建国际化词条
服务端 可视化角色菜单绑定
服务端 可视化创建菜单
服务端 可视化角色管理
多种前端布局
多种前端主题
前端国际化

每一个接口都是可以独立拆分的一个模块, 除了国际化模块下存在语言管理服务，其余模块与模块间松耦合，开发者们可以快速地进行二次开发。
-->

---
clicks: 7
---

## 我们的优势

<Stack />

<!--
技术栈方面，我们选择了

Nestjs 作为后端开发框架，Nestjs是一个老牌，社区活跃的IOC后端框架

前端方面我们使用Vue3 + Ts

构建方面，考虑到不同开发者对不同打包工具有不同的喜好，我们不仅支持Vite还支持Webpack, rspack, farme 作为打包工具。

说了这么多，我们接下来将进入演示阶段，为各位演示如何从零开始创建一个TinyPro中后台管理系统
-->

---

## 实战

<!-- 

讲了这么多，接下来我们将会进入到实战环节。本次我们将会从0开始使用官方cli搭建一个TinyPro中后台管理系统。

并展示如何

- 添加用户
- 添加菜单
- 创建权限
- 创建用户
- 分配权限
- 为用户分配菜单
- 以及如何创建一个国际化词条并在前端中使用。

-->

<v-clicks depth=3>

1. 如何新建一个TinyPro中后台管理模板
2. 如何启动TinyPro中后台管理模板
3. 如何增加用户
4. 如何增加菜单
5. 如何进行权限管理
   1. 创建权限
      1. 组件级权限管理
      2. 页面级权限管理
   2. 创建用户
   3. 分配权限给用户
6. 如何为用户绑定菜单
7. 创建好的国际化词条如何在前端中使用

</v-clicks>

<style>
.slideev-vcilck-target{
    transition: all 1s ease;
    filter: blur(0px);
    opacity: 1;
}
.slidev-vclick-hidden{
    filter: blur(2px);
    transform: translateY(20px);
    opacity: 0;
}
</style>

<!--
...(演示环节)

我们的演示到此结束，现在集中回答一下网友的提问。

...(答疑环节)

如果大家还有什么疑问，可以在 Gitee 上关注我们的开源项目：https://gitee.com/opentiny/tiny-cli。

接下来有请 Kagol 老师给大家分享如何基于 TinyPro 搭建订单管理模块的前后端。
-->