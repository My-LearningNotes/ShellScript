Shell函数
=========

Shell函数的本质就是一段可以重复使用的脚本代码, 这段代码被提前编写好了, 放在指定的位置, 使用时直接调用即可.

Shell中的函数和C/C++, Python中的函数类似, 只是在语法细节上有所差别.

函数要先定义再使用, 定义在前, 使用在后.


定义函数
--------

shell脚本中定义函数的格式如下:

.. code-block:: sh

    function funcName()
    {
        statements

        [return value]
    }

-   ``function``\ 是Shell中的关键字, 专门用来定义函数;
-   ``funcName``\ 是函数名;
-   函数名后的圆括号中不带任何参数;
-   ``statements``\ 是函数要执行的代码, 也就是一组语句;
-   函数返回, 可以使用\ ``return``\ 语句显式返回, \ ``return``\ 后跟数值n(0 - 255); 
    如果没有\ ``return``\ 语句, 将以最后一条命令的退出状态作为返回值.


函数定义的简化写法
------------------

函数定义时可以省略\ ``function``\ 关键字:

.. code-block:: sh

    funcName()
    {
        statements

        [return value]
    }

如果写了\ ``function``\ 关键字, 也可以省略函数名后面的圆括号:

.. code-block:: sh

    function funcName
    {
        statements

        [return value]
    }

.. note::

    **建议还是使用函数的标准写法, 这样可以"见名知意", 一眼就能看出来这是一个函数.**


调用函数
--------

调用Shell函数时可以给它传递参数, 也可以不传递.
如果不传递, 直接给出函数名即可:

.. code-block:: sh

    funName

如果传递参数, 那么多个参数之间用空格分隔:

.. code-block:: sh

    funName param1 param2 param3 ... paramN

**不管是哪种形式, 函数名后都不需要带括号.**

和其它编程语言不同, Shell函数在定义时不能指明参数, 但是在调用时却可以传递参数, 并且给它传递什么参数它就接收什么参数.


带参数的函数
------------

在调用函数时可以向其传递参数, 在函数内部, 通过\ ``$n``\ 的形式来获取参数的值, 例如, \ ``$1``\ 表示第一个参数, \ ``$2``\ 表示第二个参数..., 以此类推.

此外, 可以在函数中使用的特殊变量还有: ``$#``, ``$*``, ``@``, ``$?``, 见 :ref:`ShellSpecialVariable-reference-label`.

Example:

.. code-block:: sh
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
    
    当参数个个数达到或超过10个时, 需要用\ ``${n}``\ 的形式来获取参数.


函数的返回值
------------

在C/C++, Python等大部分编程语言中, 返回值是指函数被调用之后, 执行函数体中的代码所得到的结果, 这个结果通过\ ``return`` 语句返回.

但是Shell中的返回值表示的是函数的\ **退出状态**\ : 返回值为0表示函数执行成功了, 返回非0表示函数执行失败了.
if, while, for等语句都是根据函数的退出状态来判断条件是否成立.

Shell函数的返回值只能是一个介于0~255之间的整数, 其中只有0表示成功, 其它值都表示失败.
函数执行失败时, 可以根据返回值(退出状态)来判断具体出现了什么错误, 比如一个打开文件的函数, 我们可以指定1表示文件不存在, 2表示文件没有读取权限, 3表示文件类型不对.

.. note::

    在Shell函数中, 注意区分函数的返回值和函数的处理结果.

    返回值是指函数的退出状态, 是一个0~255的值, 0表示执行成功, 非0表示失败.

    处理结果, 是指函数对输入进行处理后的输出.


如果函数中没有return语句, 那么使用默认的退出状态, 也就是最后一条命令的退出状态.
如果这就是你想要的, 那么更加严谨的写法是:

.. code-block:: bash

    return $?


如何得到函数的处理结果?
^^^^^^^^^^^^^^^^^^^^^^^

既然return表示函数的退出状态, 那么该如何得到函数的处理结果呢?
比如, 我定义了一个函数, 计算从m到n的和, 最终得到的结果该如何返回呢?

这个问题有两种解决方案:

*   一种是借助全局变量, 将得到结果赋值给全局变量;

Example:

.. code-block:: sh
    :emphasize-lines: 9

    #!/usr/bin/env bash
        
    sum=0  # 全局变量

    function getSum()
    {
        for ((i = $1; i <= $2; i++))
        do
            ((sum += i))  # 改变全局变量
        done

        return $?
    }

    read m
    read n

    if getSum $m $n
    then
        echo "The sum is: $sum"  # 输出全局变量
    else
        echo "Error!"
    fi

这种方案的弊端是: 定义函数的同时还需要额外定义一个全局变量, 如果我们仅仅知道函数的名字, 但是不直到全局变量的名字, 那么是无法获取结果的.

*   一种是在函数内部使用\ ``echo``\ , \ ``printf``\ 命令将结果输出, 在函数外部使用\ ``$()``\ 或者\ ``````\ 捕获结果.

.. attention::

    如果函数中有多个\ ``echo``\ 或\ ``printf``\ 命令, 捕获第一个命令的输出作为处理结果.

Example:

.. code-block:: sh
    :emphasize-lines: 12, 19
    
    #!/usr/bin/env bash

    funciton getSum()
    {
        local sum=0  # 局部变量

        for ((i = $1; i < $2; i++))
        do
            ((sum += i))
        done

        echo $sum
        return $?
    }

    read m
    read n

    total=$(getSum $m $n)
    echo "The sum is: $total"
    
    # 也可以省略total变量, 直接写成下面的形式
    echo "The sum is: $(getSum $m $n)"

这种方法的弊端是: 如果不使用\ ``$()``\ , 而是直接调用函数, 那么就会将结果直接输出在终端上, 不过这也无所谓, 推荐使用这种方案.

