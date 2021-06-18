# gsteamer tee

https://gstreamer.freedesktop.org/documentation/tutorials/basic/multithreading-and-pad-availability.html?gi-language=c



```
gst-launch-1.0 v4l2src device=/dev/video0 ! tee name=t \
t. ! queue name=video-queue ! jpegenc ! avimux ! filesink location=test_out.avi \
t. ! queue name=stream-queue ! deinterlace ! xvimagesink \
t. ! queue name=image-queue ! videoconvert ! pngenc compression-level=0 ! filesink location=test_out.png
```

![](https://gstreamer.freedesktop.org/documentation/tutorials/basic/images/tutorials/basic-tutorial-7.png)





# jetson-gstreamer

Full details [here](https://docs.nvidia.com/jetson/l4t/index.html#page/Tegra%20Linux%20Driver%20Package%20Development%20Guide/accelerated_gstreamer.html#wwpID0E02P0HA)

Play from USB cam:
```
gst-launch-1.0 v4l2src device="/dev/video0" ! "video/x-raw, format=(string)YUY2" ! xvimagesink -e
gst-launch-1.0 v4l2src device="/dev/video0" ! "video/x-raw, width=640, height=480, format=(string)YUY2" ! xvimagesink -e

```

To play a video:
```
gst-launch-1.0 filesrc location=video.mp4 ! qtdemux name=demux ! h264parse ! omxh264dec ! nvoverlaysink -e


```

from old WaveBase hardware (with what looks like USB 3.0)

`Video: rawvideo (YUY2 / 0x32595559), yuyv422, 1920x1080, 165888 kb/s, 5 fps, 5 tbr, 1000k tbn, 1000k tbc`


HDMI to Type-C (with USB2.0 adapter):

`Video: rawvideo (YUY2 / 0x32595559), yuyv422, 1920x1080, 165888 kb/s, 5 fps, 5 tbr, 1000k tbn, 1000k tbc`


CamLink:

`Video: rawvideo (I420 / 0x30323449), yuv420p, 1920x1080, 1492992 kb/s, 60 fps, 60 tbr, 1000k tbn, 1000k tbc`
