# 11-Binary Tree Traversal

## I. Objectives

- [ ] 知道三种遍历方式的效果和实施过程，pre-order, post-order和in-order，以及depth-first traversal和level-order traversal.



## II. Binary Tree Traversal

- Depth-first traversal
  - Pre-order
  - Post-order
  - In-order
- Level-order traversal (也叫breadth-first)



### II.(1) Pre-Order

<img src="11-Binary Tree Traversal.assets/image-20201028131431240.png" alt="image-20201028131431240" width="60%;" />

### II. (2) Post-Order

<img src="11-Binary Tree Traversal.assets/image-20201028131527246.png" alt="image-20201028131527246" width="60%;" />

### II. (3) In-Order

<img src="11-Binary Tree Traversal.assets/image-20201028131733075.png" alt="image-20201028131733075" width="60%;" />

简易记法，在tree外部画一条流程线，如果是pre-order,第一次经过一个节点时，就把节点记下来。如果是post-order，在这条线最后经过这个节点时记下来。



## III. Level-Order Traversal

​		从top to bottom, 每层从左到右traverse

<img src="11-Binary Tree Traversal.assets/image-20201028132636083.png" alt="image-20201028132636083" width="50%;" />

- ### **实现方法**

  用queue，每次pop一个节点时，把他的children push到que最后。（FIFO）

<img src="11-Binary Tree Traversal.assets/image-20201028132753822.png" alt="image-20201028132753822" width="60%;" />

<img src="11-Binary Tree Traversal.assets/image-20201028132917424.png" alt="image-20201028132917424" width="45%;" />

- #### 代码实现

<img src="11-Binary Tree Traversal.assets/image-20201028133009863.png" alt="image-20201028133009863" width="65%;" />

## IV. Binary Tree Traversal Application

如果把表达式$a/b + (c-d)/e$ 放到Tree里，每个leaf是operands, 每个internal nodes是operators.

<img src="11-Binary Tree Traversal.assets/image-20201028133450821.png" alt="image-20201028133450821" width="30%;" />

如果是用in-order traverse，能得到原本的数学表达式，如果是post-order traverse, 能得到逆波兰表达式。

