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

### 2023.9.6

[1123. 最深叶节点的最近公共祖先](https://leetcode.cn/problems/lowest-common-ancestor-of-deepest-leaves/)：咋看不难的二叉树模拟，设计递归花了一些时间（个人认为自己设计的比较有趣而反常规）

```java
class Solution {
    private int height;
    private TreeNode ans;
    public TreeNode lcaDeepestLeaves(TreeNode root) {
        this.height=calculateHeight(root);
        ans=null;
        findNode(root, 0);
        return ans;
    }
    public int calculateHeight(TreeNode root){
        if(root==null){
            return 0;
        }
        return Math.max(calculateHeight(root.left),calculateHeight(root.right))+1;
    }
    public boolean findNode(TreeNode root, int depth){
        if(root==null){
            if(depth==height){
                return true;
            }else{
                return false;
            }
        }
        boolean checkLeft=findNode(root.left,depth+1);
        boolean checkRight=findNode(root.right,depth+1);
        if(checkLeft&&checkRight){
            ans=root;
            return true;
        }else if(checkLeft||checkRight){
            return true;
        }else{
            return false;
        }
    }
}
```

### 2023.9.7

一道二分答案题，开始没想到这一点，而是想到了优先队列，但因为设计不出来n->n+1很好的方法而放弃。事实上或许很多能用priority_queue的题有很大概率是二分？

[2594. 修车的最少时间](https://leetcode.cn/problems/minimum-time-to-repair-cars/)

做了一下周赛361，Q3注意“前缀和+哈希表查找“两数之和”“的套路配合取模又可以更进一层

[2845. 统计趣味子数组的数目](https://leetcode.cn/problems/count-of-interesting-subarrays/)

### 2023.9.8

重新更新了一下对BFS的认知，不存在什么递归，就是拿队列直接迭代写

[1926. 迷宫中离入口最近的出口](https://leetcode.cn/problems/nearest-exit-from-entrance-in-maze/)

[1031. 两个非重叠子数组的最大和](https://leetcode.cn/problems/maximum-sum-of-two-non-overlapping-subarrays/)：一道有趣的DP+前缀和题目，写到O(n)的时间复杂度并不容易

### 2023.9.10

百度之星看了两道题，题解思路自然，但是明显比力扣medium复杂（或者是风格不一样）

[BD202301公园]([码题集OJ-公园 (matiji.net)](https://www.matiji.net/exam/brushquestion/1/4347/179CE77A7B772D15A8C00DD8198AAC74)): 常规的BFS+提升

[BD202302蛋糕划分]([码题集OJ-蛋糕划分 (matiji.net)](https://www.matiji.net/exam/brushquestion/2/4347/179CE77A7B772D15A8C00DD8198AAC74)): 思路就是二分答案，但是check的方法比较难想

力扣周赛362

第三题暴力回溯回来看文档了，有一段时间没写了，还需要加强

[380. O(1) 时间插入、删除和获取随机元素](https://leetcode.cn/problems/insert-delete-getrandom-o1/)：之前留的坑，回来补上。注意remove函数需要把最后一个数移到remove这个数的位置

### 2023.9.11

百度之星a了一条二分答案

每日一题一个新知识点：贪心+后悔堆

### 2023.9.12

每日一题：[1462. 课程表 IV](https://leetcode.cn/problems/course-schedule-iv/)没想到拓扑排序，用暴力dfs+记忆化搜索勉强过了。看评论貌似写法还挺多的：1. 最短路 先把两个点之间是否联通跑了，后面查找就o(1)了；2. 拓扑排序；3. 类似并查集把每个节点下面的节点都标记了

### 2023.9.14

题目不难，但是好思路不好想:

[1222. 可以攻击国王的皇后](https://leetcode.cn/problems/queens-that-can-attack-the-king/)可以从国王出发

### 2023.9.19

好几天没记录了，把最近几天比较有价值的题目拿来记录一下

[LCP 34. 二叉树染色](https://leetcode.cn/problems/er-cha-shu-ran-se-UGC)：树形DP模板题，关键在于每棵子树根节点位置**每一种连续染色长度**的状态，返还给其父节点。这题搞懂以后，[337. 打家劫舍 III](https://leetcode.cn/problems/house-robber-iii)就是它的一种特殊情况

[85. 最大矩形](https://leetcode.cn/problems/maximal-rectangle)：从二维矩阵图中抠出来一些高度数组后即可转化为[84. 柱状图中最大的矩形](https://leetcode.cn/problems/largest-rectangle-in-histogram)。

[32. 最长有效括号](https://leetcode.cn/problems/longest-valid-parentheses)：用栈很容易想，但是重要的是这题要把最后一个')'放在栈底

### 2023.9.21

[310. 最小高度树](https://leetcode.cn/problems/minimum-height-trees)：两种解法，换根DP和拓扑排序，都很有启发性



