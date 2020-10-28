# 08-Hash Table Size, Rehashing, and Applications of Hashing



## I. Objectives

- [ ] 知道如何确定hash table size
- [ ] 知道为什么要rehashing以及如何rehashing
- [ ] 知道什么是amortized analysis
- [ ] 知道一些hashing的应用



## II. Determine Hash Table Size

​	1. 在给定==performance requirments==后，能够决定maximum permissible ==load factor==

<img src="08-Hash Table Size, Rehashing, and Applications of Hashing.assets/image-20201028100050346.png" width="65%;" />

​	2. 在给定table size后，确定最多能够被插入的元素个数

<img src="08-Hash Table Size, Rehashing, and Applications of Hashing.assets/image-20201028101033377.png" alt="image-20201028101033377" width="55%;" />



## III. Rehashing

- ### 思路

  当Load factor达到某个值的时候，新建一个更大的hash table，从当前的hash table中scan一遍，按照当前hash table中的顺序插入新的hash table，⚠️在插入新的表的时候按照新的hash function。另外顺序是按照之前表，而不是最开始的顺序。



## IV. Amortized Analysis of Rehashing

- ### 什么是Amortized Analysis?

  当rehashing操作的时候，会带来一些额外的复杂度，比如把之前元素复制到新的hash table，但是从长远角度，在插入之后的元素时效率变高，所以要把之前这部分复杂度均摊到之后每次insert, find, remove 里。

  <img src="08-Hash Table Size, Rehashing, and Applications of Hashing.assets/image-20201028102206158.png" alt="image-20201028102206158" width="65%;" />

  ​	所以平均下来，插入M+1个元素的每个元素插入时复杂度为$O(1)$.

## V. Hash函数的应用

1. 去除相同元素

   对每个元素进行hashing，放到hash table。因为key相同位置一定相同。

2. 两数和的问题

   如果要求一个数列里是否存在$x+y = t$

   假如用循环，时间复杂度时$O(n^2)$

   假如用哈希，先把每个元素hashing到表中，对于每个x，find(t-x)。复杂度为$O(n)$

