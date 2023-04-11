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

+ 单调栈模板：

[496. 下一个更大元素 I](https://leetcode.cn/problems/next-greater-element-i/)：

一个形象的理解：后面的矮个被前面的高个“挡住了”，故从后向前遍历，遍历后入栈。若碰到一个“高个”（即大于后面的至少一个数），那么后面的矮个对这个高个前面的所有数就没有价值了，故弹出这些矮个，高个入栈。

```c++
vector<int> nextGreaterElement(vector<int>& nums) {
    vector<int> ans(nums.size()); // 存放答案的数组
    stack<int> s;
    for (int i = nums.size() - 1; i >= 0; i--) { // 倒着往栈里放
        while (!s.empty() && s.top() <= nums[i]) { // 判定个子高矮
            s.pop(); // 矮个起开，反正也被挡着了。。。
        }
        ans[i] = s.empty() ? -1 : s.top(); // 这个元素身后的第一个高个
        s.push(nums[i]); // 进队，接受之后的身高判定吧！
    }
    return ans;
}
```

另一种写法：

从前面i=0开始遍历，先比较该节点与栈顶的大小，遇到符合情况的更新答案并出栈；将该节点入栈；直到所有节点遍历完毕

这一点在[1019. 链表中的下一个更大节点](https://leetcode.cn/problems/next-greater-node-in-linked-list/)这题中体现，此题为链表，不能从后向前遍历

```python
def nextLargerNodes(self, head: Optional[ListNode]) -> List[int]:
    stk = list()
    ans = list()
    cur = head
    idx = -1
    while cur != None:
        idx+=1
        ans.append(0)
        while stk and stk[-1][1] < cur.val:
            ans[stk[-1][0]] = cur.val
            stk.pop()
        stk.append((idx,cur.val))
        cur = cur.next
    return ans
```

+ 解决一段子数组的和>target的最长问题

先把子数组的和通过前缀和转化为两点之差，然后等价于上面的矮个高个，(左边的数+target<右边的数)

不同的是，这里需要找到右边最后一个“高个”而不是第一个“高个”，故模板不一样

[1124. 表现良好的最长时间段](https://leetcode.cn/problems/longest-well-performing-interval/)：

理解一下：若j>i时sums[j]>sums[i]，则j不可能作为左侧数（i肯定比j赚），故j不入栈

再从右边遍历到左边找最大

```c++
int longestWPI(vector<int>& hours) {
    int ans=0;
    stack<int> stk;
    int n = hours.size();
    vector<int> sums(n+1,0);
    stk.push(0);
    for(int i=0;i<n;i++)
    {
        if(hours[i]>8)
            sums[i+1]=sums[i]+1;
        else
            sums[i+1]=sums[i]-1;
        if(sums[i+1]<sums[stk.top()])
        {
            stk.push(i+1);
        }
    }
    for(int j=n;j>0;j--)
    {
        while(!stk.empty()&&sums[j]>sums[stk.top()])
        {
            ans = max(ans,j-stk.top());
            stk.pop();
        }
    }
    return ans;
}
```

<mark>这题看上去和常规的单调栈有一些不同，因这题是找最远距离而非最长距离，所以需要先从左边遍历入栈，再从右边遍历更新答案</mark>

## 单调队列

+ 解决一段子数组的和>target的最短问题

[862. 和至少为K的最短子数组](https://leetcode.cn/problems/shortest-subarray-with-sum-at-least-k/)：

为什么不能用同向双指针？数据流中有负数，不能确定每次指针移动对子数组的和是亏是赚

先算出前缀和，将子数组的和转化为分立的两点之差（通过这种方法也一定程度上解决了有负数的问题）

然后遍历前缀和数组sums，对sums[i]讨论，

若sums[i] - sums[deq.front()] >= target，则这可能是答案，故更新答案；且可能存在更优解，但以deq.front()开始的数组一定不可能是更优解了，故deq.pop_front()

若sums[i] <= sums[deq.back()]，则最优解不可能以deq.back()开头了（因为以i开头的一定更优），故deq.pop_back()

讨论完后将i插入队列

```c++
class Solution {
public:
    int shortestSubarray(vector<int>& nums, int k) {
        int n=nums.size();
        vector<long long> sums(n+1,0);
        for(int i=0;i<n;i++)
        {
            sums[i+1] = sums[i] + nums[i];
        }
        int ans = n+1;
        deque<int> que;
        for(int i=0;i<n+1;i++)
        {
            while(!que.empty()&&sums[i]-sums[que.front()]>=k)
            {
                ans = min(ans,i-que.front());
                que.pop_front();
            }
            while(!que.empty()&&sums[i]<=sums[que.back()])
            {
                que.pop_back();
            }
            que.push_back(i);
        }
        if(ans<n+1)
        return ans;
        else
        return -1;
    }
};
```

### 单调队列和同向双指针

[209. 长度最小的子数组](https://leetcode.cn/problems/minimum-size-subarray-sum/)：

因为本题所有数均为正数，故当一段和>=target时，必然左指针右移是赚的，故可以用双指针做。用单调队列依然可行，但是空间复杂度会更高



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

用一个二进制数表示一种状态，常用于【选或不选】这一思路中

这是一个技巧而非一种算法

## 快速幂：

对于指数n，底数a，o(log n)复杂度计算某数的幂

将n化成二进制，假设n=19，化为10011,则

a^19^=a<sup>2<sup>0</sup>+2<sup>1</sup>+2<sup>4</sup></sup>=a·a<sup>2</sup>·{[(a<sup>2</sup>)<sup>2</sup>]<sup>2</sup>}<sup>2</sup>

故可用位运算的方法，用一数temp存储a的2<sup>i</sup>次幂（i从1到n的二进制位数）逢位数为1时ans*=temp

```C++
double cal(double a,long long n)
{
    if(n==0)
    {
        return 1;
    }
    double ans = 1;
    double temp = a;
    while(n>0)
    {
        if(n&1)
        {
            ans*=temp;
        }
        temp *= temp;
        n = n>>1;
    }
    return ans;
}
double myPow(double x, int n) {
    long long N= n;
    if(N>=0)
    {
        return cal(x,N);
    }
    else
    {
        return 1.0/cal(x,-N);
    }
}
```



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
                temp.pop() #第i个数放进去所有情况讨论完了之后清空temp这一位，否则枚举下一个数的时候这个数还没清掉
        
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

### 排列型回溯

+ [46. 全排列](https://leetcode.cn/problems/permutations/)：排列型回溯模板题

递归参数用层数+还没枚举到的数的集合表示

```python
ans = []
n = len(nums)
path = [0] * n

def dfs(i,s):  # s用来表示还没枚举到的所有数的集合
    if i == n: # 出口条件：所有数字都填进来了，即填了n个数字了
        ans.append(path.copy()) # 一定要复制副本！
        return
    for num in s:
        path[i] = num
        dfs(i+1,s-{num})

dfs(0,set(nums))
return ans
```

==血泪教训：一定要复制副本path.copy()，而不是直接将path给append进去==

另一种写法：不将还没列举到的数用集合放到递归参数中，而是作为全局变量显示哪种还没放进去

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        ans = []
        n = len(nums)
        check = [False] * n
        path = [0] * n
        def dfs(i):
            if i == n:
                ans.append(path.copy())
                return
            for j in range(n):
                if check[j] == False:
                    path[i] = nums[j]
                    check[j] = True
                    dfs(i+1)
                    check[j] = False
        dfs(0)
        return ans
```



+ 进阶：[51. N 皇后](https://leetcode.cn/problems/n-queens/)：

基本原理：对于n*n棋盘要放n个皇后，必然有每行、每列各一个

那么对于以行号为索引的列表，必然是1~n-1的一个排列

如：

```python
.Q.. # 第1列
...Q # 第3列
Q... # 第0列
..Q. # 第2列
```

对应：

```python
[1,3,0,2]
```

故问题转化为排列型回溯

此外，还需验证一下对角线不能放置，这个在每行放的时候验证一下

+ 递归入口：从第0行开始枚举

+ 递归出口：当n行枚举完后，将答案放入ans中

+ 从一个子问题到另一个子问题：放完第i行的后放第i+1行的，已经放置的列不能再放

```python
class Solution:
    def solveNQueens(self, n: int) -> List[List[str]]:
        ans = []
        col = [0] * n
        check = [False] * n
        
        def valid(r,c): # 检验第r行，第c列能不能放（在前面的r-1行已经放好的情况下）
            for row in range(r):
                C = col[row]
                if row + C == c + r or row - C == r - c:
                    return False
            return True


        def dfs(i):
            if i == n:
                ans.append(['.'*c+'Q'+'.'*(n-c-1) for c in col]) # 生成答案
                return
            for j in range(n):
                if check[j] == False and valid(i,j): # 遍历所有没放过的列，并检验这一列能不能放了
                    col[i] = j
                    check[j] = True
                    dfs(i+1)
                    check[j] = False # 这种情况结束后记得清理现场
        
        dfs(0)
        return ans
```

### 组合型回溯



### 剪枝：

> 一些问题不需要将所有情况回溯一遍，一些不可能实现的结果直接return掉

+ 方法：

## 记忆化搜索/动态规划

+ DP萌新三步：
  + 思考回溯要怎么写
    + 入参和返回值
    + 递归到哪里
    + 递归边界和入口
  + 改成记忆化搜索
  + 1:1翻译成递归

例1.[198. 打家劫舍](https://leetcode.cn/problems/house-robber/):

+ 首先是考虑写成回溯：

  这里是子集型回溯，有【选或不选】【选哪个】这两种思路

  这里更适合用【选或不选】这个思路

  入参i应为前n个房屋待抢劫的数量

  边界条件应为：当i<0时，返回0（没有房子可以选了）

```c++
int dfs(int i)//选前i个房子的最大金额数量
{
    if(i<0)
    {
        return 0;
    }
    return max(dfs(i-1),dfs(i-2)+nums[i]);
}
```

+ 优化为记忆化搜索：

```c++
int n=nums.size();
vector<int>cache(n,-1);//-1表示没被计算过
int dfs(int i)
{
    if(i<0)
    {
        return 0;
    }
    if(cache[i]!=-1)//以前已经计算过前i给的最大值
    {
        return cache[i];
    }
    int res=max(dfs(i-1),dfs(i-2)+nums[i]);
    cache[i]=res;
    return res;
}
```

+ 逐步翻译为递推：

```c++
int n=nums.size();
vector<int>dp(n,-1);
dp[0]=nums[0];
dp[1]=nums[1];
for(int i=2;i<n;i++)
{
    dp[i]=max(dp[i-1],dp[i-2]+nums[i]);
}
return dp[n-1];
```

### 背包DP

0-1背包原型：一定容量背包，一些物品，选或不选，总价值最大

从序号最后面的物品w[i]开始枚举

dfs(i,c)表示枚举到第i个物品时（也即当任意选取所有>=i的物品的状态）总容量为c的背包能装下的最大价值

+ 出口条件：

```c++
if(i<0)//没有物品可供枚举了
{
    return 0;
}
```

+ 状态转移方程：

```c++
dfs(i,c)=max(dfs(i-1,c),dfs(i-1,c-v[i])+w[i])
```

+ 这里注意边界：c-v[i]可能小于0：当剩余容量小于v[i]时就没必要再算了，直接return dfs(i-1,c)
+ 转化为递推：

```c++
dp[i][c]表示当背包容量为c时，枚举到第i个物品时能够达到的最大价值、
dp[i][c]=max(dp[i-1][c])
```

+ 变形：

> 至多装capacity，求方案数/最大价值和
>
> 恰好装capacity，求方案数/最大/最小价值和
>
> 至少装capacity，

## 动态规划题目积累：

[1125. 最小的必要团队](https://leetcode.cn/problems/smallest-sufficient-team/):

<b>一个细节：可以状态压缩</b>

确认回溯类型：子集型回溯，选与不选

以此开始动态规划，dp[i]表示职业技能为i（一个二进制数，表示现已有的状态）所需的最少人数的情况的所有人的集合



## 思路特殊的题目积累：

（周赛332）[6356. 子字符串异或查询](https://leetcode.cn/problems/substring-xor-queries/)：暴力把字符串能表示的所有二进制数（答案能取到的）全放进容器里，然后无脑查找

[56. 合并区间](https://leetcode.cn/problems/merge-intervals/)：
