# 04-Non Comparison Sort

## Objectives

- [ ] 了解三种non-comparison sort: counting sort, bucket sort, radix sort

## I. Counting Sort

### Simple version

- #### 思路

  ​			建立一个比当前array更大的数组，确保新的array大小能够涵盖之前所有integers。然后遍历当前array，把元素值作为下标，对array中该位置++。最后按顺序把每个格子中的数字按照个数打印出来。

- #### 实现方法

<img src="04-Non Comparison Sort.assets/image-20201027150200909.png" style="zoom:50%;" />

如果范围是$[a,b]$，那么只需要把每个数减去$a$, 范围转化成$[0, b-a]$。



### General Version

