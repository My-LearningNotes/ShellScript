``declare``
===========

``declare``\ 命令用来设置变量的属性.

``declare``\ 命令的用法如下:

.. code-block:: sh

    declare [+/-] [aAfFgilprtux] [变量名=变量值]

其中, ``-``\ 表示设置属性, ``+``\ 表示取消属性, ``aAfFgilprtux``\ 都是具体的选项, 它们的含义如下:

+---------------------+----------------------------------------------------------+
| ``-f [name]``       | 列出之前由用户在脚本中定义的函数名称和函数体             |
+---------------------+----------------------------------------------------------+
| ``-F [name]``       | 仅列出自定义函数名称.                                    |
+---------------------+----------------------------------------------------------+
| ``-g name``         | 在Shell函数内部创建全局变量.                             |
+---------------------+----------------------------------------------------------+
| ``-p [name]``       | 显示指定变量的属性和值.                                  |
+---------------------+----------------------------------------------------------+
| ``-a name``         | 声明变量为普通数组.                                      |
+---------------------+----------------------------------------------------------+
| ``-A name``         | 声明变量为关联数组(支持索引下标为字符串).                |
+---------------------+----------------------------------------------------------+
| ``-i name``         | 将变量声明为整数类型.                                    |
+---------------------+----------------------------------------------------------+
| ``-r name[=value]`` | 将变量定义为只读, 等价于readonly name.                   |
+---------------------+----------------------------------------------------------+
| ``-x name[=value]`` | 将变量设置为环境变量, 等价于\ ``export name[=value]``\ . |
+---------------------+----------------------------------------------------------+


Example_1 - 将变量声明为整数并进行计算:

.. code-block:: sh

    #!/usr/bin/env bash

    declare -i m n ret
    m=10
    n=20
    ret=$m+$n
    echo $ret

