MoviePy Docker
=================


*原文链接： http://zulko.github.io/moviepy/docker.html*

前提条件
~~~~~~~~

1. 首先确保好正确安装了Docker Docker安装地址：\ `Docker for Mac, Docker
   for windows, linux, etc`_
2. 编译Dockerfile

::

   docker build -t moviepy -f Dockerfile

从Docker运行git源测试的步骤
~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. 首先在moviepy容器内自定义bash提示符

::

   cd tests
   docker run -it -v `pwd`:/tests moviepy bash

2. 运行测试

::

   cd tests
   python test_issues.py

从Docker运行你自己的moviepy脚本
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

将路径改变到你的脚本所在的地方

如果moviepy的Docker已经在运行中，你可以通过如下代码连接：

::

   docker exec -it moviepy python myscript.py

如果Docker还没有在运行

::

   docker run -it moviepy bash
   python myscript.py

你同样可以通过一行代码新建一个容器并运行你的代码

::

   docker run -it -v `pwd`:/code moviepy python myscript.py

.. _Docker for Mac, Docker for windows, linux, etc: https://www.docker.com/get-docker/