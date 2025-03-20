## TinyPro 是什么?

<div flex gap-2 justify-between mt-8 >

<v-clicks>

- tiny-cli 的一个 toolkit
- 一站式
- 开箱即用
- 中后台模板

</v-clicks>

<v-clicks>

<img src="/images/tiny-pro.png" w-100 rounded-sm/>

</v-clicks>

</div>

---
clicks: 7
---

## 为什么使用 TinyPro?

<div grid grid-cols-3 grid-justify-items-center gap-4 transform transform-translate-y-15
>

<div flex flex-col shrink-0 grow-0 items-center justify-between gap-4>

<img src="/images/ant-design.png"
w-20
h-20
v-click="1"
v-motion
:initial="{scale: 0, opacity: 0, y: 100}"
:click-1="{scale: 1, opacity: 1, y: 100}"
:click-4="{y: 0, transition: {type: 'linear'}}"
/>

<img src="/images/ant-design-pro.png" w-full v-click="4" :delay="200" />

<div w-full flex items-center justify-center v-click="5">

<span>官方实现</span>

</div>

</div>

<div flex flex-col shrink-0 grow-0 items-center justify-between gap-4>

<img src="/images/arco-design.png" w-20 h-20 v-click="2"
v-motion
:initial="{scale: 0, opacity: 0, y: 100}"
:click-2="{scale: 1, opacity: 1, y: 100}"
:click-4="{y: 0, transition: {type: 'linear'}}"
/>

<img src="/images/arco-design-pro.png" w-full v-click="4" :delay="200" />

<div v-click="6" w-full flex items-center justify-center>

<span>官方实现</span>

</div>

</div>

<div flex flex-col shrink-0 grow-0 items-center justify-between gap-4>

<img src="/images/element-plus.png" h-20
v-click="3"
v-motion
:initial="{scale: 0, opacity: 0, y: 100}"
:click-3="{scale: 1, opacity: 1, y: 100}"
:click-4="{y: 10, transition: {type: 'linear'}}"
/>

<img
src="/images/element-plus-admin.png"
w-full
v-click="4"
:delay="200"
/>

<div w-full flex items-center justify-center v-click="7">

<span>社区实现</span>

</div>

</div>

</div>

<!--
简单介绍 AntDesign Pro, ArcoDesign Pro, ElementPlus Admin. 的缺点

- 没有后端
-->
