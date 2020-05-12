Shell函数
=========

-   可以在shell脚本中定义函数, 然后调用;
-   所有函数都必须先定义再使用.

定义函数
--------

shell脚本中定义函数的格式如下:

.. code-block:: bash
    :emphasize-lines: 1

    [function] funName()
    {
        ...

        [return int;]
    }

-   定义函数, 可以以关键字\ ``function``\ 开头, 也可以没有关键字\ ``function``\ ;
-   函数名后的圆括号中不带任何参数;
-   函数返回, 可以使用\ ``return``\ 语句显式返回, \ ``return``\ 后跟数值n(0 - 255);
    如果没有\ ``return``\ 语句, 将以最后一条命令的运行结果, 作为返回值.


调用函数
--------

通过函数名调用函数, 函数名后没有圆括号.

Example:

.. code-block:: bash
    :emphasize-lines: 3, 4, 9, 10

    #! /usr/bin/env bash

    # 定义函数
    demoFun()
    {
        echo "hello, world"
    }

    # 调用函数
    demoFun


带参数的函数
------------

在调用函数时可以向其传递参数, 在函数内部, 通过\ ``$n``\ 的形式来获取参数的值, 例如, \ ``$``\ 表示第一个参数, \ ``$2``\ 表示第二个参数...


    *   不论在调用函数时是否向其传递参数, 定义函数时, 函数名后面的圆括号中都不带任何参数;
    *   调用函数时, 向其传递的参数在函数名后依次列出, 参数之间用空格分隔(就像在命令行中传递参数一样).

Example:

.. code-block:: bash
    :emphasize-lines: 12

    #! /usr/bin/env bash

    funWithParam()
    {
        echo "第一个参数为 $1 !"
        echo "第二个参数为 $2 !"
        echo "第十个参数为 ${10} !"
        echo "参数总共有 $# 个!"
        echo "作为一个字符串输出所有参数 $* !"
    }

    funWithParam 1 2 3 4 5 6 7 8 9 66 88

.. note::

    在函数中, 通过\ ``$n``\ 的形式获取参数; 当\ ``n >= 10``\ 时, 需要使用\ ``${n}``\ 来获取参数.


一些用来处理参数的特殊字符:

======  ===========================================================
``$#``  传递到脚本或函数的参数个数
``$*``  以一个单字符显示所有传递的参数
``$$``  脚本运行的当前进程号
``$!``  后台运行的最后一个进程的ID
``$@``  与\ ``$*``\ 相同, 但是使用时加引号, 并在引号中返回每个参数
``$-``  显示Shell使用的当前选项, 与\ ``set``\ 命令功能相同
``$?``  显示最后命令的退出状态, 0表示没有错误, 其他任何值表示有错误
======  ===========================================================


******

扩展
----

* 函数与命令的执行结果可以作为条件语句/循环语句中的条件使用, 但需要注意的在shell中0表示true, 0以外的值表示false.

Example:

.. code-block:: bash
    :emphasize-lines: 8, 15, 32, 39
    
    #! /usr/bin/env bash

    echo "Hello World !" | grep -e Hello
    echo $?
    echo "Hello World !" | grep -e Bye
    echo $?

    if echo "Hello World !" | grep -e Hello
    then 
        echo true
    else
        echo false
    fi

    if echo "Hello World !" | grep -e Bye
    then
        echo true
    else
        echo false
    fi

    function demoFun1()
    {
        return 0
    }

    function demoFun2()
    {
        return 1
    }

    if demoFun1
    then
        echo true
    else
        echo false
    fi

    if demoFun2
    then
        echo true
    else
        echo false
    fi
    
