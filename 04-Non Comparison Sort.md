# 04-Non Comparison Sort

## Objectives

- [ ] 了解三种non-comparison sort: counting sort, bucket sort, radix sort

## I. Counting Sort

### 👎Simple version

- #### 思路

  ​			建立一个比当前array更大的数组，确保新的array大小能够涵盖之前所有integers。然后遍历当前array，把元素值作为下标，对array中该位置++。最后按顺序把每个格子中的数字按照个数打印出来。

- #### 实现方法

<img src="04-Non Comparison Sort.assets/image-20201027150200909.png" width="70%;" />

如果范围是$[a,b]$，那么只需要把每个数减去$a$, 范围转化成$[0, b-a]$。

- #### 存在的问题

  ​			如果只是把i 答应count[i]次，那么无法保证stability。因为可能元素在排序的时候不只有一个key。



### 👌General Version

- #### 思路

  ​			在simple version的基础上，counting array 中的每一格不再是值等于该下标的元素个数，而是把前面项都加起来，意味着counting array的每一格表示值比该格下标小的元素个数。然后通过反向填充，通过从counting array末位开始，把它放在新的位置C[A[i]],并且把C[A[i]]的数量减一。这样做的目的是，不通过countring array来决定最后的排序顺序，而是通过再查找一遍原本array，把每个数所应该在的位置通过counting array来得知。

- #### 实现方式

<img src="04-Non Comparison Sort.assets/image-20201027152811076.png" alt="image-20201027152811076" width="60%;" />

<img src="04-Non Comparison Sort.assets/image-20201027153023097.png" alt="image-20201027153023097" width="45%;" /><img src="/Users/michaelxu/My Document/JI Files/Courses/大三/大三秋/VE281 数据结构与算法/My Notes/04-Non Comparison Sort.assets/image-20201027153122953.png" alt="image-20201027153122953" style="zoom:50%;" />

****



## II. Bucket Sort

- ### 思路

  ​			在之前的counting sort中，忽视了一个问题，如果要排序的数不是整数，而是其他如浮点数之类的则很难比较，因为很难把这些数安排到适当的counting array中。所以引入另一种方法：建立一些bucket，每个bucket是一个小的范围。把数字放进每个bucket后，对bucket 内部进行comparison sort。

- #### 实现方式

<img src="04-Non Comparison Sort.assets/image-20201027153750176.png" alt="image-20201027153750176" width="65%;" />

- #### 时间复杂度

  ​			平均时间复杂度为==$O(N)$==. 因为总共有$cN$个items，$N$个桶，所以每个桶有$c$个元素。对于每个桶进行comparison sort所需的复杂度是$O(c\log c)$, 总体复杂度为$O(N\times O(c\log c) = O(cN) = O(N)$



## III. Radix Sort

- ### 思路

  ​			在bucket sort中存在一个问题，那就是当所给的数字范围特别大时，需要的桶会变多，但是可能中间有许多不需要的空桶，比如说{0, 999, 5000, 888888}。或者说对于手机号码进行bucket sort，会比较困难。但是有个特点，就是每个大的数字也是由每一位0~9的数字组成的，所以可以多次进行桶排序，每次排序按照其中一位进行。排序的结果保留到下一位进行前一位桶排序比较。

- #### 实现方式

<img src="04-Non Comparison Sort.assets/image-20201027154835435.png" alt="image-20201027154835435" width="65%;" />



<img src="04-Non Comparison Sort.assets/image-20201027154927424.png" alt="image-20201027154927424" width="60%;" />

<img src="04-Non Comparison Sort.assets/image-20201027155033957.png" alt="image-20201027155033957" width="60%;" />

<img src="04-Non Comparison Sort.assets/image-20201027155106199.png" alt="image-20201027155106199" width="60%;" />

- #### 时间复杂度

  ​			平均时间复杂度为==$O(kN)$==. 其中$k$ 是所有数字里最长的key的位数。也就意味着进行了$k$ 次桶排序。

