---
layout: center
transition: view-transition
mdc: true
---

# 实操：搭建订单管理后端

<!--
话不多说，开始开干！先搭后端！
-->

---

# 表结构设计

在 nestJs/libs/models/src 中定义数据表结构，这里我们增加了一个 order.ts（订单表）。

```js {*}{maxHeight:'350px'}
// order.ts
import { BeforeInsert, Column, Entity, ManyToOne, PrimaryGeneratedColumn } from "typeorm";
import { User } from "./user";
import { v1 } from 'uuid';

@Entity('order')
export class Order {
    @PrimaryGeneratedColumn()
    id: number; // 自增主键
    @Column()
    name: string; // 商品名称
    @Column()
    desc: string; // 商品描述
    @Column()
    img: string; // 商品图
    @Column('float')
    cost: number;
    @Column({ type: 'text' })
    orderId: string; // 订单ID
    @Column('bool')
    isDel: boolean;
    @Column({ type: 'text', nullable: true })
    reason: string;
    @ManyToOne(() => User, user => user.order)
    creator: User // 定义多对一的关系，多个 order 对应一个 user
    @Column({ type: 'timestamp', default: () => 'CURRENT_TIMESTAMP' })
    createAt: Date; // 创建时间
    @Column({ type: 'timestamp', default: () => 'CURRENT_TIMESTAMP' })
    updateAt: Date;
    @Column({ type: 'text' })
    shopName: string; // 店铺名称
    @BeforeInsert()
    beforeInsert() {
        this.orderId = v1();
        this.isDel = false;
    }
}
```

<!--
在实际写代码之前，我们先做一些前期设计的工作，先设计数据库表结构...
-->

---

# 接口设计

获取订单列表 GET /order

### 请求参数

|名称|位置|类型|必选|说明|
|---|---|---|---|---|
|page|query|number| 否 |第几页|
|size|query|number| 否 |页大小|
|filter|query|string| 否 |筛选逻辑。模糊搜索 name 和 orderId 两个字段|

<!--
然后是设计接口，我们以获取订单列表接口为例，其他接口也是一样设计的。

先设计入参，需要哪些请求参数，这些参数放在哪里，比如是放在 query 里还是 body 里，参数类型是什么，是否是必选等。

订单列表接口是一个 GET 请求，包含...
-->

---

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|401 未登录|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|403 权限不足|Inline|

<!--
设计好入参，就是返回结果的设计，先设计状态码，我们一共设计了 200 成功、401 未登录、403 权限不足三种状态码，每种状态码都有对应的返回数据结构。
-->

---

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» items|[object]|true|none||none|
|»» id|integer|true|none||none|
|»» name|string|true|none||none|
|»» orderId|string|true|none||none|
|»» createAt|string|true|none||none|
|»» ...||||||
|» total|integer|true|none||none|

<!--
我们以 200 状态码为例，返回结果包含 items 订单列表数据和 total 总订单数两个字段，total 主要用于分页，items 是一个数组，包含了当前用户下的所有订单数据。
-->

---

### 返回成功示例

```json
{
  "items": [
    {
      "id": 12,
      "name": "正宗内蒙古风干超干薄脆牛肉片",
      "desc": "正宗内蒙古超干风干牛肉干原切牛排薄脆片减盐肥瘦零食牛脆脆薯片",
      "orderId": "7cdcf400-00d3-11f0-81d9-c7ce9a5d3c25",
      "img": "item_pic.jpg_460x460q90.jpg_.webp",
      "cost": 56.8,
      "shopName": "草原达尔沁",
      "isDel": false,
      "createAt": "2025-03-14T12:54:38.000Z",
      ...
    },
    ...
  ],
  "total": 23
}
```

<!--
如果前端页面请求该接口顺利的话，接口将返回类似如下的数据，前端拿到该数据就可以在页面进行渲染啦。

经过前期的设计工作，是不是整个流程就瞬间清晰了，所以说开始写代码之前，花点时间做设计是有好处的，可以让自己更加胸有成竹！
-->

---

# 接口实现

在 nestJs/src 中增加 order 文件夹，用来存放订单相关接口代码。

目录结构如下：

```bash
\order
├── dto # 接口的 body 类型和校验 schema
|  ├── create-order.dto.ts
|  ├── remove-order.ts
|  └── update-order.ts
├── init.ts # 订单列表的初始化数据
├── order.controller.ts # 订单后台接口定义
├── order.module.ts # 订单模块入口，声明 controller 和 service
└── order.service.ts # 订单数据逻辑，被 controller 消费
```

<!--
好了，现在正式开始开发接口，我们先把目录结构规划下...
-->

---

### 订单模块

```ts
import { Module } from '@nestjs/common';
import { OrderService } from './order.service';
import { OrderController } from './order.controller';
import { TypeOrmModule } from '@nestjs/typeorm';
import { User } from '@app/models';
import { Order } from '@app/models/order';

@Module({
  imports: [
    TypeOrmModule.forFeature([User, Order])
  ],
  controllers: [OrderController],
  providers: [OrderService],
  exports: [OrderService]
})
export class OrderModule { }
```

---

### 订单接口定义

```ts {*}{maxHeight:'350px'}
import { Body, Controller, Get, ParseIntPipe, Post, Query } from '@nestjs/common';
import { OrderService } from './order.service';
import { CreateOrder } from './dto/create-order.dto';
import { Permission } from '../public/permission.decorator';
...

@Controller('order')
export class OrderController {
  constructor(private readonly orderService: OrderService) { }

  // 获取订单列表 对应 Get /order 接口
  @Get('/')
  @Permission('order::list')
  getOrder(
    @Query('page', ParseIntPipe) page: number,
    @Query('size', ParseIntPipe) size: number,
    @Query('filter') filter?: string
  ) {
    return this.orderService.getOrderList(page, size, filter);
  }

  // 创建订单 对应 POST /order  接口
  @Post('/')
  @Permission('order::create')
  createOrder(
    @Body() body: CreateOrder,
    @User() user: RequestUser['user']
  ) {
    return this.orderService.createOrder(body, user.email);
  }

  ...
}
```

---

### 订单数据服务

```ts {*}{maxHeight:'350px'}
import { User } from '@app/models';
import { Order } from '@app/models/order';
import { Injectable } from '@nestjs/common';
import { InjectRepository } from '@nestjs/typeorm';
import { Like, Or, Repository } from 'typeorm';

@Injectable()
export class OrderService {
    constructor(
        @InjectRepository(User)
        private userRep: Repository<User>,
        @InjectRepository(Order)
        private order: Repository<Order>,
        private readonly i18n: I18nService<I18nTranslations>
    ) { }

    // 从数据库获取订单列表数据
    async getOrderList(
        page: number,
        size: number,
        filter?: string
    ) {
        // 计算筛选出来的总订单数量
        const total = await this.order.count({
            where: [
                {
                    isDel: false,
                    name: filter ? Like(`%${filter}%`) : undefined,
                },
                {
                    isDel: false,
                    orderId: filter ? Like(`%${filter}%`) : undefined,
                }
            ]
        });

        // 从数据库里查询订单列表数据
        const items = await this.order.find({
            skip: (Math.max(page, 1) - 1) * size,
            take: size,
            select: {
                name: true,
                desc: true,
                img: true,
                cost: true,
                shopName: true,
                id: true,
                orderId: true,
                createAt: true,
                ...
            },
            relations: {
                creator: {
                    role: true
                }
            },
            where: [
                {
                    isDel: false,
                    name: filter ? Like(`%${filter}%`) : undefined,
                },
                {
                    isDel: false,
                    orderId: filter ? Like(`%${filter}%`) : undefined,
                }
            ]
        })
        return {
            items,
            total
        }
    }
}
```
