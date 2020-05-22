Shell数组
=========

-   **Bash Shell支持一维数组(不支持多维数组), 初始化时不需要指定数组大小;**
-   **使用圆括号来定义数组, 数组元素之间用空格分隔;**
-   **数组元素可以是不同的类型;**
-   **使用下标引用数组元素, 下标从0开始, 下标可以是整数或算术表达式, 其值应该大于或等于0;**


定义数组
--------

定义数组的一般形式为:

.. code-block:: bash
    :emphasize-lines: 1

    数组名=(值1　值2　值3 ......)

Example:

.. code-block:: bash

    array_name=(
        value0
        value1
        value2
        value3
    )

-   **可以单独定义数组的某个元素, 可以使用不连续的下标, 且下标范围没有限制.**

Example:

.. code-block:: bash

    array_name[0]=0
    array_name[5]=5
    array_name[100]=100


读取数组元素的值
----------------

-   读取数组元素的值和读取变量的值类似, 其一般形式为: 

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

