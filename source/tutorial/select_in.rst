Shell select in循环
===================

``select in``\ 是Shell独有的一种循环, 非常适合终端这样的交互场景.
它可以显示出带编号的菜单, 用户输入不同的编号就可以选择不同的菜单, 并执行不同的功能.

Shell ``select in``\循环的用法如下:

.. code-block:: sh

    select variable in value_list
    do
        statements
    done

``variable``\ 表示变量, ``value_list``\ 表示取值列表, ``select``\ 和\ ``in``\ 是Shell中的关键字.

运行到\ ``select``\ 语句后, 取值列表\ ``value_list``\ 中的内容会以菜单的形式显示出来, 
用户输入菜单编号, 就表示选中了某个值, 这个值就会赋给变量\ ``variable``\ , 然后再执行循环体中的语句.

.. attention::

    ``select``\ 是无限循环, 输入空值, 或者输入的值无效, 都不会结束循环, 只有遇到\ ``break``\ 语句, 或者按下\ ``Ctrl + D``\ 组合键才能结束循环.

Example:

.. code-block:: sh

    #!/usr/bin/env bash

    echo "What is your favourite OS?"
    select name in "Linux" "Windows" "Mac OS" "Unix" "Android"
    do
        echo $name
    done

    echo "You have selected $name"

运行后, 会显示如下的列表让用户选择:

.. code-block:: text

    What is your favourite OS?
    1)Linux
    2)Windows
    3)Mac OS
    4)Unix
    5)Android

``select in``\ 通常和\ ``case in``\ 一起使用, 在用户输入不同的编号时可以作出不同的反应.

Example:

.. code-block:: sh

    #!/usr/bin/env bash

    echo "What is your favourite OS?"
    select name in "Linux" "Windows" "Mac OS" "Unix" "Android"
    do
        case $name in
            "Linux")
                echo "Linux是一个类Unix操作系统, 它开源免费, 运行在各种服务器设备和嵌入式设备"
                break
                ;;
            "Windows")
                echo "Windows是微软开发的个人电脑操作系统, 它是闭源收费的"
                break
                ;;
            "Mac OS")
                echo "Mac OS是苹果公司基于Unix开发的一款图形界面操作系统, 只能运行在苹果提供的硬件上"
                break
                ;;
            "Unix")
                echo "Unix是操作系统的开山鼻祖, 现在已经逐渐退出历史舞台, 只应用在特殊场合"
                break;
                ;;
            "Android")
                echo "Android是由Google开发的手机操作系统, 目前已经占据了70%的市场份额"
                break
                ;;
            *)
                echo "输入错误, 请重新输入"
                ;;
        esac
    done

