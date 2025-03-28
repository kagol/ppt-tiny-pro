# 项目亮点特性

1. 上手成本低：一行命令即可创建一个后台管理系统
2. 最新技术栈：前端基于 Vue3 + TypeScript + TinyVue，后端基于 NestJS
3. 强大的功能：支持组件粒度的权限管理、页签模式、多级菜单、多种布局方式、个性化主题、国际化、Mock 数据等丰富的特性，开箱即用
4. 使用成本低：支持在线方式快速配置角色、用户、菜单、权限、国际化词条，无需写代码，用户使用成本低，没有开发基础的设计师、产品经理也能操作
5. 开发者友好：支持 Vite、Webpack、Rspack、Farm 等多种构建工具

<!--
听完高能的分享，相信大家已经对 TinyPro 有了一定的了解，我对 TinyPro 的亮点特性做了个简单的整理。

我认为 TinyPro 主要有五大亮点吧。

首先就是上手成本低，只需要执行 tiny init pro 就能初始化一个包含前后端的后台管理系统，非常便捷。

其次就是...
-->

---
src: ./directory-structure.md
---

---
layout: two-cols-header
---
# 实操：增加订单管理模块

::left::

#### 后端:

- 表结构设计
- 接口规划
  - 出参入参
  - 权限规划
- 接口开发
  - 添加订单
  - 删除订单
  - 查询某个订单
  - 查询订单列表
    - 分页
    - 筛选
  - 修改订单

::right::

#### 前端：

- 在线创建菜单
  - 创建国际化词条
  - 创建菜单
  - 绑定目录
- 开发前端页面
  - 订单列表页
  - 创建订单页
- 对接后端接口，实现功能
  - 对接订单列表接口
  - 实现分页/筛选/删除
  - 对接创建订单接口
  - 文件上传

<!--
当我们对 TinyPro 的整体源码结构有了一定的了解之后，就可以开始二次开发啦！

接下来我将以“订单管理模块”为例，手把手带大家为 TinyPro 增加新的业务模块，从开发后端接口到搭建前端页面，完成整个模块的开发，让大家对 TinyPro 二开流程有个较为清晰的认识。

如果你前面已经跟着高能老师的演示，把 TinyPro 项目启动起来了，接下来你可以继续跟着我一起完成订单管理模块的开发。

我们先规划下整体的搭建步骤，左边是后端部分，开发后端接口之前，我们会先设计好数据库表结构，并设计好接口的入参出参，然后才开始正式编码，实现创建订单、删除订单、查询订单等接口。

右边是前端部分，先通过在线方式创建国际化词条、菜单和路由，然后开发前端页面，这里我们会用到 TinyVue 组件，最后对接后端接口完成开发。
-->

---
src: ./build-order-system.md
---

---

# 未来规划

- 页面设计器
- 移动端适配
- Java Spring Boot 后端
- 支持 AI

---

# 如何参与共建

- 阅读贡献指南
- 领取 Issue 任务

---

<div class="text-2xl mt-[100px]">

官网：[https://opentiny.design/pro/](https://opentiny.design/pro/)

源码：[https://github.com/opentiny/tiny-cli/](https://github.com/opentiny/tiny-cli/)（欢迎 ⭐️）

</div>

<div class="w-[200px] flex items-center flex-col mt-[100px]">
  <img src="/images/opentiny.png" alt="OpenTiny QR Code" width=120 />
  <span>OpenTiny 小助手微信</span>
</div>

---
layout: end
---
