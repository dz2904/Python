reStructuredText 标记规范
#####################################

概述
*******************

reStructuredText 是扩展名为 ``.rst`` 的纯文本文件，是轻量级标记语言的一种，也被简称为：``RST`` 或 ``reST``；
它是 Python 编程语言的 Docutils_ 项目的一部分，Docutils_ 能够从 Python 程序中提取注释和信息，并格式化为程序文档。
或由 Sphinx-Doc 这样的程序转换为 HTML 或 PDF 等多种格式。

本文语法来自 `reStructuredText Markup Specification`_。

.. _Docutils: http://docutils.sourceforge.net/

.. _Sphinx-Doc: http://www.sphinx-doc.org/en/master/

.. _`reStructuredText Markup Specification`: http://docutils.sourceforge.net/docs/ref/rst/restructuredtext.html


章节标题
*******************

章节标题由下线（也可有上线）标记，其中下线长度不得小于标准文本的长度。

官方建议使用的符号有::

    = - ` : . ' " ~ ^ _ * + #

对于相同的符号，有上标是一级标题，没有上标是二级标题。

标题最多分六级，可以自由组合使用。

全加上上标或者是全不加上标，使用不同的 6 个符号的标题依次排列，则会依次生成的标题为H1-H6。

.. code-block:: none

    Section Title
    ###############

    Section Title
    ***************

    Section Title
    ===============

    Section Title
    ----------------

    Section Title
    .............

    Section Title
    ~~~~~~~~~~~~~

段落
*******************

段落是被空行分割的文字片段，左侧必须对齐（没有空格，或者有相同多的空格）。

块
*******************

代码块
===================

| 代码块就是一段文字信息，在需要插入文本块的段落后面加上 ``::`` ，接着一个空行，然后就是内容了。
| 一般会对代码库添加边框，并保持原有格式（多行或缩进）。
| 代码块不能顶头写，要有缩进。

.. code-block:: none

    下面是文字块内容：
    ::

       这是一段文字块
       同样也是文字块
       还是文字块

    这是新的一段。

行块
===================

| 行块是以 ``|`` 开头，后跟一个空格。每一个行块可以是多行文本。行块对于地址、诗句以及无装饰列表是非常有用的。
| 行块会保持原有格式，两行紧邻并不会合并为一行。

.. code-block:: none

    下面是行块内容：

      | Lend us a couple of bob till Thursday.
      | I'm absolutely skint.
      | But I'm expecting a postal order and I can pay you back
        as soon as it comes.
      | Love, Ewan.

    这是新的一段。

块引用
===================

块引用是通过缩进来实现的，引用块要在前面的段落基础上缩进。

通常引用的结尾会加上出处，出处的文字块以 ``—`` 、 ``--`` 、 ``---`` 开头。

.. code-block:: none

    下面是引用的内容：

        “真的猛士，敢于直面惨淡的人生，敢于正视淋漓的鲜血。”

        --- 鲁迅

    ..

          “人生的意志和劳动将创造奇迹般的奇迹。”

          — 涅克拉索


文档测试块
===================

文档测试块是交互式的 Python 会话，以 ``>>>`` 开始，一个空行结束。文档测试块被视为文字块的特例，
不需要文字块语法。如果两者都存在，则文本块语法优先于文档测试块语法。

.. code-block:: none

    >>> print "This is a doctest block."
    This is a doctest block.

行内标记
*******************

行内标记必须满足以下条件：

- 行内标记开始之前和结束字符之后，都必须紧跟空白字符（空格）
- 行内标记开始之后和结束字符之前，都必须紧跟非空白字符
- 行内标记开始至结束字符之间至少包含一个字符

.. code-block:: none

    *重点，通常显示为斜体*
    `解释文字，通常显示为斜体`
    **重点强调，通常显示为粗体**
    ``行内代码，通常显示为等宽字体，空格会保留，但是换行不可以。``

列表
*******************

无序列表
===================

符号列表可以使用 ``-、*、+`` 来表示。

不同的符号结尾需要加上空行，二级列表需要缩进。

.. code-block:: none

    - 符号列表1
    - 符号列表2

      - 二级符号列表1
      - 二级符号列表2
      - 二级符号列表3

    * 符号列表3

    + 符号列表4

有序列表
===================

可用的有序列表序号：

- 阿拉伯数字: 1, 2, 3, ... (无上限)。
- 大写字母: A-Z。
- 小写字母: a-z。
- 大写罗马数字: I, II, III, IV, ..., MMMMCMXCIX (4999)。
- 小写罗马数字: i, ii, iii, iv, ..., mmmmcmxcix (4999)。

有序列表必须为序号添加后缀，下面的形式是被允许的：

. 后缀：``1., A., a., I., i.``
() 包起来: ``(1), (A), (a), (I), (i)``
) 后缀: ``1), A), a), I), i)``

有序列表可以结合 ``#`` 自动生成序号。

.. code-block:: none

    1. 有序列表 1
    #. 有序列表 2
    #. 有序列表 3

    (I) 有序列表 1
    (#) 有序列表 2
    (#) 有序列表 3

    A) 有序列表 1
    #) 有序列表 2
    #) 有序列表 3

字段列表
===================

字段列表用于扩展语法的一部分，可用于类似数据库记录（标签和数据对）的两列表类结构。
在某些上下文中，重新构造文本的应用程序可以识别字段名和转换字段或字段主体。

.. code-block:: none

    :标题: reStructuredText语法说明

    :作者: - Seay
        - Seay1
        - Seay2

    :时间: 2016年06月21日

    :概述: 这是一篇
        关于reStructuredText
        语法说明。

选项列表
===================

选项列表是一个类似两列的表格，左边是参数（不能以单词开头），右边是描述信息。当参数选项过长时，参数选项和描述信息会分行显示。

选项与参数之间有一个空格（否则参数不能有空格），参数选项与描述信息之间至少有两个空格。

.. code-block:: none

    -a            command-line option "a"
    -b file       options can have arguments
                  and long descriptions
    --long        options can be long also
    --input=file  long options can also have
                  arguments
    /V            DOS/VMS-style options too


选项列表
===================

定义列表可以理解为解释列表，即名词解释。
条目占一行，解释文本需要缩进。

.. code-block:: none

    定义1
       这是定义1的内容。

    定义2
       这是定义2的第A项。
       这是定义2的第B项。


表格
*******************

网格表
===================

网格表通过类似网格的“ASCII艺术”提供完整的表格表示。网格表允许任意单元格内容，以及行和列跨度。
但是，网格表生成起来很麻烦，特别是对于简单的数据集。

网格表是用一个由字符 ``- 、= 、| 、+`` 组成的可视化网格来描述的。
``-`` 用来分隔行，``=`` 用来分隔表头和表体行，``|`` 用来分隔列，``+`` 用来表示行和列相交的节点。

.. code-block:: none

    +------------+------------+-----------+
    | Header 1   | Header 2   | Header 3  |
    +============+============+===========+
    | body row 1 | column 2   | column 3  |
    +------------+------------+-----------+
    | body row 2 | Cells may span columns.|
    +------------+------------+-----------+
    | body row 3 | Cells may  | - Cells   |
    +------------+ span rows. | - contain |
    | body row 4 |            | - blocks. |
    +------------+------------+-----------+

简单表
===================

简单表格为简单的数据集提供了紧凑且易于输入的表格形式。
单元格内容通常是单个段落，但是在大多数单元格中可以表示任意的主体元素。

使用由 ``=`` 和 ``-`` 字符组成的水平边框描述简单表格。
等号 ``=`` 用于表格边框的顶部和底部，并用于区分标题行和表格主体。
连字符 ``-`` 用于指示单行中的列跨度，并用于视觉上分隔行。

一个简单的表格以等号的顶部边框开始，每个列边界有一个或多个空格（建议使用两个或多个空格）。
无论跨度如何，顶部边框都必须完整描述所有表格列，建议边框长度包含整列文本。表中必须至少有两列（以区别于节标题）。



.. code-block:: none

    =====  =====  =======
      A      B    A and B
    =====  =====  =======
    False  False  False
    True   False  False
    False  True   False
    True   True   True
    =====  =====  =======

    =====  =====  ======
       Inputs     Output
    ------------  ------
      A      B    A or B
    =====  =====  ======
    False  False  False
    True   False  True
    False  True   True
    True   True   True
    =====  =====  ======

链接
*******************

自动超链接
===================

reStructuredText 会自动将网址生成超链接。

.. code-block:: none

    这个网址会自动生成链接：https://www.python.org/

外部超链接
===================

外部超链接目标在其链接块中具有绝对或相对链接地址或电子邮件地址。

.. code-block:: none

    Python_ 是一种高级的程序设计语言。这是一个单词链接示例

    .. _Python: https://www.python.org/

    `Python 3.6`_ 包含许多新功能和优化。这是一个短语链接示例，注意后边是两个短横

    .. _`Python 3.6`: https://docs.python.org/3.6/

    `Python <https://www.python.org/>`_ 是一种高级的程序设计语言。

内部超链接 | 锚点
===================

一个内部的超链接目标指向目标后面的元素。

.. code-block:: none

    更多信息参考 锚点_

    这里包含其它文档内容...

    .. _锚点:

    这是锚点定位的元素

匿名超链接
===================

万维网联盟建议应“明确识别每个链接地址”，超链接引用应尽可能详细。但在实际应用中复制冗长的超链接名称是繁重且容易出错的。
匿名超链接旨在允许方便的超链接引用，类似于自动编号脚注。它们在短文档或一次性文档中特别有用。
但是，此功能很容易被滥用，并且可能导致不容易维护的文档，建议谨慎。

.. code-block:: none

    这篇文章参考的是：`Quick reStructuredText`__。

    __ http://docutils.sourceforge.net/docs/user/rst/quickref.html

间接超链接
===================

间接超链接在其链接块中具有超链接引用。实际上，类似于关联变量赋值。

.. code-block:: none

    .. _one: two_
    .. _two: three_
    .. _three:

隐式超链接
===================

隐式超链接目标由章节标题，脚注和引用自动生成，也可以由扩展构造生成。隐式超链接目标的行为与显式超链接目标的行为相同。
如果命名有冲突的话，显式超链接目标会覆盖具有相同引用名称的任何隐式目标。

.. code-block:: none

    第一节 介绍
    ===========

    其他内容...

    隐式链接到 `第一节 介绍`_，即可生成超链接。

图片
*******************

图像源文件的URI与超链接目标类似，图像URI可以与显式标记开始和目标名称在同一行开始，
或者它可以在紧随其后的缩进文本块中开始，不能有空行。

.. code-block:: none

    .. image:: picture.jpeg
       :height: 100px
       :width: 200 px
       :alt: alternate text
       :align: right


替换引用
*******************

替换引用就是用定义的指令替换对应的文字或图片，和内置指令(inline directives)类似。
替换文本不能以空格开头或结尾。

.. code-block:: none

    这是 Pythond Logo: |logo|，我的最喜欢的语言是:|name|。

    .. |logo| image:: https://www.python.org/static/img/python-logo.png
    .. |name| replace:: Python


脚注引用
*******************

脚注引用，有几种方式：

- 手工标记序号（标记序号 1、2、3 之类）
- 自动序号（填入 # 会自动填充序号）
- 自动符号（填入 * 会自动生成符号）

手工序号可以和 # 结合使用，会自动延续手工的序号。

# 表示的方法可以在后面加上一个名称，这个名称就会生成一个链接。

.. code-block:: none

    脚注引用一 [1]_
    脚注引用二 [#]_
    脚注引用三 [#]_
    脚注引用四 [#跳转]_

    .. [1] 脚注内容一
    .. [#] 脚注内容二
    .. [#] 脚注内容三
    .. [#跳转] 脚注内容四，点击“跳转”到此

    其他的文本内容...

    跳转_

引用参考
*******************

引用参考与上面的脚注有点类似。引用参考是简单的引用名称
（不区分大小写的单词，由字母数字加上下划线等连字符组成；不能有有空格）。

.. code-block:: none

    引用参考的内容通常放在页面结尾处，比如 [CIT2002]_

    .. [CIT2002] 引用参考


分隔符
*******************

分隔符就是一条水平的横线，是由最少 4 个 ``-`` 组成，前后需要添加换行。

.. code-block:: none

    上面部分

    ------------

    下面部分

注释
*******************

注释以 ``..`` 开头，后面接注释内容即可，可以是多行内容，多行时要有缩进。

.. code-block:: none

    ..
      我是注释内容
      你们看不到我
