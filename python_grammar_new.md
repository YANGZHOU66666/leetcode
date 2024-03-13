# Python Grammar

## basic data types

+ Number

Integer, Float, Complex

+ String

+ List
+ Tuple
+ Dictionary
+ Set

## compare

```python
smaller = max(a,b)
greater = min(a,b)
```

## sort

```python
arr=[5,3,8,12,1]
arr.sort() # 默认从小到大排序
arr.sort(reverse= True) # 从大到小排序

strArr = ["dav","abac","aba","abad","aacc"]
strArr.sort() # 按字典序排序

newArr = sorted(arr) # sorted会返回一个新数组，参数数组不变
print(arr,newArr)
```

```python
# 自定义排序: functools.cmp_to_key()
import functools
arr = [[1,5,6],[4,2,1],[9,4,2],[6,6,6],[6,6,7],[7,6,6],[5,6,6]]
def cmp(x,y):
    if x[1]>y[1]:
        return 1
    elif x[1]==y[1]:
        if x[0]>y[0]:
            return 1
        elif x[0]==y[0]:
            return 0
        else:
            return -1
    else:
        return -1
arr.sort(key=functools.cmp_to_key(cmp))
print(arr)
```

==注意不等号的方向和排序方向和C++是反的==

c++中`x<y return 1`是升序，python中`x>y return 1`是升序

## list

### 声明

[]方法、list()方法、列表推导式

```python
# 两种声明方式:
lis1 = []
lis2 = list()

# list()方法可以将可迭代对象转化为数组
# 元组的转化
tup = (3,5,2,34,3)
lis3 = list(tup)
# 字典的转化
dic = {5:43, 9:20, 4:34}
lis4 = list(dic) # [5,9,4]
lis5 = list(dic.values()) # [43, 20, 34]
lis6 = list(dic.keys()) # [5,9,4]

# 列表推导式
lis7 = [_*2 for _ in range(5)] # [0, 2, 4, 6, 8]
```

### 常用方法

```python
arr = [1,2]
arr.append(3) # 向后面添加
arr.extend([4,5]) # 向后面延申一个可迭代对象
arr.remove(4) # 注意移除的是第一个该值的元素而非下标
arr.insert(3,4) # 先下标，后值
arr.pop(2) # 无参数默认pop最后的，有参数就移除该下标的值
arr.count(4) # 返回列表的某种值个数
arr.index(4) # 返回列表中第一个某值的下标，后面可以指定搜索范围,找不到报错
arr.index(4,2,5) # 在[2,5)范围内找第一个4
len(arr) # 返回数组长度
arr.reverse()
arr.clear() # 清空列表
```

### 下标和截取子串问题

下标三个值分别代表起始位置（闭区间）、终点位置（开区间）、步长；可以其中有些不填；不填的话，起始默认为0，终点默认为末尾，步长默认为1

```python
arr = [1,4,3,6,7,5,0]

# 冒号后没有值: 到结尾
print(arr[4:]) # [7, 5, 0]

# 负值: 从后往前数, 最后一个下标为-1
print(arr[3:-2]) # [6, 7]

# 第三个参数: 步长
print(arr[1:6:2]) # [4, 6, 5]

# 只要冒号后: 从0开始
print(arr[:3]) # [1, 4, 3]

# 负步长: 从结尾开始算, 这里前面的两个值起始位置应该在终点位置之后
print(arr[5:1:-3]) # [5, 3]

# 特殊地，步长为-1刚好为取反:
print(arr[::-1]) # [0, 5, 7, 6, 3, 4, 1]
```

### `arr.copy()`

浅拷贝一层，如果数组元素里有数组/多层数组，那么数组还是同一块空间

```python
arr = [1,4,3,6,7,[4,5]]
newArr = arr
copyArr = arr.copy()
arr[2] = 10
arr[5][0]=6
print(newArr,copyArr) #[1, 4, 10, 6, 7, [6, 5]] [1, 4, 3, 6, 7, [6, 5]]
```

## str

### 字符串和数字的转化

```python
s = "12"
num = int(s)
```

```python
num = 10
s = str(n)
```

### 大小写相关

```python
s = "string"
newS1=s.capitalize() # 第一个字符大写，其他小写
newS2=s.upper() # 全部大写
newS3=s.lower() # 全部小写
```

### join和split

+ **join: **将字符串数组以某个字符串为分割组合起来

```python
words = ["apple", "banana", "cherry"]
string = " ".join(words)  # 使用空格作为分隔符
print(string)  # 输出： 'apple banana cherry'
```



+ **split: **将字符串以某个字符为分界点分割为字符串数组

```python
string = "apple,banana,cherry"
words = string.split(",")  # 指定逗号为分隔符
print(words)  # 输出： ['apple', 'banana', 'cherry']
```





## file

### 文件读取

+ **file = open(path, 'r')**

```python
# 打开文件
file = open('example.txt', 'r')  # 'r'模式表示只读

# 读取文件内容
content = file.read()

# 关闭文件
file.close()
```

* **with open(path, 'r') as file**

```python
# 使用with语句自动管理文件资源
with open('example.txt', 'r') as file:
    content = file.read()
    # with语句块内的代码执行完毕后，文件会被自动关闭
```

#### read, readline, readlines

+ read表示直接读完整个文件，上例所示content是整个文件所有内容的字符串

+ 还可以限制字符数：

```python
# 打开文件
file = open('example.txt', 'r')

# 分块读取文件
chunk_size = 1024  # 假设我们每次读取1KB
chunk = file.read(chunk_size)
while chunk:
    # 处理chunk
    print(chunk)
    chunk = file.read(chunk_size)

# 文件会被自动关闭，因为with语句块已经执行完毕
```



+ readlines可以将文件内容转化为一个按行分割的数组

```python
# 打开文件
file = open('example.txt', 'r')

# 读取所有行
lines = file.readlines()

# 关闭文件
file.close()

# 处理lines列表
for line in lines:
    print(line.strip())  # 使用strip()去除行尾的换行符

```



+ readline表示一次读取一行，全读完了再readline就只有空字符串了

```python
# 打开文件
file = open('example.txt', 'r')

# 逐行读取
line = file.readline()
while line:
    print(line.strip())
    line = file.readline()

# 文件会被自动关闭，因为with语句块已经执行完毕
```

