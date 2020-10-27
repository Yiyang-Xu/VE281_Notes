[TOC]



# 03-Comparison Sort

## Objectives

- [ ] 知道comparison和non-comparison sort的区别
- [ ] 知道merge sort和quick sort的过程
- [ ] 知道什么是master theorem
- [ ] 知道不同sorting algorithms之间的特点，比如时间复杂度、稳定性等等

## Characteristics of Sorting Algorithms

**三个重要特征：**

1. **Average-case time complexity**
2. **Worst-case time complexity**
3. **Space usage** (**in place** or not)
4. **Stability** : 是否保留原有顺序



## I. Insertion Sort

- ### 思路

  ​		每次把array中拿出一个元素，跟左边已经排好序的array进行比较，放入正确的位置，直到每个元素都被取完。

- ### 实现方式

<img src="03-Comparison Sort.assets/image-20201026213604109.png" alt="image-20201026213604109" style="zoom:50%;" />

- ### 具体代码

<img src="03-Comparison Sort.assets/image-20201026213906298.png" alt="image-20201026213906298" style="zoom:50%;" />

- ### 特性分析

  - **时间复杂度**：==$O(n^2)$==, 因为对于每个元素都要挑出来，再与前面已经排好的进行比较，所以n*n
  - **是否In place?** ==是==，因为每次只拿出一个元素进行比较，$O(1)$ additional memory.
  - **Stability:** ==是==，因为没有涉及到swap，而且取出牌有先后顺序，所以当两个元素有相同key的时候相对顺序不变，自己设置只有当严格小于时才放入某个元素前。

  

## II. Selection sort

- ### 思路

  ​		左边是已经排好序的数列, 每次从右边找出最小的元素,放到左边数列最后一个.

- ### 实现方式

<img src="03-Comparison Sort.assets/image-20201027121934576.png" alt="image-20201027121934576" style="zoom:50%;" />

- ### 具体代码

<img src="03-Comparison Sort.assets/image-20201027122443411.png" alt="image-20201027122443411" style="zoom:80%;" />

- ### 特性分析
  - **时间复杂度**：==$O(n^2)$==, 因为对于每个被挑出来的元素都要经历一遍linear scan, 所以是n*n; 同时worst case与best case都是$n^2$
  - **是否In place?** ==否==，因为需要一个额外的array来存放已经排好序的元素.
  - **Stability:** ==否==，因为涉及到swap.



## III. Bubble Sort

- ### 思路

  ​		对于数列遍历一遍,如果下一个元素小于当前元素,那么交换两者位置,直到数列末尾. 所以通过这种方式,每一次遍历结束都能够找到数列中最大/最小的元素,接着从再对剩下的进行bubble sort遍历.

- ### 具体代码

<img src="/Users/michaelxu/My Document/JI Files/Courses/大三/大三秋/VE281 数据结构与算法/My Notes/03-Comparison Sort.assets/image-20201027123731520.png" alt="image-20201027123731520" style="zoom:50%;" />

- ### 特性分析

  - **时间复杂度**：==$O(n^2)$==, 因为对于每个被挑出来的元素都要经历一遍与数列中剩下元素的比较bubble交换, 所以是n*n; 同时worst case与best case都是$n^2$
  - **是否In place?** ==是==，因为只是swap,不需要用到额外空间 (相比selection sort, bubble sort的思路相同,每次都是找出一个最小的放到最后,但是这个过程是通过swap来实现).
  - **Stability:** ==是==，因为自己可以定义swap的方法,而且每次只是跟自己的邻居交换.



## IV. Merge sort

- ### 思路

  ​		通过递归把数列打散成单个元素,然后在一步步返回的时候merge.

- ### 实现方式

<img src="03-Comparison Sort.assets/image-20201027124401454.png" alt="image-20201027124401454" style="zoom:50%;" />

- ### 具体代码

<img src="03-Comparison Sort.assets/image-20201027124737997.png" alt="image-20201027124737997" style="zoom:50%;" />

<img src="03-Comparison Sort.assets/image-20201027124813295.png" alt="image-20201027124813295" style="zoom:50%;" />

- ### 特性分析

  - **时间复杂度**：==$O(n\log n)$==, 在每个merge的过程中,复杂度是$O(sizeA + sizeB)$,因为我们不需要移除元素,A 和B都是已经排好序的,所以只需要一个指针来指出最小的那个元素append就可以了.在函数调用的过程中, 递归调用, 所以复杂度等于$T(N) = 2\times T(N/2)+ O(N)$. 其中$O(N)$是merge的复杂度.解出最终总体时间复杂度是$O(n\log n)$
  - **是否In place?** ==否==，每次merge的时候我们都需要一个左array和右array进行merge,然后返回一个左+右的结果.
  - **Stability:** ==是==，因为在merge的时候,在左边的一直在左边,相对位置一直没有发生变化.



## V. Quick Sort

- ### 思路:

  ​		类似于merge sort,都是采用分治(divide and conquer)思想, 每次在调用partition函数,选择出一个pivot放到正确位置(pivot左边的元素都小于等于pivot, 右边的都大于pivot). 然后再对pivot左边所有元素quick sort, 对右边所有元素quick sort.

- ### 实现方式:

<img src="03-Comparison Sort.assets/image-20201027130403934.png" alt="image-20201027130403934" style="zoom:50%;" />

 **⚠️但是在partition这部分有两种: In place or Not In place的实现方法⬇️**

****

#### Extra-Place partitioning

- ##### 思路

<img src="03-Comparison Sort.assets/image-20201027130735565.png" alt="image-20201027130735565" style="zoom:50%;" />

- ##### 代码实现

<img src="03-Comparison Sort.assets/image-20201027130928338.png" alt="image-20201027130928338" style="zoom:50%;" />

- ##### 简要说明:

  ​	因为每次把pivot放到正确位置都需要两个sub-array,所以需要额外空间

****

#### In-Place Partitioning

- ##### 思路

  ​	找到pivot以后从左右两边同时开始搜索,直到左边哨兵找到比当前pivot大,右边哨兵找到比当前pivot小的元素,且左哨兵的位置在右哨兵的左边(说明两个元素的位置错了),那么交换两个元素.

<img src="03-Comparison Sort.assets/image-20201027131431635.png" alt="image-20201027131431635" style="zoom:50%;" />

- ##### 代码实现

<img src="03-Comparison Sort.assets/image-20201027131318612.png" alt="image-20201027131318612" style="zoom:50%;" />

- ##### 简要说明:

  ​	因为每次把pivot放到正确位置是通过交换来实现的,所以不需要额外空间

****

- ### Quick sort代码实现

<img src="03-Comparison Sort.assets/image-20201027131809626.png" alt="image-20201027131809626" style="zoom:50%;" />

⚠️无论是in-place还是non-inlace,调用的时候都是一样的,只是在partitioning的部分有所不同.



- ### 特性分析

  ​		在每个partioning的过程中,时间复杂度都是$O(N)$,因为只是指针遍历一遍,然后交换元素. 所以整体的时间复杂度是$T(N) = T(LeftSz) + T(RightSz) + O(N)$.所以当worst case的时候,如果每次选中的pivot都是当前最小元素时, $T(RightSz)$始终为0, 总体复杂度为$O(N^2)$.

<img src="03-Comparison Sort.assets/image-20201027132419211.png" alt="image-20201027132419211" style="zoom:50%;" />

​				而从平均角度, 每次pivot都刚好把array分成两部分, 那么复杂度跟merge sort是相同的.

<img src="03-Comparison Sort.assets/image-20201027132540673.png" alt="image-20201027132540673" style="zoom:50%;" />

**⚠️与merge sort的比较:**

​				merge sort是先分成小的,再通过比较合并成大的;

​				quick sort是先把大的比较好, 左右分配成正确的再分别对左右进行sort.

**⚠️与insertion sort的比较:**

​				在array的size比较小的时候, insertion sort的速度比quick sort更快.

****



## Comparison Sort总结:

<img src="03-Comparison Sort.assets/image-20201027133037364.png" alt="image-20201027133037364" style="zoom:50%;" />

**⚠️是否能够比$O(n\log n)$复杂度更低?**

​				答: ==不能==, 基于pairwise比较低复杂度都是$\Omega (N\log N)$

<img src="03-Comparison Sort.assets/image-20201027133338746.png" alt="image-20201027133338746" style="zoom:50%;" />



## 重要知识点：Master Method

<img src="03-Comparison Sort.assets/image-20201027135825684.png" alt="image-20201027135825684" width="500" />

