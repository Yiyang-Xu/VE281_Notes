# 07-Hashing Collision Resolution

## Objectives

- [ ] 了解seperate chaining
- [ ] 了解open addressing的基本概念
- [ ] 了解三种open addressing的方法以及每种方法的优缺点



## I. Separate Chaining

- ### 思路

  ​			当collision发生的时候，由于每个bucket都存着一个linked list，直接把collision发生的时候，后面来的放在linked list的下一个

<img src="07-Hashing Collision Resolution.assets/image-20201027203320033.png" alt="image-20201027203320033" width="60%;" />

- ### 实现过程

#### Value find(Key key)

Compute k = h(hey)。计算出key的哈希值k，然后在k-th bucket中找直到找到key。

#### Void insert(Key key, Value value)

Compute k = h(key)。在第k个bucket中找，如果找到的话update its value, 如果没找到，把这个值插入linked list，时间复杂度为O(1)

#### Void remove(Key key)

在第k个bucket中找，如果找到的话remove。



## II. Open Addressing

<img src="07-Hashing Collision Resolution.assets/image-20201028091242229.png" alt="image-20201028091242229" width="60%;" />

- ### Linear Probing

  - #### 思路

    对key apply hash function,如果直接能找到空的slot，直接放进去。如果不能的话apply h1, h2...直到找到空的slot.

    <img src="07-Hashing Collision Resolution.assets/image-20201028091747484.png" alt="image-20201028091747484" width="60%;" />

  - #### 实现过程

    ##### find()

    先到hash function所对应的slot找，如果没有找到依次往下找，直到我们找到这个key或者我们找到了一个空的slot，也就说明我们没有找到。

    ##### ⚠️Remove()

    如果直接找到删除后，会带来的问题是：如果本来这一堆数字已经cluster了，那么移除某个元素后剩下元素也并不在应该在的位置上。所以我们用=="Lazy deletion"==，也就是在被删除的元素上标记成"delete"，所以bucket有三种状态：“occupided", "empty", and "deleted". 当**find()**的时候，如果遇到empty或者delete，则说明没找到。

    ##### Insert()

    在**insert()**的时候，如果是empty或者delete，把该位置替换成插入元素。

    

  - #### Clustering Problem

<img src="07-Hashing Collision Resolution.assets/image-20201028092753830.png" alt="image-20201028092753830" width="70%;" />



- ### Quadratic Probing

  例子：$h_i(key) = (h(key) + i^2) \% n$

#### 用途：

​		更难以形成large clusters

#### ⚠️问题

​		有时候即使table还没满，我们仍然无法找到一个空的slot。

<img src="07-Hashing Collision Resolution.assets/image-20201028093659392.png" alt="image-20201028093659392" width="50%;" />

​		理论上，如果==load factor==$L \le 0.5$，我们一定能找到一个空的slot

<img src="07-Hashing Collision Resolution.assets/image-20201028093620783.png" alt="image-20201028093620783" width="60%;" />

<img src="07-Hashing Collision Resolution.assets/image-20201028093832342.png" alt="image-20201028093832342" width="60%;" />



- ### Double Hashing

  用两个不一样的hash function，相当于hash两次

  <img src="07-Hashing Collision Resolution.assets/image-20201028094013217.png" alt="image-20201028094013217" width="45%;" />

  优点在于对于每个key的increment probing patter都是一样的



## III. Performance of Open Addressing

​	两个基本参数：

- **The expected number of comparisons in an Unsuccessful Search: $U(L)$**
- **The expected number of comparisons in a Successful Search: $S(L)$**

<img src="07-Hashing Collision Resolution.assets/image-20201028094542042.png" alt="image-20201028094542042" width="70%;" />

<img src="07-Hashing Collision Resolution.assets/image-20201028094728868.png" alt="image-20201028094728868" width="65%;" />

- ### 该采取哪种策略？

  - 如果空间matter, 用open addressing

  - 如果需要移除元素，用seperate chaining,因为remove() 在open addressing里很麻烦

    