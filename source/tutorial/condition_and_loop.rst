Shell控制流程
=============

-   在条件/循环语句中, shell的控制流程不可为空, 即不能有空语句;
-   用相同的缩进表示代码块.


条件语句
--------

.. code-block:: bash
    :emphasize-lines: 1, 2, 6, 7, 11, 15

    if confition1
    then
        command1
        command2
        ...
    elif condition2
    then
        command3
        command4
        ....
    else
        command5
        command6
        ...
    fi

-   条件语句以关键字\ ``if``\ 开头, 以关键字\ ``fi``\ 结束;
-   ``if``\ /\ ``elif``\ 的下一行总会有一个关键字\ ``then``\ ，然后才是要执行的代码块.


``while``\ 循环语句
-------------------

.. code-block:: bash
    :emphasize-lines: 1, 2, 5

    while condition
    do
        command
        ...
    done

-   以关键字\ ``while``\ 开头;
-   ``while``\ 的下一行是关键字\ ``do``\ , 之后的行才是要执行的代码块;
-   以关键字\ ``done``\ 结束.


Example:

.. code-block:: bash

    # 使用while循环从键盘读取信息
    echo "Press <CTRL-D> to quit"
    while read var
    do
        ...
    done


``while``\ 无限循环的语法格式:

.. code-block:: bash
    :emphasize-lines: 1, 2, 4

    while :
    do
        ...
    done

或者

.. code-block:: bash
    :emphasize-lines: 1, 2, 4

    while true
    do
        ...
    done


``for``\ 循环语句
-----------------

``for``\ 循环语句用来迭代一个列表, 其一般格式为:

.. code-block:: bash
    :emphasize-lines: 1, 2, 4

    for var in item1 item2 ... itemN
    do
       ...
    done

-   ``for``\ 循环语句总是以关键字\ ``for``\ 开头;
-   ``for``\ 的下一行是关键字\ ``do``\ , 之后才是要执行的代码块;
-   以关键字\ ``done``\ 结束.


``for``\ 无限循环:

.. code-block:: bash
    :emphasize-lines: 1, 2, 4

    for (( ; ; ))
    do
        ...
    done


``until``\ 循环
---------------

``until``\ 循环执行一系列命令, 直到条件为\ ``true``\ 时退出.

一般格式为:

.. code-block:: bash
    :emphasize-lines: 2, 3, 5

    # condition通常为条件表达式, 当成立时推出循环
    until condition
    do
        ...
    done


``case``
--------

``case``\ 语句就是\ ``switch``\ 语句.

一般格式为:

.. code-block:: bash
    :emphasize-lines: 1, 2, 6, 7, 11, 12

    case var in
    模式1)
        command1
        command2
        ...
        ;;
    模式2)
        command1
        command2
        ...
        ;;
    esac

-   ``var``\ 后面是关键字\ ``in``\ ;
-   每个模式以右圆括号结束;
-   var可以是变量或常数
-   每个模式下执行的代码块以\ ``;;``\ 结束;
-   整个\ ``case``\ 语句以\ ``esac``\ 结束.

