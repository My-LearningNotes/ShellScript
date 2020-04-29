简介
====


什么是Shell
-----------

-   ``Shell``\ 是一个用C语言编写的程序, 它是用户使用Linux的桥梁, 用户通过\ ``Shell``\ 访问操作系统内核的服务.


Shell脚本
---------

-   ``Shell``\ 脚本(shell script), 是一种为shell编写的脚本程序;

-   我们所说的shell通常都是指shell脚本, 但我们应该知道, \ ``shell``\ 和\ ``shell script``\ 是两个不同的概念;


Shell环境
---------

Linux的Shell种类众多, 常见的有:

-   Bourne Shell( \ ``/usr/bin/sh``\ 或\ ``/bin/sh``\ )

-   Bourne Again Shell(\ ``/bin/bash``\ )

-   C Shell(\ ``/usr/bin/csh``\ )

-   K Shell(\ ``/usr/bin/ksh``\ )

-   Shell for Root(\ ``/sbin/sh``\ )

-   ...

``bash``\ 由于易用和免费, 在日常工作中被广泛使用;
同时, \ ``bash``\ 也是大多数Linux系统默认的shell;

在一般情况下, 并不区分Bourne Shell和Bourne Again Shell, 所以像\ ``#! /bin/sh``\ 同样可以改为\ ``#! /bin/bash``;


第一个Shell脚本
---------------

.. code-block:: bash

    #! /bin/bash
   
    echo "Hello, world"

-   通常shell script的后缀为\ ``.sh``, 扩展名并不影响脚本执行, 但使用约定的后缀名可以使得我们见名知意, 通过后缀名知道这个一个shell script;

-   ``#!``\ 是一个约定标记, 告诉系统其后路径所指定的程序即是解释此脚本文件的Shell程序;

-   运行shell script有两种方法:

    -   作为解释器的参数

        这种方法运行的脚本, 可以不在第一行指定解释器信息;

    -   作为可执行程序(需要给脚本添加执行权限)


Shell注释
---------

-   以\ ``#``\ 开头的行是注释, 会被解释器忽略;

-   shell中没有多行注释, 只能单行注释;

-   如果在开发过程中, 遇到大段的代码需要临时注释, 过一会又要取消注释, 怎么办呢? 
  
    每一行加个\ ``#``\ 太费力了, 可以把这一段要注释的代码用一对花括号括起来, 定义为一个函数, 没有地方调用这个函数, 这块代码就不会执行, 达到了和注释一样的效果.

