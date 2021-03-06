列表与元组方法
####################################

Python 中元组的方法并不多，只要不尝试修改元组，与元组“打交道”通常意味着像处理列表一样。

需要注意，因为列表是可以修改的，所以列表方法会直接修改列表，而不会返回修改后的新列表。


- `list.append()`_  在列表的末尾添加一个元素
- `list.clear()`_  清空列表
- `list.copy()`_  返回一个浅复制列表
- `list.count()`_  返回元素在列表中出现的次数
- `list.extend()`_  将可迭代对象中的所有元素，依次添加到列表末尾
- `list.index()`_  查找一个元素，返回元素在列表中第一次出现的索引
- `list.insert()`_  插入一个元素
- `list.pop()`_  删除列表中给定位置（默认最后一个）的元素并返回它
- `list.remove()`_  移除列表中第一个匹配的元素
- `list.reverse()`_  反转列表中的元素
- `list.sort()`_  对列表进行排序




.. _`list.append()`:

list.append(x)
************************************

在列表的末尾添加一个元素。相当于 ``a[len(a):] = [x]`` 。

.. highlight:: none

::

    >>> a = ['a', 'b', 'c']
    >>> a.append('d')
    >>> a
    ['a', 'b', 'c', 'd']


.. _`list.clear()`:

list.clear()
************************************

移除列表中的所有元素（清空列表）。等价于 ``del a[:]`` 。

::

    >>> a = ['a', 'b', 'c']
    >>> a.clear()
    >>> a
    []


.. _`list.copy()`:

list.copy()
************************************

返回一个浅复制的列表，等价于 ``a[:]`` 或 ``list(a)`` 。

::

    >>> a = ['a', 'b', 'c']

    >>> b = a.copy()
    >>> b.append('d')
    >>> b
    ['a', 'b', 'c', 'd']


列表的浅复制和深复制
====================================

在 Python 中进行 a = b 这样的赋值时，会创建一个对 b 的新引用。对于不可变对象（数字、字符串、元组），这种赋值实际上是创建了一个副本。然而，对可变对象（列表或字典）来说，这样赋值的效果大不一样，例如：

在字符串中使用赋值：

::

    >>> a = 'abc'
    >>> b = a
    >>> a = 'ccc'
    >>> b
    'abc'

在列表中使用赋值：

::

    >>> a = ['a', 'b', 'c']
    >>> b = a

    # 在 b 中添加一个元素，a 也会改变
    >>> b.append('d')
    >>> a
    ['a', 'b', 'c', 'd']
    >>> 

为了避免这种情况，必须创建对象的副本而不是创建新引用。对于像列表和字典这样的容器对象，可以使用两种复制操作：浅复制和深复制，原对象中不包含嵌套关系时，可以忽略深浅复制的差异。

**浅复制** 将创建一个新对象，复制的是原对象中所有项的引用。在这个例子中，a 和 b 是单独的列表对象，但包含的嵌套列表是共享的。

::

    >>> a = ['a', 'b', ['c', 'd'], 'e']
    >>> b = a.copy()

    # 在 b 中添加一个元素，a 没有变化
    >>> b.append('f')
    >>> a
    ['a', 'b', ['c', 'd'], 'e']

    # 在嵌套的列表中添加一个元素，a 也会改变
    >>> b[2].append('f')
    >>> b
    ['a', 'b', ['c', 'd', 'f'], 'e', 'f']
    >>> a
    ['a', 'b', ['c', 'd', 'f'], 'e']


**深复制** 将创建一个新对象，并且递归地复制它包含的所有对象。Python 中没有内置操作对对象进行深复制，但可以使用标准库中的 ``copy.deepcopy()`` 函数完成。

::

    >>> import copy

    >>> a = ['a', 'b', ['c', 'd'], 'e']
    >>> b = copy.deepcopy(a)
    >>> b[2].append('f')
    >>> b
    ['a', 'b', ['c', 'd', 'f'], 'e']
    >>> a
    ['a', 'b', ['c', 'd'], 'e']


.. _`list.count()`:

list.count(x)
************************************

返回元素 x 在列表中出现的次数。

::

    >>> ['a', 'b', 'c', 'a', 'e', 'a'].count('a')
    3

    # 嵌套的元素会被理解为一个整体
    >>> ['a', ['a', 'b']].count('a')
    1


.. _`list.extend()`:

list.extend(iterable)
************************************

将可迭代对象 iterable 中的所有元素，依次添加到列表末尾。相当于 ``a[len(a):] = iterable`` 。
    
换言之，可以将一个列表扩展到另一个列表中。这看起来类似于拼接，但存在一个重要的差别，那就是 extend() 将直接修改原来的列表。

::

    >>> a = ['a', 'b', 'c']
    >>> b = ['d', 'e']
    >>> a.extend(b)
    >>> a
    ['a', 'b', 'c', 'd', 'e']

    # 添加元组
    >>> c = ('x', 'y', 'z')
    >>> a.extend(c)
    >>> a
    ['a', 'b', 'c', 'd', 'e', 'x', 'y', 'z']

    # 添加 range 对象
    >>> a.extend(range(3))
    >>> a
    ['a', 'b', 'c', 'd', 'e', 'x', 'y', 'z', 0, 1, 2]

    # 添加字符串
    >>> a.extend('ggg')
    >>> a
    ['a', 'b', 'c', 'd', 'e', 'x', 'y', 'z', 0, 1, 2, 'g', 'g', 'g']


.. _`list.index()`:

list.index(x[, start[, end]])
************************************


查找元素，返回元素 x 在列表中第一次出现的索引（从零开始）。如果没有找到会抛出 ValueError 异常。

可选参数 start 和 end 是切片符号，用于限定查找范围。返回的索引是相对于整个序列的开始计算的，而不是 start 参数。

::

    >>> a = ['a', 'b', 'a', 'c', 'd', 'a', 'e']
    >>> a.index('a')
    0

    # 指定开始范围
    >>> a.index('a', 1)
    2

    # 指定开始，结束范围。没找到会抛出异常
    >>> a.index('a', 3, 5)
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    ValueError: 'a' is not in list


.. _`list.insert()`:

list.insert(i, x)
************************************

在给定的位置插入一个元素。i 参数是要插入位置的索引，x 参数是要插入的元素。

::

    >>> a = ['a', 'b', 'd']
    >>> a.insert(2, 'c')
    >>> a
    ['a', 'b', 'c', 'd']

    # 位置索引大于列表元素的总数，会插入到列表末尾
    >>> a.insert(20, 'e')
    >>> a
    ['a', 'b', 'c', 'd', 'e']

    # 嵌套列表
    >>> a.insert(3, [1, 2, 3])
    >>> a
    ['a', 'b', 'c', [1, 2, 3], 'd', 'e']


.. _`list.pop()`:

list.pop([i])
************************************

删除列表中给定位置（默认最后一个）的元素并返回它。pop() 是唯一既修改列表又返回一个非 None 值的列表方法。

::

    >>> a = ['a', 'b', 'c', 'd']
    >>> a.pop()
    'd'
    >>> a
    ['a', 'b', 'c']

    >>> a.pop(0)
    'a'
    >>> a
    ['b', 'c']


.. _`list.remove()`:

list.remove(x)
************************************

移除列表中第一个值为 x 的元素。如果没有这样的元素，则抛出 ValueError 异常。

::

    >>> a = ['a', 'b', 'a', 'c', 'd']
    >>> a.remove('a')
    >>> a
    ['b', 'a', 'c', 'd']
    >>> a.remove('a')
    >>> a
    ['b', 'c', 'd']

    >>> a.remove('a')
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    ValueError: list.remove(x): x not in list


.. _`list.reverse()`:

list.reverse()
************************************

反转列表中的元素。

::

    >>> a = ['a', 'b', 'c', 'd']
    >>> a.reverse()
    >>> a
    ['d', 'c', 'b', 'a']


.. _`list.sort()`:

list.sort(key=None, reverse=False)
************************************

对列表中的元素进行排序。用于比较的类型必须一致，否则抛出 TypeError 异常。

关键字参数 key 设置一个用于排序规则的函数， ``key=len`` 根据长度对元素进行排序， ``key=str.lower`` 忽略英文字符的大小写。关键字参数 reverse 设置排列的顺序，默认值为 False 按正序排列。

::

    >>> a = [2, 4, 3, 7, 10]
    >>> a.sort()
    >>> a
    [2, 3, 4, 7, 10]

    >>> a.sort(reverse=True)
    >>> a
    [10, 7, 4, 3, 2]

