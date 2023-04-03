# Tips

1. leetcode不能用sizeof()算数组长度，可能原因是把数组名解释为指针

# conclusion from problems

# 模板题：

## #Q2：链表基础

链表基本功：
下面的结构体定义了C++语言中的一种常见的链表节点，包括数据、指针和两种种不同类型的构造函数。

```c++
struct ListNode {
    int val;        //存储数据
    ListNode *next; //next指针
    ListNode() : val(0), next(NULL) {}  //类似构造函数
    ListNode(int x) : val(x), next(NULL) {}
};
```

用new延长链表：注意到，对于尾节点tail，应为

``` c++
tail->next=new ListNode();//wrong:tail=new ListNode();
tail=tail->next;
```

赋值时，用？:语句代替复杂的if else



## #Q75快速排序

用一个i遍历数组

有n种类型即用n-1个指针表示填的位置（全部从左侧开始，若只有两个指针可以一左一右）

注意左侧的指针+1时，右侧的指针也要+1（所有排好的右移一格）

时间复杂度：o(n)

## #Q144等 二叉树前序、中序、后序遍历

迭代模板：

```c++
while(栈非空||结点非空)
{
    while(结点非空)
    {
        stk.push(head);
        head=head->left;
    }
    head=stk.top();
    stk.pop();
    head=head->right;
}
//此方法可以将所有节点过一遍
//在合适的位置进行适当操作
```

递归模板：

```c++
void dfs(tree*node)
{
    /**************/
    if(node==NULL)
    {
        return;
    }
    /**************/
    dfs(tree->left);
    dfs(tree->right);
}
```

## #Q102二叉树BFS

+ 迭代方法：用队列暂存每一层的节点，之后遍历这些队列中的结点，存储结点中值的同时，向队列中再存储这些结点的孩子结点。遍历完成后，再重复此过程（遍历下一层次的所有结点）

``` c++
queue<tree*> que;
que.push(head);
while(!que.empty())
{
    tree* temp=que.front();
    que.pop();
    if(temp->left)
       que.push(temp->left);
    if(temp->right)
       que.push(temp->right);
}
```

+ **递归方法：

## #Q200：岛屿问题

将m*n的坐标图看作图，每个元素都有<=4个与之相邻的元素，则可使用DFS或BFS遍历

核心代码如下：

```c++
//grid是地图坐标系
void dfs(vector<vector<int>> grid,int x,int y)
{
    if(x-1>=0&&grid[x-1][y]是没有被遍历过的陆地)
        dfs(grid,x-1,y);
    if(x+1<grid.size()&&grid[x+1][y]是没有被遍历过的陆地)
        dfs(grid,x+1,y);
    if(y-1>=0&&grid[x][y-1]&&grid[x][y-1]是没有被遍历过的陆地)
        dfs(grid,x,y-1);
    if(y+1<grid[0].size()&&grid[x][y+1]是没有被遍历过的陆地)
        dfs(grid,x,y+1);
}
```

> **防止循环遍历：将遍历过的陆地所在值修改(改为与水和陆地都不一样的值)**
>
> 这样做也可以避免一块面积/一块沿海的周长被重复计算

## #Q463：岛屿周长(上一题的延申)

大致思路和上题dfs一样，有一个代码细节：

```c++
//xx[4]={1,-1,0,0};
//yy[4]={0,0,-1,1};
for(int i=0;i<4;i++)
{
    ans+=dfs(x+xx[i],y+yy[i],grid);
}
//这样可以一下递归完grid[x][y]周围四个格子
```

另注意这个题，需要在dfs函数中初始化ans=0，每次返回ans，每次递归返回的ans相当于这一块地“管辖”的周长总值

## [剑指OFFER41：滑动窗口的平均值]([剑指 Offer II 041. 滑动窗口的平均值 - 力扣（LeetCode）](https://leetcode.cn/problems/qIsx9U/))（核心思想：只更新新的部分，不重新算）

注意到，每次滑动窗口移动只需要加新增的那个数，减去滑出的那个数，不需要每次都对所有求和

## **（#？）[1658. 将 x 减到 0 的最小操作数](https://leetcode.cn/problems/minimum-operations-to-reduce-x-to-zero/)

双指针：初始左指针为-1，右指针为0，若所求和大于x，则右指针右移；否则左指针右移。这样做保证每种情况都能遍历一遍，且复杂度仅为o(n)

注意到，这里求和和上一题一样，不需要每次对左右两边所有数字求和，只需加/减指针移动的那一格就行

注：一般把长度固定的算作滑动窗口，长度不固定的为双指针

> 做错的想法：按题目方式，将左右要求和的总长度从1开始暴力穷举，复杂度过高

## #Q303数组不可变多次求和（一维前缀和）

对于一个int数组nums，每次求下标为left和rightn之间的总和，若数组不变且多次计算，则每次的复杂度均为o(right-left)很大，但若记录从nums[0]到nums[n]的和sum[n]，则每次只需输出sums[right]-sums[left-1]，复杂度为常数

## #Q304矩阵不可变多次求和（二维前缀和，为Q303的进阶）

只需知道[row1,col1,row2,col2]对应的和为

```c++
sums[row2][col2]-sums[row2-1][col1]-sums[row1][col2-1]+sums[row1-1][col1-1]
```

## #[Q2381. 字母移位 II](https://leetcode.cn/problems/shifting-letters-ii/)（一维差分模板题）

差分：将一段数组区间同时加/减某个值用首位、末位后一个进行标记，返回时反过来（类似先求导，再积分）

如对数组下标[2]至[5]进行+2操作：

| 下标              | 0    | 1    | 2     | 3     | 4     | 5     | 6    | 7    |
| ----------------- | ---- | ---- | ----- | ----- | ----- | ----- | ---- | ---- |
| 初始数组          | 1    | 2    | 7     | 3     | 5     | 7     | 8    | 9    |
| 改变后应有的数组  | 1    | 2    | 7+2=9 | 3+2=5 | 5+2=7 | 7+2=9 | 8    | 9    |
| 实际的标记diff[i] | 0    | 0    | 2     | 0     | 0     | 0     | -2   | 0    |

另：对于本题应注意char类型大于127会溢出

## #Q98验证二叉搜索树

+ point1：二叉搜索树与中序遍历的关系

二叉搜索树中序遍历为递增数列

+ point2：增加辅助参数帮助递归

本题中构造helper(TreeNode*root,int min,int max)，引入min和max两个参数帮助判定root是否合法

+ point3：二叉树类似层序遍历的，递归时可以返回function(root->left)&&function(root->right)

## #[Q17. 电话号码的字母组合](https://leetcode.cn/problems/letter-combinations-of-a-phone-number/)：回溯模板题（DFS）

## #[300. 最长递增子序列](https://leetcode.cn/problems/longest-increasing-subsequence/)：记忆化搜索/DP模板题

+ dp数组：

  dp[i]表示拿原数组中第i个的前i项的最值

  注意dp[i]表示的不是一个nums[i]拿不拿，而是前i个

# 细节补充：

## Q387：

unordered_map基本功

声明后不用新增key-value对即可++umap[key]（这是一个全新的key，其值默认初始化为0）

## Q852:

注意数组边缘溢出的情况

（此题为二分查找，实际可能不只有这种情况）会造成访问arr[-1]或arr[arr.size()]的情况

## Q290：一一映射

一一映射需要两个键值对都对应。

# 思考

## 什么情况适合使用一个优先队列？

总需要一个容器中“最大”“最小”，且有其他的小操作不影响之前维护好的队列，（那么就不需要多次排序）便于维护好这样一个堆

例：[Q2530执行 K 次操作后的最大分数](https://leetcode.cn/problems/maximal-score-after-applying-k-operations/)、[414. 第三大的数](https://leetcode.cn/problems/third-maximum-number/)（也可以算）

## 同向双指针&滑动窗口

+ 双指针：涉及连续子数组（e.g.最长的不出现重复字母的子串）

[1658. 将 x 减到 0 的最小操作数](https://leetcode.cn/problems/minimum-operations-to-reduce-x-to-zero/)反向思维可知题目要数组中某个连续子序列为定值

[209. 长度最小的子数组](https://leetcode.cn/problems/minimum-size-subarray-sum/)要某个连续子数组之和大于某个target

[3. 无重复字符的最长子串](https://leetcode.cn/problems/longest-substring-without-repeating-characters/)要某个连续子数组之内不含相同元素

此类题特点：有**连续子数组**，且这个子数组的增长/减少一定会带来不利的影响，满足“只要[l,r]不满足某个要求，那么[l+1，r]也不满足/[l,r+1]也不满足”**(也即一定“单调性”)**

+ 滑动窗口：特定长度连续子数组，提示很明显

[2379. 得到 K 个黑块的最少涂色次数](https://leetcode.cn/problems/minimum-recolors-to-get-k-consecutive-black-blocks/)

## 相向双指针：

+ 有顺序（或先行排序）

  表示的往往是分立的点而不是区间（可能是与同向双指针的区别？）

  分立的数之和（或差、积等）是定值而不是区间nums[i]+nums[j]==target

  （P.S.另一种情况：是区间，则用二分。如"lower<=nums[i]+nums[j]<=upper"->"nums[i]>=lower-nums[j]&&nums[i]<=upper-nums[j]"：[6355. 统计公平数对的数目](https://leetcode.cn/problems/count-the-number-of-fair-pairs/)）

例：

[167. 两数之和 II - 输入有序数组](https://leetcode.cn/problems/two-sum-ii-input-array-is-sorted/)

[15. 三数之和](https://leetcode.cn/problems/3sum/)：对第一个数进行0->n-3遍历，然后另两个数等价于两数之和

P.S.本题另一个小细节：防止重复三元组的出现，三个指针每一个在移动时都要移动至和前一个数不一样的位置

+ “接雨水”类题：前后缀分解+相向双指针

[1237. 找出给定方程的正整数解](https://leetcode.cn/problems/find-positive-integer-solution-for-a-given-equation/)：函数单调增故能用相向双指针

本题也可以用固定x=x0，用二分查找y的方法



## 前缀和与差分：多次算和用前缀和，多次加数用差分

+ 前缀和的功用：

  将**字符串子串的运算（求和等）转化成两点之间的运算**，进而下一步处理<a href="#hash1">一个与哈希表结合的方法见下</a>.

+ 思路有点像前缀和的一题：[1139. 最大的以 1 为边界的正方形](https://leetcode.cn/problems/largest-1-bordered-square/)：算每个点的左、上连续1的个数

+ 异或和：同样也可以用前缀和

  $S_n$=$a_0$一直异或到$a_n$，则$a_i$到$a_j$的异或和为S<sub>j</sub>^S<sub>n-1</sub>

## 半贪心半dp的一种题：

每次讨论新增一个数对前面整体的影响

[1798. 你能构造出连续值的最大数目](https://leetcode.cn/problems/maximum-number-of-consecutive-values-you-can-make/)

## 单调栈

[1124. 表现良好的最长时间段](https://leetcode.cn/problems/longest-well-performing-interval/)

## <a id="hash1">哈希表找到两个数运算为target（不用相向双指针的原因是不单调）</a>

+ 简易题模板：[面试题 17.05.  字母与数字](https://leetcode.cn/problems/find-longest-subarray-lcci/)：遍历原数组，对每个num[i]若能在表中找到target-num[i]，则找到了；否则将num[i]插入表中。这样的复杂度：o(n)
+ 一类用前缀和+哈希表处理：常常处理**子数组内部所有数求值**问题，这里会用到前缀和
  + [面试题 17.05.  字母与数字](https://leetcode.cn/problems/find-longest-subarray-lcci/)：用前缀和算i位置前的字母数与数字数的差值。差值为0->字母与数字相等。此后，用哈希表找到前缀和相等的两个位置的距离最大值
  + [1590. 使数组和能被 P 整除](https://leetcode.cn/problems/make-sum-divisible-by-p/)：和上一题大同小异
  + [2488. 统计中位数为 K 的子数组](https://leetcode.cn/problems/count-subarrays-with-median-k/):

## 二分

+ 题目特点：数组部分升降序/完全升降序，找一个特定需求的值

+ 核心思想：红蓝染色，先找一个点，然后确定目标值在左侧/右侧，目标值不在的那一侧染色(目标值左点红色，目标值及其右点染成蓝色)

[162. 寻找峰值](https://leetcode.cn/problems/find-peak-element/)：对于某组left和right，讨论mid位置的值相对所求值与left、right处的关系，据此更新left或right的值

[153. 寻找旋转排序数组中的最小值](https://leetcode.cn/problems/find-minimum-in-rotated-sorted-array/)：

思路一：（暂且不认为是自然的）mid值和数组最后一位比较，若大于则必然在mid右侧，小于则必然在mid左侧（易得），注意这里不能用双闭区间，因为mid值可能就是所要求的（双闭区间会将left更新为mid+1或将right更新为mid-1）

认为更自然：正常声明left、right，若[mid]>[left]，则left=mid+1，否则right=mid



## 三个数运算暴力枚举的优化

[982. 按位与为零的三元组](https://leetcode.cn/problems/triples-with-bitwise-and-equal-to-zero/)：先将两个数按位与的值存在一个容器中，再第三个数与这个容器中所有数运算



## 状态压缩：



## 递归

+ 递归基本思路：

  > 类似**数学归纳法**：
  >
  > 1.判断出口条件（如二叉树递归到最后的空节点）；这一点类似数学归纳法中k=1的情形
  >
  > 2.从一个问题到下一个子问题

[100. 相同的树](https://leetcode.cn/problems/same-tree/)：

应该return的边界条件：某一棵树遍历到空节点时，看另一棵树这里是否为空来return

递归条件：两个对应节点不相同时return false，否则return子问题

+ 恰当的时候可以在递归参数中加入层数：

[199. 二叉树的右视图](https://leetcode.cn/problems/binary-tree-right-side-view/)：

应该return的边界条件：遍历到NULL的节点

递归条件：从一个节点先调用右孩子再调用左孩子（因右视图先看到右孩子）

如果递归层数等于ans数组长度，将节点值放入ans

## 回溯

### 回溯三问：

> 1.当前操作？是枚举什么？
>
> 2.子问题？
>
> 3.下一个子问题？

[78. 子集](https://leetcode.cn/problems/subsets/)：回溯模板题，两个模板：

+ 1.枚举nums中的每个数，看是否放进去（以输入的视角）

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        n = len(nums)
        ans = []
        temp = []
        def dfs(i):
            if i == n:
                ans.append(temp.copy())
                return
            else:
                dfs(i+1) #nums[i]不放进去
                temp.append(nums[i])
                dfs(i+1) #nums[i]放进去
                temp.pop() #第i个数放进去所有情况讨论完了之后清空temp这一位，防止
        
        dfs(0)
        return ans
```

+ 2.枚举放完nums[i]之后下一个放nums的哪一个（以答案的视角）

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        n = len(nums)
        ans = []
        temp = []
        def dfs(i):
            ans.append(temp.copy())
            if i == n:
                return
            else:
                for j in range(i,n):
                    temp.append(nums[j])
                    dfs(j+1)
                    temp.pop() 
                    # temp这个位置为nums[j]的所有情况讨论完后，要把这个位置清除，以便讨论该位置为其他数的情况
        
        dfs(0)
        return ans
```

### 剪枝：

> 一些问题不需要将所有情况回溯一遍，一些不可能实现的结果直接return掉

+ 方法：

## 思路特殊的题目积累：

（周赛332）[6356. 子字符串异或查询](https://leetcode.cn/problems/substring-xor-queries/)：暴力把字符串能表示的所有二进制数（答案能取到的）全放进容器里，然后无脑查找

[56. 合并区间](https://leetcode.cn/problems/merge-intervals/)：
