## 如何更有效率地使用MoviePy
这一节总结了一些技巧和诀窍，可以帮助你充分利用全球范围内已知的经验来使用MoviePy。

使用IPython Notebook是使用MoviePy的最好方法。它使得预览剪辑变得很容易（在此节中会介绍到），有自动完成功能，而且可以显示库里不同方法的文档。

### 我应该使用`moviepy.editor`吗？
这篇文档里的大部分示例使用了`moviepy.editor`子模块，但是这个子模块并不适用于所有需求。简单来说，如果你使用MoviePy手动编辑视频，那就建议使用此子模块；如果你在更大的库、更大的项目或web服务器上使用MoviePy，最好避免使用它，转而加载你需要的函数。

`moviepy.editor`模块能以以下三种方式加载：
```python
from moviepy.editor import * # imports everything, quick and dirty
import moviepy.editor as mpy # Clean. Then use mpy.VideoClip, etc.
from moviepy.editor import VideoFileClip # just import what you need
```
通过这些代码，`moviepy.editor`模块会做许多幕后工作：它将获取MoviePy里最常见的类、函数和子包，初始化一个PyGame会话（在PyGame已安装的情况下）使得视频剪辑可被预览，并执行一些快捷方式，例如对剪辑添加`resize`变换。以这种方式，你可以使用`clip.resize(width=240)`来替代更长的`clip.fx(resize,width=240)`写法。总之，`moviepy.editor`提供了你所需要的播放和剪辑功能，但是需要一些时间来加载（大约1秒）。所以如果你所需要的一或两个效果在别的库里，直接将你所需要的导入是更好的选择，就像这样：
```python
from moviepy.video.io.VideoFileClip import VideoFileClip
from moviepy.video.fx.resize import resize
```

### 预览剪辑的多种方法
当你使用MoviePy通过不断尝试来编辑视频或试图达到某种效果的时候，生成每个示例的视频的时间可能会很长。这一节提供了一些提高速度的小窍门。
#### clip.save_frame
很多时候，只需要视频中的一帧，即可说明你是否正确操作。你可以像这样保存剪辑中的一帧：
```python
my_clip.save_frame("frame.jpeg") # saves the first frame
my_clip.save_frame("frame.png", t=2) # saves the frame a t=2s
```
#### clip.show and clip.preview
使用`clip.show`和`clip.preview`方法，使剪辑在Pygame的窗口中可视。这两个方法是预览的最快方法，当剪辑在生成和播放的同事，它们还可以获得坐标和像素的颜色。这些方法需要PyGame的支持，以及`moviepy.editor`模块的使用。

`clip.show`模块可以在没有写入文件的情况下预览剪辑里的一帧。如下是如何在PyGame窗口中显示一帧：
```python
my_clip.show() # shows the first frame of the clip
my_clip.show(10.5) # shows the frame of the clip at t=10.5s
my_clip.show(10.5, interactive = True)
```
最后一行（有`interactive=True`的一行）以一种交互的形式显示一帧：如果你单击这一帧的任意一处，它将输出位置和像素的颜色。当你结束查看时，按下esc键。

如下代码可预览剪辑：
```python
my_clip.preview() # preview with default fps=15
my_clip.preview(fps=25)
my_clip.preview(fps=15, audio=False) # don't generate/play the audio.
my_audio_clip.preview(fps=22000)
```
如果你单击正在预览的视频剪辑中某帧的任意一处，将输出单击的位置和像素的颜色。按esc结束预览。

注意，如果剪辑很复杂而且你的电脑速度也不够快，剪辑的预览速度将会比真实速度慢。在这种情况下，你可以尝试降低帧率（例如将为10），或者用`clip.resize`降低剪辑的尺寸。

#### ipython_display
使用IPython Notebook来显示剪辑很实用，尤其是你不想用`clip.show()`和`clip.preview()`时。看起来就像这样：

![](http://zulko.github.io/moviepy/_images/demo_preview.jpeg)

通过使用`ipython_display`，你可以从文件或直接从片段里潜入视频、图片或声音：
```python
ipython_display(my_video_clip) # embeds a video
ipython_display(my_imageclip) # embeds an image
ipython_display(my_audio_clip) # embeds a sound

ipython_display("my_picture.jpeg") # embeds an image
ipython_display("my_video.mp4") # embeds a video
ipython_display("my_sound.mp3") # embeds a sound
```
只有当`ipython_display`在一个笔记本单元的最后一行才有效。你也可以调用`ipython_display`作为一个剪辑方法：
```python
my_video_clip.ipython_display()
```
如果对所呈现的视频的帧率有所要求，你可以在`ipython_display`里指定`fps=25`。

如果你只需要播放一个视频剪辑在时间t的快照，可以这样写：
```python
my_video_clip.ipython_display(t=15) # will display a snapshot at t=15s
```
你还可以提供有效的HTML5选项作为关键词的参数。例如，如果剪辑太大，你可以这么写：
```python
ipython_display(my_clip, width=400) # HTML5 will resize to 400 pixels
```
例如，当你编辑一个GIF动画，而且想检查它是否正确循环，你可以使视频自动启动和循环（即无限重复）：
```python
ipython_display(my_clip, autoplay=1, loop=1)
```
重要的是，`ipython_display`实际上是将剪辑嵌入了你的笔记本里。优势在于你可以移动笔记本或将其放在网络上发布，视频将会运行。缺陷在于笔记本的文件尺寸会变得非常巨大。根据你的浏览器，多次重新计算和播放视频会在cache和RAM中占用一些空间（仅当密集使用时出现此问题）。重启浏览器即可解决问题。