FFmpeg README
=============

FFmpeg is a collection of libraries and tools to process multimedia content
such as audio, video, subtitles and related metadata.

## Libraries

* `libavcodec` provides implementation of a wider range of codecs.
* `libavformat` implements streaming protocols, container formats and basic I/O access.
* `libavutil` includes hashers, decompressors and miscellaneous utility functions.
* `libavfilter` provides means to alter decoded audio and video through a directed graph of connected filters.
* `libavdevice` provides an abstraction to access capture and playback devices.
* `libswresample` implements audio mixing and resampling routines.
* `libswscale` implements color conversion and scaling routines.

## Tools

* [ffmpeg](https://ffmpeg.org/ffmpeg.html) is a command line toolbox to
  manipulate, convert and stream multimedia content.
* [ffplay](https://ffmpeg.org/ffplay.html) is a minimalistic multimedia player.
* [ffprobe](https://ffmpeg.org/ffprobe.html) is a simple analysis tool to inspect
  multimedia content.
* Additional small tools such as `aviocat`, `ismindex` and `qt-faststart`.

## Documentation

The offline documentation is available in the **doc/** directory.

The online documentation is available in the main [website](https://ffmpeg.org)
and in the [wiki](https://trac.ffmpeg.org).

### Examples

Coding examples are available in the **doc/examples** directory.

## License

FFmpeg codebase is mainly LGPL-licensed with optional components licensed under
GPL. Please refer to the LICENSE file for detailed information.

## Contributing

Patches should be submitted to the ffmpeg-devel mailing list using
`git format-patch` or `git send-email`. Github pull requests should be
avoided because they are not part of our review process and will be ignored.


AVC sei增加绝对时间戳，github https://github.com/chenminnj/FFmpeg/tree/sei-st 分支
      编译：
      ./configure --prefix=/home/chenmin/FFmpeg/build --enable-libsrt --disable-vaapi --enable-libx264 --enable-gpl

      推流：
      ./ffmpeg -stream_loop -1 -re  -i /home/chenmin/movie/demo.flv  -c:a aac -c:v copy -bsf:v h264_metadata=sei_user_data='086f3693-b7b3-4f2c-9653-21492feee5b8+{timestamp}' -f flv rtmp://192.168.0.101:1935/live/livestream
      
      抓屏推流：
      ./ffmpeg -video_size 1080x720 -f x11grab -i :0.0+1080,720 -bsf:v h264_metadata=sei_user_data='086f3693-b7b3-4f2c-9653-21492feee5b8+{timestamp}'  -f flv rtmp://192.168.0.102:31965/live/1
 
      播放：
      ./ffplay rtmp://192.168.0.101:1935/live/livestream，命令行输出 I-frame 传输时间差
