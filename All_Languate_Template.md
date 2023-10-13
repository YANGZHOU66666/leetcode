### max(a,b)

C++:

```c++
max(a,b);
```

Java:

```java
Math.max(a,b);
```

JavaScript:

```javascript
Math.max(a,b);
```

python:

```python
max(a,b)
```

### 数组排序

#### JavaScript:

```javascript
//默认按照字典序排序
arr1=["abandon","cat","banana"];
arr1.sort();
//数组升序排序：
arr2=[2,4,5,2,4];
arr2.sort(function(a,b){return a-b});//升序排序是a-b
arr2.sort(function(a,b){return b-a});//降序排序是b-a
//自定义排序：
var users = [{name:"张三",age:20},{name:"李四",age:5},{name:"王五",age:10},{name:"赵六",age:8}];
//userA.age - userB.age 按照年龄升序排序
users.sort(function(userA, userB){return userA.age - userB.age});
//总之，自定义函数，然后升序用a-b，降序用b-a
```

#### Java:

```java
int[] arr={1,8,9,4,2,4};
Arrays.sort(arr);//升序排序，用Arrays类内置函数
Arrays.sort(arr,(x,y) -> {return x-y;});//升序排序
Arrays.sort(arr,(x,y) -> {return y-x;});//降序排序
//或者：
Arrays.sort(arr,(x,y) -> x-y);//升序排序
List<List<Integer> lis=new ArrayList<List<Integer>>();
//对列表排序：让我们假定里面有一些元素
lis.sort((x, y)-> {return x.get(1)-y.get(1);});//按照索引为1的值升序排序
//还可以写为：
lis.sort((x, y) -> x.get(1)-y.get(1));//也是按索引为1的值升序排序
```

#### C++:

```c++
vector<int> arr;
arr.push_back(2);
arr.push_back(4);
arr.push_back(3);
arr.push_back(7);
sort(arr.begin(),arr.end());//默认从小到大排序
vector<vector<int>> grid;
grid.push_back([3,2]);
grid.push_back([5,3]);
grid.push_back([1,3]);
sort(grid.begin(),grid.end());//二维数组按照数组元素的第一个数字从小到大排序
//自定义排序：（优先队列的自定义排序也可以这么写）
struct cmp{
    bool operator()(vector<int>& a, vector<int>&b){//这里的两个参数随机应变
        return a[1]<b[1];//按照a、b数组的第二个元素从小到大排序
                         //a<b: 从小到大;a>b: 从大到小
    }
}
sort(grid.begin(),grid.end(),cmp);
```

<mark>这里需要特别注意，自定义排序c++是用小于和大于来写，Java和JavaScript是用减号来写</mark>



### lambda

#### Java:

```java
(x,y) -> x+y;//看作f(x,y){ return x+y;}
() -> System.out.println("Hello");
```

#### JavaScript:

```javascript
function(a,b){return a-b;}
```

### filter

#### JavaScript:

```javascript
let arr=[1,7,3,4,5,9,8];
let res=arr.filter((num) => {return num>=5;});
```

### 数组基本操作

#### C++: vector

```c++
vector<int> v;//声明
vector<int> v(20);//声明，且里面开始即留20个空间,默认初始化为0（及可以直接用v[i]访问）
vector<int> v(20,5);//默认初始化为20个5
//声明二维数组:
vector<vector<int>>(n,vector<int>(m,2));//n*m大小二维数组全部填满2
vector<vector<int>> move={{0,1},{1,0},{0,-1},{-1,0}};//在岛屿类题目中常见
//
v.push_back(num);//向容器末尾插入元素num
v.pop_back();//清除容器末尾的元素
v.back()//返回容器v最后一个元素
v.resize(n)//将v内部的元素个数改为n个，多出的删去，少的补（默认补0），本来就有且不超出的部分保留
v.resize(n,num)//补的部分补numv，其余同上
v.insert(v.begin(),num);//将num插入头部
v.insert(v.begin()+n,num);//将num插入某位置
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
//返回空数组:
return vector<int>(0);
```

#### Java: LinkedList——底层是双向链表

```java
List<Integer> arr=new ArrayList<Integer>();
List<Integer> lList=new LinkedList<Integer>();
List<Integer> lList2=new LinkedList<Integer>(arr);//从其他数据结构构造
lList.add(1);//向尾部插入元素，o(1)
lList.add(2);
lList.add(1,2);//向index为1的节点插入元素，并将其他挤到后面，o(n)
lList.remove(1);//移除index为1位置的元素，o(n)
lList.remove(new Integer(2));//移除某对象所在的节点，o(n)
lList.removeFirst();//移除首节点，o(1)
lList.removeLast();//移除尾节点，o(1)
lLast.addAll(arr);//加一组数
lLast.get(1);//返回下标为1位置的数
lLast.set(1,new Integer(5));//改变某下标位置的数
lLast.contains(new Integer(2));//查找是否有某元素
lLast.indexOf(new Integer(2));//查找下标
lLast.lastIndexOf(new Integer(2));//最后一个位置的下标
lLast.subList(1,3);//截取部分链表
//遍历：
for(int num: lLast){
    //do something
}
ListIterator<Integer> it=lLast.listIterator();
while(it.hasNext()){
    it.next();//do something with it
}
//反向遍历：
ListIterator<Integer> it2=lLast.listIterator(lLast.size());
while(it2.hasPrevious()){
    it.previous();//do something with it
}
```



#### Java: ArrayList

> Java的List分为ArrayList和LinkedList两种

```java
List<Integer> arr=new ArrayList<Integer>();
List<Integer> arr2=new ArrayList<Integer>(15);//开大小为15的空间
//开二维数组:
List<List<Integer>> grid=new ArrayList<List<Integer>>();
for(int i=0;i<n;i++){
    grid.add(new ArrayList<Integer>());
}
arr.add(3);//将指定元素添加到末尾
arr.addAll([4,5,6]);//将指定集合的所有元素添加到末尾
int x=arr.get(i);//返回第i个元素
arr.set(2,5);//将下标为2的位置设置为5
arr.remove(arr.size()-1);//将下标为arr.size()-1的位置的元素删除
List<Integer> arr3=new ArrayList<Integer>(arr);//通过其他集合构造
Collections.sort(arr);//按升序排序
```

#### Java: 普通数组

```java
int[] arr1=new int[5];//声明二维数组但不赋值
int[][] grid1=new int[8][4];//声明二维数组但不赋值
int[] arr2=new int[]{1,2,3,4,5};//初始化数组
int[][] move=new int[][]{{0,1},{1,0},{0,-1},{-1,0}};//初始化二维数组
int n=arr2.length;//返回数组长度
```



#### JavaScript: 普通数组([])

```javascript
let arr=[];
for(let i=0;i<n;i++){
    arr[i]=0;
}
//二维数组:
let grid=[];
for(let i=0;i<n;i++){
    grid[i]=[];
    for(let j=0;j<m;j++){
        grid[i][j]=0;
    }
}
arr.push(1);//在后端加入
arr.pop();//后端弹出
```

### 数组复制：

JavaScript和Python直接数组赋/将数组放入数组中时，由于二者公用一个地址空间存储，修改一个的过程中会改另一个。这时候需要新复制一块空间存储相同元素

#### Python:

```python
arr.copy();
```

#### JavaScript:

```javascript
arr.concat();
//else:
arr.slice();
```

### 链表：

#### C++：

官方给的默认链表格式，自己也要会写

```c++
struct ListNode{
    int val;
    ListNode* next;
    ListNode(): val(0), next(nullptr){}
    ListNode(int v): val(v), next(nullptr){}
    ListNode(int v, ListNode* nex):val(v), next(nex){}
};
```



### 栈（Stack）

#### Java: Stack

```java
Stack<Integer> stk=new Stack<Integer>();//初始化
stk.push(1);//压入栈
stk.isEmpty();//判断是否为空
stk.peek();//返回栈顶元素
stk.pop();//弹出元素
```

#### Java: Deque

```java
Deque<Integer> stk=new LinkedList<Integer>();
stk.push(1);
stk.push(2);
stk.push(3);
stk.pop();
stk.isEmpty();
stk.peekLast();//栈顶元素
stk.peekFirst();//队列头元素
```



#### C++:

```c++
stack<int> stk;
stk.push(1);
stk.empty();
stk.top();
stk.pop();
```



### 双端队列（Deque）



### 队列（Queue）

#### Java: LinkedList

```java
Queue<Integer> que=new LinkedList<Integer>();
que.offer(1);//入列
que.offer(2);
que.offer(3);
que.offer(4);
que.poll();//返回第一个元素并删除
que.element();//返回第一个元素
que.peek();//返回第一个元素
que.isEmpty();//返回是否为空
```

#### JavaScript: 数组可以当作队列来用

```javascript
let que=[];
que.push(1);//向末端添加元素
que.push(2);
que.push(3);
que.unshift(0);//向首端添加元素
que[0];//访问首部元素
que.shift();//弹出首部元素并返回首部元素
que.pop();//弹出尾部元素
que.length==0//判断是否为空
```

#### C++:

```c++
queue<tuple<int,int,int>> que;
que.emplace(1,2,3);
que.emplace(3,2,5);
auto [a,b,c]=que.front();
```



### 集合（Set）

#### C++: unordered_set

```c++
unordered_set<int> uset;
uset.insert(x);
uset.erase(x);//删去元素
uset.find(x);//找到返回迭代器，否则返回uset.end()
uset.count(x);//返回x的数目，0或者1
uset.size();//返回元素个数
uset.clear();//清空
uset.empty();//空返回1
//遍历：
unordered_set<int> set = {9,5,9,8,1,2,3,5,6,1,2,3,4,5,6,7,4,3,3};
        for(unordered_set<int>::iterator it = set.begin();it!=set.end();it++)
                cout<<*it<<" ";
```

### JavaScript: Set

```javascript
let set=new Set();
```

### 字典（Dict）

#### C++: unordered_map

```c++
unordered_map<int, string> umap;//声明
//注意：直接对未初始化的umap[i]++，直接生成默认0再操作
umap.emplace(key,value);//向umap中添加键值对
umap[1]="aaa";//向umap中添加键值对
umap.find(key);//找到此key并返回其迭代器，否则返回umap.end()
//(注意是找到key不是找到其对应的value)
umap.count(key);//找到key返回1，否则0
umap.size();//返回哈希表大小
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

#### Java: HashMap

```java
Map<Integer, String> hashMap=new HashMap<>();//初始化
hashMap.put(1,"aaa");//放入键值对
hashMap.put(2,"bbb");
hashMap.put(3,"ccc");

hashMap.get(1);//返回键为1的值
hashMap.remove(1);//删去键为1的键值对
hashMap.containsKey(2);//检查是否有键为2的键值对
hashMap.containsValue("bbb");//检查是否有值为"bbb"的键值对
hashMap.replace(3,"cccc");//replace(key,newValue): 更换哈希值
hashMap.size();//返回键值对的数量
hashMap.getOrDefault(4,0);//先找key为4有没有，没找到返回0，找到返回对应的value

//遍历1:
for (Integer key : map.keySet()) {
    System.out.println("key= "+ key + " and value= " + map.get(key));
}
//2:
Iterator<Map.Entry<Integer, String>> iterator = map.entrySet().iterator();
while(iterator.hasNext()){
    Map.Entry<Integer, String> entry = iterator.next();
    System.out.println("key:" + entry.getKey() + ",value:" + entry.getValue());
}
```

#### JavaScript: Map

```javascript
let hashing=new Map();//初始化
// set(key, value): 设置键值对
hashing.set(1,"a");
hashing.set(2,"bb");
hashing.set(3,"ccc");
// has(key): 检查是否存在某个键
hashing.has(2);//true
// get(key): 返回改键对应的值；若不存在该键值对，返回undefined
hashing.get(3);//"ccc"
// delete(key): 删除键值对
hashing.delete(2);

// values(): 返回所有键值对的值组成的一个可迭代对象
let valueSet=hashing.values();//暂时不知道有什么用
// entries(): 返回一个新的包含 [key, value] 对的 Iterator 对象，返回的迭代器的迭代顺序与 Map 对象的插入顺序相同
let entry=hashing.entries();//暂时不知道有什么用
// clear():
hashing.clear();//将Map清空
```

#### Python: dict

```python
dic={1:"a",2:"bb",3:"ccc"} # 初始化
for key, value in dic.items(): # 遍历整个字典
    # do something
dic[3]="cccc" # 修改字典值
dic[4]="dddd" # 增加字典值
del dic[3] # 删除键值对
dic.clear() # 清空字典

```



### 有序集合（multiset）

#### C++: multiset

```c++
multiset<int> mset;
mset.insert(3);//插入元素:O(log(n))
mset.insert(5);
mset.insert(1);
mset.insert(2);
mset.erase(2);//删除元素:O(log(n))，注意会删除所有等于改值的
mset.erase(mset.begin()+1);//删除某迭代器位置上的元素，即使有重复也只会删除一个
*mset.begin();//有序集合的首位元素（利用迭代器）
*mset.rbegin();//有序集合的末尾元素（利用迭代器）
//自定义排序：类似sort，不再重述
mset.find(3);//找某元素，找不到返回mset.end()
mset.count(3);//某元素数量
mset.upper_bound(5);//第一个大于5的元素的迭代器
mset.lower_bound(5);//第一个大于等于5的元素的迭代器
mset.count(5);//5的个数
```

### 其他

#### Java: Ramdom类

```java
Ramdom random = new Ramdom();
random.nextInt();//随机返回一个整数，在int范围内
```

### String

#### C++: string

```c++
string str="abcdefgfedcba";
str.length();//返回字符串长度
int place_d=str.rfind('d');//返回d字符从后往前第一次出现的位置，这里是9
int place_e=str.rfind('e',9);//返回从下标9往前数e第一次出现的下标，这里是4
int place_h=str.rfind('h');//找不到的话，返回str.npos
string segment=str.substr(0,5);//注意：1.是substr不是substring，和java不同；2.第二个参数是截取片段长度而非末尾
```

#### Java: String

```java
//1构造方法：
String str1=new String();
String str2=new String("Hello");
char[] chars={'H','e','l','l','o'};
String str3=new String(chars);
String str4=new String(chars, 1, 3);//第一个表示从第几位开始，第二个为字符数量
byte[] bytes={72,101,108,108,111};
String str5=new String(bytes);
String str6=new String(bytes,1,3);
String str7="Hello";
//2比较方法：
str2.equals(str3);
str2.compareTo(str3);//str2<str3:负数;str2==str3:0;str2>str3:正数
//3查找：
int index1=str2.indexOf("He");//第一个字符所在下标，此例为0
int index2=str2.indexOf("l",4);//从下标为4的字符开始查找，此例为4
int index3=str2.lastIndexOf("l");//最后一个出现"l"的位置，返回4
int index4=str2.lastIndexOf("l",3);//从下标为3处开始找最后一个出现"l"的位置，返回3
boolean check1=str2.startsWith("Hel");//检查是否以某个字符串开头
boolean check2=str2.endWith("lo");//检查是否以某个字符串结尾
char secondChar=str2.charAt(1);//返回字符串某下标处的值
//4转换：
char charArray=str2.toCharArray();//变成字符串数组
byte[] byteArray=str2.getBytes();//转化为字节数组
str2.toLowerCase();//转换成小写
str2.toUpperCase();//转换为大写
str2.trim();//去除开头结尾的空白
```

### PriorityQueue

#### C++: priority_queue

```c++
priority_queue<int> q;//默认大根堆
q.push();//插入元素
q.pop();//弹出元素
q.top();//返回堆顶元素
q.empty();//是否为空
q.size();//返回元素个数

//内部元素优先级设置：
priority_queue<int> q;//默认大根
priority_queue<int, vector<int>, less<int> > q;//大根
priority_queue<double, vector<double>, greater<double>> q;//小根
```



### 各种基础类型互相转化

#### Java:

```java
//Integer.parseInt(String):将字符串转化为数字
String twentyOneThousand="2100";
int num=Integer.parseInt(twentyOneThousand);//num==2100
//String类转char数组
String str="hello";
char[] charArr=str.toCharArray();
```

### 数学

Java:

```java
Math.sqrt(10);//返回double类型的值
Math.floor(4.8);//向下取整
Math.ceil(3.2);//向上取整
Math.round(4.5);//就近取整，优先靠近偶数
```

JavaScript:

```javascript
Math.floor(4.8);//向下取整
Math.ceil(3.2);//向上取整
Math.round(4.5);//就近取整，优先靠近偶数
```

### 声明函数内函数

#### C++:

```c++
int solve(int diameter){
    auto f=[&](int diameter, string diameter){
        //do something
    };
}
```

### Filter

#### JavaScript:

```javascript
let arr1=[1,2,3,4,5];
let arr2=arr1.filter(item => {
    return item>=2;
});
```



### 细节：

#### Java:

```java
1. i%2不能直接当成判定条件，需为i%2==1(可能是java不能int转boolean?)
2. 注意int和long必须得用强制类型转换，不能隐式转换
```

### 其他：

