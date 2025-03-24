---
layout: center
transition: view-transition
mdc: true
---

# 实操：搭建订单管理后端

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
