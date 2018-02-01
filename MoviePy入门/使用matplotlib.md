## 使用matplotlib
### 自定义动画
MoviePy提供了一种生成自定义动画的方式：通过定义一个函数，以numpy数组的形式返回一个在给定的时间内一帧的动画。

例如，在如下的工作流中：
```python
from moviepy.editor import VideoClip

def make_frame(t):
    """Returns an image of the frame for time t."""
    # ... create the frame with any library here ...
    return frame_for_time_t # (Height x Width x 3) Numpy array

animation = VideoClip(make_frame, duration=3) # 3-second clip
```
这个动画可以像通常一样导出：
```python
# export as a video file
animation.write_videofile("my_animation.mp4", fps=24)
# export as a GIF
animation.write_gif("my_animation.gif", fps=24) # usually slower
```

### matplotlib的简易实例
一个使用matplotlib的动画实例如下：
```python
import matplotlib.pyplot as plt
import numpy as np
from moviepy.editor import VideoClip
from moviepy.video.io.bindings import mplfig_to_npimage

x = np.linspace(-2, 2, 200)

duration = 2

fig, ax = plt.subplots()
def make_frame(t):
    ax.clear()
    ax.plot(x, np.sinc(x**2) + np.sin(x + 2*np.pi/duration * t), lw=3)
    ax.set_ylim(-1.5, 2.5)
    return mplfig_to_npimage(fig)

animation = VideoClip(make_frame, duration=duration)
animation.write_gif('matplotlib.gif', fps=20)
```

### 在Jupyter Notebook中运行
如果你在Jupyter Notebook中运行，你可以体会到用*ipython_display*方法将视频剪辑嵌入在输出单元中的优势。示例如下：
```python
import matplotlib.pyplot as plt
import numpy as np
from moviepy.editor import VideoClip
from moviepy.video.io.bindings import mplfig_to_npimage

x = np.linspace(-2, 2, 200)

duration = 2

fig, ax = plt.subplots()
def make_frame(t):
    ax.clear()
    ax.plot(x, np.sinc(x**2) + np.sin(x + 2*np.pi/duration * t), lw=3)
    ax.set_ylim(-1.5, 2.5)
    return mplfig_to_npimage(fig)

animation = VideoClip(make_frame, duration=duration)
animation.ipython_display(fps=20, loop=True, autoplay=True)
```