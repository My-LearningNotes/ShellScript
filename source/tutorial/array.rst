Shell数组
=========

和其它编程语言一样, Shell也支持数组.
数组(Array) 是若干数据的集合, 其中的每一个数据都称为元素(Element).

-   Bash Shell支持一维数组(不支持多维数组), 初始化时不需要指定数组大小;
-   使用圆括号来定义数组, 数组元素之间用空格分隔;
-   数组元素可以是不同的类型;
-   使用下标引用数组元素, 下标从0开始, 下标可以是整数或算术表达式, 其值应该大于或等于0.


定义数组
--------

在Shell中, 用圆括号\ ``()``\ 来定义数组, 数组元素之间用空格分隔.

-   定义数组的一般形式为:

.. code-block:: bash
    :emphasize-lines: 1

    array_name=(ele1 ele2 ele3 ... elen)

注意, 和变量定义一样, \ ``=``\ 两侧不能有空格.

Example:

.. code-block:: bash

    nums=(1 2 3 4 5)

-   在Shell中, 数组元素可以是不同类型的.

Example:

.. code-block:: bash

    arr=(1 2 3 "hello" "world")

-   可以单独定义数组的某个元素, 可以使用不连续的下标, 且下标范围没有限制.

Example:

.. code-block:: bash

    array_name[0]=0
    array_name[5]=5
    array_name[100]=100


获取数组元素
------------

-   获取数组元素的值和读取变量的值类似, 其一般形式为: 

.. code-block:: bash
    :emphasize-lines: 1
    
    ${arrayName[index]}

-   使用\ ``＠``\ 或\ ``*``\ 符号作为索引值可以获取数组中的所有元素, 其一般形式为: 
  
.. code-block:: bash
    :emphasize-lines: 1, 3
    
    ${arrayName[@]}
    # or
    ${arrayName[*]}

Example:

.. code-block:: bash

    array=(1 2 "hello" "world")
    echo ${array[@]}


获取数组的长度
--------------

-   获取数组长度的方法与获取字符串长度的方法相同, 其一般形式为: 
  
.. code-block:: bash
    :emphasize-lines: 1, 3
    
    ${#arrayName[@]}
    # or
    ${#arrayName[*]}

-   获取数组中单个元素的长度: 
  
.. code-block:: bash
    :emphasize-lines: 1
    
    ${#arrayName[n]}


数组拼接
--------

所谓数组拼接(数组组合), 就是将两个数组连接成一个数组.

拼接数组的思想是: 先利用\ ``@``\ 或\ ``*``\ 将数组展开成列表, 然后再合并到一起, 具体格式如下:

.. code-block:: bash
    :emphasize-lines: 1, 2

    array_new=(${array1[@] ${array2[@])
    array_new=(${array1[*] ${array2[*])

两种方式是等加的, 选择其一即可.


删除数组元素
------------

删除数组元素和删除变量一样, 使用\ ``unset``\ 关键字, 具体格式如下:

.. code-block:: bash
    :emphasize-lines: 1

    unset array_name[index]

如果不写下标, 而是下面的形式:

.. code-block:: bash
    :emphasize-lines: 1
    
    unset array_name

表示删除整个数组.

