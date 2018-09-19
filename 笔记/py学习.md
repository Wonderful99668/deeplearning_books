### python学习

2017.9.6

###一.熟悉python基本语法

**1.1**强大的python列表(list)，以及用for循环迭代

*①* list可用“+”连接。例：s=[1]+[2]+[3] ，即s=[1,2,3]。同时，list也可用append()函数进行连接。

*②* 用索引来访问list中每一个位置的元素，索引是从`0`开始的。若要取列表中的最后一个元素，可以用：index[-1]语法

python中的列表不同于数组，它可以存放任何类型的数据，而不去在乎数据的类型，一般情况下遍历列表使用for循环：

```python
for each_flick in List:
    print(each_flick) 
    #其中each_flick是目标标识符
```

迭代处理列表时，相应的会将列表中的各个数值一次赋予 “目标标识符”。

python中内置的一个BIF：instance(),它允许检验某个特定标识符是否包含某个特定类。

example：

```python
names = ["Tom","Jerry"]
print(isinstance(names,list))
>>true
length = len(names)
print(isinstance(length,list))
>>false
```

**1.2**在python中创建一个函数

创建格式：

def + "函数名" + （参数）+“：“

练习：打印嵌套list中的每个数据（遍历列表）

方法：编写递归函数：

```python
def each_item(the_list):
    for item in the_list:
        if isinstance(item,list):
            each_item(item) #递归调用each_item函数
        else:
            print(item)
```

**1.3** dict和set

*dict*

Python内置了字典：dict的支持，dict全称dictionary，在其他语言中也称为map，使用键-值（key-value）存储，具有极快的查找速度。

dict申明 m={};

要删除一个key，可用 用`pop(key)`方法。

*set*

set和dict类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在set中，没有重复的key。

要创建一个set，需要提供一个list作为输入集合：

```python
s = set([1,2,3])
```

set可以看成数学意义上的无序和无重复元素的集合，因此，两个set可以做数学意义上的交集、并集等操作：

```python
>>> s1 = set([1, 2, 3])
>>> s2 = set([2, 3, 4])
>>> s1 & s2
{2, 3}
>>> s1 | s2
{1, 2, 3, 4}
```

**1.4** 切片（slice）

`L[0:n]`表示，从索引`0`开始取，直到索引`n`为止，但不包括索引`3`。即索引为0～n-1。

若第一个索引是0，还可以省略，简写为：L[:3]。

既然Python支持`L[-1]`取倒数第一个元素，那么它同样支持倒数切片

example:L[-2,]。

例如现在有一个list：L = [range(100)]，所有数，每5个取一个：L[::5]

```python
[0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 60, 65, 70, 75, 80, 85, 90, 95]
```

Python没有针对字符串的截取函数，只需要切片一个操作就可以完成，非常简单。

### slice使用的小技巧

（1）L[:] ：原样复制原list

（2）L[-1::-1] : 将列表中的元素取相反的顺序。其中第三个参数 -1 表示从相反方向取值。

：*1.6*  tuple

tuple也是一种list，唯一区别是tuple不可变。因此，tuple也可以用切片操作，只是操作的结果仍是tuple



###二.python的一些常用函数

**1.**input()函数 和 print()函数

input()函数用于获取用户输入，返回的类型是str。str类型不能直接和数字进行比较，要进行强制类型转换。

tips：使print输出时不换行的方法：

python 2.x, print 不换行:

*print x,* 

python 3.x print 不换行

*print(x, end="")*

**2.**range()函数

例如range(6),可以生成0<=num<6的整数。

可以通过list()函数转化为list

注：range(0) = null

**3.**  enumerate()函数

对于一个可迭代的（iterable）/可遍历的对象（如列表、字符串），enumerate将其组成一个索引序列，利用它可以同时获得索引和值。

- enumerate还可以接收第二个参数，用于指定索引起始值，如：

- ```python
  list1 = ["这", "是", "一个", "测试"]
  for index, item in enumerate(list1, 1): #注：enumerate的第二个参数用于指定索引的起始值。
      print index, item
  >>>
  1 这
  2 是
  3 一个
  4 测试
  ```

  ​

**4.** 函数的默认参数

example：

```python
def power(a,x=2)
#其中x即为默认参数
```

当调用power函数时，若没有给x传入参数，则默认x = 2。

设置默认参数时，有几点要注意：

一是必选参数在前，默认参数在后，否则Python的解释器会报错（思考一下为什么默认参数不能放在必选参数前面）；

二是如何设置默认参数。

注：也可以不按顺序提供部分默认参数。当不按顺序提供部分默认参数时，需要把参数名写上。比如调用`enroll('Adam', 'M', city='Tianjin')`，意思是，`city`参数用传进去的值，其他默认参数继续使用默认值。

切记：定义默认参数要牢记一点：默认参数必须指向不变对象！

**5.** 可变参数，关键字参数，命名关键字参数

可变参数：可变参数允许传入0个或多个参数，这些可变参数在函数调用时自动组装为一个tuple。

定义可变参数和定义一个list或tuple参数相比，仅仅在参数前面加了一个`*`号。



关键字参数：如果一个函数定义中的最后一个形参有 ** （双星号）前缀,所有正常形参之外的其他的关键字参数都将被放置在一个字典中传递给函数

example：

```python
def funcF(a, **b):
  print a
  for x in b:
    print (x + ": " + str(b[x]))
```

调用funcF(100, c='你好', b=200)，执行结果
100
c: 你好
b: 200

由以上结果可知，b是一个dict对象实例，它接受了关键字参数b和c。

###三.迭代和迭代器

默认情况下，dict迭代的是key。如果要迭代value，可以用`for value in d.values()`，如果要同时迭代key和value，可以用`for k, v in d.items()`。

如果要对list实现类似Java那样的下标循环怎么办？Python内置的`enumerate`函数可以把一个list变成索引-元素对，这样就可以在`for`循环中同时迭代索引和元素本身：

example：

```python
for i,value in enumerate(['a','b','c']):
    print('索引：',i,'item：',value)
>>>    
索引： 0 item： a
索引： 1 item： b
索引： 2 item： c
```

判断是否为可迭代对象，可用collections模块的Iterable类型判断：

```python
print('Iterable? [1, 2, 3]:', isinstance([1, 2, 3],Iterable))

>>>Iterable? [1, 2, 3]: True
```

----------------------------------------------------------------------------------------------------------------------------------------------------------------

###迭代器（Iterator）

生成器都是`Iterator`对象，但`list`、`dict`、`str`虽然是`Iterable`，却不是`Iterator`。

把`list`、`dict`、`str`等`Iterable`变成`Iterator`可以使用`iter()`函数：

```python
>>> isinstance(iter([]), Iterator)
True
>>> isinstance(iter('abc'), Iterator)
True
```

其中list,dict,str并不是Iterator，这是因为Python的`Iterator`对象表示的是一个数据流，Iterator对象可以被`next()`函数调用并不断返回下一个数据，直到没有数据时抛出`StopIteration`错误。可以把这个数据流看做是一个有序序列，但我们却不能提前知道序列的长度，只能不断通过`next()`函数实现按需计算下一个数据，所以`Iterator`的计算是惰性的，只有在需要返回下一个数据时它才会计算。

### 小结

凡是可作用于`for`循环的对象都是`Iterable`类型；

凡是可作用于`next()`函数的对象都是`Iterator`类型，它们表示一个惰性计算的序列；

### 四.列表生成式和生成器

例：如果要生成`[1x1, 2x2, 3x3, ..., 10x10]`怎么做？

```python
>>> [x * x for x in range(1, 11)]
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

写列表生成式时，把要生成的元素`x * x`放到前面，后面跟`for`循环，就可以把list创建出来，十分有用。

for循环后面还可以加上if判断，这样我们就可以筛选出仅偶数的平方：

```python
>>> [x * x for x in range(1, 11) if x % 2 == 0]
[4, 16, 36, 64, 100]
```

### 生成器（generator）

在Python中，这种一边循环一边计算的机制，称为生成器：generator。

注：generator保存的是算法，并非像list保存的是每个元素。

要创建一个generator，有很多种方法

**方法1：** 只要把一个列表生成式的`[]`改成`()`，就创建了一个generator。其中generator时刻以迭代的对象，因此可以调用for循环获得generator中的元素。

**方法2：** 如果一个函数定义中包含`yield`关键字，那么这个函数就不再是一个普通函数，而是一个generator。

例：斐波那契数列的生成函数：

```python
def fib(max):
    n,a,b = 0,0,1
    while n<max:
        yield b
        b = a+b
        a = b
        n = n+1
    return '\ndone'
```

*注：generator和函数的执行流程不一样。函数是顺序执行，遇到`return`语句或者最后一行函数语句就返回。而变成generator的函数，在每次调用`next()`的时候执行，遇到`yield`语句返回，再次执行时从上次返回的`yield`语句处继续执行。*

generator函数的“调用”实际返回一个generator对象。