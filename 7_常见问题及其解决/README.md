## 常见问题及其解决

*原文链接：
http://zulko.github.io/moviepy/FAQ.html*

</br>
</br>
</br>
</br>

这个部分会随着MoviePy的进一步更新逐渐进行补充，目前的规划包括：MoviePy Studio, MoviePy WebApp, MoviePy OS, MoviePy Trust Inc., and the MoviePy 基金会。

</br>

### 并不是bug的常见错误

下面是一些并未被考虑为bug的常见错误（但你依然可以请求改变）。如果这些答案对你并不实用，请在[GitHub](https://github.com/Zulko/moviepy)上提交一个bug报告，或者提交到[Reddit](https://www.reddit.com/r/moviepy/)上专门的论坛，亦或者是[librelist](moviepy%40librelist.com)。

### MoviePy生成的视频并不能被我最喜欢的视频播放器所播放

已知问题：视频分辨率的某一维度不是偶数，例如：720*405；同时你使用了MPEG4编码器例，如libx264（MoviePy中默认）。在这种情况下，生成出来的视频的格式将会只能被某些播放器读取，例如VLC。

### 我似乎不能用MoviePy读取任何视频

已知问题：你应该使用了不被推荐的FFMPEG版本，请从网站安装最近的版本，而不是从你系统本身的仓库中安装！（详见 [下载与安装](https://github.com/APhun/moviepy-cn/tree/master/1_%E4%B8%8B%E8%BD%BD%E4%B8%8E%E5%AE%89%E8%A3%85)）

### 预览视频使得他们变得更慢了

这说明你的系统配置不足以实时渲染视频片段。这种情况下，请不要犹豫调整`preview`这个选项：例如，降低声音与食品片段的fps（11000 Hz依然足够好了）。同时，使用`resize`降低视频的大小也有帮助。