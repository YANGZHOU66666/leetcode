# c++常用模板类方法汇总

## 1.vector

``` c++
vector<int> v;//声明
vector<int> v(20);//声明，且里面开始即留20个空间,默认初始化为0（及可以直接用v[i]访问）
vector<int> v(20,5)//默认初始化为20个5
//
v.push_back(num);//向容器末尾插入元素num
v.pop_back();//清除容器末尾的元素
v.back()//返回容器v最后一个元素
v.resize(n)//将v内部的元素个数改为n个，多出的删去，少的补（默认补0），本来就有且不超出的部分保留
v.resize(n,num)//补的部分补numv，其余同上
v.empty()//是空则返回true
v.clear()//清空所有值
v.size()//v中的元素个数
v.capacity()//v占据的内存（注意和size()的区别）
//声明二维数组：
vector<vector<int>> v(n,vector<int>(m));
//在类的private中声明vector类型并初始化：
vector<int> v=vector<int>(5,5);
//迭代器的使用：
vector<int>::iterator it=v.begin();
it++;//迭代器向后移动一位
it<v.end();//判断结束
*it=10;//赋值给相对应迭代器的位置
```

##  2.unordered_map

```c++
unordered_map<int, string> umap;//声明
//
umap.emplace(key,value);//向umap中添加键值对
umap.find(key)找到此key并返回其迭代器，否则返回umap.end()
    //(注意是找到key不是找到其对应的value)
//遍历：
for(pair<int,string>key:umap)
{
    function(key.first,key.second);
}
//OR:
for(unordered_map::iterator it = map.begin();it!=map.end();it++){
    int front = it->first;//key
    int end = it->second;//value
}//（用迭代器进行遍历）
```

## 3.priority_queue（优先队列）

```c++
priority_queue<int> q;//默认大根堆
q.push();//插入元素
q.pop();//弹出元素
q.top();//返回堆顶元素
q.empty();//是否为空
q.size();//返回元素个数

//内部元素优先级设置：

```

## 4.string

```c++
string str;
str.length();//返回字符串长度
```

## 5.sort

```c++
sort(nums.begin(),nums.end());//nums为vector类型，默认升序排序

```

## 6.unordered_set

```c++
unordered_set<int> uset;
uset.insert(x);
uset.erase(x);//删去元素
uset.find(x);//找到返回迭代器，否则返回uset.end()
uset.count(x);//返回x的数目，0或者1
uset.size();//返回元素个数
uset.clear();//清空
uset.empty();//空返回1
```

## 7.pair

```c++
pair<int,int>p //初始化
pair<int,int>p(0,0)
pair.first
pair.second //分别表示第一个和第二个值
```

## 8.deque

```c++
deque<int> a; //初始化
deque<int> a(10); //空间为10
deque<int> a(10, 1); //初始化为10个1
deque<int> b(a);// a全部拷贝给b
deque<int> b(a.begin(), a.begin()+3);// a中前三个元素拷贝给b
```

基本操作：

```c++
deque<int> deq;
deq.size();//容器大小
deq.max_size();//容器最大容量
deq.resize();//更改容器大小
deq.empty();//容器判空
deq.shrink_to_fit();//减少容器大小到满足元素所占存储空间的大小
deq.push_back();//尾部增加元素
deq.pop_back(); //将最后元素弹出
deq.pop_front(); //将最前元素弹出
deq.back(); //返回末尾元素
deq.front(); //返回开始元素
```

## 9.自定义排序

```c++
vector<string> store;
store.push_back("aaa");
store.push_back("aaaa");
store.push_back("aa");
sort(store.begin(),store.end(),cmp);
bool cmp(string left, string right)
{
    return left.length() < right.length(); //按长度从小到大排列
}
注意：如果cmp为类内函数必须加static修饰
```

# 一些函数

## 1.max_element(iterator begin,iterator end)

——返回所在区间内最大值的迭代器（加*解引用即为值）

## 2.memset()

void *memset(void *s, int ch, size_t n)

将指针s后面的大小为n后面的空间赋值为ch

