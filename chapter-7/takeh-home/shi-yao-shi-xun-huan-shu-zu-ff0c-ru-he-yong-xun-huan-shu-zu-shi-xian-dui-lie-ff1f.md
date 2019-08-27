## 什么是循环数组，如何用循环数组实现队列？

#### 什么是循环数组

> Circular array = a data structure that used a**array**as if it were**connected end-to-end**

**可以图示为：**

![](http://media.jiuzhang.com/markdown/images/4/4/403995f8-37d6-11e8-ae7b-0242ac110002.jpg "circular array")

#### 如何实现队列

1. 我们需要知道队列的入队操作是只在队尾进行的，相对的出队操作是只在队头进行的，所以需要两个变量front与rear分别来指向队头与队尾
2. 由于是循环队列，我们在增加元素时，如果此时 rear = array.length - 1 ，rear 需要更新为 0；同理，在元素出队时，如果 front = array.length - 1, front 需要更新为 0. 对此，我们可以通过对数组容量取模来更新。

#### 示例代码

Python:

```py
class CircularQueue:
    def __init__(self, n):
        self.circularArray = [0]*n
        self.front = 0
        self.rear = 0
        self.size = 0
        
    """
    @return:  return true if the array is full
    """
    def isFull(self):
        return self.size == len(self.circularArray)

    """
    @return: return true if there is no element in the array
    """
    def isEmpty(self):
        return self.size == 0

    """
    @param element: the element given to be added
    @return: nothing
    """
    def enqueue(self, element):
        if self.isFull():
            raise RuntimeError("Queue is already full")
        self.rear = (self.front+self.size) % len(self.circularArray)
        self.circularArray[self.rear] = element
        self.size += 1

    """
    @return: pop an element from the queue
    """
    def dequeue(self):
        if self.isEmpty():
            raise RuntimeError("Queue is already empty")
        ele = self.circularArray[self.front]
        self.front = (self.front+1) % len(self.circularArray)
        self.size -= 1
        return ele

```

#### 在线练习

[http://www.lintcode.com/zh-cn/problem/implement-queue-by-circular-array/\#](http://www.lintcode.com/zh-cn/problem/implement-queue-by-circular-array/#)

  




