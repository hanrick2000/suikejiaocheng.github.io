## 平衡排序二叉树

### 平衡排序二叉树\(Self-balancing Binary Search Tree\)

#### 定义

平衡二叉搜索树又被称为AVL树（有别于AVL算法），且具有以下性质：

* 它是一棵空树或它的左右两个子树的高度差的绝对值不超过1
* 左右两棵子树都是一棵平衡二叉搜索树
* 平衡二叉搜索树必定是二叉搜索树，反之则不一定。

#### 平衡排序二叉树 与 二叉搜索树 对比

也许因为输入值不够随机，也许因为输入顺序的原因，还或许一些插入、删除操作，会使得二叉搜索树失去平衡，造成搜索效率低落的情况。  
![](http://media.jiuzhang.com/markdown/images/3/15/7c52db9e-27ff-11e8-af91-0242ac110002.jpg "AVL")  
比如上面两个树，在平衡树上寻找15就只要2次查找，在非平衡树上却要5次查找方能找到，效率明显下降。

#### 平衡排序二叉树节点定义

Python:

```py

```

#### 常用的实现办法

* AVL树 --&gt;[https://en.wikipedia.org/wiki/AVL\_tree](https://en.wikipedia.org/wiki/AVL_tree)
* 红黑树\(Red Black Tree\) --&gt;[http://blog.csdn.net/v\_july\_v/article/details/6105630](http://blog.csdn.net/v_july_v/article/details/6105630)

### Java中的[TreeSet](https://docs.oracle.com/javase/7/docs/api/java/util/TreeSet.html)/[TreeMap](https://docs.oracle.com/javase/7/docs/api/java/util/TreeMap.html)

TreeSet / TreeMap 是底层运用了[红黑树](https://zh.wikipedia.org/wiki/%E7%BA%A2%E9%BB%91%E6%A0%91)的数据结构

#### 对比 HashSet / HashMap

* HashSet / HashMap 存取的时间复杂度为**O\(1\)**,而 TreeSet / TreeMap 存取的时间复杂度为**O\(logn\)**所以在存取上并不占优。
* HashSet / HashMap 内元素是无序的，而TreeSet / TreeMap 内部是有序的\(可以是按自然顺序排列也可以自定义排序\)。
* TreeSet / TreeMap 还提供了类似[lowerBound](http://www.cplusplus.com/reference/algorithm/lower_bound/)和[upperBound](http://www.cplusplus.com/reference/algorithm/upper_bound/)这两个其他数据结构没有的方法
  * 对于 TreeSet, 实现上述两个方法的方法为：
    * **lowerBound**
      * **public E lower\(E e\)**
        --
        &gt;
         返回set中
        **严格小于**
        给出元素的
        **最大元素**
        ，如果没有满足条件的元素则返回
        **null**
        。
      * **public E floor\(E e\)**
        --
        &gt;
         返回set中
        **不大于**
        给出元素的
        **最大元素**
        ，如果没有满足条件的元素则返回
        **null**
        。
    * **upperBound**
      * **public E higher\(E e\)**
        --
        &gt;
         返回set中
        **严格大于**
        给出元素的
        **最小元素**
        ，如果没有满足条件的元素则返回
        **null**
        。
      * **public E ceiling\(E e\)**
        --
        &gt;
         返回set中
        **不小于**
        给出元素的
        **最小元素**
        ，如果没有满足条件的元素则返回
        **null**
        。
  * 对于 TreeMap, 实现上述两个方法的方法为：
    * **lowerBound**
      * **public Map.Entry**
        **&lt;**
        **K,V**
        **&gt;**
        ** lowerEntry\(K key\)**
        --
        &gt;
         返回map中
        **严格小于**
        给出的key值的
        **最大key**
        对应的
        **key-value对**
        ，如果没有满足条件的key则返回
        **null**
        。
      * **public K lowerKey\(K key\)**
        --
        &gt;
         返回map中
        **严格小于**
        给出的key值的
        **最大key**
        ，如果没有满足条件的key则返回
        **null**
        。
      * **public Map.Entry**
        **&lt;**
        **K,V**
        **&gt;**
        ** floorEntry\(K key\)**
        --
        &gt;
         返回map中
        **不大于**
        给出的key值的
        **最大key**
        对应的
        **key-value对**
        ，如果没有满足条件的key则返回
        **null**
        。
      * **public K floorKey\(K key\)**
        --
        &gt;
         返回map中
        **不大于**
        给出的key值的
        **最大key**
        ，如果没有满足条件的key则返回
        **null**
        。
    * **upperBound**
      * **public Map.Entry**
        **&lt;**
        **K,V**
        **&gt;**
        ** higherEntry\(K key\)**
        --
        &gt;
         返回map中
        **严格大于**
        给出的key值的
        **最小key**
        对应的
        **key-value对**
        ，如果没有满足条件的key则返回
        **null**
        。
      * **public K higherKey\(K key\)**
        --
        &gt;
         返回map中
        **严格大于**
        给出的key值的
        **最小key**
        ，如果没有满足条件的key则返回
        **null**
        。
      * **public Map.Entry**
        **&lt;**
        **K,V**
        **&gt;**
        ** ceilingEntry\(K key\)**
        --
        &gt;
         返回map中
        **不小于**
        给出的key值的
        **最小key**
        对应的
        **key-value对**
        ，如果没有满足条件的key则返回
        **null**
        。
      * **public K ceilingKey\(K key\)**
        --
        &gt;
         返回map中
        **不小于**
        给出的key值的
        **最小key**
        ，如果没有满足条件的key则返回
        **null**
        。
  * lowerBound 与 upperBound 均为二分查找\(因此要求有序\)，时间复杂度为
    **O\(logn\)**
    .

#### 对比 PriorityQueue\(Heap\)

**PriorityQueue**是基于Heap实现的，它可以保证队头元素是优先级最高的元素，但其余元素是不保证有序的。

* 方法时间复杂度对比：
  * 添加元素 add\(\) / offer\(\)
    * TreeSet: O\(logn\)
    * PriorityQueue: O\(logn\)
  * 删除元素 poll\(\) / remove\(\)
    * TreeSet: O\(logn\)
    * PriorityQueue: O\(n\)
  * 查找 contains\(\)
    * TreeSet: O\(logn\)
    * PriorityQueue: O\(n\)
  * 取最小值 first\(\) / peek\(\)
    * TreeSet: O\(logn\)
    * PriorityQueue: O\(1\)

#### 常见用法

比如滑动窗口需要保证有序，那么这时可以用到TreeSet,因为TreeSet是有序的，并且不需要每次移动窗口都重新排序，只需要插入和删除\(O\(logn\)\)就可以了。

注：在 C++ 中类似的结构为 set / map。在Python中没有内置的TreeSet、TreeMap，需要使用第三方库或者自己实现。

#### 练习

[http://www.lintcode.com/problem/consistent-hashing-ii/](http://www.lintcode.com/problem/consistent-hashing-ii/)



