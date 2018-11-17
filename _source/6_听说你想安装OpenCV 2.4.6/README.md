## 听说你想安装OpenCV 2.4.6？

*原文链接：
http://zulko.github.io/moviepy/opencv_instructions.html*

</br>
</br>
</br>
</br>

OpenCV对于moviepy来说并不是特别推荐安装，他的安装过程并不总是简单，而且我发现其十分不稳定。若要使用，使用时请额外小心！

</br>

安装过程对于Windows来说似乎比较简单，而在Linux上，这是我在网上找到的教程：

- 如果你之前通过包管理器安装过OpenCV，请在继续之前先移除任何版本的OpenCV；
- 将OpenCV的源码解压到任意目录下，并在该目录下启动终端；
- 建立一个新的目录并进入该目录：

```
mkdir release
cd release
```

- 运行`cmake`。这是我所使用的命令：

```
cmake -D WITH_TBB=ON -D BUILD_NEW_PYTHON_SUPPORT=ON -D WITH_V4L=OFF -D INSTALL_C_EXAMPLES=ON -D INSTALL_PYTHON_EXAMPLES=ON -D BUILD_EXAMPLES=ON ..
```

- 运行`make`。这个过程可能需要几分钟（在我的电脑上大约用了15分钟）。

```
make
```

- 最后，进行安装。

```
sudo make install
```

大功告成！

</br>

你可以通过打开python控制台并输入如下代码来检查OpenCV是否正常运行：

```
import cv2
print cv2.__version__
```

</br>

### 建议
请不要删除你的`release`文件夹。如果以后你碰到了跟`.so`文件相关的OpenCV奇怪的bug，
可以直接重做`sudo make install`这一步。