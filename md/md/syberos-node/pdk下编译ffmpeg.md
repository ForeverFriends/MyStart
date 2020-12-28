- github 下载ffmpeg源码

  [ffmpeg](https://github.com/FFmpeg/FFmpeg)

- 添加编译脚本文件

  ```shell
  #!/bin/bash
  make clean
  #编译后的文件会放置在 当前路径下的ffmpeg-syberos下
  export PREFIX=$(pwd)/ffmpeg-syberos
  
  #./configure 即为ffmpeg 根目录下的可执行文件configure
  #你可以在ffmpeg根目录下使用./configure --hellp 查看 ./configure后可填入的参数。
  
  ./configure --target-os=linux \
      --prefix= PREFIX \
      --enable-shared \
      --extra-cflags="-Os -fPIC$ADDI_CFLAGS" \
      --disable-doc \
      --disable-static \
      --disable-yasm \
      --disable-symver \
      --disable-ffmpeg \
      --disable-ffplay \
      --disable-ffprobe
  make
  make install
  
  
```
  
  



