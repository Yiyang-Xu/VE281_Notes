# 06-Hashing Basics

## I.Objectives

- [ ] 了解hashing的目的
- [ ] 了解什么是collision problem
- [ ] 知道如何设计一个好的hash function



## II. Hashing用途及基本需求

- 用途：

  ​		通常用一个数据结构，叫做dictionary, 每个含有两个数据$(key, value)$, 目的是为了给出一个key能够快速找到value。

- 基本操作：

  - `Value find (Key k)`: 

    如果没有找到，返回Null。如果找到了返回value。

  - `Void insert (Key k, Value v)`: 

    插入一个pair. 如果这个pair已经存在，更新值。

  - `Value remove(Key k)`: 

    把dictionary中的一个pair移除，并且返回其值，如果不存在，返回Null.

  试想，如果用普通的Array来实现以上操作，需要的时间复杂度如何？

<img src="06-Hashing Basics.assets/image-20201027195051542.png" alt="image-20201027195051542" width="60%;" />

**⚠️我们能否把find, insert, remove的复杂度都降到$O(1)$?**

​		👀利用Hashing!



## III. Hashing

<img src="06-Hashing Basics.assets/image-20201027200735741.png" alt="image-20201027200735741" width="60%;" />

⚠️问题：此时find(), insert(), remove()的复杂度是多少？

​				答：$O(1)$.

例子：

<img src="06-Hashing Basics.assets/image-20201027201013417.png" alt="image-20201027201013417" style="zoom:50%;" />

出现的问题：

当两个数的hashing 结果相同的时候，一个格子内不能放两个元素，这种情况叫做collision. 通常解决Collision有两种方式：

- Seperate Chaning
- Open Addressing



### III. 2 如何设计一个好的Hash Function?

Criteria:

1. **每一个key都要计算一个所对应的bucket**
2. **如果两个key相同，那么一定结果得到的bucket也是相同的**
3. **需要能够快速计算得到结果**
4. **需要最小化collision**

> 第四条是最难的，因为如果是随机hashing的话，遇到collision的概率是1/n



### III. 3 Compression Map

目的：需要把每个integer map到一个home bucket. 最常见的是modulo arithmetic.

比如说	$homeBucket = c(hashcode) = hashcode \% n$

通常来说，hash table size $n$ 都是奇数因为否则偶数integers始终会被hash到even  home buckets.