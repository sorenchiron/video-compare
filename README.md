# video-compare

# 特别说明

本代码经过修改，适用于在mac上编译，为适配目前最新的ffmpeg-devel而删除了少数过时代码。

本代码使用pkg-config查找依赖。

如果有错误出现，请：

```
export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig:/usr/lib/pkgconfig
```


Split screen video comparison tool written in C++14 using FFmpeg libraries and SDL2. 

`video-compare` can be used to visually compare e.g. the effect of codecs and resizing algorithms on
two video files played in sync. The tool is not very restrictive as videos are not required to be the
same resolution, color format, container format, codec or duration. However, for the best result video
files should have the same frame rate.

A movable slider enables easy viewing of the difference across any region of interest.

Thanks to the versatility of FFmpeg, it is actually also possible to use `video-compare` to compare
two images. The common PNG and JPEG formats have been successfully tested to work.

Screenshots
-----------

Visual compare mode:
![Visual compare mode](screenshot_1.jpg?raw=true)

Subtraction mode (and zoom activated):
![Subtraction mode"](screenshot_2.jpg?raw=true)

Credits
-------

`video-compare` was created by Jon Frydensbjerg (email: jon@pixop.com). The code is mainly based on
the excellent video player GitHub project: https://github.com/pockethook/player

Many thanks to the FFmpeg and SDL2 authors.

Usage
-----

Launch in disallow high DPI mode. Video pixels become doubled on high DPI displays. Recommended
for displaying HD 1080p video on e.g. a Retina 5K display:

    ./video-compare video1.mp4 video2.mp4

Allow high DPI mode on systems which supports that. Video pixels are displayed "1-to-1". Useful
for e.g. displaying UHD 4K video on a Retina 5K display:

    ./video-compare -d video1.mp4 video2.mp4

Use a specific window size instead of deriving the window size from the video dimensions. The video 
frame will be scaled to fit. Useful for downscaling high resolution video onto a low resolution 
display:

    ./video-compare -w 1280x720 video1.mp4 video2.mp4

The allow high DPI mode and window size arguments can be combined if so desired.

Note that in order to work, the `SourceCodePro-Regular.ttf` font must be located in the same directory 
as the main executable. It is recommended to leave the compiled software in its source folder to 
ensure access to external dependencies and run the program from a different working directory:

    [path-to-video-compare-source-code]/video-compare video1.mp4 video2.mp4

Controls
--------

* Space: Toggle play/pause
* Escape: Quit
* Down arrow: Seek 15 seconds backward
* Left arrow: Seek 1 second backward
* Page down: Seek 600 seconds backward
* Up arrow: Seek 15 seconds forward
* Right arrow: Seek 1 second forward
* Page up: Seek 600 seconds forward
* S: Swap left and right video
* A: Previous frame
* D: Next frame
* Z: Zoom area around cursor (result shown in lower left corner)
* C: Zoom area around cursor (result shown in lower right corner)
* 1: Toggle hide/show left video
* 2: Toggle hide/show right video
* 3: Toggle hide/show HUD
* 0: Toggle video/subtraction mode

Move the mouse horizontally to adjust the movable slider position. Click the mouse to perform a time
seek based on the horizontal position of the slider relative to the window width.

Requirements
------------

Requires FFmpeg headers and development libraries to be installed, along with SDL2
and its TrueType font rendering add on (libsdl2_ttf).

Build
-----

    make

Notes
-----

1. Audio playback is not supported.

2. The code is hard to maintain at the moment (too many copy/paste and lazy solutions).
My intention has mainly been to build a tool in a few days which gets the job done. 
A lot of refactoring and clean-up is required when I have the time for it. Consider
yourself warned! ;-)

3. Pre-built Windows 64-bit releases are available from this page (simply extract the 
.zip-archive and run `video-compare.exe` from a command prompt).
