Shell字符串
===========

字符串是shell编程中最常用最有用的数据类型, 字符串可以使用单引号包裹, 也可以使用双引号, 也可以不用引号.

.. code-block:: bash

    str1='hello'
    str2="hello"
    str3=hello


单引号
------

单引号字符串的限制:

-   单引号里的任何字符都会作为原始字符原样输出(所见即所得), 单引号字符串中的变量是无效的;

-   单引号字符串中不能出现单引号(对单引号使用转义字符后也不行, 因为单引号中的所有字符都作为原始字符, 转义字符在单引号中也是作为原始字符, 失去了转义的作用).


双引号
------

双引号的优点:

-   双引号里可以有变量;

-   双引号里可以出现转义字符.


拼接字符串
----------

-   拼接字符串时, 把两个字符串写在一起, 中间不能有空白字符;

Example:

.. code-block:: bash

    str1="hello""world"
    echo ${str1}

    str2="hello"
    str3="world"
    str4=${str2}${str3}
    echo ${str4}

    str5="hello"${str3}
    echo ${str5}


获取字符换长度
--------------

获取字符串长度的语法形式为: \ ``${#strName}``

.. code-block:: bash

    str="hello,world."
    echo ${#str}


提取子字符串
------------

提取子字符串的语法形式为: 

.. code-block:: bash
    
    ${strName:start:length}

表示从索引值为\ ``start``\ 的位置开始, 提取长度为length的字符串.

.. code-block:: bash

    str="hello,world."
    str1=${str:1:4}
    echo ${str1}

.. note::

    提取子字符串, 类似于Python中的切片.


