# 09-Universal Hashing and Bloom Filter

## I. Objectives

- [ ] 知道什么是universal hashing
- [ ] 知道什么是Bloom filter以及它是如何工作的
- [ ] 知道Bloom filter的优缺点



## II. Universal Hashing

- ### 为什么要用universal hashing?

  因为在之前如果一个hashing function是确定的话，总归能找到一个方法来最大化collisions。解决的办法是越随机越好。有点类似quick sort里选pivot。

- ### Universal Hashing的定义

<img src="09-Universal Hashing and Bloom Filter.assets/image-20201028103913637.png" alt="image-20201028103913637" width="60%;" />

- Hash Function Families的例子

  之前的mod也是一个Hash function family的例子，⬇️是Matrix method

<img src="09-Universal Hashing and Bloom Filter.assets/image-20201028104150129.png" alt="image-20201028104150129" width="60%;" />

> 解释：因为h(x)有三位，所以能表示的数是$(2^b)$个，table size也就是$2^b$. u 是keys的长度。

<img src="09-Universal Hashing and Bloom Filter.assets/image-20201028105053638.png" alt="image-20201028105053638" width="70%;" />



## III. Bloom Filter

- ### 特点

  支持快速insert和find

- ### 优缺点：

  - 优点：更加space efficient
  - 缺点：
    - can't store an associated object
    - No deletion
    - False positive，$x$没有被insert，但是告诉你inserted了。但不会$x$没有被insert但是告诉你insert了

- ### 实现方式

<img src="09-Universal Hashing and Bloom Filter.assets/image-20201028105620169.png" alt="image-20201028105620169" width="60%;" />

​				Find():

​				计算出$h_1(x), h_2(x)...$去查看是否该位置是1，如果都是1，那么说明x被找到了，反之如果有一个位置是0，说明x不在表里。可能出现的错误情况，别的几个数填入的时候把x所对应的这些位置已经设成1了。所以当表全是1的时候，是一张没用的表。

- ### False Probability

<img src="09-Universal Hashing and Bloom Filter.assets/image-20201028110127627.png" alt="image-20201028110127627" width="60%;" />

<img src="09-Universal Hashing and Bloom Filter.assets/image-20201028110206078.png" alt="image-20201028110206078" width="60%;" />

<img src="09-Universal Hashing and Bloom Filter.assets/image-20201028110539936.png" alt="image-20201028110539936" width="60%;" />

