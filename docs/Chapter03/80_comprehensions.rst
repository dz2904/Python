推导式
####################################

推导式 comprehensions（又称解析式），是 Python 的一种独有特性，它只用一条简洁的表达式就可以构造一个新对象。共有三种推导形式：

- 列表（list）推导式
- 字典（dict）推导式
- 集合（set）推导式


列表推导
************************************

假如要把列表中所有的值都乘以 5，然后构建一个新列表，像下边这样：

.. highlight:: none

::

    nums = [1, 2, 3, 4, 5]
    squares = []
    for n in nums:
    　　squares.append(5 * n)

这种操作很常见，因此才出现了列表推导。在 Python 中应该这样做：

::

    nums = [1, 2, 3, 4, 5]
    squares = [5 * n for n in nums]

列表推导的一般语法如下所示：

::

    [表达式 for 变量 in 列表]  或  [表达式 for 变量 in 列表 if 条件]

    [expression for item1 in iterable1 if condition1
    　　　　　　 for item2 in iterable2 if condition2
    　　　　　　 ...
    　　　　　　 for itemN in iterableN if conditionN ]

这种语法大致上等价于以下代码：

::

    s = []
    for item1 in iterable1:
    　　if condition1:
    　　　　for item2 in iterable2:
    　　　　　 if condition2:
    　　　　　　　 ...
    　　　　　　　 for itemN in iterableN:
    　　　　　　　　　 if conditionN: s.append(expression)

if 语句是可选的，但如果使用它，那么只有 condition 为真的时候才会对 expression 求值并添加到结果中。

::

    a = [-3,5,2,-10,7,8]
    b = 'abc'

    c = [2*s for s in a]
    # c = [-6,10,4,-20,14,16]
    
    d = [s for s in a if s >= 0]
    # d = [5,2,7,8]
    
    e = [(x,y) for x in a for y in b if x > 0 ] 
    # e = [(5,'a'),(5,'b'),(5,'c'), (2,'a'),(2,'b'),(2,'c'), 
    #      (7,'a'),(7,'b'),(7,'c'), (8,'a'),(8,'b'),(8,'c')]
    
    f = [(1,2), (3,4), (5,6)]
    g = [math.sqrt(x*x+y*y) for x,y in f]
    # f = [2.23606, 5.0, 7.81024]

提供给列表推导的序列其长度不必相同，因为从上面的代码可以看出，我们使用了一组嵌套的 for 循环来迭代它们的内容。结果列表包含了各个表达式的运算值。

如果使用列表推导构造元组列表，则元组值必须放在圆括号中。例如， ``[(x, y) for x in a for y in b]`` 是合法的语法，而 ``[x, y for x in a for y in b]`` 是不合法的。


字典推导和集合推导
************************************

字典推导和列表推导的使用方法是类似的，只不过要把 ``[]`` 该改成 ``{}`` ：

::

    # 字典的键乘以 3，字典的值加上 3。
    dic = {1:2, 3:4, 5:6}
    a = { k*3 : v+3 for k,v in dic.items() }
    # a = {3: 5, 9: 7, 15: 9}
    
    # 注意列表推导和字典推导的区别
    b = [(x*3, y+3) for x,y in dic.items()]
    # b = [(3, 5), (9, 7), (15, 9)]

集合推导式也是使用大括号 ``{}`` ，只是传入的值是集合：

::

    a = [-3, 5, -3, 5, 7]
    c = {2*s for s in a}
    # c = {-6, 10, 14}
