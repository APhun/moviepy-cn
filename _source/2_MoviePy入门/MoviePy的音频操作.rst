MoviePy的音频操作
-----------------

这个章节会告诉你如何使用MoviePy去创建和编辑音频剪辑。

注意，当你使用MoviePy来剪切、混合或连接视频剪辑时，音频是自动处理的。如果你有兴趣来编辑音频文件，或者你想自定义视频的音频剪辑，请阅读此章。

音频剪辑的构成
~~~~~~~~~~~~~~

在MoviePy中，音频剪辑和视频剪辑很相似：它们拥有长度，能以同样的方式被剪辑和组成，等等。一个显著的差异是\ ``audioclip.get_frame(t)``

创建一个新的音频剪辑
--------------------

音频剪辑可由一个音频文件创建，或从视频剪辑的音轨里提取出来。

.. code:: python

   from moviepy.editor import *
   audioclip = AudioFileClip("some_audiofile.mp3")
   audioclip = AudioFileClip("some_video.avi")

详见\ ``AudioFileClip``\ 。

或者你也可以得到一个已创建的视频剪辑的音轨。

.. code:: python

   videoclip = VideoFileClip("some_video.avi")
   audioclip = videoclip.audio

合成音频剪辑
~~~~~~~~~~~~

导出和预览音频剪辑
~~~~~~~~~~~~~~~~~~

你也可以导出分配一个音频剪辑当作视频剪辑的音轨。

.. code:: python

   videoclip2 = videoclip.set_audio(my_audioclip)