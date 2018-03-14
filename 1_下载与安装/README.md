## 下载与安装

### 安装

**pip安装方式**：如果你安装了`pip`，只需要在终端输入如下命令（若没有安装ez_setup，则会自动安装）

```
(sudo) pip install moviepy
```

如果你既没有安装`setuptools`也没有安装`ez_setup`，那么上述命令就会运行失败。在这种情况下，你需要在安装前运行：

```
(sudo) pip install ez_setep
```

**手动安装方式**：从 [PyPI](https://pypi.python.org/pypi/moviepy) 或者 [Github](https://github.com/Zulko/moviepy) （开发版本）上下载源码。将所有文件解压到同一文件夹，打开终端并输入

```
(sudo) python setup.py install
```

MoviePy依赖 [Numpy](https://www.scipy.org/install.html) 、 [imageio](https://imageio.github.io/) 、 [Decorator](https://pypi.python.org/pypi/decorator) 和 [tqdm](https://pypi.python.org/pypi/tqdm) ，他们将在安装MoviePy的同时自动安装。运行平台为Windows/Mac/Linux，并使用Python2.7以上的版本和Python3。如果在安装MoviePy及其依赖包的过程中存在问题，请提供反馈。

MoviePy依赖FFMPEG软件对视频进行读写。不用对此担心，在你第一次使用MoviePy的时候，FFMPEG将会自动由ImageIO下载和安装（不过需要花一些时间）。如果你想使用FFMPEG的特定版本，你可以设置FFMPEG_BINARY环境变量。详见`moviepy/config_defaults.py`。

### 可选但有用的依赖包

[ImageMagick](https://www.imagemagick.org/script/index.php) 只有在你想要添加文字时需要用到。它可作为一个后端用在GIF上，但如果不安装ImageMagick，你也可以用MoviePy处理GIF。

一旦你安装了ImageMagick，它会被MoviePy自动检测到，**除了Windows环境！** Windows用户在手动安装MoviePy之前，应在`moviepy/config_defaults.py`文件中指定ImageMagick binary的路径，并叫做*convert*。看起来应该像是这样：

```python
IMAGEMAGICK_BINARY = "C:\\Program Files\\ImageMagick_VERSION\\convert.exe"
```

你也可以设置IMAGEMAGICK_BINARY环境变量，详见`moviepy/config_defaults.py`。

[PyGame](https://www.pygame.org/download.shtml) 在视频和声音预览中会使用到。不过如果你想要在服务器上使用MoviePy，但的确需要手动进行高级的视频编辑，Pygame就没什么用处啦。

对于高级的图片处理，你至少需要一个以下所列的包。例如使用`clip.resize`方法，就至少需要安装Scipy、PIL、Pillow或OpenCV其中一个。

- Python图片库（PIL）或它的分支 [Pillow](https://pillow.readthedocs.org/en/latest/) 更好。
- [Scipy](https://www.scipy.org/) （用于追踪、分割等）可在没有安装PIL和OpenCV的情况下用于调整视频剪辑的大小。
- [Scikit Image](http://scikit-image.org/download.html) 可能被用于高级的图片处理。
- [OpenCV 2.4.6](https://sourceforge.net/projects/opencvlibrary/files/) 或更高版本（在`cv2`包中提供）可能被用于高级的图片处理。

如果你使用linux，这些软件都一定在你的仓库中。