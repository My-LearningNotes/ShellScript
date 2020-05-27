循环语句
========


``while``\ 循环
---------------

``while``\ 循环是Shell脚本中最简单的一种循环, 当条件满足时, \  ``while``\ 重复地执行一组语句, 当条件不满足时, 就退出\ ``while``\ 循环.

Shell while循环的用法如下:

.. code-block:: bash
    :emphasize-lines: 1, 2, 3, 4

    while condition
    do
        statements
    done

``condition``\ 表示判断条件, \ ``statements``\ 表示要执行的语句(可以只有一条, 可以有多条, 但不能为空), \ ``do``\ 和\ ``done``\ 都是Shell中的关键字.

.. note::

    ``while``\ 语句和\ ``if else``\ 语句中的\ ``condition``\ 用法都是一样的, 可以使用\ ``test``\ 或\ ``[]``\ 命令, 也可以使用\ ``(())``\ 或\ ``[[]]``\ .


Example:

.. code-block:: bash

    #!/usr/bin/env bash

    i=1
    sum=0

    while ((i <= 100))
    do
        ((sum += i))
        ((i++))
    done

    echo "The sum is: $sum"


``while``\ 无限循环的语法格式:

.. code-block:: bash
    :emphasize-lines: 1, 2, 3, 4

    while :
    do
        ...
    done

或者

.. code-block:: bash
    :emphasize-lines: 1, 2, 3 ,4

    while true
    do
        ...
    done


``until``\ 循环
---------------

``until``\ 循环和\ ``while``\ 循环恰好相反, 当判断条件不成立时才进行循环, 一旦判断条件成立, 就终止循环.

``until``\ 的使用场景很少, 一般使用\ ``while``\ 即可.

Shell until循环的用法如下:

.. code-block:: bash
    :emphasize-lines: 1, 2, 3, 4

    until condition
    do
        statements
    done

``condition``\ 表示判断条件, \ ``statements``\ 表示要执行的语句(可以只有一条, 可以有多条, 但不能为空), \ ``do``\ 和\ ``done``\ 都是Shell中的关键字.

Example:

    .. code-block:: bash

        #!/usr/bin/env bash

        i=1
        sum=0

        until ((i > 100))
        do
            ((sum += i))
            ((i++))
        done

        echo "The sum is: $sum"


``for``\ 循环
-------------


C语言风格的\ ``for``\ 循环
^^^^^^^^^^^^^^^^^^^^^^^^^^

C语言风格的\ ``for``\ 循环的用法如下:

    .. code-block:: bash
        :emphasize-lines: 1, 2, 3, 4

        for ((expr1; expr2; expr3))
        do
            statements
        done

*   ``expr1``\ 是初始化语句, \ ``expr2``\ 是判断条件, \ ``expr3``\ 在每次循环语句执行之后执行, 他们都是可选的，都可以省略(但分号必须保留);
*   ``statements``\ 是循环体语句, 可以有一条, 也可以有多条, 但是不能为空;
*   ``do``\ 和\ ``done``\ 是Shell中的关键字.


Example:

    .. code-block:: bash

        #!/usr/bin/env bash

        sum=0

        for ((i = 1; i <= 100; i++)
        do
            ((sum += i))
            ((i++))
        done

        echo "The sum is: $sum"

.. note::

    在Shell中, 对Shell变量赋值时, \ ``=``\ 两侧不能有空格;
    但是在其它的情况下, 为了更好的代码格式, 可以在运算符的两侧加上空格.


Python风格的for in循环
^^^^^^^^^^^^^^^^^^^^^^

Python风格的for in循环的用法如下:

    .. code-block:: bash
        :emphasize-lines: 1, 2, 3, 4

        for variable in value_list:
        do
            statements
        done

``variable``\ 表示变量, \ ``value_list``\ 表示取值列表, \ ``in``\ 是Shell中的关键字.

每次循环都会从\ ``value_list``\ 中取出一个值赋给变量\ ``variable``\ , 然后进入循环体, 直到取完\ ``value_list``\ 中的所有值, 循环就结束了.

Example:

    .. code-block:: bash

        #!/usr/bin/env bash

        sum=0

        for n in 1 2 3 4 5 6
        do
            echo $n
            ((sum += n))
        done

        echo "The sum is: $sum"


对value_list的说明
******************

取值列表\ ``value_list``\ 的形式有很多种.

*   **直接给出具体的值**

可以在\ ``in``\ 关键字后面直接给出具体的值, 多个值之间用空格分隔.

Example:

    .. code-block:: bash

        #!/usr/bin/env bash

        for str in "hello" "world" "welcome"
        do
            echo $str
        done

*   **给出一个取值范围**

给出一个取值范围的具体格式为:\ ``{start..end}``\ .

``start``\ 表示起始值, ``end``\ 表示终止值(包括终止值), 注意中间用两个点号相连, 而不是三个点号.

.. attention::

    这种形式只支持数字和字母.

Exmaple:

    .. code-block:: bash

        #!/usr/bin/env bash

        for n in {1..10}
        do
            echo $n
        done

        # 输出从A到z之间的所有字符:
        for c in {A..z}
        do
            echo $c
        done

输出字符时, Shell是根据ASCII码值来输出的.

*   **使用命令的执行结果**

使用反引号\ ``````\ 或者\ ``$()``\ 都可以取得命令的执行结果.

Example:

    .. code-block:: bash

        #/usr/bin/env bash

        # 列出当前目录下的所有Shell脚本
        for filename in $(ls *.sh)
        do
            echo $filename
        done

*   **使用Shell通配符**

Shell通配符可以认为是一种精简化的正则表达式, 通常用来匹配目录或者文件, 而不是文本.

Example:

    .. code-block:: bash

        #/usr/bin/env bash

        # 列出当前目录下的所有脚本文件
        for filename in *.sh
        do
            echo $filename
        done

*   **使用特殊变量**

Shell中有多个特殊变量, 例如: ``$# $* $@ $? $$``\ 等, 在\ ``value_list``\ 中就可以使用它们.

Example:

    .. code-block:: bash

        function func()
        {
            for str in $@
            do
                echo $str
            done
        }

        func C++ Java Python C#

还可以省略\ ``value_list``\ , 省略后的效果和使用\ ``$@``\ 一样.

Example:

    .. code-block:: bash

        function func()
        {
            for str
            do
                echo $str
            done
        }

        func C++ Java Python C#

