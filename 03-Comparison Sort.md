[TOC]



# 03-Comparison Sort

## Objectives

- [ ] 知道comparison和non-comparison sort的区别
- [ ] 知道merge sort和quick sort的过程
- [ ] 知道什么是master theorem
- [ ] 知道不同sorting algorithms之间的特点，比如时间复杂度、稳定性等等

## Characteristics of Sorting Algorithms

三个重要特征：

1. **Average-case time complexity**
2. **Worst-case time complexity**
3. **Space usage** (**in place** or not)
4. **Stability** : 是否保留原有顺序



## I. Insertion Sort

- **思路**：每次把array中拿出一个元素，跟左边已经排好序的array进行比较，放入正确的位置，直到每个元素都被取完。
- **实现方式**：

<img src="03-Comparison Sort.assets/image-20201026213604109.png" alt="image-20201026213604109" style="zoom:50%;" />

- **具体代码**：

<img src="03-Comparison Sort.assets/image-20201026213906298.png" alt="image-20201026213906298" style="zoom:50%;" />



