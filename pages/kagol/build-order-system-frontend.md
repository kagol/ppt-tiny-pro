---
layout: center
transition: view-transition
mdc: true
---

# 实操：搭建订单管理前端

---

<div flex flex-col h-full>

<div h-fit mb-8>

## 创建菜单

</div>

<div grid grid-cols-3 gap-4>

<div shrink-0 grow-0 h-full>

#### 菜单设计

<div mb-8></div>

```
我的订单
- 已买到的宝贝
- 创建订单
```

</div>

<div shrink-0 grow-0 h-full>

#### 在线创建菜单/路由

<div mb-8></div>

<div flex items-center gap-4>
<img src="/images/order-add-locale.png" alt="增加国际化词条" class="h-[150px]">
<img src="/images/order-add-menu-order.png" alt="增加菜单-我的订单" class="h-[300px]">
<img src="/images/order-bind-menu.png" alt="绑定菜单" class="h-[300px]">
</div>

</div>

</div>

</div>

---

## 开发订单页面

在 web/src/views 下创建 order 文件夹。

目录结构如下：

```bash
order
├── list # 订单列表页面
|  └── index.vue
├── create # 创建订单页面
|  └── index.vue
└── index.vue
```

---


<div flex flex-col h-full>

<div h-fit mb-8>

## 订单列表页面 list/index.vue

</div>

<div grid grid-cols-2 gap-4>

<div shrink-0 grow-0 h-full>

使用 TinyVue 组件，快速开发页面。

主要使用 TinyVue 组件库的以下组件：
1. Search 搜索框
2. Button 按钮
3. Grid 表格
4. Pager 分页
5. Divider 分割线
6. Link 超链接
7. Statistic 统计数值
8. Tag 标签
9. PopConfirm 气泡确认框
10. Icon 图标


</div>

<div shrink-0 grow-0 h-full>

模板结构：

```html {*}{maxHeight:'350px'}
<template>
  <div class="flex mt-[12px] mb-[12px]">
    <tiny-search
      @search="search"
      is-enter-search
      clearable
      @clear="clear"
      placeholder="商品标题/订单号/店铺名"
      class="!w-[222px] !mr-[8px]"
    ></tiny-search>
    <tiny-button>筛选<tiny-icon-chevron-down></tiny-icon-chevron-down></tiny-button>
    <tiny-button :icon="TinyIconDownload">导出订单</tiny-button>
  </div>
  <div class="overflow-auto h-[calc(100vh-280px)]">
    <tiny-grid :fetch-data="fetchData" :highlight-hover-row="false" ref="gridRef">
      <tiny-grid-column field="orderInfo" title="订单信息">
        <template #default="{ row }">
          <div class="flex items-center mt-[16px] mb-[16px]">
            <span>{{ row.createAt }}</span>
            <tiny-divider direction="vertical"></tiny-divider>
            <span>订单号: {{ row.orderId }}</span>
            <tiny-divider direction="vertical"></tiny-divider>
            <img :src="'xxx.png'" :alt="row.shopName" class="w-[26px]! h-[12px]! mr-[4px]">
            <tiny-link
              href="https://opentiny.design/tiny-vue"
              :underline="false"
              class="mr-[4px]"
            >{{ row.shopName }}</tiny-link>
            <a
              href="https://opentiny.design/tiny-vue"
              target="_blank"
              class="no-underline w-[20px] h-[20px] inline-block align-text-bottom mr-[4px]"
            ></a>
            <tiny-link href="https://opentiny.design/tiny-vue" :underline="false">
              订单详情<tiny-icon-angle-right></tiny-icon-angle-right>
              </tiny-link>
          </div>
          <div class="flex flex-row">
            <img :src="row.img" :alt="row.name" class="rounded-[8px] w-[96px] h-[96px] mr-[12px]">
            <div>
              <h3 class="mb-[4px] leading-[22px]">{{ row.name }}</h3>
              <p class="text-[#7a7a7a] mb-[4px] leading-[22px]">{{ row.desc }}</p>
              <div>
                <tiny-button>退换</tiny-button>
                <tiny-button>加入购物车</tiny-button>
              </div>
            </div>
          </div>
        </template>
      </tiny-grid-column>
      <tiny-grid-column field="goodsAmount" title="商品金额" width="160px">
        <template #default="{ row }">
          <tiny-statistic prefix="￥" :value="row.cost"></tiny-statistic>
          x{{ row.goodsQuantity || 1 }}
        </template>
      </tiny-grid-column>
      <tiny-grid-column field="disbursements" title="实付款" width="160px">
        <template #default="{ row }">
          <div class="flex">
            <span class="inline-flex items-center w-[80px]">实付款</span>
            <tiny-statistic prefix="￥" :value="row.disbursements"></tiny-statistic>
          </div>
          <tiny-tag>手机订单</tiny-tag>
        </template>
      </tiny-grid-column>
      <tiny-grid-column
        field="operation"
        title="操作列"
        width="120px"
      >
        <template #default="{ row }">
          <div class="flex flex-col">
            <tiny-button type="primary">再买一单</tiny-button>
            <tiny-button type="text">加入购物车</tiny-button>
            <tiny-button type="text">申请开票</tiny-button>
            <tiny-popconfirm
              title="是否确认删除"
              message="删除后不可恢复，确定要删除本订单吗？"
              type="warning"
              trigger="click"
              class="pl-[20px]"
              @confirm="deleteOrder({
                id: row.id
              })">
              <template #reference>
                <tiny-button type="text">删除订单</tiny-button>
              </template>
            </tiny-popconfirm>
          </div>
        </template>
      </tiny-grid-column>
    </tiny-grid>
  </div>
  <tiny-pager
    :current-page="pagerConfig.currentPage"
    :page-size="pagerConfig.pageSize"
    :total="pagerConfig.total"
    :page-sizes="[10, 20, 50, 100]"
    @current-change="currentChange"
    @size-change="sizeChange"
    layout="total, sizes, prev, pager, next, jumper"
  ></tiny-pager>
</template>
```

</div>

</div>

</div>

---


<div flex flex-col h-full>

<div h-fit mb-8>

## 对接后台接口 Get /order

</div>

<div grid grid-cols-2 gap-4>

<div shrink-0 grow-0 h-full>

## 定义请求方法

在 `web/src/api` 先创建 `order.ts` 文件

```ts
import axios from 'axios';

// 获取所有订单
export function getOrderList(params) {
  return axios.get(`/api/order`, { params });
}

// 创建订单

// ...
```


</div>

<div shrink-0 grow-0 h-full>

## 调接口 => 取数据 => 绑 UI

```ts {*}{maxHeight:'350px'}
import { TinyGrid, TinyGridColumn, ... } from '@opentiny/vue'
import { ref } from 'vue'
import { getOrderList } from '@/api/order'

const pagerConfig = ref({
  currentPage: 1,
  pageSize: 10,
  total: 100
})

const getData = async ({ filterArgs, page }) => {
  const params = {
    page: page?.currentPage || 1,
    size: page?.pageSize || 10,
    filter: filterArgs,
  }

  // 获取后台接口数据
  let { data } = await getOrderList(params);

  pagerConfig.value.total = data.total;
  return data.items
}

// 绑定 Grid 组件的 fetch-data 属性
const fetchData = ref({
  api: getData
})
```

</div>

</div>

</div>

---

## 增加分页、筛选、删除订单等功能

<div mt-8>

```ts {*}{maxHeight:'350px'}
import { TinyGrid, TinyGridColumn, ... } from '@opentiny/vue'
...

const gridRef = ref()

// 切换页码
function currentChange(current) {
  pagerConfig.value.currentPage = current

  fetchData.value.args = { page: { currentPage: current } }
  gridRef.value.handleFetch()
}

// 切换每页显示的数据条数
function sizeChange(size) {
  pagerConfig.value.pageSize = size

  fetchData.value.args = { page: { pageSize: size } }
  gridRef.value.handleFetch()
}

// 筛选
const search = (key, val) => {
  fetchData.value.args = { filterArgs: val }
  gridRef.value.handleFetch()
}

// 清除搜索框内容
const clear = () => {
  fetchData.value.args = { filterArgs: '' }
  gridRef.value.handleFetch()
}
```

</div>

---

## 效果

![Order List](/images/order-list.png)

---

<div flex flex-col h-full>

<div h-fit>

## 创建订单页面 create/index.vue

主要使用 TinyVue 的 Form / Input / Numeric / FileUpload 等表单类组件。

</div>

<div grid grid-cols-2 gap-4>

<div shrink-0 grow-0 h-full>

### 页面模板

```html {*}{maxHeight:'350px'}
<template>
  <tiny-form ref="ruleFormRef" :model="createData" :rules="rules" label-width="100px" class="w-[600px]! ml-auto mr-auto mt-[40px] mb-[40px]">
    <tiny-form-item label="商品名称" prop="name">
      <tiny-input v-model="createData.name"></tiny-input>
    </tiny-form-item>
    <tiny-form-item label="商品描述" prop="desc">
      <tiny-input v-model="createData.desc"></tiny-input>
    </tiny-form-item>
    <tiny-form-item label="金额" prop="cost">
      <tiny-numeric v-model="createData.cost"></tiny-numeric>
    </tiny-form-item>
    <tiny-form-item label="商家名称" prop="shopName">
      <tiny-input v-model="createData.shopName"></tiny-input>
    </tiny-form-item>
    <tiny-form-item label="商品图片" prop="orderImage">

      <tiny-file-upload :http-request="uploadImage" action="http://localhost:3000/api/order/upload">
        <template #trigger>
          <tiny-button>点击上传</tiny-button>
        </template>
      </tiny-file-upload>
    </tiny-form-item>
    <tiny-form-item>
      <tiny-button type="primary" @click="handleSubmit()">
        提交
      </tiny-button>
      <tiny-button @click="resetForm">重置</tiny-button>
    </tiny-form-item>
  </tiny-form>
</template>
```
</div>

<div shrink-0 grow-0 h-full>

### 页面逻辑

```ts {*}{maxHeight:'350px'}
import { ref, reactive } from 'vue'
import { TinyForm, TinyFormItem, ... } from '@opentiny/vue'
import { createOrder, uploadOrderImage } from '@/api/order'

const ruleFormRef = ref()

// 绑定表单数据
const createData = reactive({
  name: '',
  desc: '',
  orderImage: 'http://dummyimage.com/400x400',
  cost: 0,
  shopName: '',
})

// 创建订单
const handleSubmit = async () => {
  try {
    await createOrder(createData)
    Notify({
      type: 'success',
      message: '创建成功！',
      position: 'top-right'
    })
  } catch (error) {
    Notify({
      type: 'error',
      message: `创建失败！${error}`,
      position: 'top-right'
    })
  }
}

// 商品图片上传
const uploadImage = ({onSuccess, file}) => {
  return uploadOrderImage(file)
  .then((resp) => {
    createData.orderImage = `/api/${resp.data}`;
  })
  .catch(console.error);
}

// 表单项重置
function resetForm() {
  ruleFormRef.value.resetFields()
}

```

</div>

</div>

</div>

---

## 效果

![Create Order](/images/create-order.png)
