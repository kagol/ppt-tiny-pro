<div flex flex-col h-full>

<div h-fit>

# UI 效果

</div>

<div grid grid-cols-2 gap-4>

<div shrink-0 grow-0 h-full>

#### 订单列表页面

![Order List](/images/order-list.png)

</div>

<div shrink-0 grow-0 h-full>

#### 创建订单页面

![Create Order](/images/create-order.png)

</div>

</div>

</div>

---
src: ./build-order-system-backend.md
---

---
src: ./build-order-system-frontend.md
---

---

# 小结：如何给 TinyPro 增加订单管理模块

<div mt-8></div>

后端接口开发：

```mermaid
flowchart LR
    设计数据库表结构-->设计接口协议-->开发后端服务和接口
```

前端页面开发：

```mermaid
flowchart LR
    在线创建菜单/路由-->使用TinyVue搭建页面-->对接后端接口
```
