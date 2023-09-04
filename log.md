> 本文档为我学习算法并刷leetcode的日志文档，主要用于个人记录每日学习进展

### 2023.8.18

[1388. 3n 块披萨](https://leetcode.cn/problems/pizza-with-3n-slices/)：

js二维数组巩固；

循环数组dp巩固；

### 2023.8.19

[29. 两数相除](https://leetcode.cn/problems/divide-two-integers/):

对于int溢出非常麻烦，没有想到合适的解法

<mark>需要重刷</mark>

[24. 两两交换链表中的节点](https://leetcode.cn/problems/swap-nodes-in-pairs/)：

想了个递归写法，链表递归相较以前有进步

[7. 整数反转](https://leetcode.cn/problems/reverse-integer/):

不难的模拟，主要处理好

[2101. 引爆最多的炸弹](https://leetcode.cn/problems/detonate-the-maximum-bombs/)：

就是一个简单的BFS

不知道为什么，每次重开一个vector(n,0)会超时，但是将vector重新赋值每个位置为0就不会，甚至击败90%

resize(n,0)貌似不能用，用循环赋值。

### 2023.8.21

[2337. 移动片段得到字符串](https://leetcode.cn/problems/move-pieces-to-obtain-a-string/)：

思路不难，注意边界溢出和极端情况讨论。一个指针到头，另一个可能没到。

### 2023.9.4 

前一段时间准备GRE忘了记录（可能也没有特别特殊值得记录的）

[449. 序列化和反序列化二叉搜索树](https://leetcode.cn/problems/serialize-and-deserialize-bst/)：今日每日一题的核心之前没见过，题为后序遍历+中序遍历确定一颗二叉树；已学会，后可能要<mark>复习</mark>

母题：[106. 从中序与后序遍历序列构造二叉树](https://leetcode.cn/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)今天用三种语言实现了

补充了一下Java以及JavaScript的Map的写法，补充了一下Java一部分关于字符串与数组、字符串与数字转换的内容。

### 同一天（2023.9.4）补记一下之前一条还算重要的一题：

[84. 柱状图中最大的矩形](https://leetcode.cn/problems/largest-rectangle-in-histogram/)：hard中可能算简单，就是找到每一个竖长条（水平方向长度为单位一的）两侧最近的比他矮的长条，然后算每个矩形的面积取最大。用单调栈就可以实现了，不难。（当时应该是自己想出来了就没记录）

