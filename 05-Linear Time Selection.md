# 05-Linear Time Selection

## Objectives

- [ ] 了解randomized selection algorithm
- [ ] 了解deterministic selection algorithm
- [ ] 了解如何分析以上两种selection algorithm的复杂度



## 什么是Selection Problem?

​				给定一个array, 和一个数字i, 选出array 中第 i 小的数字。

例子：`A = (6, 3, 5, 4, 2), i = 3`

​			✅应该返回结果：4



## 解决方法一：直接对数组sorting

​				sorting 之后找出第 i 个元素。时间复杂度是$O(n\log n)$。



## 解决方法二：Randomized Selection

- ### 思路：

  ​			类似于quick sort中的partition, 因为每次在partition结束后都能确定pivot左边的元素都小于等于pivot, pivot右边的元素大于pivot。而且知道pivotAt的位置后可以知道当前比pivot小的有几个，比pivot多的有几个。

  ==例子==：如果要找array中第6小的元素。

  ​			case 1: pivot的位置是4，那么我们下一步找pivot右边数列第二小的元素。

  ​			case 2: pivot的位置是8，那么我们下一步找pivot左边数列第六小的元素。

- ### 实现方式

<img src="05-Linear Time Selection.assets/image-20201027162922040.png" alt="image-20201027162922040" width="60%;" />

#### ⚠️练习：

<img src="05-Linear Time Selection.assets/image-20201027163709690.png" alt="image-20201027163709690" width="70%;" />

> 解析：
>
> B. 当每次选择当pivot都没能分成两个部分，也就是说其中一部分的复杂度是T(0), 那么总体复杂度是n + (n-1) + ......  = $O(n^2)$
>
> D. Best-case 发生的情况是直接找到的pivot 位置正好是i，但是这种情况需要经历一遍partition才能知道pivot的位置，所以runtime是$\theta (1)$.



- ### Rselect的Average Runtime

<img src="05-Linear Time Selection.assets/image-20201027164243035.png" alt="image-20201027164243035" width="60%;" />



- **如何分析Average Runtime**
  - 因为每次递归调用的时候整体array都会缩短，如果pivot落在array的$[\frac{1}{4}, \frac{3}{4}]$的位置，那么最少能够让array长度缩短1/4，最多能让长度缩短3/4，所以平均缩短1/2，而pivot落在1/4～3/4的概率是50%，所以总体平均下来，每次递归后，新的长度 = 1- 1/2 * 50% = 3/4. 	

<img src="05-Linear Time Selection.assets/image-20201027170308967.png" alt="image-20201027170308967" width="50%;" />

​		❓如何理解$E[X_j]$❓

> $E[X_j] \le$ Expected number of times you need to get a good pivot. 比如抛硬币正面向上，E[head] = 2 



## 解决方法三：Deterministic Selection Algorithm

- ### 思路

  - 在先前的random selection中，我们获得good pivot完全依靠随机以及概率。试想能否产生一种方式直接让我们找到的pivot "good enough"?
  - 用=="median of medians"==作为pivot

- ### 实现方式

<img src="05-Linear Time Selection.assets/image-20201027185142980.png" alt="image-20201027185142980" width="60%;" />

<img src="05-Linear Time Selection.assets/image-20201027185250638.png" alt="image-20201027185250638" width="60%;" />

- ### Dselect的Runtime

  ​		Dselect的runtime是$O(n)$，但是跟Rselect比起来，constant更大，所以没有Rselect速度快。而且not in place,因为需要一个额外的array来放n/5 medians.

  

<img src="05-Linear Time Selection.assets/image-20201027185821422.png" alt="image-20201027185821422" width="60%;" />

- **如何分析Average Runtime?**

  ​			在选出了median of median后，把每一组的5个元素从小到大排序，而每组之间的顺序由median比较得出。因此能保证左下角elements都比pivot小，右上角元素都大于pivot。

  <img src="05-Linear Time Selection.assets/image-20201027192239786.png" alt="image-20201027192239786" width="60%;" />

  ​			所以能够删掉的部分至少是左下角的这一块或者是右上角的这一块。

  <img src="05-Linear Time Selection.assets/image-20201027192406511.png" alt="image-20201027192406511" width="35%;" />

  ​			其中左边表示的是能够删掉的元素个数，大约是30%整个array。所以在递归的时候，每次长度变化是变成了上一次递归时候的==0.7==

**⚠️master method不能用，因为在这个过程中有两个recursive call**
$$
T(n) \le cn+ T(\frac{n}{5}) + T(\frac{7n}{10})
$$
最终结果是

<img src="05-Linear Time Selection.assets/image-20201027192839668.png" alt="image-20201027192839668" width="60%;" />

