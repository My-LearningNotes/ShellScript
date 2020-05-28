Shell ``break``\ 和\ ``continue``
=================================

使用\ ``while``\ , \ ``until``\ , \ ``for``\ , \ ``select``\ 循环时, 如果想提前结束循环, 可以使用\ ``break``\ 或\ ``continue``\ 关键字.

在C/C++, Python等大部分编程语言中, \ ``break``\ 和\ ``continue``\ 只能跳出当前层次的循环, 内层循环中的\ ``break``\ 和\ ``continue``\ 对外层循环不起作用; 
但是Shell中的\ ``break``\ 和\ ``continue``\ 却能够跳出多层循环, 也即使说, 内层循环中的\ ``break``\ 和\ ``continue``\ 能够跳出外层循环.

**在实际开发中, break和continue一般只用来跳出当前层次的循环, 很少有需要跳出多层循环的情况.**


``break``
---------

Shell ``break``\ 关键字的用法为:

.. code-block:: sh

    break n

``n``\ 表示要跳出的循环的层数, 如果省略\ ``n``\ , 表示跳出当前的循环.

``break``\ 关键字通常和\ ``if``\ 语句一起使用, 即满足条件时便跳出循环.

Example:

.. code-block:: sh

    #!/usr/bin/env bash

    sum=0

    while read n
    do
        if ((n>0))
        then
            ((sum += $n))
        else
            break
        fi
    done

    echo "sum=$sum"


``continue``
------------

Shell ``continue``\ 关键字的用法为:

.. code-block:: sh

    continue n

``n``\ 表示循环的层数:

    *   如果省略\ ``n``\ , 表示\ ``continue``\ 只对当前层次的循环语句有效, 忽略本次循环的剩余代码, 直接进入下一次循环;
    *   如果带上\ ``n``\ , 那么\ ``continue``\ 对内层和外层循环语句都有效, 不但内层会跳过本次循环, 外层也会跳过本次循环.

``continue``\ 关键字也通常和\ ``if``\ 语句一起使用, 即满足条件时便跳出循环.

Example:

.. code-block:: sh

    #!/usr/bin/env bash

    sum=0

    while read n
    do
        if ((n<1 || n>100))
        then
            continue
        fi

        ((sum += $n))
    done

    echo "sum=$sum"

