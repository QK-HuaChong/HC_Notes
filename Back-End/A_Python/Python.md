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

>列表由一系列按特定顺序排列的元素组成。在Python中，用`方括号`[]来表示列表，并用逗号来分隔其中的元素。

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

```python

    bicycles = ['trek','connondale','honda','redline']

    bicycles.pop()
    bicycles.remove('connondale')
    del.bicycles(1)

    #输出结果
    ['trek','connondale','honda']
    ['trek','honda']
    ['trek']

```

#### 列表排序

- sort()方法

>永久性地修改了列表元素的排列顺序。默认是按照字母顺序排序，若想要按`相反的顺序`只需要传递参数`reverse=True`

```python
    cars = ['bmw','audi','toyota']

    cars.sort()
    print(cars)

    #输出结果
    ['audi','bmw','toyota']

    cars.sort(reverse=True)
    print(cars)

    #输出结果
    ['toyota','bmw','audi']
```

- sorted()函数

>对列表进行临时排序

```python
    cars = ['bmw','audi','toyota']

    print(sorted(cars))

```

- reverse()方法

>反转列表排序

- len()函数

>获取列表的长度

```python
    cars = ['bmw','audi','toyota']

    len(cars)

    3
```

### 元组（tuple）

#### 定义元组

>Python将不能修改的值称为不可变的，而`不可变的`列表被称为元组。元组看起来犹如列表，但使用`圆括号()`而不是方括号来标识。定义元组后，就可以使用索引来访问其元素，就像访问列表元素一样。

```python
    dimensions = (200,300,500)

    print(dimensions(0))

    #输出结果
    200
```

### 集合（set)

#### 定义集合

>- 集合则更接近数学上集合的概念。每一个集合中的元素是`无序的、不重复的`任意对象，通过花括号`{}`来标识我们可以通过集合去判断数据的从属关系，有时还可以通过集合把数据结构中重复的元素减掉
>
>- 定义一个空的集合必须使用`set()`,因为{}是用来创建一个空的字典的。

```python
    student = {'Tom', 'Jim', 'Mary','Jack', 'Rose'}

    #定义空的集合
    num = set()
```

#### 集合的添加与删除

- add()
- discard()

```python
    student = {'Tom', 'Jim', 'Mary','Jack', 'Rose'}

    student.add('Johnaon')
    student.discard('Tom')
```

### 字典

#### 定义字典

>在Python中，字典是一系列键-值对。每个键都与一个值相关联，在Python中，字典用放在花括号`{key:value}`中的一系列键-值对表示

```python
    alien = {'color':'green','point':20}
```

#### 字典的特征

1. 字典中数据必须是以键值对的形式出现的；
2. 逻辑上讲，`键是不能重复的`，而`值可以重复`；
3. 字典中的键（key）是不可变的，也就是无法修改的；而值（value）是可变的，可修改的，可以是任何对象。

#### 访问字典里的值

>要获取与键相关联的值，可依次指定字典名和放在方括号内的键

```python
    alien = {'color':'green','point':20}

    print(alien['color'])

    #输出结果
    'green'
```

#### 添加字典元素

>字典是一种动态结构，可随时在其中添加键-值对。要添加键-值对，可依次指定字典名、用括号括起的键和相关联的值。

```python
    alien = {'color':'green','point':20}

    alien['x_position'] = 0
    alien['y_position'] = 20
```

- update() 方法

>添加多个元素

#### 修改字典中值

>要修改字典中的值，可依次指定字典名、用方括号括起的键以及与该键相关联的新值。

```python
    alien = {'color':'green','point':20}

    alien['color'] = 'black'
```

#### 删除字典元素

- del 语句

```python
    alien = {'color':'green','point':20}

    del alien['color']
```

## 三、 循环与判断

### 运算符

#### 比较运算符

符号|意义
--|--|
==|左右两边等值的时候返回 True
!=|左右两边不相等时返回True
>|左边大于右边的时候返回True
<|左边小于右边的时候返回True
<=|左边小于或等于右边的时候返回True
>=|左边大于或等于右边的时候返回True

#### 成员运算符/身份运算符

>成员运算符和身份运算符的关键词是in与is。把in放在两个对象中间的含义是，测试前者是否存在于in后面的集合中。

#### 布尔运算符

> and和or经常用于处理复合条件

A|B
--|--
not x|如果×是True，则返回False，否则返回True。
x and y|and表示“并且”，如果x和y都是True，则返回True；如果x xandy 和y有一个是False，则返回 False。
x or y|or表示“或者”，如果x或y有其中一个是True，则返回True；Xofy如果×和y都是False，则返回 False。

### 条件控制

#### if...else语句

```python
    def account_login():
        password = input('Password:')
        if password == '123654':
            print('Login success!')
        else:
            print('Wrong password or invalid input!')

    account_login()
```

#### for 循环

```python
    for every_letter in 'Hello World':
        print(every_letter)
```

- range(start, stop[, step])

>range会返回一个整数序列，statr为整数序列的起始值，end为整数序列的结束值，在生成的整数序列中，不包含结束值。step为整数序列中递增的步长，默认为1。

#### while 循环

>但如果while循环不能像for循环那样，在集合被穷尽之后停下来，我们又怎么样才能控制 while循环呢？其中一种方式就是：在循环过程中制造某种可以使循环停下来的条件

```python
    count = 0
    while True:
        print('Repeat this line!')
        count = count +1
        if count = 3:
            break
```

#### break

> break语句用来终止循环语句，即循环条件没有False条件或者序列还没被完全递归完，也会停止执行循环语句。

#### continue

>continue 语句用来告诉Python跳过当前循环的剩余语句，然后继续进行下一轮循环。

#### pass

>Python pass 是空语句，是为了保持程序结构的完整性。

## 四、函数

### 函数的定义

>使用关键字`def`来告诉Python你要定义一个函数。这是函数定义，向Python指出了函数名，还可能在括号内指出函数为完成其任务需要什么样的信息。

```python
    def greet_user():
        print('Hello!')

    geet_user()

    #输出结果
    'Hello'
```

### 导入模板中的函数

#### 模块

>ython 模块(Module)，是一个 Python 文件，以 .py 结尾，包含了 Python 对象定义和Python语句。模块让你能够有逻辑地组织你的 Python 代码段。

- import

>import语句并在其中指定模块名，就可在程序中使用该模块中的所有函数。

- from ... import ...

>导入模块中的特定函数

- import ... as ...

>使用as给模块指定别名

- from ... import *

>导入模块中的所有函数

## 五、类

### 创建和使用类

>关键字class是用来定义一个类

```python
    class Dog():
        def __init__(self,name,age):
            self.name = name
            self.age = age

        def sit(self):
            print(self.name.title()+"is now sitting")
```

### 方法__init__()

>它是一个指向实例本身的引用，让实例能够访问类中的属性和方法。每当你根据一个类创建新实例时，Python都会自动运行。

### 根据类创建实例

```python
    my_dog = Dog('willie',8)

    print("My Dog name is"+my_dog.name.title())
```

## 继承

>编写类时，并非总是要从空白开始。如果你要编写的类是另一个现成类的特殊版本，可使用继承。一个类继承另一个类时，它将自动获得另一个类的所有属性和方法；原有的类称为`父类`，而新类称为`子类`。子类继承了其父类的所有属性和方法，同时还可以定义自己的属性和方法。

```python
    class Person():
        def show(self):
            print("我是父类")
        def home(self):
            print("涟水")

    class Man(Person):
        def show(self):
            print("我是子类"）

    son = Man()
    son.show()
    son.home()

```

### 多继承

>一个类可以继承多个父类

```python
    class Father():
        def father_show(self):
        print("我是孩子的父亲")
    class Developer():
        def dev_show(self):
        print("我是一名程序员")
    class Myself(Father,Developer):
        def myself_show(self):
        print("我是QK-HuaChong")
    me = Myself()
    me.myself_show()
    me.father_show()
    me.dev_show()
```

### 重写父类方法

>对于父类的方法，只要它不符合子类模拟的实物的行为，都可对其进行重写。为此，可在子类中定义一个这样的方法，即它与要重写的父类方法同名。这样，Python将不会考虑这个父类方法，而只关注你在子类中定义的相应方法。

## 六、文件与异常

### 从文件中读取数据

- open()

>函数open(),打开文件，这样才能访问它。函数open（）接受一个参数：要打开的文件的名称。

- with

>关键字with在不再需要访问文件后将其关闭。

- read()

>使用方法read(),读取这个文件的全部内容

### 写入文件

- open(filename,w)

>调用open()时提供了两个实参。第一个实参也是要打开的文件的名称；第二个实参（'w’）告诉Python，我们要以写入模式打开这个文件。打开文件时，可指定`读取模式（'r’）`、`写入模式（‘w’）`、`附加模式（‘a’）`或让你能够读取和写入文件的模式（'r+'）。

- write()

>我们使用文件对象的方法write()将一个字符串写入文件。

## 七、异常

>Python使用被称为异常的特殊对象来管理程序执行期间发生的错误。每当发生让Python不知所措的错误时，它都会创建一个异常对象。如果你编写了处理该异常的代码，程序将继续运行；如果你未对异常进行处理，程序将停止，并显示一个raceback，其中包含有关异常的报告。

### try-except-else代码块

```python
    try:
        print(5/0)
    except ZeroDivisionError:
        print('You can’t divide by zero')
    else:
        #正确时执行
        print('Correct output')
```

### 存储数据

#### 使用json.dump() 和 json.load()

- json.dump()

>函数json.dump（）接受两个实参：要存储的数据以及可用于存储数据的文件对象。

```python
    import json

    number = [84,46,4587,12]

    filename = 'number.json'
    with open(filename,'w') as f_w:
        json.dimp(number,f_w)
```

- json.load()

>使用json.load()将这个列表读取到内存中

```python
    import json

    filename = 'number.json'
    with open(filename) as f_r:
        numbers = json.load(f_r)
```

#### 实例：

```python
    import json

    class Greet(object):

        def __init__(self, *args, **kwargs):
            return super().__init__(*args, **kwargs)

        def user_new_get(self,username):
            filename = 'userInfo.json'
            with open(filename,'w') as f_w:
                json.dump(username,f_w)
            return username

        def user_save_get(self):
            filename = 'userInfo.json'
            try:
                with open(filename) as f_r:
                    username = json.load(f_r)
            except FileNotFoundError:
                return None
            else:
                return username

        def greet_user(self):
            username = input('Please Enter Your Name:')
            username_saved = self.user_save_get()
            if username == username_saved:
                print('Welcome '+username+' come back!!')
            else:
                username = self.user_new_get(username)
                print('We’ll remeber you when you come back! '+username+'!')

    greet = Greet()

    greet.greet_user()
```