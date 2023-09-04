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

+ JavaScript:

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

+ Java:

```java
int[] arr={1,8,9,4,2,4};
Arrays.sort(arr);//升序排序
```



### 数组基本操作

+ **C++: vector**

```c++
vector<int> v;//声明
vector<int> v(20);//声明，且里面开始即留20个空间,默认初始化为0（及可以直接用v[i]访问）
vector<int> v(20,5)//默认初始化为20个5
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
```



### 数组复制：

JavaScript和Python直接数组赋/将数组放入数组中时，由于二者公用一个地址空间存储，修改一个的过程中会改另一个。这时候需要新复制一块空间存储相同元素

```python
arr.copy()
```

```javascript
arr.concat()
```

### 栈（Stack）

#### Java:

```java
Stack<Integer> stk=new Stack<Integer>();//初始化
stk.push(1);//压入栈
stk.isEmpty();//判断是否为空
stk.peek();//返回栈顶元素
stk.pop();//弹出元素
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



### 字典（Dict）

#### C++: unordered_map

```c++
unordered_map<int, string> umap;//声明
//
umap.emplace(key,value);//向umap中添加键值对
umap[1]="aaa";//向umap中添加键值对
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

#### Java: HashMap

```java
Map<Integer, String> hashMap=new HashMap<>();//初始化
map.put(1,"aaa");//放入键值对
map.put(2,"bbb");

map.get(1);//返回键为1的值
map.remove(1);//删去键为1的键值对
map.containsKey(2);//检查是否有键为2的键值对
map.containsValue("bbb");//检查是否有值为"bbb"的键值对
map.size();//返回键值对的数量
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

### 其他

#### Java: Ramdom类

```java
Ramdom random = new Ramdom();
random.nextInt();//随机返回一个整数，在int范围内
```

### String

#### C++: string

```c++
string str;
str.length();//返回字符串长度

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

### 字符串和数字转化

#### Java:

```java
//Integer.parseInt(String):将字符串转化为数字
String twentyOneThousand="2100";
int num=Integer.parseInt(twentyOneThousand);//num==2100
```

