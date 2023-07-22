# Python Grammar

## IO

### output:

#### format():construct things from other information

```python
age = 20
name = 'Swaroop'

print('{0} was {1} years old when he wrote this book'.format(name, age))
print('Why is {0} playing with that python?'.format(name))
```

output:

```python
Swaroop was 20 years old when he wrote this book
Why is Swaroop playing with that python?
```

same effect:

```python
age = 20
name = 'Swaroop'

print('{} was {} years old when he wrote this book'.format(name, age))
print('Why is {} playing with that python?'.format(name))
```

```python
age = 20
name = 'Swaroop'

print('{name} was {age} years old when he wrote this book'.format(name=name, age=age))
print('Why is {name} playing with that python?'.format(name=name))
```

Python 3.6 introduced a shorter way to do named parameters, called "f-strings":

```python
age = 20
name = 'Swaroop'

print(f'{name} was {age} years old when he wrote this book')  # notice the 'f' before the string
print(f'Why is {name} playing with that python?')  # notice the 'f' before the string
```

detailed specifications:

```python
# decimal (.) precision of 3 for float '0.333'
print('{0:.3f}'.format(1.0/3))
# fill with underscores (_) with the text centered
# (^) to 11 width '___hello___'
print('{0:_^11}'.format('hello'))
# keyword-based 'Swaroop wrote A Byte of Python'
print('{name} wrote {book}'.format(name='Swaroop', book='A Byte of Python'))
```

output:



#### print(……,end='……')

without end='……', automatically '\n'

One thing to note is that in a string, a single backslash at the end of the line indicates that the string is continued in the next line, but no newline is added. For example:

```python
"This is the first sentence. \
This is the second sentence."
```

is equivalent to

```python
"This is the first sentence. This is the second sentence."
```

specify a *raw* string by prefixing `r` or `R` to the string

```python
r"Newlines are indicated by \n"
```



print(string, expression)

```python
length = 5
breadth = 2
area = length * breadth
print('Area is', area) # automatically add a space between "Area is" and the value of area
print('Perimeter is', 2 * (length + breadth))
```

### input:

input more than one integer:

```python
a, b = map(int, input().split())
a, b, c = map(int, input().split())
```

input many strs into a list:

```python
lis = list(input().split())
```



## judging statements:

### if:

```python
if test-statement:
    do something
elif test-statement:
    do something
else:
    do something
```

### while:

```python
number = 23
running = True
while running:
    guess = int(input('Enter an integer : '))
    if guess == number:
        print('Congratulations, you guessed it.')
# this causes the while loop to stop
        running = False
    elif guess < number:
        print('No, it is a little higher than that.')
    else:
        print('No, it is a little lower than that.')
else:
    print('The while loop is over.')
# Do anything else you want to do here
print('Done')
```

## containers:

### number:

int, float, bool, complex

type(a)函数返回a的类型

isinstance()函数打印是否为某类型：

```python
a = 12
print(type(a))
isinstance(a,int)
```

输出：

```python
<class 'int'>
True
```

> 注：bool是int的子类，即True == 1, False == 0

### string:

'+'表示连接字符串，'*'表示复制字符串

![image-20230310164023864](C:\Users\18326\AppData\Roaming\Typora\typora-user-images\image-20230310164023864.png)

str[i:j]表示从i->j-1所有字符；特殊：str[i:]表示从i开始所有

字符串前加'r'表示raw字符串

**python字符串不能被按照索引改变**

> 如：str[1] = 'r'是错的
>
> 但是可以重新输入: str = input()

### list：

写在方括号[]之间，用逗号分隔开的元素列表

与string类似，可以用方括号截取lis[i:j]

+ 二维列表：

```python
list = [[0 for i in range(5)] for i in range(5)] #初始化5*5二维列表为0
```

#### list推倒式：

```python
[out_exp_res for out_exp in input_list]
或者：
[out_exp_res for out_exp in input_list if condition]
```

#### list方法：

```python
element = [1,0]
sample = []
sample.append(element) #传递指针，sample内的这个列表会随element内值变化而变化
sample.append(element.copy()) #sample内的这个列表不会随element变化而变化，传递固定值
sample.pop()#弹出栈顶
sample.copy()#拷贝数组，这样就不会变
```

==血泪教训：将数组append到ans中时一定要记得拷贝数组！！！！！==



### tuple:

写在圆括号()之间，元素不可改变

```python
tup0 = (1, 2, 3)
```

也可以截取、索引、复制、延长

构造包含 0 个或 1 个元素的元组比较特殊，所以有一些额外的语法规则：

```python
tup1 = ()    # 空元组
tup2 = (20,) # 一个元素，需要在元素后添加逗号
```

> string, tuple, list都属于序列

#### tuple推倒式：

```python
(expression for item in Sequence )
或
(expression for item in Sequence if conditional )
```



### set

可以使用大括号 { } 或者 set() 函数创建集合，注意：创建一个空集合必须用 set() 而不是 { }，因为 { } 是用来创建一个空字典。

```python
parame = {value01,value02,...} # 重复的元素会自动被删去
或
set(value)
```

+ 成员测试：

```python
if a in sites # a是某元素，sites是集合
```

+ 进行集合运算：

```python
print(a - b)     # a 和 b 的差集

print(a | b)     # a 和 b 的并集

print(a & b)     # a 和 b 的交集

print(a ^ b)     # a 和 b 中不同时存在的元素
```

#### set推倒式：

```python
{ expression for item in Sequence }
或
{ expression for item in Sequence if conditional }
```



### dictionary

初始化：

```py
dict = {}
dict[0] = 'aaa'
dict[1] = 'bbb'
或者：
tinydict = {'name': 'runoob','code':1, 'site': 'www.runoob.com'}
```

#### dictionary推导格式：

```python
{ key_expr: value_expr for value in collection }
或
{ key_expr: value_expr for value in collection if condition }
```

*dictionary不能像c++的unordered_map那样自动为没有键的值赋值为1：

```c++
unordered_map<int,int> a
    a[10]+=1 //In C++ this is valid
```

```python
a = dict()
a[10] += 1 #invalid
a[10] = 1
a[10] += 1 #valid
```

#### dictionary方法：

```python
a = dict()
a.keys() #表示a的所有键的集合
for key in a.keys(): #遍历a的所有键
    # code
if key in a.keys(): #判断key是否是a的键
```



### transition between string and list:

#### 1. string可以通过split方法得到list:

```python
c=‘a;s;d;f;g;h’
d=c.split(‘;’)
print(d)
# 输出：[‘a’, ‘s’, ‘d’, ‘f’, ‘g’, ‘h’]
```

#### 2. list可以通过join方法得到string:

```python
a=[‘a’, ‘s’, ‘d’, ‘f’, ‘g’, ‘h’]
c=‘;’.join(a)
print(c)

# ‘a;s;d;f;g;h’
```

> 注意:
> 当多个变量接收split后的结果时,这多个变量不是列表,而还是字符串



## 数据类型转换：

| 函数                   | 描述                                              |
| :--------------------- | :------------------------------------------------ |
| int(x [,base\])        | 将x转换为一个整数                                 |
| float(x)               | 换到一个浮点数                                    |
| complex(real [,imag\]) | 创建一个复数                                      |
| str(x)                 | 将对象 x 转换为字符串                             |
| repr(x)                | 将对象 x 转换为表达式字符串                       |
| eval(str)              | 算在字符串中的有效Python表达式,并返回一个对象     |
| tuple(s)               | 将序列 s 转换为一个元组                           |
| list(s)                | 将序列 s 转换为一个列表                           |
| set(s)                 | 转换为可变集合                                    |
| dict(d)                | 创建一个字典。d 必须是一个 (key, value)元组序列。 |
| frozenset(s)           | 转换为不可变集合                                  |
| chr(x)                 | 将一个整数转换为一个字符                          |
| ord(x)                 | 将一个字符转换为它的整数值                        |
| hex(x)                 | 将一个整数转换为一个十六进制字符串                |
| oct(x)                 | 将一个整数转换为一个八进制字符串                  |





## operators:

### arithmetic operators:

| 运算符 | 描述                                            | 实例                                |
| :----- | :---------------------------------------------- | :---------------------------------- |
| +      | 加 - 两个对象相加                               | a + b 输出结果 31                   |
| -      | 减 - 得到负数或是一个数减去另一个数             | a - b 输出结果 -11                  |
| *      | 乘 - 两个数相乘或是返回一个被重复若干次的字符串 | a * b 输出结果 210                  |
| /      | 除 - x 除以 y                                   | b / a 输出结果 2.1                  |
| %      | 取模 - 返回除法的余数                           | b % a 输出结果 1                    |
| **     | 幂 - 返回x的y次幂                               | a**b 为10的21次方                   |
| //     | 取整除 - 往小的方向取整数                       | >>> 9//2 <br>4<br> >>> -9//2 <br>-5 |

### logical operators:

| 运算符 | 逻辑表达式 | 描述                                                         | 实例                    |
| :----- | :--------- | :----------------------------------------------------------- | :---------------------- |
| and    | x and y    | 布尔"与" - 如果 x 为 False，x and y 返回 x 的值，否则返回 y 的计算值。 | (a and b) 返回 20。     |
| or     | x or y     | 布尔"或" - 如果 x 是 True，它返回 x 的值，否则它返回 y 的计算值。 | (a or b) 返回 10。      |
| not    | not x      | 布尔"非" - 如果 x 为 True，返回 False 。如果 x 为 False，它返回 True。 | not(a and b) 返回 False |

### member operators:

| 运算符 | 描述                                                    | 实例                                              |
| :----- | :------------------------------------------------------ | :------------------------------------------------ |
| in     | 如果在指定的序列中找到值返回 True，否则返回 False。     | x 在 y 序列中 , 如果 x 在 y 序列中返回 True。     |
| not in | 如果在指定的序列中没有找到值返回 True，否则返回 False。 | x 不在 y 序列中 , 如果 x 不在 y 序列中返回 True。 |

### 身份运算符：

| 运算符 | 描述                                        | 实例                                                         |
| :----- | :------------------------------------------ | :----------------------------------------------------------- |
| is     | is 是判断两个标识符是不是引用自一个对象     | **x is y**, 类似 **id(x) == id(y)** , 如果引用的是同一个对象则返回 True，否则返回 False |
| is not | is not 是判断两个标识符是不是引用自不同对象 | **x is not y** ， 类似 **id(x) != id(y)**。如果引用的不是同一个对象则返回结果 True，否则返回 False。 |

## 文件IO

打开文件：

```python
f = open(file_address, mode) #常用的是只用这两个参数
```

mode类型：

'a'：在文件后追加

'w'：重写文件

'r'：读取文件

'x'：创建文件

### 读取：

```python
f = open(file_address, 'r')
line = f.readline() 
# 一次只读一行（读到换行符结束），返回str类型，注意返回的字符串末尾有'\n'
# 若是读到末尾无东西可读，返回空字符串''
while(line!=''):
    print(line,end='')
    line = f.readline()
f.close()
```

```python
f = open(file_address, 'r')
line = f.read()
# 一次性读完，包含所有换行符、字符放到一个字符串里
print(line)
f.close()
```

> 以上两种方法读取结果相同

另：如果用readline()方法读了一部分，那么再用read()方法只能读取剩余所有

关闭文件：

```python
f.close()
```

### 写/追加

```python
f = open(file_address, 'w')
f.write("abcdefg\n")
f.close()
```



## 常用方法积累

#### 倒序for循环

```python
for i in range(n-1,-1,-1)
#第一个参数是起始数，第二个是终止数（不包含），第三个-1表示倒序
```

#### enumerate：返回一个enumerate对象，多用于在for循环中进行计数

```python
s=[1,3,5,7,9]
e=enumerate(s)
for i,value in e:
    print(i,value)
```

output:

```python
0 1
1 3
2 5
3 7
4 9
```

#### sum：对数组求和

直接sum(nums)即可

```python
s = [1, 3, 5, 7, 9]
n = sum(s)
print(n)
```

output:

```python
25
```

#### 字符串的strip()方法：将字符串两边多余的字符移除

默认去除空格，也可以自行设定

```python
a = '   abc dd '
a = a.strip()
print(a)
```

output:

```python
abc dd
```

#### 字符串小写、大写转化

str类型的内置方法：

```python
a = 'defgFFfdil'
a.upper() # 返回全部转化为大写的字符串
a.lower() # 返回全部转化为小写的字符串
```

#### 输入一行整数：

```python
lis = map(int,input().split())
```

#### max(a,b)返回a,b中大值

#### 直接计算前缀和

```python
s = list(accumulate(nums, initial=0))  # 计算前缀和
```

