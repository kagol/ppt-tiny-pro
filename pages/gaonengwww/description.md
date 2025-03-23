## TinyPro 是什么?

<div flex gap-2 justify-between mt-8 >

<v-clicks>

- tiny-cli 的一个 toolkit
- 基于 TinyVue 组件库
- 一站式
- 开箱即用
- 中后台模板

</v-clicks>

<v-clicks>

<img src="/images/tiny-pro.png" w-100 rounded-sm/>

</v-clicks>

</div>

---
layout: center
transition: view-transition
mdc: true
---

## 一个页面是如何诞生的 {.inline-block.view-transition-title}

---
layout: center
transition: view-transition
mdc: true
---

## 一个页面是如何诞生的 {.inline-block.view-transition-title}

<img src="/images/old.svg" size-full class="view-transition-img" />

<!--
一个传统的页面通常是由 UI + 工程师完成。工程师拿到设计图后进行开发, 在代码中配置路由/菜单/国际化词条。工程师需要负责一些与开发任务不相关的事情，例如国际化、菜单。

为什么说菜单和开发任务不相关，因为实际部分菜单可能需要权限，如果某个角色没有某个权限，那么就不展示这个菜单。
-->

---

## 一个页面是如何诞生的 {.inline-block.view-transition-title}

<img src="/images/new.svg" size-full class="view-transition-img" />

<!--
为此我们开发了TinyPro, 工程师只需要去开发接口和页面, 而剩下的一人或多人可以通过TinyPro的接口来在线的更改角色，权限，国际化词条等。

这样就减轻了工程师的压力，成员的利用率也更高(不会造成“一核有难多核围观”的情况)
-->

---
clicks: 7
---

## 为什么使用 TinyPro?

<div grid grid-cols-3 grid-justify-items-center gap-4 transform transform-translate-y-15
>

<div flex flex-col shrink-0 grow-0 items-center justify-between gap-4>

<img src="/images/ruoyi.png"
w-20
h-20
v-click="1"
v-motion
:initial="{scale: 0, opacity: 0, y: 100}"
:click-1="{scale: 1, opacity: 1, y: 100}"
:click-4="{y: 0, transition: {type: 'linear'}}"
/>

<img src="/images/ruoyi-preview.png" w-full v-click="4" :delay="200" />

<div w-full flex items-center justify-center v-click="5">

<span>官方实现</span>

</div>

</div>

<div flex flex-col shrink-0 grow-0 items-center justify-between gap-4>

<img src="/images/ant-design.png"
w-20
h-20
v-click="2"
v-motion
:initial="{scale: 0, opacity: 0, y: 100}"
:click-1="{scale: 1, opacity: 1, y: 100}"
:click-4="{y: 0, transition: {type: 'linear'}}"
/>

<img src="/images/ant-design-pro.png" w-full v-click="4" :delay="200" />

<div w-full flex items-center justify-center v-click="6">

<span>官方实现</span>

</div>

</div>

<div flex flex-col shrink-0 grow-0 items-center justify-between gap-4>

<img src="/images/arco-design.png" w-20 h-20 v-click="3"
v-motion
:initial="{scale: 0, opacity: 0, y: 100}"
:click-2="{scale: 1, opacity: 1, y: 100}"
:click-4="{y: 0, transition: {type: 'linear'}}"
/>

<img src="/images/arco-design-pro.png" w-full v-click="4" :delay="200" />

<div v-click="7" w-full flex items-center justify-center>

<span>官方实现</span>

</div>

</div>

</div>

<!--
所以我们为什么要使用TinyPro呢？明明还有很多产品。例如

- RuoYi
- Ant Pro
- Arco Pro

当然在这里我先声明一点. 并不是其他产品不好，每个产品都有他们独自的特点。

RuoYi作为老牌的后端管理系统, 虽说也有前后端分离版本, 但官方实现似乎是Vue2，技术栈相对较老

AntPro和ArcoPro实际上都只是一个前端的模板，没有相应的后端。

Ruoyi,AntPro,ArcoPro 的前端国际化管理并没有使用接口的方法，而是直接塞进了前端里。

TinyPro则提供了包括但不仅限于
-->
