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