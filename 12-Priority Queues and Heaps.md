# 12-Priority Queues and Heaps

## I. Objectives

- [ ] 知道什么是priority queue
- [ ] 知道什么是min heap
- [ ] 知道min heap是如何实现enqueue和extractMin 操作的
- [ ] 知道如何便捷得初始化一个min heap



## II. Priority Queues

- ### 什么是min priority queue?

  每个元素都有个key ("priority")

  支持一下操作：

  - **isEmpty**
  - **size**
  - **Enqueue**: 把元素放入
  - **dequeueMin**：把有着min key的元素移除
  - **getMin**：get item with min key

  也就是说，这个queue总是知道当前那个元素是最小的，如果是用array来实现，需要的复杂度是

  | Operation      | Complexity         |
  | -------------- | ------------------ |
  | **isEmpty**    | $O(1)$             |
  | **size**       | **$O(1) or O(n)$** |
  | **Enqueue**    | **$O(1)$**         |
  | **dequeueMin** | $O(n)$             |
  | **getMin**     | $O(n)$             |

  而在Priority Queue中

  | Operation      | Complexity      |
  | -------------- | --------------- |
  | **isEmpty**    | $O(1)$          |
  | **size**       | **$O(1）$**     |
  | **Enqueue**    | **$O(\log n)$** |
  | **dequeueMin** | $O(\log n)$     |
  | **getMin**     | $O(1)$          |

- ### 什么是Min Heap?

  Min heap 是一个complete binary heap（只有最后一层可以不full, 而且是populate从左到右）, 而且是一个Tree, 在这个binary tree中，任何一个节点都比自己subtree中任何一个元素要小

<img src="12-Priority Queues and Heaps.assets/image-20201028135506793.png" alt="image-20201028135506793" width="65%;" />

<img src="12-Priority Queues and Heaps.assets/image-20201028135719698.png" alt="image-20201028135719698" width="65%;" />

## III. Min Heap Implementation

- **isEmpty()**: return size==0;
- **size()**: return size;
- **getMin**: return heap[1];

- ### Enqueue

  ​	先把需要插入的新元素放在最后的空的位置。然后通过percolateUp找到其正确的位置。

  <img src="12-Priority Queues and Heaps.assets/image-20201028141326877.png" alt="image-20201028141326877" width="65%;" />

```c++
void minHeap::percolateUp (int id){
  while (id > 1 && heap[id/2] > heap[id]){//parent 比 child大，交换两者位置
    swap(heap[id], heap[id/2]);
    id = id/2; // 换完位置后，id变成原来1/2，再去跟自己的parent比较
  }
}

void minHeap::enqueue (Item newItem){
  heap[++size] = newItem;
  percolateUp(size);
}
```

时间复杂度是$O(\log n)$。

- ### dequeueMin

- #### 思路

  先把heap顶的元素跟heap中最后一个元素交换。现在对heap顶的元素percolate down。每次去跟两个children比较大小，如果key比自己两个children都小，那么把这个元素跟小的那个child交换。

  <img src="12-Priority Queues and Heaps.assets/image-20201028142937875.png" alt="image-20201028142937875" width="60%;" />

```c++
void minHeap::percolateDown (int id){
  for (j = 2*id; j < size; j = 2*id){//每次j更新成2*id，也就是当前这个节点的left child
    if（j < size && heap[j] > heap[j+1]) j++; //如果left child > right child，那么把j更新成right children
    if (heap[id] <= heap[j]) break;
    swap(heap[id], heap[j]);
    id = j;
  }
}

Item minHeap::dequeueMin(){
  swap(heap[1], heap[size--]);
  percolateDown(1);
  return heap[size+1];//把当前放在最后的一个返回
}
```

什么时候可以停下？

> 当目前已经reach leaf node或者两个children的key 都大于等于自己



## IV. Initializing a Min Heap

- ### Simple Solution

  每次插入一个元素。每次insert的复杂度是$O(\log k)$, 所以完整构建需要的复杂度是$O(n\log n)$

- ### 更好的做法：

  先按照array顺序建立一个complete binary tree。

  接着从最大的non-leaf节点开始（size / 2）一直到1，percolateDown(i). 之所以从最大的non leaf开始到1做一个反向操作是因为如果是从顶开始，每次顶部元素都会被更新换掉，需要多次从头遍历检查是否排序好了。而从底部可以保证遍历一遍就能确定每个顺序。

<img src="12-Priority Queues and Heaps.assets/image-20201028151025246.png" alt="image-20201028151025246" width="60%;" />

<img src="12-Priority Queues and Heaps.assets/image-20201028151059862.png" alt="image-20201028151059862" width="60%;" />

<img src="12-Priority Queues and Heaps.assets/image-20201028151131347.png" alt="image-20201028151131347" width="60%;" />

<img src="12-Priority Queues and Heaps.assets/image-20201028151156189.png" alt="image-20201028151156189" width="60%;" />

<img src="12-Priority Queues and Heaps.assets/image-20201028151226839.png" alt="image-20201028151226839" width="60%;" />

- ### 复杂度分析

  因为在level k,总共有$2^k$个node, 每个node最多交换$（h-k）$ 次，h是树的高度。所以在worst case

  <img src="12-Priority Queues and Heaps.assets/image-20201028151858499.png" alt="image-20201028151858499" width="50%;" />

<img src="12-Priority Queues and Heaps.assets/image-20201028152137550.png" alt="image-20201028152137550" width="60%;" />