Shell输入/输出重定向
====================

一般情况下, 每个Linux命令运行时都会打开三个文件:

    *   标准输入文件(``stdin``): 文件描述符为\ **0**\ , 命令从\ ``stdin``\ 读取数据, 默认情况下是终端;
    *   标准输出文件(``stdout``): 文件描述符为\ **1**\ , 命令向\ ``stdout``\ 输出数据, 默认情况下也是终端;
    *   标准错误文件(``stderr``): 文件描述符为\ **2**\ , 命令向\ ``stderr``\ 写入错误信息, 默认情况下也是终端.

重定向命令列表如下:

====================  ==============================================
``command < file``    将标准输入重定向到file
``command > file``    将标准输出重定向到file, 
``command >> file``   将标准输出以追加的方式重定向到file
``command 2> file``   将标准错误重定向到file
``command 2>> file``  将标准错误以追加的方式重定向到file
``m>&n``              将输出m和n合并
``<< tag``            将开始标记tag和结束标记tag之间的内容作为输入
====================  ==============================================


``m>&n``
---------

表示将输出\ *m*\ 合并到\ *n*\ , \ *m*\ 和\ *n*\ 都表示文件描述符.

例如, 将\ ``stderr``\ 合并到\ ``stderr``\ :

.. code-block:: bash

    # 将stderr合并到stdout
    command 2&>1

    # 将stderr合并到stdout，然后重定向到file
    command >> file 2&>1


Here Document
-------------

Here Document是Shell中的一种特殊的重定向方式, 用来将输入重定向到一个交互式脚本或者程序.

它的基本形式如下:

.. code-block:: bash
    :emphasize-lines: 1, 2, 3

    command << delimiter
        document
    delimiter

它的作用是将两个delimiter之间的内容(document)作为输入传递给command.

.. note::

    *   delimiter可以是任意的名称, 但为了可读性, 最好选用恰当的名称且不要和关键字冲突;
    *   结尾的delimiter一定要顶格写, 前面不能有任何字符, 后面也不能有任何字符, 包括空格和tab缩进;
    *   开始的delimiter前后的空格会被忽略掉.

Example:

.. code-block:: bash

    # 在命令行中通过wc -l命令计算行数
    wc -l << EOF
        Hello
        World
    EOF

    # 输出结果为2

也可以写在脚本中:

.. code-block:: bash

    #! /usr/bin/env bash

    cat << Tag
        Hello
        , 
        World
    Tag


/dev/null文件
-------------

如果希望执行某个命令, 但又不希望在屏幕上显示输出结果, 那么可以将输出重定向到\ ``/dev/null``\ :

.. code-block:: bash
    :emphasize-lines: 1

    command > /dev/null

``/dev/null``\ 是一个特殊的文件, 写入到它的内容都会被丢弃; 如果尝试冲该文件读取内容, 什么也读不到.
但是\ ``/dev/null``\ 文件非常有用, 将命令的输出重定向到它, 会起到"禁止输出"的效果.

如果希望屏蔽stdout和stderr, 可以这样写:

.. code-block:: bash
    :emphasize-lines: 1

    command > /dev/null 2>&1

