条件语句
========


``if``\ 语句
------------

最简单的用法就是只使用if语句, 它的语法格式如下:

.. code-block:: bash
    :emphasize-lines: 1, 2, 3, 4

    if condition
    then
        statement(s)
    fi

也可以将\ ``then``\ 和\ ``if``\ 写在一行:

.. code-block:: bash
    :emphasize-lines: 1, 2, 3

    if condition; then
        statement(s)
    fi

注意, 将\ ``then``\ 和\ ``if``\ 写在一行时, \ ``condition``\ 后边的分号是必须的, 否则会有语法错误.


``condition``\ 是判断条件, 如果\ ``condition``\ 成立(返回"真"), 那么\ ``then``\ 后边的语句将会被执行;
如果\ ``condition``\ 不成立(返回"假"), 那么不会执行任何语句.

注意, 最后必须以\ ``fi``\ 来闭合, 也正是因为有了\ ``fi``\ 来结尾, 所以即使有多条语句也需要用\ ``{}``\ 包围起来.

.. note::

    在Shell中, 语句块不需要使用\ ``{}``\ 包围起来; 也不像Python中, 一定要用相同的缩进.

    但是, 作为一种好的编程习惯, 语句块应该使用相同的缩进.


``if else``\ 语句
^^^^^^^^^^^^^^^^^

.. code-block:: bash
    :emphasize-lines: 1, 2, 3, 4, 5, 6

    if condition
    then
        statement1
    else
        statement2
    fi

如果\ ``condition``\ 成立, 那么\ ``then``\ 后边的\ ``statement1``\ 语句将会被执行; 否则, 执行\ ``else``\ 后边的\ ``statement2``\ 语句.


``if elif else``\ 语句
^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash
    :emphasize-lines: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13

    if condtion1
    then
        statement1
    elif condition2
    then
        statement2
    elif condition3
    then 
        statement3
    ...
    else
        statement
    fi

-   条件语句以关键字\ ``if``\ 开头, 以关键字\ ``fi``\ 结束;
-   ``if``\ /\ ``elif``\ 的下一行总会有一个关键字\ ``then``\ ，然后才是要执行的代码块;
-   不能有空语句, 否则会报错.


``case in``\ 语句
-----------------

当分支较多,  并且判断条件比较简单时, 使用\ ``case in``\ 语句就比较方便了.

``case in``\ 语句的基本格式如下:

    .. code-block:: bash
        :emphasize-lines: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15

        case expression in
            pattern1)
                statement1
                ;;
            pattern2)
                statement2
                ;;
            pattern3)
                statement3
                ;;
            ......
            *)
                statementn
                ;;
         esac

``case`` ``in``\ 和\ ``esac``\ 都是Shell关键字, \ ``expression``\ 表示表达式, \ ``pattern``\ 表示匹配模式.

*   ``expression``\ 既可以是一个变量, 一个数字, 一个字符串, 还可以是一个数学计算表达式, 或者是命令的执行结果, 只要能够得到\ ``expression``\ 的值就可以;
*   ``pattern``\ 可以是一个数字, 一个字符串, 甚至是一个简单的正则表达式.

``case``\ 会将\ ``expression``\ 的值与\ ``pattern1 pattern2 ...``\ 逐个进行匹配:

*   如果\ ``expression``\ 和某个模式匹配成功, 就会执行这个模式后面对应的所有语句(该语句可以有一条, 也可以有多条, 但不能为空), 直到遇到双分号\ ``;;``\ 才停止;
    然后整个\ ``case``\ 语句就执行完了，程序会跳出整个\ ``case``\ 语句, 执行\ ``esac``\ 后面的其它语句;
*   如果\ ``expression``\ 没有匹配到任何一个模式, 那么就执行\ ``*)``\ 后面的语句(\ ``*``\ 表示其它所有值), 直到遇到双分号\ ``;;``\ 或者\ ``esac``\ 才结束.
*   可以没有\ ``*)``\ 部分. 如果\ ``expression``\ 没有匹配到任何一个模式, 那么就不执行任何操作.

.. note::

    case语句就相当与C/C++中的switch语句, \ ``;;``\ 和\ ``*``\ 就相当于\ ``break``\ 和\ ``default``\ .

除最后一个分支外(这个分支可以是普通分支, 也可以是\ ``*)``\ 分支), 其它的每个分支都必须以\ ``;;``\ 结尾, \ ``;;``\ 代表一个分支的结束, 不写的话会有语法错误.
最后一个分支可以写\ ``;;``\ , 也可以不写, 因为无论如何, 执行到\ ``esac``\ 都会结束整个\ ``case in``\ 语句.

Example:

    .. code-block::  bash

        printf "Input integer number:"
        read num

        case $num in
            1)
                echo "Monday"
                ;;
            2)
                echo "Tuesday"
                ;;
            3)
                echo "Wednesday"
                ;;
            4)
                echo "Thursday"
                ;;
            5)
                echo "Friday"
                ;;
            6)
                echo "Saturday"
                ;;
            7)
                echo "Sunday"
                ;;
            *)
                echo "Error"
                ;;
        ecac


``case in``\ 和正则表达式
^^^^^^^^^^^^^^^^^^^^^^^^^

``case in``\ 的\ ``pattern``\ 部分支持简单的正则表达式, 具体来说, 可以使用以下几种格式:

============ ================================================================================
格式         说明
``*``        表示任意字符串
``[abc...]`` 表示字符集合中的任意一个字符. 比如, [15ZH]表示1, 5, Z, H四个字符中的任意一个
``[m-n]``    表示从m到n的任意一个字符. 比如, [0-9]表示任意一个数字,[0-9a-zA-z]表示字母或数字
``|``        表示多重选择, 类似逻辑运算符中的或运算. 比如, abc | xyz表示匹配字符串"abc"或"xyz
============ ================================================================================

如果不加说明, Shell的值都是字符串, \ ``expression``\ 和\ ``pattern``\ 也是按照字符串的方式来匹配的.

最后一个分支\ ``*)``\ 并不是什么语法规定, 它只是一个正则表达式, \ ``*``\ 表示任意字符, 所以不管\ ``expression``\ 的值是什么, \ ``*)``\ 总能匹配成功.

Example:

    .. code-block:: bash

        printf "Input a character:"
        read -n 1 char

        case $char in
            [a-zA-Z])
                printf "\nLetter\n"
                ;;
            [0-9])
                printf "\nDigit\n"
                ;;
            [,.?!])
                printf "\nPunctuation\n"
                ;;
            *)
                printf "\nError\n"
                ;;
        esac

