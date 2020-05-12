Shell文件包含
=============

和其它语言一样, Shell也可以包含外部脚本.

Shell文件包含的语法格式如下:

.. code-block:: bash
    :emphasize-lines: 1, 5

    . filename  # 注意点号(.)和文件名中间有一个空格

    或

    source filename


.. note::

    被包含的脚本不需要可执行权限.

