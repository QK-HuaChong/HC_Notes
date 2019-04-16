# Python

## 一、变量和简单数据类型

### 变量的命名和使用

- 只能包含字母、数字和下划线，并且只能以字母和下划线开头。
- 不能包含空格，可以通过下划线分割其中的单词。
- 不可以使用Python的关键字或函数名。
- 变量名应简短而具有描述性。

```python
    msg_drive = '道路千万条，安全第一条'
```

### 字符串

> 字符串是一系列字符。在Python中，用引号包含起来的就是字符串，其中引号可以是单引号也可以是双引号。

```python
    name = 'HuaChong'
    country = "China"
```

#### 字符串大小写转换

- 单词首字母大写 ---> title()
- 全部大写 ---> upper()
- 全部小写 ---> lower()

```python
    name = 'anne hathaway'
    name_2 = 'SCARLETT JOHANSSON'

    print(name.title())
    print(name.upper())
    print(name_2.lower())

    #输出结果
    'Anne Hathaway'
    'ANNE HATHAWAY'
    'scarlett johansson'

```

#### 合并/拼接字符串

>通过加号（+）来合并字符串

```python
    first_name = 'Hua'
    last_name = 'chong'
    full_name = first_name + " " + last_name

    print(full_name)

    #输出结果
    'Hua Chong'
```

#### 删除空白

- strip() 删除开头和末尾的空格
- lstrip() 删除开头的空格
- rstrip() 删除末尾的空格

#### 分片和索引

>字符串的分片是从字符串截取下片段存储到另外的地方。string[index] 截取指定下标位的字符，string[start:end] 截取指定长度的字符串

```python
    introduce = 'My name is HuaChong'

    print(introduce[0])
    print(introduce[11:19])

    #输出结果
    'M'
    'HuaChong'
```

### 注释

- 单行注释 ---> #注释内容
- 多行注释 ---> """注释内容"""

## 二、数据结构

### 列表（list）

>列表由一系列按特定顺序排列的元素组成。在Python中，用`方括号`（[]）来表示列表，并用逗号来分隔其中的元素。

#### 列表的特征

1. 列表中的每一个元素都是`可变的`；
2. 列表中的元素是`有序的`，也就是说每一个元素都有一个位置；
3. 列表可以容纳Python中的`任何对象`。

#### 访问列表

>列表中的每一个元素都对应看一个位置，我们通过输入索引而访问该位置所对应值

```python
    bicycles = ['trek','connondale','redline']

    print(bicyles[0])

    #输出结果
    'trek'
```

#### 修改元素

>对指定位置重新赋值

```python
    bicycles[2] = 'honda'

    print(bicycles)

    #输出结果
    ['trek','connondale','honda']
```

#### 添加元素

- append()方法

>在列表的末尾添加新的元素

- insert(index,element)

>在指定位置添加元素

```python
    bicycles.append('suzuki')
    bicycles.insert(0,'ducail')

    print(bicycles)

    #输出结果
     ['ducail','trek','connondale','honda','suzuki']
```

#### 删除元素

- pop() 方法

>删除末尾的元素

- del 关键字

>删除指定位置的元素

- remove(element) 方法

>根据值删除指定位置的元素