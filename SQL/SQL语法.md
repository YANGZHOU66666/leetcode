# SQL Grammar

## 数据筛选与排序

### SELECT

SELECT table_name.col_name_1, ... FROM table_name



### WHERE

SELECT ... FROM ... WHERE condition

condition部分由以下内容组成：

**基础工具-比较运算符：**`=`, `!=`, `>`, `<`, `>=`, `<=`

**逻辑工具：**`OR`, `AND`, `NOT`

**专用工具：**

- `IN`：某个值在某个元组的里

  ```SQL
  -- 找出 '电子产品', '家居用品', '图书' 这三个品类的商品
  -- 不好的写法 (繁琐且慢):
  -- WHERE category = '电子产品' OR category = '家居用品' OR category = '图书'
  
  -- 好的写法 (简洁且快):
  SELECT * FROM products
  WHERE category IN ('电子产品', '家居用品', '图书');
  
  -- 配合 NOT 使用：
  SELECT * FROM products
  WHERE category NOT IN ('食品', '饮料');
  ```

- `BETWEEN`：某个值在某个**闭区间**里

- `LIKE`：**模糊匹配（用于字符串）** 这是**非常强大且常用**的工具，它依赖两个特殊的“通配符”：

  - **`%` (百分号)**：代表**零个或多个**任意字符。
  - **`_` (下划线)**：代表**一个**任意字符。

  ```SQL
  -- 找出所有名字以 '手机' 开头的商品 (如 '手机壳', '手机充电器')
  SELECT * FROM products WHERE product_name LIKE '手机%';
  
  -- 找出所有名字以 'Pro' 结尾的商品 (如 'iPhone 15 Pro')
  SELECT * FROM products WHERE product_name LIKE '%Pro';
  
  -- 找出所有名字包含 '充电' 的商品 (如 '手机充电器', '充电宝')
  SELECT * FROM products WHERE product_name LIKE '%充电%';
  
  -- 找出名字是三个字，且中间一个是 'A' 的商品 (如 'PAd')
  SELECT * FROM products WHERE product_name LIKE '_A_';
  ```

**用`()`控制优先级：**

当 `AND` 和 `OR` 一起使用时，`AND` 的优先级**高于** `OR`

```SQL
-- 错误的写法 (会先算 AND):
WHERE category = '电子产品' AND price > 1000 OR category = '食品'
-- 它的意思是: (category = '电子产品' AND price > 1000) OR (category = '食品')
-- 这会漏掉价格低于1000的电子产品。

-- 正确的写法 (使用括号明确你的逻辑):
WHERE (category = '电子产品' OR category = '食品') AND price > 1000
-- 它的意思是：找出 (电子产品或食品)，并且 它们的价格都要大于1000
```



### ORDER BY 子句

将返回的结果按某一（几）列进行排序

**核心语法：**

```SQL
SELECT column1, column2
FROM table_name
WHERE condition
ORDER BY column_to_sort_by [ASC | DESC];
```

ASC：升序

DESC：降序

**多列排序：**

优先按照写在前面的列排序

例如：优先按照category升序，category相同时按照price降序

```SQL
SELECT product_name, category, price
FROM products
ORDER BY category ASC, price DESC;
```

### IS NULL / IS NOT NULL：检查空值

在数据库中，`NULL` 是一个特殊状态，代表“缺失”或“未知”。你**不能**用 `=` 或 `!=` 来比较 `NULL`。

```SQL
-- 找出所有没有填写库存数量 (stock_quantity 为 NULL) 的商品
-- 错误的写法:
-- WHERE stock_quantity = NULL

-- 正确的写法:
SELECT * FROM products WHERE stock_quantity IS NULL;

-- 找出所有填写了库存数量的商品
SELECT * FROM products WHERE stock_quantity IS NOT NULL;
```

### LIMIT 子句

1-限制取Top k条数据；2-限制从第offset个开始，取row_count条

```SQL
-- 语法 1：只指定数量 (最常用)
LIMIT row_count;

-- 语法 2：指定偏移量和数量 (用于分页)
LIMIT offset, row_count;
```

## 聚合与分组

### 聚合函数

**COUNT()：**

直接统计行的数量：

```SQL
SELECT COUNT(*) FROM products;
-- 结果可能返回：150
```

统计某列不为NULL的值的数量：

```SQL
SELECT COUNT(description) FROM products;
-- 假设有150个商品，但有10个商品的 description 是 NULL
-- 结果会返回：140
```

统计某列不重复的值的数量：使用DISTINCT

```SQL
SELECT COUNT(DISTINCT category) FROM products;
-- 假设150个商品分属 12 个品类
-- 结果会返回：12
```

**SUM(), AVG(), MAX(), MIN()：**

用法类似

```SQL
SELECT SUM(stock_quantity) 
FROM products 
WHERE category = '电子产品';
```

**注意：**

1. 除了`COUNT(*)`之外，聚合函数都会忽略NULL的值

2. 聚合函数和正常的列没法一起SELECT

   **错误的查询：**

   ```SQL
   -- 你想看“每个商品”和“所有商品的总价”？
   -- 这种查询是无意义的
   SELECT product_name, SUM(price) FROM products;
   ```

   数据库会报错。为什么？因为 `product_name` 有 150 行，而 `SUM(price)` 只有 1 行。它们无法“对齐”显示。



### GROUP BY

按照某个列分桶，将FROM的数据源分成好几块，每块分别进行SELECT

例如：

```SQL
SELECT category, COUNT(*)
FROM products
GROUP BY category;
```

这样，products会先按照category进行分桶，对每个桶分别执行SELECT category和`COUNT(*)`的操作。可能的输出如下：

| **category** | **COUNT(\*)** |
| ------------ | ------------- |
| 电子产品     | 3             |
| 食品         | 2             |

**黄金法则：**

> **当你使用了 `GROUP BY`，你的 `SELECT` 子句中**
>
> 1. **要么是 `GROUP BY` 后面“出现过的列” (如 `category`)**
> 2. **要么是“聚合函数” (如 `COUNT(\*)`, `SUM(price)`)**
> 3. **不能有任何其他列！**

这是因为对于没有GROUP BY的字段，每个桶里很可能不止一种值，则SELECT不出唯一的那个值

以下是一个错误案例：

```SQL
-- 错误！
SELECT category, product_name, COUNT(*)
FROM products
GROUP BY category;
-- 报错：product_name 既没有在 GROUP BY 中，也不是一个聚合函数。
```



**`WHERE`和`GROUP BY`的配合：**

`WHERE` 子句在 `GROUP BY` 之前执行。

执行顺序是：`FROM` -> `WHERE` -> `GROUP BY` -> `SELECT`

```SQL
SELECT category, COUNT(*)
FROM products
WHERE price > 10     -- 1. 先把所有价格 <= 10 的商品全部扔掉
GROUP BY category;   -- 2. 然后对“幸存”的商品进行分组
```

**按多列分组：**

会按照所有可能的组合进行分桶

```SQL
SELECT category, region, SUM(sales)
FROM orders
GROUP BY category, region;
```

结果可能形如：

| **category** | **region** | **SUM(sales)** |
| ------------ | ---------- | -------------- |
| 电子产品     | 华东       | 50000          |
| 电子产品     | 华北       | 30000          |
| 食品         | 华东       | 15000          |
| 食品         | 华南       | 12000          |
| ...          | ...        | ...            |

### HAVING

核心：类似WHERE，但WHERE在GROUP BY之前过滤行，HAVING在GROUP BY之后过滤组。HAVING写在GROUP BY之后

SQL 逻辑执行顺序： `... WHERE ...` -> `... GROUP BY ...` -> **`... HAVING ...`** -> `... ORDER BY ...`

示例：假设你要统计公司里， “职级高于 P5”的员工“平均工资超过 1 万” 的部门。

职级P5是个体属性，用WHERE过滤；“平均工资超过1万”只能按照部门分组之后计算，因为是群体属性，因此用HAVING

```SQL
SELECT
    department,
    AVG(salary) AS avg_salary
FROM
    employees
WHERE
    level > 'P5'      -- 1. WHERE 过滤 “打工人”
                      --    先把所有 P5 及以下的员工全部开除，不参与后续计算
GROUP BY
    department        -- 2. GROUP BY 按部门分组
                      --    对“幸存”的 P5 以上员工按部门分组
HAVING
    AVG(salary) > 10000; -- 3. HAVING 过滤 “部门经理” (整个组)
                       --    计算每个部门的平均工资，然后开除那些 avg_salary <= 10000 的部门
```

