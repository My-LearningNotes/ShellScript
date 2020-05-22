Shell变量
=========


定义Shell变量
-------------

-   **定义变量时, 没有变量类型, 直接给出变量名;**
-   变量名只能包含数字, 字母和下划线, 且不能以数字开头(和C语言中变量的命名规则相同);
-   变量名不能使用\ ``bash``\ 里的关键字(可以用\ ``help``\ 命令查看保留关键字);
-   **变量名, 值和等号之间不能有空格.**

Example:

.. code-block:: bash

    str="hello, world"  # 正确
    str = "hello, world"  # 错误


使用变量
--------

-   使用一个定义过的变量的值, 只要在变量名前加上\ ``$``\ 即可;

.. code-block:: bash
    :emphasize-lines: 2

    str="Hello, world"
    echo $str


.. attention::

    注意区分变量名和变量的值.

    变量名只是一个名称(符号), 变量的值是这个名称绑定的值.

-   变量名外面的花括号是可选的, 加不加都行, 加花括号是为了帮助解释器识别变量的边界;

Example:

.. code-block:: bash

    #! /bin/bash

    for skill in Ada Coffe Action Java; do
        echo "I am good at ${skill}script
    done

    # 如果不给skill变量加上花括号
    # 写成 echo "I am good at $skillscript",解释器会把$shillscript当成一个变量
    # 代码执行的结果就不是我们期望的样子了

**建议给所有变量加上花括号, 这是一个好的编程习惯.**

-   已定义的变量, 可以重新赋值;

Example:

.. code-block:: bash

    name="hello"
    name="world"


只读变量
--------

-   使用\ ``readonly``\ 可以将变量定义为只读的;

-   可以在定义变量的同时将其声明为\ ``readonly``\ 的;

.. code-block:: bash

    readonly name="hello"

-   也可以先定义变量, 再将其声明为\ ``readonly``\ 的.

.. code-block:: bash

    name="hello"
    readonly name


删除变量
--------

-   使用\ ``unset``\ 命令可以删除变量, 其语法为:

    .. code-block:: bash

        unset variable_name

变量删除之后不能再次使用, ``unset``\ 命令不能删除只读变量.


变量类型
--------

运行Shell时, 会同时存在三种变量:

-   **局部变量**

局部变量是在脚本或命令中定义, 仅在当前shell实例中有效, 其他shell启动的程序不能访问局部变量.

-   **环境变量**

整个系统的环境配置, 所有的程序, 包括shell启动的程序, 都能访问环境变量, 有些程序需要环境变量来保证其正常运行.
必要的时候shell脚本也可以定义环境变量.

-   **Shell内置变量**

Shell内置变量是由Shell程序设置的特殊变量.

